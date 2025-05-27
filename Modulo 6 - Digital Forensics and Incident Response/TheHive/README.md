# 🐝 Análisis de Exfiltración FTP con TheHive
---

## 🎯 Objetivo
Como parte del entrenamiento en análisis de incidentes y manejo de casos en un entorno SOC, se nos presenta un escenario en el que debemos investigar una posible `exfiltración de datos` a través de FTP. En este caso, se nos proporciona un archivo `.pcap` con la captura del tráfico de red, y se espera que utilicemos `TheHive` para gestionar el proceso de investigación.

---

## ⚙️ Pasos realizados en TheHive

### 1. 📁 Creación del Caso

#### Primero, abrí un nuevo caso en TheHive titulado `Analisis FTP`, asignándole una severidad `media (M)`, etiquetado con `TLP:AMBER` y `PAP:GREEN`, lo cual es apropiado para compartir la información dentro de un equipo de respuesta, manteniendo un nivel adecuado de confidencialidad.

> **Descripción del caso:**  
> *"Este caso aborda el análisis de tráfico de red, tras sospechar una exfiltración de datos."*

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/TheHive/01.png)

---

### 2. 👁️‍🗨️ Carga del Observable

#### A continuación, añadí el archivo `Analisis FTP.pcap` como un `observable` de tipo `file`, etiquetado con palabras clave:  `FTP`, `PCAP`, `Data Exfiltration`, `Prueba`.
#### También incluí una descripción clara del propósito del observable:
> *"Captura de tráfico de red que muestra una posible exfiltración de datos a través de FTP."*
#### Esto permite trazar una línea clara de auditoría y asociar este archivo a una investigación concreta dentro del entorno de TheHive.

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/TheHive/02.png)

---

### 3. 🔍 Revisión del Contenido y Obtención del Flag

#### Una vez subido el observable, y siguiendo el análisis del tráfico FTP, identifiqué la dirección de destino: `http://10.10.133.58/files/flag.html`
#### Al acceder a este enlace, logré capturar la flag:

> `THM{FILES_ARE_OBSERVABLERS}`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/TheHive/03.png)

---

# 🎖️ Conclusión
## Me pareció una herramienta excelente porque una vez que haces el análisis por fuera (usando Wireshark por ejemplo) y encontrás algo importante, puedo usar TheHive para documentar y trabajar en equipo de forma ágil. Sin perder tiempo.
