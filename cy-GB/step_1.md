
Mae `rotate()` yn symud y sgrin o amgylch set o gyfesurynnau. Yn Processing, mae cylchdroadau'n digwydd mewn **radianau** ond fe allwch chi ysgrifennu rhif y **graddau** a defnyddio'r swyddogaeth `radians()` i'w trosi'n radianau, byddai `rotate(radians(90))` yr un peth â chylchdroi `90` gradd.

Mae rhifau positif yn cylchdroi gwrthrychau yn glocwedd ac mae rhifau negatif yn cylchdroi yn wrthglocwedd.

### Cylchdroi'r sgrin

Yn yr enghraifft hon, mae'r delwedd o'r blaned wedi'i lleoli gyda chanol y blaned yng nghanol y sgrin. Mae'r sgrin wedi'i gosod i gylchdroi o amgylch y canol gan symud un radd bob tro mae'n cael ei hail-lunio.

![Yr ardal allbwn gyda phlaned yn cylchdroi o amgylch y canol](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200)  # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### Cylchdroi rhannau o'r lluniad

Yn yr enghraifft hon, mae'r sgrin yn cael ei chylchdroi `45` gradd pan fydd y llygaid yn cael eu llunio i roi'r argraff eu bod yn symud o gwmpas.

Ond i alinio'r llygaid yn llorweddol ar draws y sgrin, rydyn ni am adfer y gosodiadau gwreiddiol cyn llunio'r llygad nesaf. Mae'r swyddogaeth `pushMatrix()` yn cadw'r gosodiadau fel yr oedden nhw cyn llunio'r llygad gyntaf ac yna mae'r swyddogaeth `popMatrix()` yn adfer y gosodiadau hynny cyn llunio'r ail lygad.

Mae'r holl drosiadau a chylchdroadau'n cael eu hailosod bob tro mae `draw()` yn dechrau eto.

![Yr ardal allbwn gyda delwedd yn symud, yn dangos llygad wedi'i gwneud o gylchoedd yn cylchdroi](images/rotate_eyes.gif)

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
