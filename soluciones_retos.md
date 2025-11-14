# 🔑 Soluciones de los Retos - Guía del Profesor

## SESIÓN 1 - De Bloques a Código

### Reto 1: Semáforo ⭐
```python
from microbit import *

while True:
    # Rojo
    display.show(Image.SQUARE_SMALL)
    sleep(3000)

    # Amarillo
    display.show(Image.DIAMOND_SMALL)
    sleep(1000)

    # Verde
    display.show(Image.HEART_SMALL)
    sleep(3000)
```

---

### Reto 2: Dado Digital ⭐⭐
```python
from microbit import *
import random

while True:
    if button_a.was_pressed():
        numero = random.randint(1, 6)
        display.show(numero)

    sleep(100)
```

---

### Reto 3: Calculadora de Edad ⭐
```python
from microbit import *

nacimiento = 2012
edad = 2025 - nacimiento
display.scroll("Tienes " + str(edad) + " años")
```

---

### Reto 4: Nombre Animado ⭐⭐
```python
from microbit import *

nombre = "ANA"

for letra in nombre:
    display.show(letra)
    sleep(1000)

# Alternativa sin bucle (más básica):
# display.show("A")
# sleep(1000)
# display.show("N")
# sleep(1000)
# display.show("A")
# sleep(1000)
```

---

### Reto 5: Botón Secreto ⭐⭐⭐
```python
from microbit import *

while True:
    if button_a.is_pressed() and button_b.is_pressed():
        display.show(Image.HAPPY)
    elif button_a.is_pressed() or button_b.is_pressed():
        display.show(Image.NO)
    else:
        display.show("?")

    sleep(100)
```

---

## SESIÓN 2 - Bucles, Listas y Lógica

### Reto 6: Contador con Límite ⭐
```python
from microbit import *

contador = 0

while True:
    if button_a.was_pressed():
        if contador < 20:
            contador = contador + 1
        display.show(contador)

    if button_b.was_pressed():
        contador = 0
        display.show(contador)

    sleep(100)
```

---

### Reto 7: Secuencia de Luces ⭐⭐
```python
from microbit import *

display.clear()

# Arriba (fila 0)
for x in range(5):
    display.set_pixel(x, 0, 9)
    sleep(200)

# Derecha (columna 4)
for y in range(1, 5):
    display.set_pixel(4, y, 9)
    sleep(200)

# Abajo (fila 4, de derecha a izquierda)
for x in range(3, -1, -1):
    display.set_pixel(x, 4, 9)
    sleep(200)

# Izquierda (columna 0, de abajo a arriba)
for y in range(3, 0, -1):
    display.set_pixel(0, y, 9)
    sleep(200)
```

---

### Reto 8: Adivina el Número ⭐⭐⭐
```python
from microbit import *
import random

numero_secreto = random.randint(1, 5)
mi_numero = 1

display.scroll("Adivina 1-5")
display.show(mi_numero)

while True:
    if button_a.was_pressed():
        mi_numero = mi_numero + 1
        if mi_numero > 5:
            mi_numero = 1
        display.show(mi_numero)

    if button_b.was_pressed():
        if mi_numero == numero_secreto:
            display.show(Image.HAPPY)
            sleep(2000)
            # Nuevo juego
            numero_secreto = random.randint(1, 5)
            mi_numero = 1
            display.show(mi_numero)
        else:
            display.show(Image.SAD)
            sleep(1000)
            display.scroll("Era: " + str(numero_secreto))
            sleep(2000)
            # Nuevo juego
            numero_secreto = random.randint(1, 5)
            mi_numero = 1
            display.show(mi_numero)

    sleep(100)
```

---

### Reto 9: Lista de Tareas ⭐⭐
```python
from microbit import *

tareas = ["Estudiar", "Jugar", "Dormir", "Comer"]
indice = 0

display.scroll(tareas[indice])

while True:
    if button_a.was_pressed():
        indice = indice + 1
        if indice >= len(tareas):
            indice = 0
        display.scroll(tareas[indice])

    sleep(100)
```

---

### Reto 10: Cronómetro ⭐⭐⭐
```python
from microbit import *

activo = False
tiempo_inicio = 0
tiempo_pausado = 0

while True:
    if button_a.was_pressed():
        if not activo:
            # Iniciar
            activo = True
            tiempo_inicio = running_time() - tiempo_pausado
        else:
            # Pausar
            activo = False
            tiempo_pausado = running_time() - tiempo_inicio

    if button_b.was_pressed():
        # Reiniciar
        activo = False
        tiempo_inicio = 0
        tiempo_pausado = 0
        display.show("0")

    if activo:
        segundos = (running_time() - tiempo_inicio) // 1000
        display.scroll(segundos, wait=False, loop=True)

    sleep(100)
```

---

## SESIÓN 3 - Funciones y Proyecto Final

### Reto 11: Función Multiplicar ⭐
```python
from microbit import *

def multiplicar(a, b):
    resultado = a * b
    return resultado

# Probar
resultado = multiplicar(5, 3)
display.scroll("5 x 3 = " + str(resultado))

resultado = multiplicar(7, 8)
display.scroll("7 x 8 = " + str(resultado))
```

---

### Reto 12: Detector de Agitación ⭐⭐
```python
from microbit import *

contador = 0
display.show(contador)

while True:
    if accelerometer.was_gesture("shake"):
        contador = contador + 1
        display.show(contador)

    if button_b.was_pressed():
        contador = 0
        display.show(contador)

    sleep(100)
```

---

### Reto 13: Brújula Digital ⭐⭐⭐
```python
from microbit import *

# Calibrar (solo primera vez)
display.scroll("Calibra girando")
compass.calibrate()
display.show(Image.HAPPY)
sleep(1000)

while True:
    direccion = compass.heading()

    # Norte: 0° (337.5° - 22.5°)
    if direccion < 45 or direccion >= 315:
        display.show(Image.ARROW_N)

    # Este: 90° (67.5° - 112.5°)
    elif direccion >= 45 and direccion < 135:
        display.show(Image.ARROW_E)

    # Sur: 180° (157.5° - 202.5°)
    elif direccion >= 135 and direccion < 225:
        display.show(Image.ARROW_S)

    # Oeste: 270° (247.5° - 292.5°)
    else:
        display.show(Image.ARROW_W)

    sleep(500)
```

---

### Reto 14: Piedra, Papel, Tijera ⭐⭐⭐
```python
from microbit import *
import random

opciones = ["Piedra", "Papel", "Tijera"]

imagenes = [
    Image("00000:09990:09990:09990:00000"),  # Piedra (cuadrado)
    Image("99999:90009:90009:90009:99999"),  # Papel (rectángulo)
    Image("90009:09090:00900:09090:90009")   # Tijera (X)
]

display.scroll("Agita!")

while True:
    if accelerometer.was_gesture("shake"):
        eleccion = random.randint(0, 2)
        display.show(imagenes[eleccion])
        sleep(2000)
        display.scroll(opciones[eleccion])
        sleep(2000)
        display.clear()

    sleep(100)
```

---

### Reto 15: PROYECTO LIBRE ⭐⭐⭐⭐

#### Ejemplo 1: Mascota Virtual
```python
from microbit import *

hambre = 0
felicidad = 10

while True:
    # Cada 30 segundos aumenta hambre
    if running_time() % 30000 < 100:
        hambre = hambre + 1
        if hambre > 10:
            hambre = 10

    # Mostrar estado
    if hambre > 7:
        display.show(Image.SAD)
    elif felicidad > 7:
        display.show(Image.HAPPY)
    else:
        display.show(Image.CONFUSED)

    # A = dar comida
    if button_a.was_pressed():
        hambre = hambre - 2
        if hambre < 0:
            hambre = 0
        felicidad = felicidad + 1
        display.show(Image.HEART)
        sleep(1000)

    # B = jugar
    if button_b.was_pressed():
        felicidad = felicidad + 2
        if felicidad > 10:
            felicidad = 10
        display.show(Image.HAPPY)
        sleep(1000)

    # Agitar = check stats
    if accelerometer.was_gesture("shake"):
        display.scroll("Hambre: " + str(hambre))
        display.scroll("Feliz: " + str(felicidad))

    sleep(100)
```

#### Ejemplo 2: Juego de Memoria
```python
from microbit import *
import random

def mostrar_secuencia(secuencia):
    for numero in secuencia:
        display.show(numero)
        sleep(1000)
        display.clear()
        sleep(500)

secuencia = []
nivel = 1

display.scroll("Memoria")
sleep(1000)

while True:
    # Añadir nuevo número a la secuencia
    secuencia.append(random.randint(1, 4))

    display.scroll("Nivel " + str(nivel))
    sleep(1000)

    # Mostrar secuencia
    mostrar_secuencia(secuencia)

    # Jugador repite
    display.show("?")
    for numero_correcto in secuencia:
        esperando = True
        while esperando:
            if button_a.was_pressed():
                numero_usuario = 1
                display.show(numero_usuario)
                esperando = False
            elif button_b.was_pressed():
                numero_usuario = 2
                display.show(numero_usuario)
                esperando = False
            # Añadir A+B para 3 y shake para 4 si quieres
            sleep(100)

        sleep(500)

        # Verificar
        if numero_usuario != numero_correcto:
            display.show(Image.SAD)
            sleep(2000)
            display.scroll("Nivel: " + str(nivel))
            # Reiniciar
            secuencia = []
            nivel = 1
            sleep(2000)
            break

    # Si llegó hasta aquí, pasó el nivel
    if len(secuencia) == nivel:
        display.show(Image.HAPPY)
        nivel = nivel + 1
        sleep(1000)
```

---

## 📋 NOTAS PEDAGÓGICAS

### Dificultades comunes:
1. **Indentación:** Muchos olvidan los espacios después de `if`, `while`, `for`
2. **Diferencia `=` vs `==`:** Asignación vs comparación
3. **Strings y números:** Olvidar `str()` al concatenar
4. **Bucle infinito sin sleep:** Olvidar `sleep()` en `while True`

### Soluciones:
- Usa el editor online que marca errores de sintaxis
- Haz énfasis visual en la indentación (4 espacios)
- Ejercicios de debugging: dale código con errores para que corrijan

### Extensiones para avanzados:
- Comunicación radio entre micro:bits
- Proyectos con hardware externo (servos, neopixels)
- Persistencia de datos (guardar puntuación)
- Crear biblioteca de funciones reutilizables

---

## 🎯 RÚBRICA DE EVALUACIÓN

| Criterio | Básico (1) | Intermedio (2) | Avanzado (3) |
|----------|------------|----------------|--------------|
| **Sintaxis** | Código con errores | Código funcional | Código limpio y eficiente |
| **Lógica** | Resuelve problema simple | Usa condicionales y bucles | Usa funciones y estructuras complejas |
| **Creatividad** | Replica ejemplos | Modifica ejemplos | Crea soluciones originales |
| **Autonomía** | Necesita ayuda constante | Pregunta puntualmente | Resuelve solo y ayuda a otros |

**Mínimo para aprobar:** 6/12 puntos
**Excelente:** 10-12 puntos

---

## ✅ CHECKLIST FINAL DE APRENDIZAJE

Al finalizar las 3 sesiones, el alumno debe ser capaz de:

- [ ] Escribir programa básico en Python (no bloques)
- [ ] Declarar y usar variables
- [ ] Usar condicionales (if, elif, else)
- [ ] Crear bucles (while, for)
- [ ] Trabajar con listas
- [ ] Definir funciones propias
- [ ] Leer sensores (botones, acelerómetro)
- [ ] Crear animaciones en display
- [ ] Combinar conceptos en proyecto propio
- [ ] Debuggear errores básicos

---

**¡Éxito con tus clases! 🚀**
