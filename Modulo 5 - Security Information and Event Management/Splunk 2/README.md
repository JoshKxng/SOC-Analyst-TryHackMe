# 🏆 Splunk Challenge - Investigating with Splunk

## 📘 Contexto

Durante un turno habitual en el SOC, se nos notificó una alerta generada por un sistema EDR que reportaba **comportamiento anómalo en uno de los hosts del dominio interno**. Según los primeros registros, se detectó una posible **creación de una cuenta sospechosa** y la ejecución de **comandos PowerShell**. 
Mi rol como **Analista SOC L1 Jr.** fue revisar minuciosamente los eventos de seguridad en Splunk, correlacionar logs y construir una narrativa clara de los movimientos del adversario. Lo que inicialmente parecía una actividad menor, escaló rápidamente cuando identifiqué un patrón de **persistencia mediante una cuenta backdoor** y un intento de **recolección y exfiltración a través de web requests**.

---

### 🧑‍🚪 ¿Qué nombre tenía el nuevo usuario backdoor creado en uno de los hosts infectados?  
### ✅ **`a1berto`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/01.png)

---

### 🧾 ¿Cuál es la ruta completa de la clave del registro que fue modificada respecto al nuevo usuario backdoor?  
### ✅ **`HKLM\SAM\SAM\Domains\Account\Users\Names\A1berto`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Investigating%20with%20Splunk/02.png)

---

