## 🏆 Aquí verás el desafío: Friday Overtime.  
### Te invito a visitar el desafío Trooper 👇
* 👉  [Trooper](Trooper/README.md) - Investigación de TTPs - Aplicación de OpenCTI


## 📌 Desarrollo del Desafío
En este write-up mostraré algunas capturas de pantalla sobre el desafío en cuestión.   
Es Viernes, últimos minutos de la jornada, ya muchos se preparaban para su fin de semana y yo recibí una alerta crítica en la plataforma de CTI. La empresa financiera **SwiftSpend Finance** había detectado actividad sospechosa y necesitaba un análisis **inmediato de posibles amenazas**. 

###
  
**Herramientas usadas:**  
✅ OSINT, MITRE ATT&CK  
✅ Bash, Análisis de IOCs  

## 🛠 Paso 1: Análisis de Malware con DocIntel
* Este correo electrónico simula un escenario de alerta de malware en un entorno corporativo,  lo cual es relevante para el rol de un SOC L1.  
* Se adjuntan IOCs.
* Se solicita analizar la muestra de malware adjunta.

![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/main/imagenes/Overtime-1.png)  

## 🔍 Paso 2: Identificación de Hashes, Técnicas MITRE ATT&CK y Aplicación de Métodología OSINT  
* Inicié la operación desde Bash. Extraje el SHA1 hash del archivo pRsm.dll:
* Identifiqué que pertenecía al framework ***<ins>MgBot</ins>***, usado para ataques dirigidos.
* Mapeé la actividad con MITRE ATT&CK, vinculándolo a la técnica T1123 (Audio Capture).
  
![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/main/imagenes/Overtime-2.png)  
![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/main/imagenes/Overtime-3.png)  
![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/main/imagenes/Overtime-4.png)  

## 🚀 Paso 3: Detección y Compartición de IoCs
* Analicé la URL maliciosa del malware con CyberChef:
* Identifiqué la dirección IP del servidor de comando y control (C&C):

![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/main/imagenes/Overtime-5.png)
![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/main/imagenes/Overtime-6.png) 
![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/main/imagenes/Overtime-7.png) 



