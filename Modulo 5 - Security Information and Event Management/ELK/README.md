# 🕵️‍♂️ ItsyBitsy - Investigación de comunicación C2 con ELK Stack

## 🧠 Escenario

Durante una jornada habitual en el SOC, recibimos una alerta de nuestro sistema IDS relacionada con una **posible comunicación C2 proveniente del usuario Browne**, perteneciente al departamento de Recursos Humanos.

Como Analista SOC Nivel 1 Jr., mi responsabilidad fue realizar la investigación preliminar para confirmar o descartar actividad maliciosa. Debido a limitaciones operativas, únicamente se recolectaron y cargaron los **logs HTTP de conexión** en el índice `connection_logs` de Kibana, abarcando una semana completa de actividad.

---

## 🔎 Paso a paso de la investigación

### 📅 1. ¿Cuántos eventos fueron registrados durante marzo de 2022?

Para empezar, filtré por el rango de fechas correspondiente a marzo de 2022. Esto me permitió tener un panorama general del volumen de eventos HTTP disponibles en el índice **`connection_logs`**.  
✅ **Resultado:** **`1.482`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/ELK%20Challenge/01.png)

---

### 🌐 2. ¿Cuál es la IP asociada al usuario sospechoso?

A continuación, exploré los registros en búsqueda de la IP vinculada al usuario. Utilicé los campos `source_ip` y analicé su frecuencia. Observé que había **una IP con presencia muy reducida respecto al resto**, lo cual me llamó la atención.  
✅ **Resultado:** **`192.166.65.54`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/ELK%20Challenge/02.png)

---

### 🧰 3. ¿Qué binario legítimo de Windows fue usado para descargar un archivo desde el servidor C2?

El siguiente objetivo era identificar si se había utilizado algún binario legítimo del sistema operativo para descargar contenido malicioso, una táctica común conocida como *Living Off The Land Binaries (LOLBins)*.

Revisando los campos de los logs, encontré en `user_agent` la cadena **`bitsadmin`**, un binario clásico que puede ser abusado para realizar descargas desde la línea de comandos.  
✅ **Resultado:** **`bitsadmin`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/ELK%20Challenge/03.png)

---

### ☁️ 4. ¿A qué sitio de archivos se conectó la máquina infectada?

Mediante los mismos registros, identifiqué que la IP sospechosa había establecido comunicación con un dominio conocido: **`pastebin.com`**, una popular plataforma de almacenamiento de texto plano. Esta técnica es frecuentemente utilizada por actores maliciosos para alojar cargas útiles o instrucciones de comando y control.  
✅ **Resultado:** **`pastebin.com`**
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/ELK%20Challenge/04.png)

---

### 🔗 5. ¿Cuál es la URL completa del C2 con la que se conectó el host infectado?

El campo **`uri`** junto con **`host`** me permitió reconstruir la URL exacta accedida por la máquina comprometida:

- **`host`**: **`pastebin.com`**
- **`uri`**: **`/yTg0Ah6a`**

Al unir ambos componentes:

✅ **Resultado:** **`pastebin.com/yTg0Ah6a`**

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/ELK%20Challenge/05.png)

---

### 📄 6. ¿Qué archivo fue accedido en el sitio y qué código secreto contenía?

Aunque los logs no mostraban directamente el contenido del archivo descargado ni su nombre, el contexto de la simulación indicaba que el enlace contenía un archivo accesible. En un entorno real, esta información podría obtenerse mediante inspección profunda de paquetes o mediante herramientas de análisis forense en endpoints.
En este caso, la plataforma simuló que el nombre del archivo era visible como parte del contenido del enlace accedido. Por lo tanto ingresé a **`pastebin.com/yTg0Ah6a`** y allí se encontraba el archivo **`secret.txt`** el cual contenia el código secreto.
✅ **Resultado:** **`secret.txt`**  
✅ **Resultado:** **`THM{SECRET__CODE}`**  

![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/ELK%20Challenge/06.png)

---
# 🎖️ Conclusión
### Fue un desafío muy entretenido y prospero porque pude simular una investigación real dentro de un SOC, donde con recursos limitados **(solo logs HTTP)**, pude rastrear una actividad anómala desde una alerta IDS inicial hasta identificar:

- El host comprometido.
- El binario usado para la descarga.
- La infraestructura de comando y control utilizada.
- El archivo accedido y su contenido malicioso.

