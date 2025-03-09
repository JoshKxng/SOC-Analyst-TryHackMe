# 🏆 DESAFÍO - ZEEK

## 🛡️ Nuestro equipo ha recibido una alerta: **"Anomalous DNS Activity"**. Como analista SOC L1, me han asignado la responsabilidad de investigar esta alerta y determinar si se trata de un **True Positive** o un **False Positive**. Para ello, analizaremos los registros generados a partir del archivo *pcap*.

---

### ✅ **Paso 1: Análisis del Tráfico DNS**

Antes de tomar cualquier decisión, vamos a analizar el archivo **dns.log**, que contiene información detallada sobre las consultas DNS registradas en la captura y vamos a buscar cuántos registros DNS están vinculados a la dirección IPv6. Se nos avisa que los registros DNS **"AAAA"** almacenan direcciones IPV6.

![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/0dc6b0fb447af7f5cbbaf6aa2cfcfd443cd09224/imagenes/Zeek/Zeek-DNS/Zeek%201.png)

### 💡 El análisis revela que existen **"320"** registros con direcciones IPv6, lo que sugiere una cantidad inusual de actividad DNS en la red.

---

### ✅ **Paso 2: Identificación de Conexiones Sospechosas**

El siguiente paso es inspeccionar las conexiones para encontrar actividades inusuales. Para ello, analizamos el **conn.log**, que contiene información detallada sobre las conexiones establecidas en la red. Aquí buscaremos cuál es la duración de la conexión más larga.

![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/refs/heads/main/imagenes/Zeek/Zeek-DNS/Zeek%202.png)

### 💡 El resultado muestra que la conexión más larga duró **"9.420791" segundos**, lo cual es un posible indicio de actividad maliciosa si lo comparamos con el comportamiento normal de la red.

---

### ✅ Paso 3: Identificación de Consultas de Dominio Únicas

Para detectar patrones sospechosos en las consultas DNS, analizamos la cantidad de dominios únicos consultados. Buscaré cuantas consultas de dominio únicas hay en los registros DNS.

![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/0dc6b0fb447af7f5cbbaf6aa2cfcfd443cd09224/imagenes/Zeek/Zeek-DNS/Zeek%203.png)

### 💡 El resultado indica que hay **"5" consultas únicas**, lo que podría indicarnos una actividad anómala si los dominios no son legítimos o si están relacionados con **DNS Tunneling**.

---

### ✅ **Paso 4: Identificación del Host de Origen**

Uno de los patrones clásicos de abuso de DNS es el **uso masivo de consultas dirigidas al mismo dominio**, lo que podría ser un intento de tunneling o exfiltración de datos.
Aquí buscaré cuál es la dirección IP del host que originó esta actividad sospechosa.

![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/0dc6b0fb447af7f5cbbaf6aa2cfcfd443cd09224/imagenes/Zeek/Zeek-DNS/Zeek%204.png)

### 💡 El análisis muestra que la IP de origen es **"10.20.57.3"**, lo que confirma que un único host ha estado generando un volumen inusualmente alto de consultas DNS a un dominio en particular. 🔍

---

## 🎖️ **Conclusión**

#### Tras este análisis, hemos recopilado suficiente evidencia para determinar que la alerta de "Anomalous DNS Activity" es un True Positive. Nuestro resultado puede sugerir la posibilidad de un **DNS Tunneling** o exfiltración de datos. Este caso será escalado al equipo de respuesta a incidentes para una investigación más profunda y la mitigación de la amenaza.

