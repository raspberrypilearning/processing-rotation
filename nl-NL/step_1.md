
`rotate()` draait het scherm rond een aantal coördinaten. In Processing, rotations happen in **radians** but you can write the number of **degrees** and use the `radians()` function to convert it to radians, `rotate(radians(90))` would be equal to rotating `90` degrees.

Positieve getallen draaien objecten met de klok mee en negatieve getallen draaien tegen de klok in.

### Het scherm draaien

In dit voorbeeld wordt de afbeelding van de planeet geplaatst met het centrum van de planeet in het midden van het scherm. Het scherm is zo ingesteld dat het één graad om het midden wordt gedraaid elke keer dat het opnieuw wordt getekend.

![Het uitvoergebied met een planeet die rond het midden draait](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw():
  translate(200,200) # Het midden van het scherm
  for i in range(frame_count):
    image(planet, -150, -150, 300, 300) 
    rotate(radians(1))

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

def draw():
  
  global BLAUW, ZWART, WIT

  BLAUW = color(1, 32, 100)
  ZWART = color(0, 0, 0)
  WIT = color(255, 255, 255)
 
  background(WIT)
  translate(width/2, height/2) # Scherm naar het midden verplaatsen 

  stroke(ZWART)
  ellipse(0, 0, 300, 300) # Hoofd
  
  pushMatrix() # Slaat huidige scherminstellingen op
  
  translate(-100, 0) # Verplaats het scherm naar links voor het linkeroog
  for i in range(frame_count):
    oog()
    rotate(radians(45))

  popMatrix() # Herstel vorige scherminstellingen (verwijdert de locatie en draaiing van het oog)
  
  translate(100, 0) # Verplaats het scherm naar rechts voor het rechteroog
  for i in range(frame_count):
    oog()
    rotate(radians(45))    
  
def oog():
  
# Een oog maken
  fill(WIT)
  ellipse(0, 0, 150, 150) # Buitenkant oog
  no_stroke()
  fill(BLAUW)
  ellipse(0, 0, 80, 80) # Iris
  fill(ZWART)
  ellipse(0, 0, 35, 35) # Pupil
  fill(WIT, 70)
  ellipse(-25, -20, 30, 30) # Lichtinval 1 met doorzichtigheid
  ellipse(25, 25, 10, 10) # Lichtinval 2 met doorzichtigheid

--- /code ---
