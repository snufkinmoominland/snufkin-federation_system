

## ปัญหา
โจทย์/ข้อความบางที่ฝัง **อักขระที่มองด้วยตาเปล่าไม่เห็น** เช่น
`U+200B` (Zero-Width Space), `U+200C`, `U+200D`, `U+FEFF` (BOM), `U+2060`
เวลา copy-paste จะติดไปโดยไม่รู้ตัว ซึ่ง:
- ใช้เป็น "ลายเซ็น" สำหรับตรวจจับว่าข้อความถูก copy ไปให้ AI
- ทำให้โค้ด/ข้อความมี garbage เก็บซ่อนอยู่

## วิธีลบ: PowerShell

````markdown
```powershell
$f = "path\to\file.txt"
$c = Get-Content -Raw -LiteralPath $f
$c = $c -replace '[\u200B-\u200F\uFEFF\u2060]',''
Set-Content -LiteralPath $f -Value $c -NoNewline
````

หรือแบบ loop หลายไฟล์:

```powershell
Get-ChildItem -Path "C:\folder" -Filter *.txt -Recurse | ForEach-Object {
    $c = Get-Content -Raw -LiteralPath $_.FullName
    $c = $c -replace '[\u200B-\u200F\uFEFF\u2060]',''
    Set-Content -LiteralPath $_.FullName -Value $c -NoNewline
}
```

## หมายเหตุ

- ใช้ regex: `[\u200B-\u200F\uFEFF\u2060]` ครอบอักขระ invisible ทั้งหมด
- ทำกับ **ไฟล์ copy/สำรอง** ก่อนรัน เพื่อกัน damage ไฟล์ต้นฉบับ
- เหมาะกับการทำความสะอาดข้อความก่อน process โดยเครื่องมือ AI