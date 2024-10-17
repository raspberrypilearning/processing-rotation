
`rotate()` bewegt den Bildschirm um eine Menge von Koordinaten. Beim Verarbeiten erfolgen Rotationen im **Bogenmaß (Radiant)**. Du kannst jedoch auch die Zahl in **Grad** schreiben und die Funktion `radians()` verwenden, um sie in Bogenmaß umzuwandeln. `rotate(radians(90))` entspricht einer Rotation um `90` Grad.

Positive Zahlen drehen Objekte im Uhrzeigersinn und negative Zahlen gegen den Uhrzeigersinn.

### Drehen des Bildschirms

In diesem Beispiel ist das Planetenbild mit dem Planetenmittelpunkt in der Bildschirmmitte positioniert. Der Bildschirm ist so eingestellt, dass er sich bei jeder Neuzeichnung um die Mitte dreht und sich um ein Grad verschiebt.

![Der Ausgabebereich mit einem Planeten, der um das Zentrum rotiert](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw():
    translate(200,200)  # Die Mitte des Bildschirms
    for i in range(frame_count):
        image(planet, -150, -150, 300, 300) 
        rotate(radians(1))
    
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

def draw():
    global BLAU, SCHWARZ, WEISS
    
    BLAU = Color(1, 32, 100)
    SCHWARZ = Color(0, 0, 0)
    WEISS = Color(255, 255, 255)
    
    background(WEISS)
    translate(width/2, height/2)  # Bildschirm in die Mitte verschieben
    
    stroke(SCHWARZ)
    ellipse(0, 0, 300, 300)  # Kopf
    
    push_matrix()  # Speichert aktuelle Bildschirmeinstellungen
    
    translate(-100, 0)  # Bewege den Bildschirm für das linke Auge nach links
    for i in range(frame_count):
        auge()
        rotate(radians(45))
    
    pop_matrix()  # Stellt die vorherigen Bildschirmeinstellungen wieder her (entfernt die Augenverschiebung und -rotation)
    
    translate(100, 0)  # Bildschirm für das rechte Auge nach rechts verschieben
    for i in range(frame_count):
        auge()
        rotate(radians(45))    
  
def auge():
    # Ein Auge erstellen
    fill(WEISS)
    ellipse(0, 0, 150, 150)  # Äußeres Auge
    no_stroke()
    fill(BLAU)
    ellipse(0, 0, 80, 80)  # Iris
    fill(SCHWARZ)
    ellipse(0, 0, 35, 35)  # Pupille
    fill(WEISS, 70)
    ellipse(-25, -20, 30, 30)  # Lichtglanz 1 mit Durchsichtigkeit
    ellipse(25, 25, 10, 10)  # Lichtglanz 2 mit Durchsichtigkeit

--- /code ---
