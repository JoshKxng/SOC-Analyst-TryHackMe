# 🟢 The Greenholt Phish - Análisis de un correo malicioso

## Hoy tocó investigar un correo sospechoso recibido por un empleado de la organización `Greenholt`. Mi tarea fue examinar detenidamente los encabezados del correo y el archivo adjunto con el objetivo de determinar si se trataba de un intento de phishing, y si era así, recolectar toda la evidencia necesaria para reportarlo.
---

### 📌 Al abrir el correo electrónico podemos encontrar las respuestas a las siguientes preguntas
### - 1 💷 ¿Cuál es el número de referencia de transferencia que aparece en el asunto del correo?
### - 2 💼 ¿Quién es el remitente del correo?
### - 3 🔁 ¿A qué dirección se enviaría una posible respuesta?
### - 4 ✉️ ¿Cuál es la dirección de correo del remitente?
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/The%20Greenholt%20Phish/02.png)

---
### 🌐 ¿Cuál es la IP de origen del mensaje?
### Al analizar el header, encontré que la IP de origen era 192.119.71.157
### Por lo tanto decidí scanearla en DomainTools para obtener más detalles

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/The%20Greenholt%20Phish/03.png)

---

### 🏢 ¿A qué organización pertenece la IP de origen?

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/The%20Greenholt%20Phish/04.png)

---

### 🔒 ¿Cuál es el registro SPF del dominio en la cabecera Return-Path?

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/The%20Greenholt%20Phish/07.png)

---

### 📊 ¿Cuál es el registro DMARC del dominio en la cabecera Return-Path?

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/The%20Greenholt%20Phish/08.png)

---

### 📎 ¿Cuál es el nombre del archivo adjunto? y ¿Cuál es el hash SHA256 del archivo adjunto?

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/The%20Greenholt%20Phish/09.png)

---

### 🧮 ¿Cuál es el tamaño del archivo adjunto? *(No olvides "KB")*

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/The%20Greenholt%20Phish/10.png)

---

### 🧩 ¿Cuál es la extensión real del archivo adjunto?

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/The%20Greenholt%20Phish/11.png)

---

# 🎖️ Conclusión
## Fue un formidable ejercicio práctico para manejar el análisis de headers, archivos maliciosos e implementar una investigación desde la IP del atacante para más información.

