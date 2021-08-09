
`Rotate()` moves the screen around a set of coordinates. In Processing, rotations happen in **radians** but you can convert this to **degrees** using the `radians()` function, `rotate(radians(90))` would be equal to rotating `90` degrees. 

Positive numbers rotate objects in a clockwise direction and negative numbers rotate in the couterclockwise direction. 

In this example, the screen is rotated `45` degrees everytime the `eye()` is drawn. 

![The output area with a moving image showing a rotating eye made of circles](images/rotate_eye.gif)

--- collapse ---

---
title: Rotation
---

--- code ---
---
language: python
---

def draw():
  
  translate(width/2, height/2) # Move screen to the middle 

  for i in range(frame_count):
    eye()
    rotate(radians(45)) # 45 degrees
  
def eye():

# Eye colours
  BLUE = color(1, 32, 100)
  BLACK = color(0, 0, 0)
  WHITE = color(255, 255, 255)
  
# Create an eye
  stroke(BLACK)
  fill(WHITE)
  ellipse(0, 0, 150, 150) # Outer Eye
  no_stroke()
  fill(BLUE)
  ellipse(0, 0, 80, 80) # Iris
  fill(BLACK)
  ellipse(0, 0, 35, 35) # Pupil
  fill(WHITE, 70)
  ellipse(-25, -20, 30, 30) # Catchlight
  ellipse(25, 25, 10, 10) # Catchlight

--- /code ---
