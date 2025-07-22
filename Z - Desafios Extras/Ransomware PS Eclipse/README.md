# 🧠 Análisis SOC – Ramsomware PS Eclipse (TryHackMe)

## 📌 Descripción del escenario

🔍 En esta práctica simulada trabajamos como Analista SOC para un **MSSP** llamado `TryNotHackMe`. Un cliente reportó actividad sospechosa en la máquina de un empleado llamado 👨‍💼 **(Keegan)** el día **lunes 16 de mayo de 2022**. Aunque el equipo seguía operativo, algunos archivos aparecían con **extensiones extrañas**, lo cual generó la sospecha de un posible ataque de **ransomware**. Mi tarea fue investigar lo ocurrido usando **Splunk** como herramienta principal.

---

## 🎯 Objetivo

Determinar si realmente hubo un intento de ransomware en el equipo afectado, identificando:
- Descargas sospechosas
- Comportamientos anómalos
- Conexiones remotas
- Evidencias en el sistema (IOCs)

---
### 1️⃣ ¿Qué binario sospechoso fue descargado en el endpoint?
Primero filtré por el campo `DestinationIp`. Allí vemos que la primer IP tiene un valor totalmente desproporcionado comparado con las otras IPs que tienen 76, 4, 3, 2 o 1 conexión. Luego filtré por el campo `Image` donde encontramos la ruta de malware en cuestión.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q1/01.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q1/02.png)

---

### 2️⃣ ¿Desde qué dirección fue descargado el binario?  
Una vez que ya localicé el .exe procedí a visualizar que me mostraba el campo **ParentCommandLine** para ver cómo se ejecutó el proceso padre. Luego procedí a decodificarlo en la shell y por último pasarlo por Cyberchef como lo pedía la consigna.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q2/01.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q2/02.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q2/02a.png)

---

### 3️⃣ ¿Qué ejecutable de Windows fue usado para descargar el binario sospechoso?  
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q3/01.png)

---

### 4️⃣ ¿Qué comando fue ejecutado para configurar el binario sospechoso con privilegios elevados?
Acá ya entré en el punto cúlmine de la investigación. Como podemos ver, la parte `/RU SYSTEM` significa `"Run User SYSTEM"`.  
Esto es crucial porque está configurando el .exe con los máximos privilegios posibles, no solo como administrador sino mucho más potente.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q4/01.png)

---

### 5️⃣ ¿A qué dirección se conectó el binario sospechoso?
Para agilizar la busqueda, en esta parte agregamos el campo `QueryName` porque cuando se trata de eventos de DNS,  
`QueryName` es un campo común que contiene el nombre de dominio o el host que se estuvo buscado.

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q6/01.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q6/02.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q6/03.png)

---

### 6️⃣ Se descargó un script de PowerShell en la misma ubicación del binario sospechoso. ¿Cuál es el nombre del archivo?
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q8/01.png)

---

### 7️⃣ El Script malicioso fue marcado como tal. ¿Cuál crees que era su nombre real?
Extraemos el hash y dentro de VirusTotal podemos visualizar el nombre real de este Script. `BlackSun.ps1`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q9/01.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q9/02.png)

---

### 8️⃣ Se guardó una nota de ransomware en el disco, que puede servir como IOC. ¿Cuál es la ruta completa donde se guardó la nota de rescate?
Filtrando por el nombre de nuestro Script malicioso, agilizamos nuestra búsqueda.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q10/01.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q10/02.png)

---
### 9️⃣ El script guardó un archivo de imagen en el disco para reemplazar el fondo de pantalla del usuario, que también puede servir como IOC. ¿Cuál es la ruta completa de la imagen?
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/PS%20Eclipse/Q11/01.png)

# 🎖️ Conclusión

## Este desafío fue un excelente caso para prácticar y entender mejor cómo se mueve una amenaza dentro de un sistema. Desde la descarga de un binario malicioso hasta la creación de notas de rescate.
