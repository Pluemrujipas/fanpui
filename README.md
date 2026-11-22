# ฝันปุย Fanpui Tales เว็บไซต์

เว็บหน้าเดียว (static) พร้อมขึ้น GitHub Pages แล้วผูกโดเมนจาก Hostinger

> ⚠️ โดเมนในไฟล์ตอนนี้เป็นตัวอย่าง `www.fanpuitales.com`
> เมื่อได้โดเมนจริงแล้ว ให้เปลี่ยนในไฟล์ `index.html`, `robots.txt`, `sitemap.xml`, `CNAME`
> (หรือบอก Claude ให้เปลี่ยนให้ทั้งหมด)

## ไฟล์
| ไฟล์ | ใช้ทำอะไร |
|---|---|
| index.html | หน้าเว็บ (meta, Open Graph, JSON-LD Organization / WebSite / VideoObject) |
| logo.png, logo.webp, favicon.* | โลโก้และไอคอน |
| og.png | รูปตอนแชร์ลิงก์ใน Facebook/LINE (1200x630) |
| thumbs/*.png | ภาพปกคลิปที่วาดเอง ใช้ใน JSON-LD |
| robots.txt, sitemap.xml | สำหรับ Google |
| CNAME | บอก GitHub Pages ว่าใช้โดเมนอะไร |
| .nojekyll | ให้ GitHub ส่งไฟล์ตรงๆ ไม่ต้องแปลง |

## ขั้นตอน 1: อัปขึ้น GitHub
1. สร้าง repo ใหม่ใน GitHub เช่น `fanpui-tales` (Public)
2. อัปไฟล์ทั้งหมดในโฟลเดอร์นี้ขึ้นไปที่ root ของ repo (ลากวางในหน้า "Add file > Upload files" ได้เลย)
3. ไปที่ Settings > Pages > Source เลือก `Deploy from a branch` > branch `main` / `/ (root)` แล้วกด Save
4. ในช่อง Custom domain ใส่โดเมน (เช่น `www.fanpuitales.com`) แล้วกด Save

## ขั้นตอน 2: ตั้งค่า DNS ที่ Hostinger
hPanel > Domains > เลือกโดเมน > DNS / Nameservers แล้วเพิ่ม record:

| Type | Name | Points to |
|---|---|---|
| A | @ | 185.199.108.153 |
| A | @ | 185.199.109.153 |
| A | @ | 185.199.110.153 |
| A | @ | 185.199.111.153 |
| CNAME | www | `<ชื่อผู้ใช้ GitHub>.github.io` |

- ลบ A record เดิมของ `@` และ CNAME เดิมของ `www` ที่ Hostinger ใส่ไว้ (มักชี้ไปที่ parking page)
- รอ DNS 10 นาทีถึงไม่กี่ชั่วโมง แล้วกลับไปที่ Settings > Pages ติ๊ก **Enforce HTTPS**

## ขั้นตอน 3: Google
1. เข้า Google Search Console เพิ่ม property เป็นโดเมน (ยืนยันด้วย TXT record ที่ Hostinger)
2. ส่ง sitemap: `https://<โดเมน>/sitemap.xml`

## ใส่ลิงก์ YouTube ให้การ์ดวิดีโอ (แนะนำ)
ใช้ลิงก์ YouTube แทนการอัปไฟล์วิดีโอขึ้นเว็บ เว็บจะเบามาก
- การ์ดจะใช้ภาพปกจาก YouTube อัตโนมัติ (ถ้าโหลดไม่ได้จะใช้ภาพวาดเดิม)
- กดการ์ดแล้วเล่นคลิปในหน้าเว็บเลย (โหลด YouTube เฉพาะตอนกดดู หน้าแรกจึงไม่ช้า)
- JSON-LD จะได้ embedUrl / contentUrl / thumbnailUrl ให้ Google แสดงเป็นผลวิดีโอ

วิธีแก้: เปิด `../source/site.json` ใส่ลิงก์ใน `"youtube": ""` ของแต่ละเรื่อง (รองรับลิงก์ youtube.com/watch, youtu.be และ youtube.com/shorts) แล้วรัน
`cd source && OUT=../site python3 build.py` หรือส่งลิงก์ให้ Claude ทำให้
