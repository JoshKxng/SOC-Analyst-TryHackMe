# 🏆 Wazuh - Challenge: Endpoint Monitoring Investigation
## 🎯 *Contexto profesional:*

Como parte de un ejercicio de validación de controles, el equipo de seguridad de **Swiftspend Finance** ejecutó una serie de simulaciones en un endpoint monitoreado con **Wazuh** y **Sysmon**, entre las 12:00 y las 20:00 hs del 29 de abril de 2024. El objetivo: medir la capacidad del sistema de monitoreo para detectar amenazas reales y evaluar la respuesta del analista ante un posible compromiso del host.

Bajo la supervisión del Senior Security Engineer **John Sterling**, fui asignado para llevar a cabo una investigación completa del incidente simulado. Esta tarea reflejó fielmente un entorno real de trabajo en un Security Operations Center (SOC), y consistió en analizar eventos registrados por Wazuh para:

- Detectar vectores de acceso inicial.
- Identificar persistencia en el sistema.
- Reconocer técnicas de escalada de privilegios y exfiltración de datos.

---

# 🔎 Proceso de análisis y hallazgos
## 1️⃣ Acceso inicial: archivo malicioso descargado

### Uno de los primeros indicadores de compromiso fue la ejecución de un archivo descargado que permitió el acceso inicial al sistema. Para detectar esta actividad, tuve que probrar con varios filtros, el que me sirvió fue 👉 `rule.description: *download* OR *network* OR *suspicious*`. Una vez aplicado, inspeccioné varios eventos en `data.win.eventdata.commandLine` que incluían comandos como `powershell -c`, `Invoke-WebRequest`.
### El archivo malicioso es ✅SwiftSpend_Financial_Expenses.xlsm
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wazuh/02.png)
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wazuh/02b.png)

---

## 2️⃣ Tarea programada maliciosa
### Poco después del acceso inicial, se estableció persistencia mediante la creación de una tarea programada (`schtasks`). Esta técnica permite al atacante mantener el acceso al sistema incluso luego de un reinicio.
### Filtré eventos de schtasks con varios filtros sin suerte, hasta que lo simplifiqué a 👉 `data.win.eventdata.commandLine: *schtasks*` y corroboré que se trataba de una tarea automatizada destinada a relanzar código malicioso.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wazuh/03.png)

---
## 3️⃣ Contenido codificado detectado
### Durante la fase de persistencia, noté una cadena codificada en Base64 que llamó mi atención. Al reconocer esta codificación, decidí decodificarla y confirmé mis sospechas.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wazuh/04.png)
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wazuh/04b.png)

---
## 4️⃣ Creación de usuario con contraseña sospechosa
### En este punto, la investigación se puso más interesante y más difícil. Apliqué muchos filtros y ninguno me servía. Entonces ajusté mi estrategía y decidí no perderme entre cientos de logs y enfoqué mis ojos en lo que estaba buscando. Por lo tanto, despues de muchos intentos fallidos apliqué el filtro de 👉 `cmd.exe /c net user` y agregué la columna `data.win.eventdata.commandLine` para visualizar de manera más practica lo que estaba buscando.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wazuh/05.png)

---

## 5️⃣ Herramienta de volcado de credenciales
### Acá busqué evidencias de robo de credenciales. Apliqué el filtro `data.win.eventdata.commandLine: *dump*` que me permitió rastrear esta etapa de la intrusión. y entre varios `.exe` sospechosos, detecté el uso de una herramienta no convencional: `memotech.exe`.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wazuh/06.png)

---
## 6️⃣ Exfiltración de datos y descubrimiento de la flag 
### La etapa final del ataque fue la exfiltración de datos sensibles mediante PowerShell y servicios externos (Pastebin). En esta transmisión, el atacante incluyó una *flag de evaluación* que sirvió como validación del análisis exitoso. El filtro que me sirvió para encontrar esta flag fue `cmd.exe /c net user ...`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Wazuh/07.png)

# 🎖️ Conclusión
## Este análisis simulado fue, hasta el momento, una de las experiencias más inmersivas y realistas de mi formación. Me llevó a desafiarme a mi mismo como nunca antes. Durante el proceso, fue prueba y error muchas veces. Comandos que no me llevaban a ninguna parte y otros que me acercaban a lo que me decía mi intuición. Entendí que a veces, un enfoque preciso y calibrar la mirada me van a llevar a destino. Más cuando trabajamos con cientos y cientos de logs a diaro. Una experiencia enriquecedora en todo sentido.

