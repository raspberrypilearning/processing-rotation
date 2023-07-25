
`تدوير ()` يحرك الشاشة حول مجموعة إحداثيات. In Processing, rotations happen in **radians** but you can write the number of **degrees** and use the `radians()` function to convert it to radians, `rotate(radians(90))` would be equal to rotating `90` degrees.

تعمل الأرقام الموجبة على تدوير الكائنات في اتجاه عقارب الساعة وتدور الأرقام السالبة الكائنات عكس اتجاه عقارب الساعة.

### تدوير الشاشة

في هذا المثال ، يتم وضع صورة الكوكب مع وجود مركز الكوكب في منتصف الشاشة. يتم ضبط الشاشة أن تدور حول المركز درجة واحدة في كل مرة يتم إعادة رسمها.

![منطقة الإخراج مع كوكب يدور حول المركز](images/rotate_planet.gif)

--- code ---
---
language: python
---

def draw(): translate(200,200)  # The middle of the screen for i in range(frame_count): image(planet, -150, -150, 300, 300) rotate(radians(1))

--- /code ---

### تدوير أجزاء من الرسم

في هذا المثال، يتم تدوير الشاشة بمقدار `45` درجة عند رسم العينين لمنحها الانطباع بأنها تتحرك.

ومع ذلك، لمحاذاة العيون أفقيًا عبر الشاشة، نريد استعادة الإعدادات الأصلية قبل رسم العين التالية. تقوم الدالة `pushMatrix ()` بحفظ الإعدادات كما كانت قبل رسم العين الأولى ثم تستعيد الدالة `popMatrix ()` هذه الإعدادات قبل رسم العين الثانية.

تتم إعادة تعيين جميع الترجمات والتدويرات في كل مرة يبدأ فيها الرسم `draw()` مرة أخرى.

![منطقة الإخراج مع صورة متحركة تظهر عين دوارة مصنوعة من الدوائر](images/rotate_eyes.gif)

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
