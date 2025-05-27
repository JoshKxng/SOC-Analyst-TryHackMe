# 💾 Volatility - Case 001: *BOB! THIS ISN'T A HORSE!*

## 📁 Descripción del Caso
Mi equipo del SOC me informó que se había aislado un endpoint potencialmente comprometido. Se sospechaba que el usuario había abierto un supuesto documento de Adobe que en realidad contenía un **troyano bancario**. Se realizó un volcado de memoria desde la máquina comprometida y mi tarea fue aplicar análisis forense para identificar evidencia del compromiso.
---

## 🎯 Objetivo

Obtener información básica del sistema infectado, identificar procesos sospechosos y por último analizar el árbol de procesos para entender cómo ocurrió la ejecución maliciosa.
---

### 🖥️ ¿Cuál es la versión de compilación del sistema comprometido?

#### A través del plugin `windows.info`, obtuve detalles clave del sistema operativo, como la versión de Windows, arquitectura, fecha de instalación y, en este caso, la build del sistema.
![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/VOLATILY/01.png)


---

### ⏰ ¿A qué hora se adquirió el volcado de memoria?

#### Utilizando los datos disponibles en el análisis con `windows.info`, logré identificar la hora exacta en la que se generó el dump de memoria.

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/VOLATILY/02.png)

---

### 🧪 ¿Qué proceso puede considerarse sospechoso?

#### Ejecutando el plugin `pscsan`, observé la lista de procesos activos. Uno de ellos se destacaba por su nombre extraño. A simple vista, parecía una instancia disfrazada de una aplicación legítima, pero en realidad no coincidía con ninguna ruta ni comportamiento esperable.


![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/VOLATILY/03.png)

---

### 👤 ¿Cuál es el proceso padre del proceso sospechoso?

#### El árbol de procesos reveló que el proceso malicioso había sido iniciado por `explorer.exe`

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/VOLATILY/04.png)

---

### 🆔 ¿Cuál es el PID del proceso sospechoso?

#### ✅ `1484`

![](https://github.com/JoshKxng/SOC-Analyst-TryHackMe/blob/main/imagenes/VOLATILY/06.png)

---

# 🎖️ Reflexión final
## Fue enriquecedor y entretenido el haber trabajado con Volatility. Si bien sólo trabajé con un análisis breve y seguro que en otro caso sería mucho más extenso, fue suficiente para saber como puedo utilizar Volatility para `reconstruir eventos, detectar actividad sospechosa y empezar una investigación a partir de un volcado de memoria`.
