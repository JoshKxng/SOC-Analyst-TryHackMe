# 🖥 Wireshark - Análisis forense de tráfico de red
### 📅 Escenario: El SOC está en alerta. Se detectaron varios eventos sospechosos en la red interna de la organización y el equipo de ciberseguridad me solicitó un análisis forense para identificar actividad anómala. mi tarea es investigar el tráfico capturado con Wireshark y extraer información clave que nos ayude a comprender lo que ha sucedido.

### A continuación, documento mis hallazgos en cuatro áreas críticas: 
✅ Identificación de hosts  
✅ Túneles de tráfico  
✅ Protocolos en texto claro  
✅ Análisis de tráfico encriptado.  

---
# 🔍 Task 1: Identificación de hosts (DHCP, NetBIOS y Kerberos)
### 📌 Detección de dispositivos en la red
### 📡 Un dispositivo "Galaxy A30" se ha conectado a la red. ¿Cuál es su dirección MAC?

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wireshark/DHCP%20-%201.png)

---

### 📌 Registros NetBIOS sospechosos
### 💻 La estación de trabajo "LIVALJM" ha realizado múltiples solicitudes NetBIOS. ¿Cuántas solicitudes de registro se detectaron?

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wireshark/DHCP%20-%202.png)

---
### 📌 Solicitud de IP desconocida
### 🌐 Se ha detectado una solicitud de IP que podría estar relacionada con actividad maliciosa. ¿Qué host solicitó la dirección IP 172.16.13.85? 

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wireshark/DHCP%20-%203.png)

---

# 🚦 Task 2: Tráfico tunelizado a través de DNS e ICMP
### 📌 Investigación de paquetes anómalos
### ⚠️ Se detectó un patrón sospechoso en las consultas DNS. ¿Cuál es el dominio principal que recibe estas consultas anómalas? (Formato defanged) ✅ dataexfil[.]com
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wireshark/Tunneling%201.png)

### 💡 Los atacantes a suelen utilizar consultas DNS para exfiltrar datos o aplicar la táctica C2. Este tipo de tráfico es una alerta temprana de actividad maliciosa en la red.

---

# 📂 Task 3: Análisis de protocolos en texto claro (FTP)
### 📌 Fuerza bruta en FTP
### 🔑 Se han registrado múltiples intentos fallidos de inicio de sesión en un servidor FTP. ¿Cuántos intentos incorrectos se detectaron?

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wireshark/FTP%20-%201.png)

---

### 📌 Acceso a archivos
### 📁 Un atacante logró acceder a un archivo en el servidor. ¿Cuál es su tamaño?

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wireshark/FTP%20-%202.png)

----

### 📌 Subida de archivos sospechosos
### 📥 Se detectó la carga de un archivo en el servidor FTP. ¿Cuál es el nombre del archivo subido?
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wireshark/FTP%20-%203.png)

---

### 📌 Intento de ejecución maliciosa
### 🛠️ Después de subir el archivo, el atacante intentó modificar sus permisos para hacerlo ejecutable. ¿Qué comando utilizó?
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Wireshark/FTP%20-%204.png)

---

# 🔐 Task 4: Análisis de tráfico encriptado (HTTPS)
### 📌 Inspección de tráfico cifrado
### 🔎 Se ha capturado tráfico HTTPS en el Frame 322. ¿Cuál es el header de autoridad del paquete HTTP2? (Formato defanged)

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wireshark/HTTPS%20-%201.png)
