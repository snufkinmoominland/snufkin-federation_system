```dataview
TABLE category AS "เครื่องมือ/ระบบ", description AS "คำอธิบายการทำงาน", usage AS "ความบ่อยในการใช้"

FROM #linux
SORT category ASC
```

### 🔍 รวมคำสั่ง Nmap สำหรับสแกนระบบ


```bash
# สแกนหาเวอร์ชันของบริการ (Service Version Detection)
nmap -sV 192.168.1.1

# สแกนพอร์ตแบบเร็วและเปิดเผยน้อยที่สุด (Syn Stealth Scan)
nmap -sS -Pn 10.0.0.5

```