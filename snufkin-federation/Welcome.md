"เริ่มต้นสร้างสหพันธ์ความรู้"
https://github.com/snufkinmoominland/snufkin-federation_system
https://snufmin-moominland.gitbook.io/snufmin.moominland-docs/~/changes/1


### 🏛️ สรุปโครงสร้าง:

```
[ Obsidian ในเครื่อง ] 
       │
       ▼ (สั่ง git push)
  [ GitHub ] 
       │
       ▼ (ผูกท่อ Auto-Sync)
  [ GitBook ]  ──►  เว็บไซต์อ่านฟรีสำหรับทุกคน (Learn in Public)
```

### 🛠️ วิธีใช้งานในชีวิตประจำวัน (Workflow)

อัปเดตบทความหรือเขียนเนื้อหาเพิ่ม:

1. **เขียนโน้ตใน Obsidian:** พิมพ์บทความ สร้างลิงก์ หรือเซฟไฟล์รูปตามปกติ
    
2. **เปิด Terminal ในโฟลเดอร์งาน:** (ใช้ทริคพิมพ์ `cmd` ใน Address Bar)
    
3. **ร่ายเวทมนตร์ 3 บรรสั่ง:**
    
    - `git add .`
        
    - `git commit -m "เพิ่มบทเรียนเรื่อง..."`
        
    - `git push`
        

 หน้าเว็บ GitBook ก็จะอัปเดตเนื้อหาใหม่

กดปุ่ม **`Close`** ปิดหน้าต่างนี้ 
ไปอ่านหน้าเว็บ GitBook 