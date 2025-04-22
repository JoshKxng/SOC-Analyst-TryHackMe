# 🏆 Sysmon Challenge - El ransomware que se arrepintió

# 📍 *Contexto profesional:*
### Durante mi rotación como Analista SOC L1 Jr., recibimos una alerta proveniente del equipo de atención interna. Una usuaria —empleada de una organización sin fines de lucro que trabaja con información sensible— reportó que su equipo sufrió un comportamiento inusual tras ejecutar un supuesto instalador de antivirus descargado desde un enlace no verificado.

### Según la usuaria, sus archivos quedaron ilegibles, el fondo de pantalla cambió a una nota de rescate, y minutos después todo volvió a la normalidad. Al regresar a su puesto, solo encontró un mensaje en el escritorio que le sugería “revisar su billetera de Bitcoin”.

---

## 🔍 Investigación del Incidente  
### Una vez dentro del entorno comprometido, comenzamos el análisis de logs, cambios en el sistema y comportamiento de red. Se trató de un caso de ransomware peculiar: el atacante ejecutó la infección, pero luego accedió vía RDP al equipo, restauró los archivos y dejó un mensaje final.

---

## 🧩 Detalles Técnicos Detectados  
### La investigación fue conducida con herramientas de monitoreo en endpoint, registros del sistema y correlación de eventos.

---
## Nombre del archivo malicioso descargado | `✅ AvastInstaller.exe`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Sysmon%201/TASK%20-%20A/1.png)

---

## Ubicación de descarga	| `✅ C:\Users\Sophie\Downloads\`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Sysmon%201/TASK%20-%20A/2.png)

---

## Extensión añadida por el ransomware	| ✅ `.dmp`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Sysmon%201/TASK%20-%20A/3.png)

---

## IP de contacto externo del ejecutable | ✅ `10.10.8.111`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Sysmon%201/TASK%20-%20A/4.png)

---

## IP del atacante vía RDP	| ✅ `10.11.27.46`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Sysmon%201/TASK%20-%20B/1.png)
