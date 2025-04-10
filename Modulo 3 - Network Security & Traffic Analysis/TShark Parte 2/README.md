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

## 🌍 **Dirección IP asociada al dominio: 
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

## Este caso reafirmó la importancia de monitorear cuidadosamente las interacciones HTTP y DNS dentro de la red, incluso cuando provienen de acciones aparentemente inofensivas como navegar por un índice web. Gracias al uso de herramientas como **TShark** y **VirusTotal**, pude seguir el rastro del incidente desde la navegación inicial hasta el análisis forense del archivo descargado. Documentar estos pasos fortalece nuestra capacidad de detección futura y contribuye al enriquecimiento continuo del equipo SOC.

