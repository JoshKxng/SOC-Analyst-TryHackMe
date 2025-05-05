# 🏆 Splunk Challenge - Investigating with Splunk

## 📘 Contexto

Durante un turno habitual en el SOC, se nos notificó una alerta generada por un sistema EDR que reportaba **comportamiento anómalo en uno de los hosts del dominio interno**. Según los primeros registros, se detectó una posible **creación de una cuenta sospechosa** y la ejecución de **comandos PowerShell**. 
Mi rol como **Analista SOC L1** fue revisar minuciosamente los eventos de seguridad en Splunk, correlacionar logs y construir una narrativa clara de los movimientos del adversario. Lo que inicialmente parecía una actividad menor, escaló rápidamente cuando identifiqué un patrón de **persistencia mediante una cuenta backdoor** y un intento de **recolección y exfiltración a través de web requests**.

---

### 🧑‍🚪 ¿Qué nombre tenía el nuevo usuario backdoor creado en uno de los hosts infectados?  
### ✅ **`a1berto`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/01.png)

---

### 🧾 ¿Cuál es la ruta completa de la clave del registro que fue modificada respecto al nuevo usuario backdoor?  
### ✅ **`HKLM\SAM\SAM\Domains\Account\Users\Names\A1berto`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/02.png)

---

### 🕵️‍♂️ ¿Qué usuario legítimo intentó suplantar el adversario durante el ataque?  
### ✅ **`Alberto`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/03.png)

---

### 🖥️ ¿Qué comando se utilizó para crear el usuario backdoor desde un equipo remoto?
### ✅ **`C:\windows\System32\Wbem\WMIC.exe" /node:WORKSTATION6 process call create "net user /add A1berto paw0rd1`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/04.png)

---

### 🧑‍💻 ¿Cuál es el nombre del host infectado en el que se ejecutaron comandos PowerShell maliciosos y cuántos eventos de PowerShell se registraron relacionados con la ejecución del script malicioso?
### ✅ **`79 Eventos`**
### ✅ **`James.browne`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/05.png)

---

### 🌐 ¿Cuál es la URL completa que fue contactada desde el host infectado mediante un script PowerShell codificado?
### ✅ **`hxxp[://]10[.]10[.]10[.]5/news[.]php`**
### 1️⃣
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/06.png)

### 2️⃣
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/07.png)

### 3️⃣
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/08.png)

### 4️⃣
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/09.png)

---

# 🎖️ Conclusión

### Un nuevo desafío productivo y enriquecedor. A medida que iba avanzando con la investigación sentí que estaba dentro de un entorno real de trabajo en un SOC, analizando eventos, cruzando información y sacando conclusiones. Se volvió a hacer hincapié en la importancia de la persistencia y análisis de eventos de Windows, pero también a afinar mi propio razonamiento investigativo.
