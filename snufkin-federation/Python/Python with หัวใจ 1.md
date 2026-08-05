---
tags:
  - python
  - heart
due_date: 2026-07-30
priority: High
status: In-Progress
links1:
links2:
---


```python


for row in range(6):
	for col in range(7):
		if (row==() and col%3!=0) or (row==1 and col%3==0) or (row-col==2) or (row+col==8):
			print('*',end=" ")
		else:
			print(end="  ")
	print()

