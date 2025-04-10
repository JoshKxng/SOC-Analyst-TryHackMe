# 📡 TShark Challenge I - Teamwork
# 🏆 Desafío:
### Me asignaron el análisis del archivo *teamwork.pcap* para investigar un dominio sospechoso detectado por el equipo de Threat Intelligence. Para resolver esto, utilicé TShark desde la terminal para extraer el tráfico DNS,  identifiqué los dominios involucrados y luego verifiqué su reputación en VirusTotal. Gracias a esto, pude seguir el rastro del tráfico malicioso, identificar una suplantación de identidad y generar información clave que podría sumarse a las reglas de detección para reforzar la postura del equipo de seguridad.

### 🛠️ Herramientas Utilizadas
### ✅ TShark – Inspección y filtrado de paquetes desde la consola.
### ✅ VirusTotal – Verificación de reputación de dominios y URLs.

---

## 1️⃣ ¿Cuál es la URL completa del dominio marcado como malicioso/sospechoso?
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-shark%201/Inicio%201.png)

---

## 2️⃣ ¿Cuándo fue enviada por primera vez esta URL a VirusTotal?
### ✅ 2017-04-17 22:52:53 UTC
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-shark%201/Inicio%202.png)

---

## 3️⃣ ¿Qué servicio conocido estaba intentando suplantar el dominio?
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-shark%201/Inicio%203.png)

---

## 4️⃣ ¿Cuál es la dirección IP del dominio malicioso?
### ✅ 184.154.127.226
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-shark%201/Inicio%204.png)

---

## 5️⃣ ¿Cuál fue la dirección de correo electrónico utilizada?
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/T-shark%201/Inicio%205.png)

---

# 🎖️ Conclusión
## Este desafío me permitió poner en práctica todo lo aprendido sobre el uso de TShark desde la línea de comandos, el análisis de tráfico DNS y la verificación de indicadores en VirusTotal. Cada paso fue un ejercicio realista de lo que se espera en un entorno SOC, donde la precisión y el criterio analítico marcan la diferencia.
