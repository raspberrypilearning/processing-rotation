
`rotate()` mueve la pantalla alrededor de un eje de coordenadas. En Procesamiento, las rotaciones ocurren en **radianes** pero pueden convertirse a **grados** usando la función `radians()`, `rotate(radians(90))` sería igual a rotar `90` grados.

Los números positivos giran los objetos en el sentido de las agujas del reloj y los números negativos giran en el sentido contrario a las agujas del reloj.

### Girando la pantalla

En este ejemplo, la imagen del planeta se coloca con el centro del planeta en el centro de la pantalla. La pantalla está configurada para girar alrededor del centro, moviéndose un grado cada vez que se vuelve a dibujar.

![El área de salida con un planeta girando alrededor del centro](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw():
  translate(200,200) # El medio de la pantalla
  for i in range(frame_count):
    image(planet, -150, -150, 300, 300) 
    rotate(radians(1))

--- /code ---

### Girando partes del dibujo

En este ejemplo, la pantalla gira `45` grados cuando se dibujan los ojos para darles la impresión de que se están moviendo.

Sin embargo, para alinear los ojos horizontalmente en la pantalla, queremos restaurar la configuración original antes de dibujar el siguiente ojo. La función `pushMatrix()` guarda la configuración tal como estaba antes de dibujar el primer ojo, luego la función `popMatrix()` restaura esa configuración antes de dibujar el segundo ojo.

Todas las traslaciones y rotaciones se restablecen cada vez que `draw()` (dibujar) comienza de nuevo.

![El área de salida con una imagen en movimiento que muestra un ojo giratorio hecho de círculos](images/rotate_ojos.gif)

--- code ---
---
language: python
---

def draw():
  
  global AZUL, NEGRO, BLANCO

  AZUL = color(1, 32, 100)
  NEGRO = color(0, 0, 0)
  BLANCO = color(255, 255, 255)
 
  background(BLANCO)
  translate(width/2, height/2) # Mueve la pantalla al centro 

  stroke(NEGRO)
  ellipse(0, 0, 300, 300) # Cabeza
  
  pushMatrix() # Guarda la configuración de pantalla actual
  
  translate(-100, 0) # Mueve la pantalla a la izquierda para el ojo izquierdo
  for i in range(frame_count):
    ojo()
    rotate(radians(45))

  popMatrix() # Restaura la configuración de pantalla anterior (elimina la traslación y rotación de los ojos)
  
  translate(100, 0) # Mueve la pantalla a la derecha para el ojo derecho
  for i in range(frame_count):
    ojo()
    rotate(radians(45))    
  
def ojo():
  
# Crea un ojo
  fill(BLANCO)
  ellipse(0, 0, 150, 150) # Exterior del ojo
  no_stroke()
  fill(AZUL)
  ellipse(0, 0, 80, 80) # Iris
  fill(NEGRO)
  ellipse(0, 0, 35, 35) # Pupila
  fill(BLANCO, 70)
  ellipse(-25, -20, 30, 30) # Brillo ocular 1 con opacidad
  ellipse(25, 25, 10, 10) # Brillo ocular 2 con opacidad

--- /code ---
