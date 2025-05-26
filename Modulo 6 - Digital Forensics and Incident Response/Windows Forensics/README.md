# 🏆 Desafío: Windows Registry Forensics - ☕ Secret Recipe   

## 📍 Introducción:
### En esta Room, me enfrenté a un caso muy común: Un usuario con permisos de IT que tiene acceso privilegiado al equipo de la directiva. Este usuario, es sospechoso de haber `extraído información confidencial`. Mi tarea fue examinar artefactos forenses del Registro de Windows para reconstruir lo ocurrido y determinar si hubo o no exfiltración de datos sensibles.
### Me concentré en correlacionar elementos claves del registro. En este tipo de análisis, la correcta identificación del Hive apropiado para cada tipo de dato es clave.
---

### 🖥️ 1. ¿Cuál es el nombre del equipo encontrado en el registro?
### ✅ `JAMES`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/01.png)

---

### 👤 2. ¿Cuándo fue creada la cuenta de Administrador en esta máquina?
### ✅ `2021-03-17 14:58:48`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/02.png)
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/02b.png)

---

### 🔐 3. ¿Cuál es el RID asociado a la cuenta de Administrador?
### ✅ `500`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/02-03.png)

---

### 👥 4. ¿Cuántas cuentas de usuario se observaron en esta máquina?
### ✅ `7`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/04.png)

---

### 🕳️ 5. Parece haber una cuenta sospechosa creada como backdoor con RID 1013. ¿Cuál es el nombre de la cuenta?
### ✅ `bdoor`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/5.png)

---

### 🌐 6. ¿A qué conexión VPN se conectó este equipo? Y Cuándo se observó por primera vez una conexión VPN?

### ✅ `ProtonVPN`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/006.png)

---

### 📅 7. ¿Cuándo se observó por primera vez una conexión VPN?
### ✅ `2022-10-12 19:52:36`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/006b.png)

---

### 📁 8. Se observaron tres carpetas compartidas en la máquina. ¿Cuál es la ruta de la tercera?
### ✅ `C:\RESTRICTED FILES`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/07.png)

---

### 📡 9. ¿Cuál fue la última IP DHCP asignada a este host?
### ✅ `172.31.2.197`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/08.png)

---

### 📄 10. Parece que el sospechoso accedió a un archivo con la receta secreta del café. ¿Cuál es el nombre del archivo?
### ✅ `secret-recipe.pdf`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/09.png)

---

### 🖥️ 11. El sospechoso ejecutó múltiples comandos en la ventana "Ejecutar". ¿Qué comando usó para enumerar interfaces de red?
### ✅ `pnputil /enum-interfaces`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/10.png)

---

### 🧰 12. En el explorador de archivos, el usuario buscó una utilidad de red para transferir archivos. ¿Cuál es el nombre de esa herramienta?
### ✅ `netcat`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/11.png)

---

### 📑 13. ¿Cuál es el archivo de texto reciente abierto por el sospechoso?
### ✅ `secret-code.txt`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/12.png)

---

### ⚙️ 14. ¿Cuántas veces se ejecutó PowerShell en este equipo?
### ✅ `3`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/13.png)

---

### 📶 15. El sospechoso también ejecutó una herramienta de monitoreo de red. ¿Cuál es su nombre?
### ✅ `wireshark`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/14.png)

---

### 🔍 16. `Everything.exe` es una utilidad para buscar archivos. ¿Cuál es la ruta completa desde donde se ejecutó?
### ✅ `C:\Users\Administrator\Downloads\tools\Everything\Everything.exe`
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/Windows%20Forensics/15.png)

# 🎖️ Conclusión
## Este ejercicio me acercó un paso más al entorno profesional de un analista SOC. Pude no solo detectar la posible exfiltración de información, sino reconstruir el modus operandi completo del sospechoso usando solo artefactos del sistema. 

