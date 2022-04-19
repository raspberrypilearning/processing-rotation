
`rotate()` moves the screen around a set of coordinates. In Processing, rotations happen in **radians** but you can write the number of **degrees** and use the `radians()` function to convert it to radians, `rotate(radians(90))` would be equal to rotating `90` degrees. 

Positive numbers rotate objects in a clockwise direction and negative numbers rotate in the counterclockwise direction. 

### Rotating the screen

In this example, the planet image is positioned with the planet centre in the middle of the screen. The screen is set to rotate around the middle moving one degrees each time it is redrawn. 

![The output area with a planet rotating around the centre](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw():
  translate(200,200) # The middle of the screen
  for i in range(frame_count):
    image(planet, -150, -150, 300, 300) 
    rotate(radians(1))
    
--- /code ---

### Rotating parts of the drawing

In this example, the screen is rotated by `45` degrees when the eyes are being drawn to give them the impression they are moving around. 

However, to align the eyes horizontally across the screen we want to restore the original settings before drawing the next eye. The `pushMatrix()` function saves the settings as they were before the first eye is drawn then the `popMatrix()` function restores those settings before the second eye is drawn. 

All translations and rotations are reset every time `draw()` begins again. 

![The output area with a moving image showing a rotating eye made of circles](images/rotate_eyes.gif)

--- code ---
---
language: python
---

def draw():
  
  global BLUE, BLACK, WHITE

  BLUE = color(1, 32, 100)
  BLACK = color(0, 0, 0)
  WHITE = color(255, 255, 255)
 
  background(WHITE)
  translate(width/2, height/2) # Move screen to the middle 

  stroke(BLACK)
  ellipse(0, 0, 300, 300) # Head
  
  pushMatrix() # Saves current screen settings
  
  translate(-100, 0) # Move screen to the left for left eye
  for i in range(frame_count):
    eye()
    rotate(radians(45))

  popMatrix() # Restores previous screen settings (removes the eye translation and rotation)
  
  translate(100, 0) # Move screen to the right for right eye
  for i in range(frame_count):
    eye()
    rotate(radians(45))    
  
def eye():
  
# Create an eye
  fill(WHITE)
  ellipse(0, 0, 150, 150) # Outer eye
  no_stroke()
  fill(BLUE)
  ellipse(0, 0, 80, 80) # Iris
  fill(BLACK)
  ellipse(0, 0, 35, 35) # Pupil
  fill(WHITE, 70)
  ellipse(-25, -20, 30, 30) # Catchlight 1 with opacity
  ellipse(25, 25, 10, 10) # Catchlight 2 with opacity

--- /code ---
