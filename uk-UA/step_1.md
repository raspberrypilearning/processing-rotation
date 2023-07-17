
`rotate()` переміщує екран навколо заданих координат. У Processing, обертання відбуваються в **радіанах**, але ти можеш написати кількість **градусів** та використати функцію `radians()`, щоб перерахувати градуси в радіани, `rotate(radians(90))` буде дорівнювати обертанню на `90` градусів.

Додатні числа обертають об'єкти за годинниковою стрілкою, а від'ємні - проти годинникової стрілки.

### Обертання екрана

У цьому прикладі центр планети розташований посередині екрана. Екран обертається навколо середини, переміщуючись на один градус при кожному повторному малюванні.

![Вихідна область з планетою, що обертається навколо центру](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200) # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### Обертання окремих елементів

У цьому прикладі, коли малюються очі, екран повертається на `45` градусів, щоб створити враження, що очі рухаються.

Однак, щоб розташувати очі горизонтально по екрана, нам потрібно відновити початкові налаштування перед тим, як намалювати наступне око. Функція `pushMatrix()` зберігає налаштування в тому вигляді, у якому вони були до малювання першого ока, а потім функція `popMatrix()` відновлює ці налаштування перед малюванням другого ока.

Усі переклади та ротації обнуляються щоразу, коли `draw()` викликається знову.

![Область виводу з рухомим зображенням, на якому зображено око, що обертається](images/rotate_eyes.gif)

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

# Створення ока
  fill(WHITE) ellipse(0, 0, 150, 150) # Outer eye no_stroke() fill(BLUE) ellipse(0, 0, 80, 80) # Iris fill(BLACK) ellipse(0, 0, 35, 35) # Pupil fill(WHITE, 70) ellipse(-25, -20, 30, 30) # Catchlight 1 with opacity ellipse(25, 25, 10, 10) # Catchlight 2 with opacity

--- /code ---
