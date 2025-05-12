# 🏆 Splunk Challenge - Caso de Defacement Web en Wayne Enterprises

### Otro día más como como Analista SOC L1, formé parte del equipo que respondió a un incidente en el cual el sitio web corporativo `imreallynotbatman.com`,
### perteneciente a **Wayne Enterprises**, fue comprometido y **defaceado**. Tuve que analizar el ataque usando la estructura de la Cyber Kill Chain para rastrear el origen, desarrollo y consecuencias del ataque.

---

## 🛰️ Reconocimiento: El primer contacto con el adversario

#### Todo comenzó cuando nuestro sistema IDS (Suricata) levantó una alerta relacionada con una vulnerabilidad específica, lo que nos permitió asociarla a un **CVE conocido**. Esta alerta fue el primer indicio de que alguien estaba explorando activamente nuestras superficies de ataque.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%204/01.png)
#### Al revisar los registros del servidor web, descubrimos que el sistema vulnerable estaba basado en un **CMS popular**. Los patrones en los logs y los encabezados del User-Agent revelaron que el atacante estaba utilizando **Acunetix**, una herramienta automatizada de escaneo de vulnerabilidades web.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%204/03.png)

---

## 🛠️ Explotación: Acceso no autorizado confirmado

#### Una vez identificado el reconocimiento, pasamos a analizar los intentos de explotación. Observamos una serie de **intentos de fuerza bruta** dirigidos contra el panel de administración del CMS. Gracias a los registros, descubrimos que los ataques estaban enfocados al usuario `admin`, y que finalmente uno de los intentos fue exitoso al utilizar la contraseña correcta.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Splunk%20Challenge/TASK%205/02.png)
#### Se realizaron **142 intentos únicos de contraseña**, lo que confirmó que se trataba de un ataque automatizado. La IP de origen de este ataque fue **23.22.63.114**, mientras que la IP que realizó el login exitoso al panel de administración fue **40.80.148.42**, posiblemente para disociar la etapa de reconocimiento/explotación de la de ejecución.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%205/03.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%205/04.png)
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Splunk%20Challenge/TASK%205/05.png)

---

## 💿 Instalación: El atacante introduce malware

#### Con acceso administrativo, el atacante logró subir un archivo ejecutable malicioso al sistema. Este ejecutable fue capturado por Sysmon, que nos proporcionó su **hash MD5**, el cual luego analizamos en VirusTotal. El malware estaba identificado con otro nombre alternativo, lo que nos permitió expandir nuestra investigación sobre su comportamiento conocido.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Splunk%20Challenge/TASK%206/01.png)

#### Además, identificamos que el archivo fue ejecutado por un usuario específico del sistema, lo que refuerza la evidencia de una **ejecución manual posterior al acceso remoto**.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%206/02.png)

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%206/03.png)

---

## 🎯 Acción sobre el objetivo: Website defaceado

#### Luego de establecer presencia en el sistema, el atacante modificó el sitio web de la empresa, subiendo un archivo con fines de **defacement**. A través del análisis de tráfico saliente, detectamos una conexión hacia un dominio sospechoso desde donde se descargó una imagen utilizada para alterar visualmente la página principal.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%207/01.png)
#### Simultáneamente, nuestro firewall Fortigate detectó intentos de **SQL Injection** provenientes de la IP **40.80.148.42**, que activaron una regla de protección específica configurada previamente. Esto confirma que el atacante intentó múltiples vectores en paralelo para acceder a más información del backend.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Splunk%20Challenge/TASK%207/02.png)

-----

## 💬 Comando y Control: Resolución dinámica sospechosa

Durante el análisis de comunicaciones externas, observamos que el sistema comprometido realizaba conexiones hacia un **dominio dinámico sospechoso**, asociado con infraestructura maliciosa. Esta técnica es común entre grupos APT, ya que les permite cambiar dinámicamente la IP del servidor de C2 (Command & Control).

El FQDN utilizado para resolver hacia la IP atacante fue esencial para trazar la relación entre los eventos internos y el ecosistema externo del atacante.

---

## 🔧 Armas preconfiguradas: Infraestructura de ataque

#### Gracias al cruce de datos con plataformas como Robtex y VirusTotal, encontré una dirección de correo asociada a esta infraestructura: **Lillian.rose@po1s0n1vy.com**, vinculada al grupo APT conocido como **P01s0n1vy**.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%209/02.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%208/01.png)

---

## 📦 Entrega del Malware: Último eslabón

#### En la etapa final de la Kill Chain, identificamos el malware asociado con esta campaña: **`MirandaTateScreensaver.scr.exe`**. Este archivo, detectado por múltiples motores antivirus, posee un **hash MD5 único** que logramos extraer y verificar en bases públicas.
#### Este ejecutable parece haber sido preparado como un segundo vector de ataque en caso de que la primera cadena de infección fallara, lo cual indica **sofisticación y redundancia** en las tácticas del atacante.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Splunk%20Challenge/TASK%209/01.png)

---

# 🎖️ Conclusión
#### Este incidente se trató de una **campaña planificada**, con elementos de automatización, infraestructura preconfigurada, técnicas de evasión y múltiples fases encadenadas, tal como lo plantea el modelo de la **Cyber Kill Chain**.


