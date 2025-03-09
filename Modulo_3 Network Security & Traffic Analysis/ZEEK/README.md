# 🏆 DESAFÍO - ZEEK

## 🛡️ Nuestro equipo ha recibido una alerta: **"Anomalous DNS Activity"**. Como analista SOC, me han asignado responsabilidad de investigar esta alerta y determinar si se trata de un **True Positive** o un **False Positive**. Para ello, analizaremos los registros generados a partir del archivo *pcap*. 🛡️

---

### ✅ **Paso 1: Análisis del Tráfico DNS**

Antes de tomar cualquier decisión, vamos a analizar el archivo **dns.log**, que contiene información detallada sobre las consultas DNS registradas en la captura
Y vamos a buscar cuántos registros DNS están vinculados a la dirección IPv6. Se nos avisa que los registros DNS **"AAAA"** almacenan direcciones IPV6.

Utilizamos el siguiente comando para filtrar las entradas del log relacionadas con IPv6:

![](https://raw.githubusercontent.com/JoshKxng/SOC-Level-1-THM/0dc6b0fb447af7f5cbbaf6aa2cfcfd443cd09224/imagenes/Zeek/Zeek-DNS/Zeek%201.png)

### 💡 El análisis revela que existen **320** registros con direcciones IPv6, lo que sugiere una cantidad inusual de actividad DNS en la red.

---

### **Paso 2: Identificación de Conexiones Sospechosas**

El siguiente paso es inspeccionar las conexiones para encontrar actividades inusuales. Para ello, analizamos el **conn.log**, que contiene información detallada sobre las conexiones establecidas en la red.

**Pregunta 2:** ¿Cuál es la duración de la conexión más larga?

Ejecutamos el siguiente comando para encontrar la conexión con la mayor duración:

```bash
cat conn.log | zeek-cut duration | sort -nr | head -1
```

📌 *Imagen adjunta mostrando la ejecución y el resultado obtenido.*

🔄 El resultado muestra que la conexión más larga duró **X segundos**, lo cual es un posible indicio de actividad maliciosa si se compara con el comportamiento normal de la red. 🔄

---

### **Paso 3: Identificación de Consultas de Dominio Únicas**

Para detectar patrones sospechosos en las consultas DNS, analizamos la cantidad de dominios únicos consultados.

**Pregunta 3:** ¿Cuántas consultas de dominio únicas hay en los registros DNS?

Ejecutamos el siguiente comando:

```bash
cat dns.log | zeek-cut query | sort | uniq | wc -l
```

📌 *Imagen adjunta mostrando la ejecución y el resultado obtenido.*

🌐 El resultado indica que hay **X consultas únicas**, lo que podría indicar una actividad anómala si los dominios no son legítimos o si están relacionados con **DNS Tunneling**. 🌐

---

### **Paso 4: Identificación del Host de Origen**

Uno de los patrones clásicos de abuso de DNS es el **uso masivo de consultas dirigidas al mismo dominio**, lo que podría ser un intento de tunneling o exfiltración de datos.

**Pregunta 4:** ¿Cuál es la dirección IP del host que originó esta actividad sospechosa?

Ejecutamos el siguiente comando para identificar la IP de origen:

```bash
cat conn.log | zeek-cut id.orig_h | sort | uniq -c | sort -nr | head -1
```

📌 *Imagen adjunta mostrando la ejecución y el resultado obtenido.*

🔍 El análisis muestra que la IP de origen es **X.X.X.X**, lo que confirma que un único host ha estado generando un volumen inusualmente alto de consultas DNS a un dominio en particular. 🔍

---

### **Conclusión**

🎉 Tras el análisis, hemos recopilado suficiente evidencia para determinar que la alerta de **"Anomalous DNS Activity"** es un **True Positive**. La combinación de **un alto número de registros vinculados a IPv6**, **una conexión de larga duración**, **un gran número de consultas únicas** y **una única IP generando tráfico masivo** sugiere la posibilidad de **DNS Tunneling** o exfiltración de datos. 🎉

Este caso será escalado al equipo de respuesta a incidentes para una investigación más profunda y la mitigación de la amenaza.

---

📝 *Todos los comandos y capturas de pantalla utilizadas en esta investigación están disponibles en mi repositorio de GitHub.*

