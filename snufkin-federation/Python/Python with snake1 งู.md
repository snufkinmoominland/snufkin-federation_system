---
tags:
  - python
  - snake
due_date: 2026-07-26
priority: High
status: In-Progress
links1: https://docs.python.org/3/library/turtle.html
links2: https://www.pythonclassroom.com/turtle-graphics
---

Turtle Snake

### Step 1: Import the required Python modules
เริ่มต้นด้วยการเรียกใช้เครื่องมือที่จำเป็น และตั้งค่าตัวแปรเริ่มต้น (รวมถึงตัวแปรคะแนนจาก Step 13)

```python
# Import modules
import turtle
import time
import random

# Game variables
delay = 0.1
score = 0
high_score = 0
```



### Step 2: Setup the Turtle screen
สร้างหน้าต่างเกมและตั้งค่าขนาดหน้าจอ
```python
# Turtle screen setup
wn = turtle.Screen()
wn.title("My Snake Game")
wn.bgcolor("black")
wn.setup(width=600, height=600)
wn.tracer(0) # ปิดการอัปเดตหน้าจออัตโนมัติ เพื่อให้ภาพเคลื่อนไหวสมูทขึ้น
```


### Step 3: Create the Snake turtle
สร้าง "หัวงู" (แก้ไขคำสั่ง speed และลบ Typo อักขระที่ซ่อนอยู่ออกทั้งหมด)
```python
# Snake head setup
head = turtle.Turtle()
head.speed(0) # ความเร็วในการวาด (0 คือเร็วสุด)
head.shape("square") # ใช้คำสั่ง shape แทน speed สำหรับรูปทรง
head.color("orange")
head.penup()
head.goto(0, 0)
head.direction = "stop"
```



### Step 4: Function to move the snake
สร้างฟังก์ชันอัปเดตพิกัดตามทิศทาง (แก้ไขคำสั่ง `seat` เป็น `sety` ให้ถูกต้องตามหลักไวยากรณ์)
```python
# Function to move the snake
def move():
    if head.direction == "up":
        y = head.ycor() # y coordinate of the turtle
        head.sety(y + 20)
        
    if head.direction == "down":
        y = head.ycor() # y coordinate of the turtle
        head.sety(y - 20)
        
    if head.direction == "right":
        x = head.xcor() # x coordinate of the turtle
        head.setx(x + 20)
        
    if head.direction == "left":
        x = head.xcor() # x coordinate of the turtle
        head.setx(x - 20)
```



### Step 5: Function to go up, down, right, left
สร้างฟังก์ชันกำหนดทิศทาง โดยต้องมีตรรกะป้องกันไม่ให้งูถอยหลังทับตัวเอง (แก้ไขฟังก์ชันที่ซ้ำกันให้มีครบทั้ง 4 ทิศ)
```python
# Function to go up, down, right, left
def go_up():
    if head.direction != "down":
        head.direction = "up"

def go_down():
    if head.direction != "up":
        head.direction = "down"

def go_right():
    if head.direction != "left":
        head.direction = "right"
            
def go_left():
    if head.direction != "right":
        head.direction = "left"
	
```



### Step 6: Bind the Up, Left, Down, Right keys
เชื่อมโยงปุ่มบนคีย์บอร์ดเข้ากับฟังก์ชัน
```python
# Bind the keys to the functions
wn.listen()
wn.onkeypress(go_up, "Up") # ใช้ onkeypress จะตอบสนองไวกว่า onkey
wn.onkeypress(go_left, "Left")
wn.onkeypress(go_down, "Down")
wn.onkeypress(go_right, "Right")

```


###  Step 7: Create the Snake Food Turtle

สร้างอาหารของงู

```python
# Snake food setup
food = turtle.Turtle()
food.speed(0)
food.shape("circle")
food.color("red")
food.penup()
food.goto(100, 100)
```

### Step  8: Create the Scoreboard (เตรียมการจาก Step 13)

_ตรรกะ: เราควรสร้างป้ายคะแนนเตรียมไว้ตั้งแต่แรก ก่อนที่จะเริ่มเข้าสู่ลูปเกมหลัก_
```python
# Scoreboard setup
pen = turtle.Turtle()
pen.speed(0)
pen.shape("square")
pen.color("white")
pen.penup()
pen.hideturtle() # ซ่อนตัวปากกา โชว์แค่ข้อความ
pen.goto(0, 260)
pen.write("Score: 0  High Score: 0", align="center", font=("Courier", 24, "normal"))
```


### Step 9: Add segments list

สร้าง List ว่างๆ เพื่อเตรียมเก็บ "ส่วนหาง" ของงูที่จะเพิ่มขึ้นมา (แก้ไขตัวสะกด `sefments` เป็น `segments`)
```python
# Add segments list
segments = []
```


### Step 10: Main Game Loop & Border Collision
เริ่มต้นลูปหลักของเกม และใส่ตรรกะเช็คการชนขอบจอ (ถ้าชน ให้รีเซ็ตกลับมาตรงกลาง)
```python
# Main game loop
while True:
    wn.update()
    
    # Check for collision with the border
    if head.xcor() > 290 or head.xcor() < -290 or head.ycor() > 290 or head.ycor() < -290:
        time.sleep(1)
        head.goto(0, 0)
        head.direction = "stop"
        
        # Hide the segments
        for segment in segments:
            segment.goto(1000, 1000)
            
        # Clear segment list
        segments.clear()
        
        # Reset score
        score = 0
        pen.clear()
        pen.write(f"Score: {score}  High Score: {high_score}", align="center", font=("Courier", 24, "normal"))
```

### Step 11: Detect Food Collision & Add Segment (เขียนต่อใน while True)
ตรรกะเมื่อหัวงูกินอาหาร ให้สุ่มตำแหน่งอาหารใหม่ สร้างหางเพิ่ม และอัปเดตคะแนน
```python
# Detect if there's a collision with food (ระยะ 20 เหมาะสมที่สุด)
    if head.distance(food) < 20:
        # Move the food to a random position
        x = random.randint(-290, 290)
        y = random.randint(-290, 290)
        food.goto(x, y)
        
        # Add a segment
        new_segment = turtle.Turtle()
        new_segment.speed(0)
        new_segment.shape("square")
        new_segment.color("gray")
        new_segment.penup()
        segments.append(new_segment)
        
        # Update score
        score += 10
        if score > high_score:
            high_score = score
        pen.clear()
        pen.write(f"Score: {score}  High Score: {high_score}", align="center", font=("Courier", 24, "normal"))
```


### Step 12: Move the Segments (เขียนต่อใน while True)
_ตรรกะสำคัญ: คุณต้องสอนให้ผู้เรียนรู้ว่า เราต้องขยับหางชิ้นสุดท้ายไปหาชิ้นก่อนหน้าไล่มาเรื่อยๆ จนถึงหัว "ห้ามขยับหัวก่อน" ไม่เช่นนั้นหางจะไม่เดินตาม_
```python
# Move the end segments first in reverse order
    for index in range(len(segments)-1, 0, -1):
        x = segments[index-1].xcor()
        y = segments[index-1].ycor()
        segments[index].goto(x, y)
        
    # Move segment 0 to where the head is
    if len(segments) > 0:
        x = head.xcor()
        y = head.ycor()
        segments[0].goto(x, y)
        
    # Move the head (เรียกฟังก์ชัน move หลังจากขยับหางเสร็จแล้ว)
    move()
```

### Step 13: Self-Collision Detection (เขียนต่อใน while True)
สุดท้าย เช็คว่าหัวงูชนกับหางของตัวเองหรือไม่ ถ้าชนก็จบเกมและรีเซ็ต
```python
# Check for head collision with the body segments
    for segment in segments:
        if segment.distance(head) < 20:
            time.sleep(1)
            head.goto(0, 0)
            head.direction = "stop"
            
            # Hide the segments & clear list
            for seg in segments:
                seg.goto(1000, 1000)
            segments.clear()
            
            # Reset score
            score = 0
            pen.clear()
            pen.write(f"Score: {score}  High Score: {high_score}", align="center", font=("Courier", 24, "normal"))

    # Delay of the game loop
    time.sleep(delay)

```

**ข้อแนะนำเพิ่มเติมสำหรับการสอน:** เวลาคุณนำไปสอนจริง ตรง **Step 10, 11, 12, และ 13** คุณควรย้ำกับผู้เรียนว่า _"โค้ดเหล่านี้ต้องอยู่ในระดับย่อหน้า (Indentation) เดียวกันภายใต้คำสั่ง `while True:`"_ เพราะนี่คือจุดที่มือใหม่เขียน Python มักจะพลาดเรื่องการเว้นวรรค (Space/Tab) มากที่สุดครับ



### Step 14: Total  code 

```python
import turtle
import time
import random

# ตั้งค่าดีเลย์และคะแนน (Step 13)
delay = 0.1
score = 0
high_score = 0

# Step 2: Setup the Turtle screen
wn = turtle.Screen()
wn.title("My Snake Game")
wn.bgcolor("black")
wn.setup(width=600, height=600)
wn.tracer(0) # ปิดการอัปเดตหน้าจออัตโนมัติ เพื่อให้ภาพสมูท

# Step 3: Create the Snake turtle (แก้ไข Typo และ Shape แล้ว)
head = turtle.Turtle()
head.speed(0) # 0 คือความเร็วสูงสุดในการวาด
head.shape("square")
head.color("orange")
head.penup()
head.goto(0, 0)
head.direction = "stop"

# Step 7: Create the Snake Food Turtle
food = turtle.Turtle()
food.speed(0)
food.shape("circle")
food.color("red")
food.penup()
food.goto(100, 100)

# Step 9: Add segments list (แก้ไข Typo แล้ว)
segments = []

# Step 13 (ส่วนที่ 1): Scoreboard
pen = turtle.Turtle()
pen.speed(0)
pen.shape("square")
pen.color("white")
pen.penup()
pen.hideturtle() # ซ่อนตัวปากกา โชว์แค่ตัวหนังสือ
pen.goto(0, 260)
pen.write("Score: 0  High Score: 0", align="center", font=("Courier", 24, "normal"))

# Step 4: Function to move the snake (แก้ไข seat เป็น sety แล้ว)
def move():
    if head.direction == "up":
        y = head.ycor()
        head.sety(y + 20)
    if head.direction == "down":
        y = head.ycor()
        head.sety(y - 20)
    if head.direction == "right":
        x = head.xcor()
        head.setx(x + 20)
    if head.direction == "left":
        x = head.xcor()
        head.setx(x - 20)

# Step 5: Function to go up, down, right, left (แก้ไขฟังก์ชันซ้ำแล้ว)
def go_up():
    if head.direction != "down":
        head.direction = "up"
def go_down():
    if head.direction != "up":
        head.direction = "down"
def go_right():
    if head.direction != "left":
        head.direction = "right"
def go_left():
    if head.direction != "right":
        head.direction = "left"

# Step 6: Bind the keys
wn.listen()
wn.onkeypress(go_up, "Up") # แนะนำให้ใช้ onkeypress แทน onkey เพื่อการตอบสนองที่ดีกว่า
wn.onkeypress(go_left, "Left")
wn.onkeypress(go_down, "Down")
wn.onkeypress(go_right, "Right")

# Step 8, 10, 11, 12, 13: Main game loop
while True:
    wn.update()

    # Step 11: Check for collision with border
    if head.xcor() > 290 or head.xcor() < -290 or head.ycor() > 290 or head.ycor() < -290:
        time.sleep(1)
        head.goto(0, 0)
        head.direction = "stop"
        
        # Step 12: Hide the segments & clear list
        for segment in segments:
            segment.goto(1000, 1000)
        segments.clear()
        
        # รีเซ็ตคะแนน
        score = 0
        pen.clear()
        pen.write(f"Score: {score}  High Score: {high_score}", align="center", font=("Courier", 24, "normal"))

    # Step 10: Detect if there's a collision with food (ปรับระยะชนเป็น 20 เพื่อความแม่นยำ)
    if head.distance(food) < 20:
        # Move the food to a random position
        x = random.randint(-290, 290)
        y = random.randint(-290, 290)
        food.goto(x, y)
        
        # Add a segment
        new_segment = turtle.Turtle()
        new_segment.speed(0)
        new_segment.shape("square")
        new_segment.color("gray")
        new_segment.penup()
        segments.append(new_segment)
        
        # เพิ่มคะแนน (Step 13)
        score += 10
        if score > high_score:
            high_score = score
        pen.clear()
        pen.write(f"Score: {score}  High Score: {high_score}", align="center", font=("Courier", 24, "normal"))

    # Move the end segments in reverse order (ต้องทำก่อนเลื่อนหัวงู)
    for index in range(len(segments)-1, 0, -1):
        x = segments[index-1].xcor()
        y = segments[index-1].ycor()
        segments[index].goto(x, y)
        
    # Move segment 0 to where the head is
    if len(segments) > 0:
        x = head.xcor()
        y = head.ycor()
        segments[0].goto(x, y)

    move()

    # Step 13 (ส่วนที่ 2): Check for head collision with body segments
    for segment in segments:
        if segment.distance(head) < 20:
            time.sleep(1)
            head.goto(0, 0)
            head.direction = "stop"
            
            # ซ่อนหางและล้างข้อมูล
            for seg in segments:
                seg.goto(1000, 1000)
            segments.clear()
            
            # รีเซ็ตคะแนน
            score = 0
            pen.clear()
            pen.write(f"Score: {score}  High Score: {high_score}", align="center", font=("Courier", 24, "normal"))

    time.sleep(delay)


```