# 🏆 Benign Challenge – Incident Response Case Study
 
### 📁 Categoría: Investigación de incidentes en entornos reales  
### 🕵️‍♂️ Enfoque: Razonamiento lógico, detección de anomalías, análisis de logs en Splunk

---

## 📚 Escenario

> **“Uno de los IDS del cliente indicó una ejecución de un proceso potencialmente sospechoso, lo que indica que uno de los hosts del departamento de RRHH estaba comprometido…”**

Como analista SOC Jr., recibí una alerta generada por un sistema IDS del cliente. El aviso sugería una actividad sospechosa proveniente de uno de los hosts del departamento de RRHH. Dada la naturaleza sensible de la información que maneja esta área, se trataba de una prioridad alta para el equipo.

Debido a limitaciones operativas, sólo se nos proporcionaron los logs de eventos de procesos (Windows Event ID 4688), los cuales fueron ingeridos en Splunk bajo el índice `win_eventlogs`. A partir de ahí, comencé mi investigación.

---

## 💼 Entorno de red

La red del cliente se encuentra segmentada en tres departamentos:

| Departamento | Usuarios                    |
|--------------|-----------------------------|
| IT           | James, Moin, Katrina        |
| RRHH           | Haroon, Chris, Diana        |
| Marketing    | Bell, Amelia, Deepak        |

---

## 🧭 Línea de Investigación

### 🔹 ¿Cuántos logs fueron ingeridos del mes de marzo de 2022?
Ajustando la fecha de inicio de investigación, logré indentificar que fueron **13,959 logs**. Este fue el primer paso para delimitar la ventana temporal de análisis.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Benign/01.png)

---
## 🚨 Impostor detectado
Sabía que tenia que rastrear a la persona infiltrada, por eso decidí aplicar el filtro `source="win_event_logs.json" EventID=4688 HostName=*HR_0*`. Al buscar inconsistencias en los usuarios, noté la presencia de un nombre no esperado en los registros: **`⚠️Amel1a`**. Aunque Amelia pertenece al departamento de Marketing, no es un usuario legítimo del departamento de RRHH y también, tiene un nombre que imita a la usuaria del departamento de Marketing: **Amelia**.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Benign/02.png)

---
## 🕒 ¿Qué usuario del área de RRHH ejecutó tareas programadas?
Partiendo de un filtrado inicial por **`EventID=4688`** y acotando por los hostnames relacionados con RRHH **`*HR_0*`**, razoné que las tareas programadas **(scheduled tasks)** suelen invocar el binario **schtasks.exe.** Por eso decidí buscar comandos que incluyeran **.exe** y encontré un comando sospechoso ejecutado por el usuario 👉 **Chris.fort**.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Benign/03.png)

---

## ⚔️ ¿Qué usuario del departamento de RRHH ejecutó un proceso del sistema (LOLBIN) para descargar una carga útil de un host de intercambio de archivos? Y para eludir los controles de seguridad, ¿Qué proceso del sistema (LOLBIN) se utilizó para descargar una carga útil de Internet?
Al investigar los procesos ejecutados en los equipos de RRHH, detecté un uso sospechoso del binario **`certutil.exe`**. Aquí me pregunté, ¿Para que sirve un binario de este tipo? Al investigar, me encuentro con el termino **`LOLBIN (Living Off the Land Binary)`** y resultó ser una herramienta legítima de Windows, pero comúnmente es usada por atacantes para ejecutar código, mover archivos o descargar payloads.
Por lo tanto, el usuario que ejecutó el proceso fue 👉 **`haroon`** y el proceso que ejecutó fue 👉 **`certutil.exe`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Benign/04.png)

---

## 📥 ¿A qué sitio de terceros se accedió para descargar la carga maliciosa?
Refiné mi búsqueda enfocándome en el binario **`certutil.exe`** y en su uso como herramienta de descarga desde una fuente externa. El objetivo era identificar con precisión el sitio accedido. Por lo tanto, ajusté mi filtro incluyendo el uso de **`-urlcache`** y la URL completa. Por lo tanto, confirmé que el sitio accedido fue 👉 **`controlc.com`**, un servicio utilizado como servidor de **comando y control (C2)** en este caso.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Benign/05.png)

---
## 📂 ¿Cuál es el nombre del archivo que se guardó en la máquina host desde el servidor C2 durante la fase posterior a la explotación?
En la misma evidencia resalté el nombre del archivo que fue descargado en el host comprometido durante la fase de post-explotación: 👉 **`benign.exe`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Benign/06.png)

--
# 🎖️ Conclusión
## Este desafío fue uno de mis favoritos (y ya son varios jajaja), porque fue una experiencia sumamente enriquecedora, voy experimentando como mi razonamiento lógico e intuición van siendo cada vez más clave para llegar a las respuestas correctas. Muchas veces, antes de confirmar una pista, fue mi instinto analítico el que me llevó a hacer clic en el campo correcto o ajustar el filtro justo como debía ser. El poder moverme entre eventos, examinar comandos y extraer conclusiones dentro de un entorno realista de trabajo SOC es una sensación de crecimiento enorme.
