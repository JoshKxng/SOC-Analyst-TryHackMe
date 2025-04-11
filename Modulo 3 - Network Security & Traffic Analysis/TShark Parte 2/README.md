# 🏆 TShark Challenge II: Directory Curiosity

# 📍 *Contexto profesional:*

### Durante una jornada típica como Analista SOC Jr., recibí una nueva alerta disparada por nuestro sistema de detección temprana:  
> **"Un usuario accedió a un índice de archivos mal configurado, y su curiosidad lo llevó a problemas."**  

### Mi tarea consistía en analizar el tráfico registrado en el archivo `directory-curiosity.pcap`, detectar si el incidente representaba una amenaza real, y documentar los artefactos clave para fortalecer las capacidades de respuesta y detección del equipo.

---

## 🔍 Herramientas utilizadas

- `📡 TShark`: Para inspección en profundidad de los paquetes de red desde CLI.
- `🧪 VirusTotal`: Para análisis de reputación de dominios y archivos sospechosos.
- `🛠️ sha256sum + PEiD + HTTP object export`: Para examinar artefactos descargados y firmas de empaquetado.

---

# 🧩 Análisis y hallazgos
## Durante el análisis de las consultas DNS detecté un dominio con comportamiento irregular. Consultando VirusTotal, se confirmó como **sospechoso/malicioso**, lo que validó la alerta como un **true positive**.

## 🔗 Dominio malicioso:  
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/Directory%201.png)

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/Directory%202.png)

---

## 📨 Número de solicitudes HTTP al dominio:
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/Directory%204.png)

---

## 🌍 Dirección IP asociada al dominio: 
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/Directory%205.png)

---

## 🖥️ Información del servidor:  
## ✅ `Apache/2.2.11 (Win32) DAV/2 mod_ssl/2.2.11 OpenSSL/0.9.8i PHP/5.2.9`  
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/Directory%206.png)

---

## 📂 Listado del índice de archivos (vía TCP Stream ASCII) más el Archivo ejecutable descargado vía HTTP:  
## ✅ `123.php` | ## ✅ `vlauto[.]exe` | ## ✅ `vlauto.php`

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/Directory%207.png)

---

## 🔐 SHA256 del archivo malicioso:
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/Directory%208-A.png).

---

## 🧬 **PEiD packer:**  
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/pEid%20Packer.png)

## 🧫 Análisis en VirusTotal (Lastline Sandbox): 
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-Shark%202/Directory%209.png)

---

# 🎖️ Conclusión

## Este caso fue una gran oportunidad para aplicar lo aprendido con TShark y reforzar lo importante que es prestar atención a los detalles del tráfico HTTP y DNS. Lo que empezó como una simple navegación a un índice web terminó revelando un archivo malicioso. Usando herramientas como TShark y VirusTotal, pude seguir todo el recorrido, identificar el dominio sospechoso, analizar el archivo y dejar todo bien documentado para que el equipo pueda actuar más rápido en el futuro.

