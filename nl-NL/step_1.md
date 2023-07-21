
`rotate()` draait het scherm rond een aantal coördinaten. In Processing gebeurt draaien met **radialen**, maar je kunt dit veranderen naar **graden** door de `radians()` functie te gebruiken. `rotate(radians(90))` staat gelijk aan `90` graden draaien.

Positieve getallen draaien objecten met de klok mee en negatieve getallen draaien tegen de klok in.

### Het scherm draaien

In dit voorbeeld wordt de afbeelding van de planeet geplaatst met het centrum van de planeet in het midden van het scherm. Het scherm is zo ingesteld dat het één graad om het midden wordt gedraaid elke keer dat het opnieuw wordt getekend.

![Het uitvoergebied met een planeet die rond het midden draait](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200) # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### Delen van de tekening draaien

In dit voorbeeld wordt het scherm `45` graden gedraaid wanneer de ogen worden getekend om de indruk te geven dat ze bewegen.

Maar om de ogen horizontaal over het scherm uit te lijnen, willen we de oorspronkelijke instellingen herstellen voordat we het volgende oog tekenen. De functie `pushMatrix()` slaat de instellingen op zoals ze waren voordat het eerste oog werd getekend, en de functie `popMatrix()` herstelt die instellingen voordat het tweede oog werd getekend.

Elke keer dat `draw()` opnieuw begint worden alle verschuivingen en draaiingen opnieuw ingesteld.

![Het uitvoergebied met een bewegend beeld van een roterend oog gemaakt van cirkels](images/rotate_eyes.gif)

--- code ---
---
language: python
---

def draw(): global BLUE, BLACK, WHITE

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

def eye(): # Create an eye fill(WHITE) ellipse(0, 0, 150, 150) # Outer eye no_stroke() fill(BLUE) ellipse(0, 0, 80, 80) # Iris fill(BLACK) ellipse(0, 0, 35, 35) # Pupil fill(WHITE, 70) ellipse(-25, -20, 30, 30) # Catchlight 1 with opacity ellipse(25, 25, 10, 10) # Catchlight 2 with opacity

--- /code ---
