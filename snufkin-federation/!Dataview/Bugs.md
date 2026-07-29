
```dataview
TABLE due_date AS "เดดไลน์", priority AS "ความสำคัญ", status AS "สถานะ"
FROM #Bugs
WHERE status != "Completed"
SORT due_date ASC
```