
`rotate()` moves the screen around a set of coordinates. In Processing, rotations happen in **radians** but you can write the number of **degrees** and use the `radians()` function to convert it to radians, `rotate(radians(90))` would be equal to rotating `90` degrees.

Positive numbers rotate objects in a clockwise direction and negative numbers rotate in the counterclockwise direction.

### Girando a tela

In this example, the planet image is positioned with the planet centre in the middle of the screen. The screen is set to rotate around the middle moving one degrees each time it is redrawn.

![A área de saída com um planeta girando em torno do centro](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200) # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### Partes rotativas do desenho

Neste exemplo, a tela é girada em `45` graus quando os olhos estão sendo desenhados para dar a impressão de que estão se movendo.

No entanto, para alinhar os olhos horizontalmente na tela, queremos restaurar as configurações originais antes de desenhar o próximo olho. A função `pushMatrix()` salva as configurações como estavam antes do primeiro olho ser desenhado, então a função `popMatrix()` restaura essas configurações antes que o segundo olho seja desenhado.

All translations and rotations are reset every time `draw()` begins again.

![A área de saída com uma imagem em movimento mostrando um olho giratório feito de círculos](images/rotate_eyes.gif)

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

# Crie um olho
  fill(WHITE) ellipse(0, 0, 150, 150) # Outer eye no_stroke() fill(BLUE) ellipse(0, 0, 80, 80) # Iris fill(BLACK) ellipse(0, 0, 35, 35) # Pupil fill(WHITE, 70) ellipse(-25, -20, 30, 30) # Catchlight 1 with opacity ellipse(25, 25, 10, 10) # Catchlight 2 with opacity

--- /code ---
