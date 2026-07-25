ระบบจะดึงโน้ตทุกใบที่มี Tag `#cybersecurity` มาทำเป็นตารางสรุปให้คุณทันทีโดยไม่ต้องค้นหาเอง

```dataview
TABLE severity AS "ระดับความรุนแรง", status AS "สถานะ"
FROM #cybersecurity
SORT severity DESC
```





คำอธิบายโค้ด: ระบบจะดึงโน้ตทุกใบที่มีแท็ก `#task` มาร้อยเรียงเป็นตาราง โดยกรองเอาเฉพาะงานที่ยังทำไม่เสร็จ (`status != "Completed"`) และเรียงลำดับตามวันเดดไลน์ที่ใกล้ที่สุดขึ้นก่อนอัตโนมัติครับ

```dataview
TABLE due_date AS "เดดไลน์", priority AS "ความสำคัญ", status AS "สถานะ"
FROM #task
WHERE status != "Completed"
SORT due_date ASC
```