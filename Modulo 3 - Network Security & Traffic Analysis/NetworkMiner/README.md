# 🌐 Investigación con NetworkMiner - Análisis de PCAPs  

## 🕵️‍♂️ Escenario 
### Un correo interno del equipo de Threat Intelligence acaba de llegar: "Hemos detectado actividad sospechosa en la red. Necesitamos que analices estos archivos PCAP y determines si hay indicios de compromiso". Como SOC Analyst Level 1, mi tarea es clara: identificar los sistemas involucrados, analizar la transferencia de datos y extraer cualquier artefacto que pueda ayudarnos a entender qué está ocurriendo en la red.
##

# 📁 Caso 1: Identificación de Host y Análisis de Tráfico
### 📌 ¿Cuál es el nombre del sistema operativo del host 131.151.37.122?  

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/NetworkMiner/1.%20Nombre%20del%20sistema%20operativo.png)

## 📌 Investigación de hosts 131.151.37.122 y 131.151.32.91
### Se detectó un canal de comunicación a través del puerto 1065. Necesitamos determinar cuántos bytes de datos fueron recibidos desde el host 131.151.32.91 hacia 131.151.37.122.

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/NetworkMiner/2.%20Data%20recibida.png)

## 📌 ¿Cuál es el número de secuencia en el frame 9?
### Un detalle crítico en la reconstrucción de la sesión de tráfico.

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/NetworkMiner/3.%20Numero%20de%20Secuencia.png)

# 📁 Caso 2: Análisis de Archivos Extraídos  
### 📌 Identificación de dispositivos USB conectados
### Al analizar los archivos extraídos, encontramos una pista clave: un dispositivo USB que podría haber sido utilizado en la transferencia de datos. Necesitamos determinar la marca del producto.

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/NetworkMiner/4.%20Nombre%20de%20la%20marca%20del%20USB.png)

### 📌 ¿Cuál es la dirección IP de origen de la imagen del pez?
### Entre los archivos capturados, encontramos una imagen de un pez. ¿Cuál es la IP desde la cual se originó?

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/NetworkMiner/5.%20IP%20de%20origen%20de%20la%20imagen.png)

### 📌 Rastreo de credenciales comprometidas
### Encontramos información relacionada con el correo homer.pwned.se@gmx.com. ¿Cuál es la contraseña asociada?

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/NetworkMiner/6.%20Contrase%C3%B1a.png)


# 🎖️ Conclusión
## Este análisis con NetworkMiner me permitió reconstruir eventos clave en la red, identificar posibles compromisos y extraer artefactos forenses esenciales. Asumiendo plenamente el rol de un SOC Analyst Level 1, fue fundamental saber interpretar capturas de tráfico para responder eficazmente ante incidentes.
