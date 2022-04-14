
`rotate()` mueve la pantalla alrededor de un eje de coordenadas. En Procesamiento, las rotaciones ocurren en **radianes** pero pueden convertirse a **grados** usando la función `radians()`, `rotate (radians (90))` sería igual a rotar `90` grados.

Los números positivos giran los objetos en el sentido de las agujas del reloj y los números negativos giran en el sentido contrario a las agujas del reloj.

### Girando la pantalla

En este ejemplo, la imagen del planeta se coloca con el centro del planeta en el centro de la pantalla. La pantalla está configurada para girar alrededor del centro, moviéndose un grado cada vez que se vuelve a dibujar.

![El área de salida con un planeta girando alrededor del centro](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200) # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### Girando partes del dibujo

En este ejemplo, la pantalla gira `45` grados cuando se dibujan los ojos para darles la impresión de que se están moviendo.

Sin embargo, para alinear los ojos horizontalmente en la pantalla, queremos restaurar la configuración original antes de dibujar el siguiente ojo. La función `pushMatrix()` guarda la configuración tal como estaba antes de dibujar el primer ojo, luego la función `popMatrix()` restaura esa configuración antes de dibujar el segundo ojo.

Todas las traslaciones y rotaciones se restablecen cada vez que `draw()` (dibujar) comienza de nuevo.

![El área de salida con una imagen en movimiento que muestra un ojo giratorio hecho de círculos](images/rotate_eyes.gif)

--- code ---
---
language: python
---

def draw():

  global BLUE, BLACK, WHITE

  BLUE = color(1, 32, 100) BLACK = color(0, 0, 0) WHITE = color(255, 255, 255)

  background(WHITE) translate(width/2, height/2) # Move screen to the middle

  stroke(BLACK) ellipse(0, 0, 300, 300) # Head

  pushMatrix() # Saves current screen settings

  translate(-100, 0) # Move screen to the left for left eye for i in range(frame_count): eye() rotate(radians(45))

  popMatrix() # Restores previous screen settings (removes the eye translation and rotation)

  translate(100, 0) # Move screen to the right for right eye for i in range(frame_count): eye() rotate(radians(45))

def eye():

# Crea un ojo
  fill(WHITE) ellipse(0, 0, 150, 150) # Outer eye no_stroke() fill(BLUE) ellipse(0, 0, 80, 80) # Iris fill(BLACK) ellipse(0, 0, 35, 35) # Pupil fill(WHITE, 70) ellipse(-25, -20, 30, 30) # Catchlight 1 with opacity ellipse(25, 25, 10, 10) # Catchlight 2 with opacity

--- /code ---
