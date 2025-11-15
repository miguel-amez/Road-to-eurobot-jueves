# 🐍 Plan de Aprendizaje Python para Alumnos 12-13 años
## De Bloques a Código con micro:bit

**Perfil del alumno:**
- Edad: 12-13 años
- Experiencia: Programación con bloques en micro:bit
- Objetivo: Transición a Python (MicroPython)
- Formato: 3 masterclasses + 15 retos de refuerzo

---

## 📚 MASTERCLASS 1: De Bloques a Código
**Duración:** 60-90 min
**Objetivo:** Entender que el código Python hace lo mismo que los bloques, pero escrito

### 🎯 Conceptos Clave
- Variables → cajas que guardan datos
- `display.show()` → mostrar en LED
- `display.scroll()` → texto que se mueve
- `button_a.is_pressed()` → leer botones
- Secuencias y tiempo (`sleep`)

### 📖 Contenido de la Clase

#### Parte 1: Hola micro:bit en Python (15 min)
```python
from microbit import *

# Esto es lo mismo que el bloque "mostrar texto"
display.show("Hola")
```

**Comparación visual:**
- BLOQUES: [mostrar texto "Hola"]
- PYTHON: `display.show("Hola")`

**Ejercicio en clase:** Mostrar tu inicial en la pantalla

---

#### Parte 2: Variables = Cajas con nombres (20 min)
```python
from microbit import *

# Variable es como poner un nombre a un número
puntos = 0
vidas = 3

display.scroll("Puntos: " + str(puntos))
```

**Ejercicio en clase:** Crear un contador que muestre un número y lo cambie

---

#### Parte 3: Botones y decisiones (25 min)
```python
from microbit import *

while True:
    if button_a.is_pressed():
        display.show("A")
    elif button_b.is_pressed():
        display.show("B")
    else:
        display.clear()
    sleep(100)
```

**Ejercicio en clase:** Programa que al pulsar A muestra 😊 y al pulsar B muestra 😢

---

#### Parte 4: Mini-proyecto guiado (20 min)
**Contador de clicks**
```python
from microbit import *

clicks = 0

while True:
    if button_a.was_pressed():
        clicks = clicks + 1
        display.scroll(clicks)

    if button_b.was_pressed():
        clicks = 0
        display.show("0")

    sleep(100)
```

---

### 🏠 RETOS DE REFUERZO PARA CASA - SESIÓN 1

#### Reto 1: Semáforo ⭐
Programa un semáforo que cambie cada 3 segundos:
- 🔴 Rojo (3 seg)
- 🟡 Amarillo (1 seg)
- 🟢 Verde (3 seg)

**Pista:** Usa `Image.HAPPY`, `Image.SAD`, y colores inventados

---

#### Reto 2: Dado Digital ⭐⭐
Al pulsar el botón A, muestra un número aleatorio del 1 al 6

**Pista:**
```python
import random
numero = random.randint(1, 6)
```

---

#### Reto 3: Calculadora de Edad ⭐
Guarda tu año de nacimiento en una variable y calcula tu edad en 2025

**Ejemplo:**
```python
nacimiento = 2012
edad = 2025 - nacimiento
display.scroll("Tienes " + str(edad))
```

---

#### Reto 4: Nombre Animado ⭐⭐
Muestra tu nombre letra por letra con 1 segundo de pausa entre cada letra

**Pista:** Usa `display.show()` y `sleep(1000)` varias veces

---

#### Reto 5: Botón Secreto ⭐⭐⭐
Crea un programa que:
- Muestre "?" normalmente
- Al pulsar A y B a la vez, muestre "😊"
- Si solo pulsas uno, muestre "❌"

**Pista:**
```python
if button_a.is_pressed() and button_b.is_pressed():
    # ambos pulsados
```

---

## 📚 MASTERCLASS 2: Bucles, Listas y Lógica
**Duración:** 60-90 min
**Objetivo:** Dominar bucles `for` y trabajar con colecciones de datos

### 🎯 Conceptos Clave
- `for` → repetir con lista
- Listas `[]` → múltiples valores
- Animaciones con bucles
- Operadores lógicos (`and`, `or`, `not`)

### 📖 Contenido de la Clase

#### Parte 1: Bucle FOR es tu amigo (15 min)
```python
from microbit import *

# Mostrar números del 0 al 9
for numero in range(10):
    display.show(numero)
    sleep(500)
```

**Diferencia con WHILE:**
- `while` → repite "mientras sea verdad"
- `for` → repite "para cada elemento"

**Ejercicio en clase:** Cuenta atrás desde 10 hasta 0 y muestra "🚀"

---

#### Parte 2: Listas = Colecciones (20 min)
```python
from microbit import *

# Lista de emociones
emociones = [Image.HAPPY, Image.SAD, Image.ANGRY, Image.SURPRISED]

for emocion in emociones:
    display.show(emocion)
    sleep(1000)
```

**Ejercicio en clase:** Crea una lista con 5 imágenes y muéstralas en bucle

---

#### Parte 3: Animaciones fluidas (20 min)
```python
from microbit import *

# Animación de corazón
animacion = [Image.HEART, Image.HEART_SMALL, Image.HEART, Image.HEART_SMALL]

while True:
    for frame in animacion:
        display.show(frame)
        sleep(300)
```

**Ejercicio en clase:** Crea tu propia animación de 4 frames

---

#### Parte 4: Mini-proyecto guiado (25 min)
**Juego de Reacción**
```python
from microbit import *
import random

display.scroll("Preparado?")
sleep(random.randint(2000, 5000))

display.show("!")
inicio = running_time()

while not button_a.is_pressed():
    pass

tiempo = running_time() - inicio
display.scroll("Tiempo: " + str(tiempo) + " ms")
```

---

### 🏠 RETOS DE REFUERZO PARA CASA - SESIÓN 2

#### Reto 6: Contador con Límite ⭐
Crea un contador del 0 al 20 que:
- Incrementa con botón A
- NO puede pasar de 20
- Reinicia con botón B

**Pista:** Usa `if contador < 20:`

---

#### Reto 7: Secuencia de Luces ⭐⭐
Crea una animación que encienda los LEDs uno por uno formando un cuadrado

**Pista:** Usa coordenadas `display.set_pixel(x, y, 9)`
```python
for x in range(5):
    display.set_pixel(x, 0, 9)
    sleep(200)
```

---

#### Reto 8: Adivina el Número ⭐⭐⭐
El micro:bit piensa un número del 1 al 5. Tú incrementas con A y adivinas con B.
- Si aciertas: 😊
- Si fallas: muestra el número correcto

---

#### Reto 9: Lista de Tareas ⭐⭐
Crea una lista de tareas y muéstralas con el botón A (siguiente tarea)

```python
tareas = ["Estudiar", "Jugar", "Dormir"]
indice = 0

# Al pulsar A, muestra la siguiente tarea
```

---

#### Reto 10: Cronómetro ⭐⭐⭐
Crea un cronómetro:
- Botón A: empieza/para
- Botón B: reinicia
- Muestra segundos transcurridos

**Pista:** Usa `running_time()` que devuelve milisegundos

---

## 📚 MASTERCLASS 3: Funciones y Proyecto Final
**Duración:** 90-120 min
**Objetivo:** Crear código reutilizable y proyecto creativo completo

### 🎯 Conceptos Clave
- `def` → definir función
- Parámetros y retorno
- Sensor de acelerómetro
- Proyecto integrador

### 📖 Contenido de la Clase

#### Parte 1: Funciones = Bloques Personalizados (20 min)
```python
from microbit import *

# Función que muestra emoción por 2 segundos
def mostrar_emocion(imagen):
    display.show(imagen)
    sleep(2000)
    display.clear()

# Usar la función
mostrar_emocion(Image.HAPPY)
mostrar_emocion(Image.SAD)
```

**Comparación con bloques:**
- BLOQUES: "crear bloque personalizado"
- PYTHON: `def nombre_funcion():`

**Ejercicio en clase:** Crea función `parpadear()` que haga parpadear un LED

---

#### Parte 2: Funciones con parámetros (20 min)
```python
from microbit import *

def sumar_puntos(puntos_actuales, puntos_nuevos):
    total = puntos_actuales + puntos_nuevos
    return total

puntos = 0
puntos = sumar_puntos(puntos, 10)  # ahora puntos = 10
display.scroll(puntos)
```

**Ejercicio en clase:** Función que recibe dos números y devuelve el mayor

---

#### Parte 3: Acelerómetro = Sensor de Movimiento (20 min)
```python
from microbit import *

while True:
    # Leer inclinación (valores de -1024 a 1024)
    x = accelerometer.get_x()

    if x > 200:
        display.show(Image.ARROW_E)
    elif x < -200:
        display.show(Image.ARROW_W)
    else:
        display.clear()

    sleep(100)
```

**Ejercicio en clase:** Nivel de burbuja (muestra flecha según inclinación)

---

#### Parte 4: PROYECTO FINAL GUIADO (40 min)
**🎮 Juego del Laberinto**

```python
from microbit import *

# Posición del jugador
x = 2
y = 2

# Meta
meta_x = 4
meta_y = 4

while True:
    # Borrar pantalla
    display.clear()

    # Mostrar jugador
    display.set_pixel(x, y, 9)

    # Mostrar meta parpadeando
    if running_time() % 1000 < 500:
        display.set_pixel(meta_x, meta_y, 5)

    # Leer acelerómetro
    accel_x = accelerometer.get_x()
    accel_y = accelerometer.get_y()

    # Mover jugador
    if accel_x > 200 and x < 4:
        x = x + 1
    elif accel_x < -200 and x > 0:
        x = x - 1

    if accel_y > 200 and y < 4:
        y = y + 1
    elif accel_y < -200 and y > 0:
        y = y - 1

    # ¿Ganó?
    if x == meta_x and y == meta_y:
        display.show(Image.HAPPY)
        break

    sleep(200)

display.scroll("¡GANASTE!")
```

---

### 🏠 RETOS DE REFUERZO PARA CASA - SESIÓN 3

#### Reto 11: Función Multiplicar ⭐
Crea una función `multiplicar(a, b)` que devuelva el resultado y muéstralo en pantalla

**Ejemplo:**
```python
resultado = multiplicar(5, 3)
display.scroll(resultado)  # Muestra 15
```

---

#### Reto 12: Detector de Agitación ⭐⭐
Programa que detecte cuando agitas el micro:bit y cuente cuántas veces lo agitaste

**Pista:**
```python
if accelerometer.was_gesture("shake"):
    contador = contador + 1
```

---

#### Reto 13: Brújula Digital ⭐⭐⭐
Usa `compass.heading()` para mostrar flechas según la dirección:
- Norte: ↑
- Sur: ↓
- Este: →
- Oeste: ←

**Nota:** Necesitas calibrar primero con `compass.calibrate()`

---

#### Reto 14: Piedra, Papel, Tijera ⭐⭐⭐
Al agitar el micro:bit, elige aleatoriamente:
- Piedra: ⬜
- Papel: 📄 (un rectángulo)
- Tijera: ✂️ (dos líneas cruzadas)

---

#### Reto 15: PROYECTO LIBRE ⭐⭐⭐⭐
Crea tu propio juego o programa combinando todo lo aprendido.

**Ideas:**
- Mascotas virtual (cuida un animal digital)
- Juego de memoria (repite la secuencia)
- Medidor de pasos (cuenta movimientos)
- Alarma con temporizador
- Juego de ping-pong (pelota rebotando)

---

## 📊 EVALUACIÓN Y SEGUIMIENTO

### Sistema de Estrellas
- ⭐ Básico (todos deben lograrlo)
- ⭐⭐ Intermedio (mayoría debería lograrlo)
- ⭐⭐⭐ Avanzado (desafío extra)
- ⭐⭐⭐⭐ Experto (creatividad libre)

### Checklist de Progreso
Masterclass 1: ✅
- [ ] Ejecuté mi primer programa en Python
- [ ] Entiendo qué son las variables
- [ ] Uso botones en código
- [ ] Completé al menos 3 retos

Masterclass 2: ✅
- [ ] Uso bucles `for` correctamente
- [ ] Creo listas con datos
- [ ] Hago animaciones
- [ ] Completé al menos 3 retos

Masterclass 3: ✅
- [ ] Creo mis propias funciones
- [ ] Uso el acelerómetro
- [ ] Hice el proyecto del laberinto
- [ ] Creé mi proyecto libre

---

## 🎓 RECURSOS ADICIONALES

### Para los alumnos
- Editor online: https://python.microbit.org/v/3
- Simulador: https://create.withcode.uk/
- Documentación: https://microbit-micropython.readthedocs.io/

### Para el profesor
- Soluciones de todos los retos disponibles
- Ideas de extensión para alumnos avanzados
- Rúbricas de evaluación por competencias

---

## 💡 CONSEJOS PEDAGÓGICOS

1. **Muestra el código Y los bloques lado a lado** en la primera sesión
2. **Deja que experimenten** antes de dar la solución
3. **Celebra los errores** como oportunidades de aprendizaje
4. **Proyectos en parejas** fomenta colaboración
5. **Tiempo para mostrar** sus creaciones motiva mucho

---

## 🚀 EXTENSIONES POSIBLES

Si terminen rápido o quieren más:
- Radio (comunicación entre micro:bits)
- Música (`music.play()`)
- Persistencia de datos
- Proyectos con hardware externo

---

**Creado para alumnos de 12-13 años | Transición Bloques → Python**
