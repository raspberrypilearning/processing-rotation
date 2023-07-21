
Η `rotate()` μετακινεί την οθόνη γύρω από ένα ζεύγος συντεταγμένων. In Processing, rotations happen in **radians** but you can write the number of **degrees** and use the `radians()` function to convert it to radians, `rotate(radians(90))` would be equal to rotating `90` degrees.

Οι θετικοί αριθμοί περιστρέφουν αντικείμενα προς τη φορά των δεικτών του ρολογιού και οι αρνητικοί αριθμοί τα περιστρέφουν αριστερόστροφα.

### Περιστρέφοντας την οθόνη

Σε αυτό το παράδειγμα, η εικόνα του πλανήτη τοποθετείται με το κέντρο του πλανήτη στη μέση της οθόνης. Η οθόνη έχει ρυθμιστεί να περιστρέφεται γύρω από τη μέση κινούμενη κατά μία μοίρα κάθε φορά που επανασχεδιάζεται.

![Η περιοχή εξόδου με έναν πλανήτη που περιστρέφεται γύρω από το κέντρο](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200) # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### Περιστρέφοντας μέρη του σχεδίου

Σε αυτό το παράδειγμα, η οθόνη περιστρέφεται κατά `45` μοίρες όταν σχεδιάζονται τα μάτια για να τους δώσει την εντύπωση ότι κινούνται.

Ωστόσο, για να ευθυγραμμιστούν τα μάτια οριζόντια κατά μήκος της οθόνης, θέλουμε να επαναφέρουμε τις αρχικές ρυθμίσεις πριν σχεδιάσουμε το επόμενο μάτι. Η συνάρτηση `pushMatrix()` αποθηκεύει τις ρυθμίσεις όπως ήταν πριν από τη σχεδίαση του πρώτου ματιού και, στη συνέχεια, η συνάρτηση `popMatrix()` επαναφέρει αυτές τις ρυθμίσεις πριν σχεδιαστεί το δεύτερο μάτι.

Όλες οι μεταφορές και οι περιστροφές επαναφέρονται κάθε φορά που το `draw()` ξεκινά ξανά.

![Η περιοχή εξόδου με μια κινούμενη εικόνα που δείχνει ένα περιστρεφόμενο μάτι από κύκλους](images/rotate_eyes.gif)

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
