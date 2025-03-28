# 📊 Brim - Análisis de tráfico y detección de amenazas
## 📅 La jornada transcurre sin incidentes graves hasta que un ticket prioritario llega a nuestro dashboard. Un cliente ha reportado actividad sospechosa en su red y necesita un análisis inmediato. Como Analista SOC Nivel 1, mi tarea es revisar los logs de tráfico con Brim y correlacionar eventos para identificar posibles amenazas.
---

# 🚨 1 - Análisis inicial de tráfico y alertas 

### 📂 Se identificaron archivos sospechosos en la red. ¿Cuál es el nombre del archivo GIF detectado?**  
### ✅ Cat01_with_hidden_text.gif

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/BRIM/1%20-%20File_Name.png)

---

## 📌 Alertas de Suricata:
### 📂 Suricata ha generado alertas bajo la categoría "Potential Corporate Privacy Violation". ¿Cuál es el Signature ID asociado?
### ✅ 2,012,887

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/BRIM/3%20-%20Signature.png)

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/BRIM/4%20-%20Signature.png)

---

# 🚨 2 - Detección de CobaltStrike en la red
### 📥 Se detectó una posible descarga desde un servidor de CobaltStrike C2. ¿Cuál es el nombre del archivo descargado?  
### ✅ 4564.Exe

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/BRIM/Pcap6%20-1.png)

---

## 📌 Análisis de conexiones en puertos críticos:
### 🔗 Se identificaron múltiples conexiones CobaltStrike en la red. ¿Cuántas conexiones utilizaron el puerto 443?  
### ✅ 328

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/BRIM/Pcap6%20-%202.png)

# 🎖️ Conclusión:
## Este análisis realizado con Brim me permitió detectar actividad maliciosa en la red, correlacionando conexiones y eventos de seguridad en tiempo real. Esta información es clave para generar reportes de incidentes y tomar medidas preventivas.

