
`rotate()` déplace l'écran autour d'un ensemble de coordonnées. Dans Processing, les rotations se produisent en **radians** mais tu peux les convertir en **degrés** en utilisant la fonction `radians()` , `rotate(radians(90))` serait égal à une rotation de `90` degrés.

Les nombres positifs font pivoter les objets dans le sens des aiguilles d'une montre et les nombres négatifs dans le sens inverse des aiguilles d'une montre.

### Rotation de l'écran

Dans cet exemple, l'image de la planète est positionnée avec le centre de la planète au milieu de l'écran. L'écran est configuré pour tourner autour du milieu en se déplaçant d'un degré à chaque fois qu'il est redessiné.

![La zone de sortie avec une planète tournant autour du centre](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200) # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### Rotation des parties du dessin

Dans cet exemple, l'écran est tourné de `45` degrés lorsque les yeux sont dessinés pour leur donner l'impression qu'ils bougent.

Cependant, pour aligner les yeux horizontalement sur l'écran, nous souhaitons restaurer les paramètres d'origine avant de dessiner l'œil suivant. La fonction `pushMatrix()` enregistre les paramètres tels qu'ils étaient avant le dessin du premier œil, puis la fonction `popMatrix()` restaure ces paramètres avant le dessin du deuxième œil.

Toutes les translations et rotations sont réinitialisées à chaque fois que `dessiner()` recommence.

![La zone de sortie avec une image animée montrant un œil rotatif composé de cercles](images/rotate_eyes.gif)

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

# Créer un œil
  fill(WHITE) ellipse(0, 0, 150, 150) # Outer eye no_stroke() fill(BLUE) ellipse(0, 0, 80, 80) # Iris fill(BLACK) ellipse(0, 0, 35, 35) # Pupil fill(WHITE, 70) ellipse(-25, -20, 30, 30) # Catchlight 1 with opacity ellipse(25, 25, 10, 10) # Catchlight 2 with opacity

--- /code ---
