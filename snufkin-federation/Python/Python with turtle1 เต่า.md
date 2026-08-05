---
tags:
  - python
  - turtle
due_date: 2026-07-26
priority: High
status: In-Progress
links: https://docs.python.org/3/library/turtle.html
---

ใช้วาดรูปทรงเรขาคณิต

วาดรูป 4 เหลี่ยม 

```python
import turtle as t

#การทำ loop วนซ้ำ 4 ครั้ง
for i in range(4):
#t = turtleเต่า 
#ไปข้างหน้า 100
#หันซ้าย 90 องศา 
	t.forward(100)
	t.left(90)
	
```



วาดรูป 5 เหลี่ยม
```python
import turtle as t
#สร้างตัวแปร 
countSide = 6
#เปลี่ยนค่าคงที่ เป็นชื่อ ตัวแปร
for i in range(countSide):
	t.forward(100)
	#แทนการเลี้ยว 90 ก็ใช้ 360องศา หารด้วยจำนวนด้านที่เราต้องการ
	t.left(360/countSide)
```



```python

import turtle as t

#รับค่าตัวแปรชื่อcountSideมา
def writePic(countSide):
	for i in range(countSide):
		t.forward(100)
		t.left(360/countSide)

countSide = 5

#เรียกให้ทำงาน
writePic(countSide)

```



ลองดู 
```python
from turtle import *

for steps in range(100):
    for c in ('blue', 'red', 'green'):
        color(c)
        forward(steps)
        right(30)
```



สามารถทดลองเพิ่มเติมได้ตามลิ้งค์ [[https://docs.python.org/3/library/turtle.html]]