ระบบจะดึงโน้ตทุกใบที่มี Tag `#cybersecurity` มาทำเป็นตารางสรุปให้คุณทันทีโดยไม่ต้องค้นหาเอง

```dataview
TABLE severity AS "ระดับความรุนแรง", status AS "สถานะ"
FROM #cybersecurity
SORT severity DESC
```

