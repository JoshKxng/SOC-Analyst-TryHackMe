# 🕵️ Escenario SOC: Análisis forense con Autopsy

### Durante una jornada en el SOC, se me asignó una tarea típica en un entorno de análisis forense: revisar una imagen forense con evidencia digital utilizando `Autopsy`, una herramienta ampliamente utilizada para investigaciones en sistemas Windows. El objetivo era detectar indicadores de actividad sospechosa y artefactos de interés en el sistema. El caso incluía múltiples líneas de investigación, desde búsquedas web hasta archivos marcados como interesantes, pasando por contraseñas, notas y análisis de red.
---

## 📌 Preguntas del análisis y hallazgos

### 🔍 1. Qué programa instalado tiene la versión 6.2.0.2962?
### Al inspeccionar la vista de resultados del módulo que analiza programas instalados, identifiqué el software correspondiente a la versión solicitada.
### ✅ `Eraser`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Autopsy/01.png)

---

### 🔐 2. ¿Cuál es la pista de contraseña registrada por un usuario??

### Usé la función de **Keyword Search** con la palabra `secret`, en modalidad de substring. Y lo que razoné fue: si la palabra aparece en varios archivos, el que más impacto tendría sería el que está vinculado a configuraciones de perfiles de usuario. Con esa lógica, localicé un archivo que contenía la pista de contraseña del usuario.
### ✅ `IAMAN`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Autopsy/02.png)

---

### 🌐 3. ¿Qué dirección IP accedió a numerosos archivos etiquetados como SECRET desde una unidad de red?

### Revisando la actividad de archivos etiquetados como interesantes, y cruzando esa información con registros de acceso a unidades de red, localicé la dirección IP relacionada con los archivos “SECRET”.  
### ✅ `10.11.11.128`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Autopsy/03.png)

---

### 🔎 4. ¿Cuál fue el término más buscado en internet por el usuario?

### Explorando los resultados del módulo de historial del navegador, agrupé las búsquedas por frecuencia y logré identificar el término más utilizado.
### ✅ `information leakage cases`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Autopsy/04.png)

---

### 🕒 5. ¿Qué búsqueda web se realizó el 25 de marzo de 2015 a las 21:46:44?

### Gracias a los metadatos temporales asociados a cada búsqueda, filtré por la fecha y hora exacta para obtener la cadena de búsqueda correspondiente.
### ✅ `anti-forensic tools`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Autopsy/05.png)

---

### 💾 6. ¿Cuál es el valor del hash MD5 del ejecutable listado como archivo interesante?
### A través del módulo **Interesting Files Identifier**, Autopsy listó un archivo binario sospechoso junto con su hash MD5. Este tipo de información es vital para realizar búsquedas cruzadas en servicios como VirusTotal.
### ✅ `fe18b02e890f7a789c576be8abccdc99`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Autopsy/06.png)

---

### 🗒️ ¿Qué mensaje motivacional escribió el usuario ‘Informant’ en una nota adhesiva?

### Explorando artefactos de notas adhesivas, localicé un mensaje escrito por el usuario apodado “Informant”. Este tipo de notas puede aportar contexto emocional o motivaciones del usuario, lo cual es útil en investigaciones internas.
### ✅ `Tomorrow...Everything will be OK...`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Autopsy/07.png)

---

# 🎖️ Conclusión
### Este ejercicio fue una excelente oportunidad para aplicar un flujo de trabajo real utilizando Autopsy.

