# 🏆 Osquery - Challenge: Análisis de Actividad Sospechosa en un Endpoint
# 🎯 *Contexto del caso:*

### Durante un turno de monitoreo como Analista SOC Jr., se me asignó la tarea de revisar un host con actividad sospechosa utilizando Osquery. El objetivo era recolectar evidencia sobre posibles intentos de borrar rastros, conexiones ocultas y archivos que se ejecutan automáticamente en el sistema.

---

### A continuación, documento cómo abordé cada requerimiento técnico a través de consultas SQL en Osquery, simulando una investigación forense en un entorno real de trabajo.

## 📌 1. Detección de herramienta para eliminación de rastros
Una revisión inicial de las tablas de procesos reveló que uno de los usuarios ejecutó una aplicación diseñada para eliminar trazas del sistema.
🔍 Programa detectado: [nombre del ejecutable]
Este hallazgo fue clave para escalar el incidente, ya que indica un posible intento de antiforense.

📌 2. Detección de VPN instalada en el host
Se me solicitó identificar la presencia de software VPN. A través de una consulta en la tabla de paquetes instalados (programs), logré detectar la aplicación utilizada.
🔍 VPN instalada: [nombre del software]
Este tipo de software podría estar facilitando conexiones remotas no autorizadas, por lo que fue marcado para monitoreo.

📌 3. Servicios activos en el sistema
Ejecuté una consulta a la tabla services para determinar la cantidad de servicios en ejecución en el host.
🔍 Servicios activos: [cantidad]
Esto me dio una idea del nivel de actividad general en el equipo y posibles vectores de ataque persistentes.

📌 4. Identificación de ejecutables en autoejecución
Al inspeccionar la tabla autoexec, detecté un archivo .bat configurado para ejecutarse automáticamente.
🔍 Archivo sospechoso: [nombre_del_batch.bat]
Este tipo de archivos pueden contener scripts maliciosos que se ejecutan sin intervención del usuario.

📌 5. Ruta completa del archivo .bat
Para cerrar el análisis, localicé la ubicación exacta del archivo batch dentro del sistema.
🗂️ Ruta absoluta: [C:\Ruta\completa\archivo.bat]
La evidencia fue documentada y reportada al equipo de respuesta para su análisis profundo.
