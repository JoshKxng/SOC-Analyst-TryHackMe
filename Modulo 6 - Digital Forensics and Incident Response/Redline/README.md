# 🏮 Redline - Desafio de Análisis Forense

### Durante una jornada laboral habitual como Analista SOC Jr. en entrenamiento, se me asignó una tarea urgente: uno de los equipos de la red mostraba comportamiento anómalo y se sospechaba una posible intrusión. Mi objetivo fue realizar un análisis de memoria para identificar cualquier `Indicador de Compromiso (IOC)` y rastrear la actividad del intruso.

---

## 🛠️ Metodología Aplicada

La investigación se desarrolló en las siguientes fases:

1. **Recolección de datos** desde un endpoint sospechoso con Redline Collector.
2. **Análisis del volcado de memoria** y eventos del sistema operativo con Redline.
3. **Identificación de IOCs** utilizando el IOC Search Collector.
4. **Revisión de tareas programadas, logs de eventos y archivos sospechosos.**
5. **Documentación detallada de hallazgos clave.**

---

### 🖥️ 1. ¿Qué sistema operativo se detectó en el equipo comprometido?
### ✅ `Windows Server 2019 Standard 17763`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Redline/01.png)

---

### ⏰ 2. ¿Qué tarea programada sospechosa se creó en el equipo?
### Detecté una tarea programada maliciosa que ejecutaba un archivo sospechoso en intervalos regulares, lo cual coincidía con los picos de tráfico anómalo detectados.
### ✅ `MSOfficeUpdateFa.ke`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Redline/02.png)

---

### 📝 3. ¿Qué mensaje dejó el intruso dentro de la tarea programada?  
### El atacante incluyó un mensaje personalizado, posiblemente con intenciones de intimidar o marcar su presencia. Este tipo de comportamiento se ha visto en campañas de malware dirigidas.
### ✅ `THM-p3R5IStENCe-m3Chani$m`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Redline/03.png)

---

### 📚 4. Se creó un nuevo evento del sistema con el nombre de origen “THM-Redline-User” y tipo “ERROR”. ¿Cuál fue el ID de ese evento?
### Tras filtrar los eventos por origen y tipo, identifiqué el **Event ID** específico asociado a la actividad del intruso. ✅ `546`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Redline/04.png)


---

### 💬 5. ¿Cuál fue el mensaje contenido dentro de ese evento del sistema?
### El mensaje brindó contexto adicional sobre las acciones del atacante y reforzó la relación con el archivo ejecutado por la tarea programada.
### ✅ `Someone cracked my password. Now I need to rename my puppy-++-`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Redline/05.png)

---

### 🌐 6. ¿Desde qué URL se descargó el archivo con la bandera?
### Rastreando las conexiones de red y rutas sospechosas, encontré la **URL completa** desde la que se descargó un archivo clave relacionado con la intrusión.
### ✅ `https://wormhole.app/download-stream/gI9vQtChjyYAmZ8Ody0AuA`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Redline/06a.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Redline/06b.png)

---

### 🗂️ 7. ¿Dónde se almacenó ese archivo en el sistema y qué mensaje dejó el atacante dentro de él?
### Identifiqué la `ruta completa del archivo` descargado y analicé su contenido. Nuevamente, el atacante había dejado un mensaje, esta vez incrustado dentro del archivo, posiblemente con fines de burla o para señalar una victoria temporal.
### ✅ `C:\Program Files (x86)\Windows Mail\SomeMailFolder\flag.txt`
### ✅ `THM{600D-C@7cH-My-FR1EnD}`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Redline/07.png) 

---

# 🎖️ Conclusión
## Esta simulación fue una excelente oportunidad para aplicar técnicas forenses reales en un entorno controlado. La experiencia reforzó mi capacidad para investigar compromisos en endpoints, un paso clave en mi camino como Analista SOC L1.

