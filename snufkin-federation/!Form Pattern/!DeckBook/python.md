ระบบจะดึงโน้ตทุกใบที่มี Tag `#Python` มาทำเป็นตารางสรุปให้คุณทันทีโดยไม่ต้องค้นหาเอง
```dataview
TABLE severity AS "เรื่อง", status AS "สถานะ"
FROM #python
SORT severity DESC
```