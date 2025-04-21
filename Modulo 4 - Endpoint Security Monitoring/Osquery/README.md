# 🏆 Osquery - Challenge: Análisis de Actividad Sospechosa en un Endpoint
# 🎯 *Contexto del caso:*

### Durante un turno de monitoreo como Analista SOC Jr., se me asignó la tarea de revisar un host con actividad sospechosa utilizando Osquery. El objetivo era recolectar evidencia sobre posibles intentos de borrar rastros, conexiones ocultas y archivos que se ejecutan automáticamente en el sistema.  A continuación, documento cómo abordé cada requerimiento técnico a través de consultas SQL en Osquery, simulando una investigación forense en un entorno real de trabajo.

---

## 🧹 1. Herramienta para eliminar rastros del sistema
## Al revisar los procesos activos, encontré que uno de los usuarios había ejecutado una herramienta diseñada para borrar huellas del sistema. Este tipo de actividad suele estar asociada a intentos de ocultamiento, así que lo marqué como un posible indicio de antiforense.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Osquery/2.png)

---

## 🔐 2. Software VPN instalado
## Me pidieron verificar si el equipo tenía alguna VPN instalada. Usando una consulta sobre los programas registrados, identifiqué una aplicación que podría estar siendo usada para establecer conexiones remotas fuera del control corporativo. La dejé registrada para seguimiento. `✅ProtonVPN`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Osquery/3.png)

---

## ⚙️ 3. Servicios activos en ejecución
## Consulté la tabla `services` para tener un panorama de cuántos servicios estaban corriendo en el host. Esto me ayudó a dimensionar la actividad del sistema y pensar en posibles puntos de entrada o persistencia.`✅214`
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Osquery/4.png)

--- 

## 📄 4. Archivo .bat en autoejecución
## Al inspeccionar la tabla `autoexec`, detecté un archivo .bat que se ejecutaba automáticamente. Este tipo de archivos puede ser aprovechado para cargar scripts maliciosos al inicio del sistema, así que lo marqué para análisis posterior.
![](https://raw.githubusercontent.com/JoshKxng/SOC-Analyst-TryHackMe/refs/heads/main/imagenes/Osquery/5a.png)

---

## 🗂️ 5. Ruta completa del archivo .bat
## Finalmente, localicé la ruta exacta donde estaba ese archivo .bat. Tener este dato fue clave para adjuntar la evidencia al informe y escalar el caso al equipo de respuesta.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Osquery/6.png)
