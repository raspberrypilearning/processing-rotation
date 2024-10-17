
`rotate()` bewegt den Bildschirm um eine Menge von Koordinaten. Beim Verarbeiten erfolgen Rotationen im **Bogenmaß (Radiant)**. Du kannst jedoch auch die Zahl in **Grad** schreiben und die Funktion `radians()` verwenden, um sie in Bogenmaß umzuwandeln. `rotate(radians(90))` entspricht einer Rotation um `90` Grad.

Positive Zahlen drehen Objekte im Uhrzeigersinn und negative Zahlen gegen den Uhrzeigersinn.

### Drehen des Bildschirms

In diesem Beispiel ist das Planetenbild mit dem Planetenmittelpunkt in der Bildschirmmitte positioniert. Der Bildschirm ist so eingestellt, dass er sich bei jeder Neuzeichnung um die Mitte dreht und sich um ein Grad verschiebt.

![Der Ausgabebereich mit einem Planeten, der um das Zentrum rotiert](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200)  # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### Drehen von Teilen der Zeichnung

In diesem Beispiel wird der Bildschirm beim Zeichnen der Augen um `45` Grad gedreht, um den Eindruck zu erwecken, dass sie sich bewegen.

Um die Augen jedoch horizontal über den Bildschirm auszurichten, möchten wir vor dem Zeichnen des nächsten Auges die ursprünglichen Einstellungen wiederherstellen. Die Funktion `pushMatrix()` speichert die Einstellungen, wie sie waren, bevor das erste Auge gezeichnet wird. Anschließend stellt die Funktion `popMatrix()` diese Einstellungen wieder her, bevor das zweite Auge gezeichnet wird.

Alle Verschiebungen und Drehungen werden jedes Mal zurückgesetzt, wenn `draw()` erneut beginnt.

![Der Ausgabebereich mit einem bewegten Bild, das ein rotierendes Auge aus Kreisen zeigt](images/rotate_eyes.gif)

--- code ---
---
language: python
---

def draw(): global BLUE, BLACK, WHITE

    BLUE = Color(1, 32, 100)
    BLACK = Color(0, 0, 0)
    WHITE = Color(255, 255, 255)
    
    background(WHITE)
    translate(width/2, height/2)  # Move screen to the middle 
    
    stroke(BLACK)
    ellipse(0, 0, 300, 300)  # Head
    
    push_matrix()  # Saves current screen settings
    
    translate(-100, 0)  # Move screen to the left for left eye
    for i in range(frame_count):
        eye()
        rotate(radians(45))
    
    pop_matrix()  # Restores previous screen settings (removes the eye translation and rotation)
    
    translate(100, 0)  # Move screen to the right for right eye
    for i in range(frame_count):
        eye()
        rotate(radians(45))

def eye(): # Create an eye fill(WHITE) ellipse(0, 0, 150, 150)  # Outer eye no_stroke() fill(BLUE) ellipse(0, 0, 80, 80)  # Iris fill(BLACK) ellipse(0, 0, 35, 35)  # Pupil fill(WHITE, 70) ellipse(-25, -20, 30, 30)  # Catchlight 1 with opacity ellipse(25, 25, 10, 10)  # Catchlight 2 with opacity

--- /code ---
