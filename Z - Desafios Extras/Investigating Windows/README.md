# 🕵️‍♂️ Investigating Windows - Analizando un sistema Windows comprometido

Este es un ejercicio de investigación forense realizado como parte de mi formación práctica en ciberseguridad. El escenario corresponde a la room **"Investigating Windows"** de TryHackMe, en donde se simula un incidente real en un entorno Windows comprometido.
Aquí comparto mi experiencia como analista SOC L1 Jr. resolviendo este desafío técnico.

---
## 📌 Objetivo:
Reconstruir la cronología de los eventos, detectar persistencia maliciosa, herramientas usadas y puntos de entrada.

---

## 🔍 Proceso de Investigación y Hallazgos Técnicos

### 🧱 Reconocimiento Inicial: Versión del Sistema Operativo 
Para comenzar, identifiqué el sistema afectado: **Windows Server 2016**.
Esto podemos hacerlo con el comando **`winver`** o con el comando **`systeminfo`**. Éste último nos da información más detallada del sistema: versión, arquitectura, fecha de instalación, etc.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/01.png)

--- 

### 👤 Último Usuario Logueado
¿Qué estaba búscando acá? Saber quién usó por última vez el sistema. De hecho, fuimos nosotros que somos **`Administrator`**. Para más detalles sobre este usuario podemos ejecutar el comando **`Net user Administrator`** 

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/02a.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/02b.png)

---

### 👨 Último Inicio de Sesión de John
Se nos pregunta cuándo fue la última vez que ingresó John al sistema.  
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/03.png)

---

### 📡 Persistencia y Comportamiento Malicioso | Usuarios con Privilegios Administrativos 
Encontré que además del usuario Administrator, también los usuarios **`Guest`** y **`Jenny`** tenían privilegios administrativos.

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/04.png)

---

### ⏲️ Tarea Programada Maliciosa y Puerto Local en Escucha  
Explorando el **`Task Scheduler`**, encontré una tarea sospechosa llamada **`Clean file system`**. Al investigar más a fondo, observé que se ejecutaba diariamente un script llamado **`nc.ps1`**. Dicho script abría un **listener en el puerto 1348**, permitiendo al atacante mantener una shell persistente en el sistema.  
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/05-06-07.png)

---

### 👩 ¿Cuándo fue la última vez que Jenny inició sesión?
#### `Nunca` 
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/08.png)

---

### 🤔 ¿Cuándo se asignaron privilegios especiales a una sesión por primera vez?
Para encontrar esto, me dirigí a **`Event Viewer`**. Allí filtré por fecha: **`2/3/2019`** y por evento de seguridad: **`ID 4672`** que indican asignación de privilegios especiales. Dada la cantidad extensiva de logs, TryHackMe nos da una pista que dice: **`00/00/0000 0:00:49 PM`**.
Allí pude encontrar cuando se asignaron privilegios especiales.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/10.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/10c.png)


---

## 🧰 Herramientas y Técnicas Usadas por el Atacante

### 🔑🕵️‍♂️ Dumping de Credenciales 
Durante la investigación, identifiqué el uso de **`Mimikatz`**, una herramienta muy conocida para la extracción de credenciales de Windows.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/11a.png)

---
### 📡⚙️ Servidor de Comando y Control (C2) 
El atacante mantenía comunicación con la IP externa **`76.32.97.132`**, utilizada como **`servidor C2`**, lo cual confirmaba el control remoto del equipo comprometido.
Investigando por la web pude saber que este archivo puede ser modificado por el atacante para redirigir tráfico (ej: google.com → IP maliciosa).
Por lo tanto, ver esto es vital para detectar un caso de **`DNS poisoning`** o **`persistencia remota`**.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/12.png)

---
### 📂🕸️ ¿Cuál era el nombre de la extensión del shell cargado a través del sitio web del servidor?

Explorando la carpeta **`C:\inetpub\wwwroot\`** , encontré la carga de una **`web shell`** con extensión **`.jsp`**, usada para ejecución remota de comandos. 
Busacando más información en internet, encontré que es una técnica muy común para lograr web shells que otorgan acceso remoto a través del navegador.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/13.png)

---
### 🔓🚪 Último Puerto Abierto por el Atacante 
A través del Firewall del equipo, sabemos que el atacante habilitó una nueva vía de acceso abriendo el puerto **`1337`**.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Investigating%20Windows/14.png)

---

# 🎖️ Conclusión
## Fue un desafío atrapante que me llevó a investigar un sistema Windows comprometido, desde la mirada analítica de un Analista SOC L1 Jr, reforzando mis habilidades en detección y análisis.
