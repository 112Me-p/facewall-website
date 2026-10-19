# FACEWALL — Website Draft 01

เว็บไซต์ต้นแบบแบบ Static (HTML/CSS/JavaScript) สำหรับตรวจดีไซน์ก่อนนำไปพัฒนา **WordPress** จริง

## หน้าเว็บไซต์

| หน้า | ไฟล์ | ทดลองทำอะไรได้บ้าง |
|---|---|---|
| Home | `index.html` | Hero / หมวดสินค้า / preview เปรียบเทียบภาพ / คอลเลกชันตัวอย่าง |
| Showcase | `showcase.html` | Before/After Slider ที่ลากและใช้คีย์บอร์ดได้ / กรองประเภทแนวคิด |
| Catalog | `catalog.html` | ค้นหา / กรองประเภท สี สไตล์ / ดูรายละเอียด / ♡ บันทึก / เพิ่มรายการ |
| Contact | `contact.html` | สรุปรายการวัสดุ / กรอกบรีฟ / ดูข้อความตัวอย่าง / คัดลอกข้อความสอบถาม |

## อัปโหลดขึ้น GitHub Pages

1. สร้าง Repository ใหม่บน GitHub เช่น `facewall-website` (เลือก Public หากใช้ Pages แบบ public)
2. แตกไฟล์ ZIP ให้เรียบร้อย แล้วอัปโหลด **ไฟล์และโฟลเดอร์ด้านใน** ทั้งหมดเข้าไปที่ Root ของ Repository (ต้องมี `index.html` อยู่ด้านบนสุด)
3. Commit ไฟล์ไปยังสาขา `main`
4. ไปที่ **Settings → Pages → Build and deployment** และเลือก **Deploy from a branch**, `main`, `/ (root)` แล้ว Save
5. รอ GitHub Pages เผยแพร่ แล้วเข้า URL ประมาณ `https://<username>.github.io/facewall-website/`
6. ทดสอบบนคอมพิวเตอร์และมือถือ แล้วส่งข้อแก้ไขสำหรับ Draft 02

อีกวิธี: ถ้าติดตั้ง Git ใช้ `git add . && git commit -m "FACEWALL Draft 01" && git push` ในโฟลเดอร์โปรเจกต์

## ข้อจำกัดใน Draft 01 (สำคัญ)

- **ไม่ใช่ WordPress ที่ทำงานจริง**: ไม่มีหลังบ้าน ไม่มีฐานข้อมูล และไม่มีการเชื่อมระบบสมาชิก
- ข้อมูลสินค้า ชื่อ รหัส สเปก และลวดลายเป็น **Demo** ไม่ใช่สินค้า/สต็อก/ราคา FACEWALL จริง
- Before / After เป็น **ภาพตัวอย่างจำลอง** ไม่ใช่ผลงานติดตั้งจริงหรือภาพการเปลี่ยนแปลงเดียวกันทั้งหมด
- ภาพตกแต่งห้องบางรูปดึงจาก **Unsplash image CDN** และต้องใช้อินเทอร์เน็ต ขณะออฟไลน์จะมีภาพ SVG สำรอง (ควรเปลี่ยนเป็นภาพที่แบรนด์มีสิทธิใช้งานก่อนเปิดเว็บจริง)
- แบบฟอร์ม Contact จะสร้างและคัดลอกข้อความไปยังคลิปบอร์ดเท่านั้น **ไม่ได้ส่งข้อมูลถึงบริษัท** เพราะยังไม่มีบัญชี LINE OA/ช่องทาง API จริง
- Favorites และรายการปรึกษาจัดเก็บใน `localStorage` เฉพาะเบราว์เซอร์นั้น ไม่ซิงค์ข้ามอุปกรณ์
- หน้าเว็บมี `noindex,nofollow` กันไม่ให้เว็บต้นแบบถูกทำดัชนี ต้องยกเลิกเมื่อเว็บไซต์จริงพร้อมเผยแพร่และตรวจ SEO แล้ว

## แก้ไข CI และเตรียมเปลี่ยนชื่อแบรนด์

- `js/config.js` มี `brandName: 'FACEWALL'`, `brandSubtitle: 'WALLPAPER & FLOORING'`, และ `futureBrandName: 'FACEWALL FLOORING'`
- ปรับชุดสีหลักที่ `js/config.js` หรือ `css/style.css` (สีส้มหลักประมาณ `#dc7d5e`)
- เปลี่ยนภาพโลโก้ส่วนหัว/ท้ายเว็บที่ `assets/facewall-logo-white.png` เป็น wordmark ใหม่เมื่อตัดสินใจเปลี่ยนชื่อ เพราะตัวอักษรโลโก้เป็นไฟล์รูป
- โลโก้ปัจจุบันนำมาจากภาพ CI ที่ผู้ใช้ให้แล้วลบฉากหลังสีส้มเพื่อทำไฟล์สำหรับเว็บไซต์

## แนวทางย้ายไป WordPress

- ใช้ธีมเบา ๆ + Elementor หรือ WordPress Block Editor เพื่อทำส่วนหน้า (Header, Hero, CTA, Footer)
- สร้าง `Custom Post Type` สำหรับ **Projects** (Before/After + วัสดุที่ใช้) และ **Materials** (ชื่อ / รหัส / รูป / ประเภท / สี / สไตล์)
- สร้าง taxonomy สำหรับประเภทวัสดุ สี สไตล์ เพื่อให้ filter ใช้ข้อมูลจริงแทน `products.js`
- Before/After Slider ย้ายได้ด้วย Elementor HTML widget หรือ JavaScript enqueued ในธีมลูก
- ฟอร์ม Contact ใช้ปลั๊กอินฟอร์มที่มีการแจ้งเตือนและจัดการข้อมูลตาม PDPA ก่อนเปิดรับข้อมูลจริง

## โครงสร้างไฟล์

```
facewall-draft01/
├── index.html
├── showcase.html
├── catalog.html
├── contact.html
├── css/style.css
├── js/config.js
├── js/products.js
├── js/app.js
└── assets/ (โลโก้ SVG ภาพประกอบสำรอง)
```

**หมายเหตุ:** เว็บต้นแบบเป็นงานนำเสนอเพื่อเลือกดีไซน์ ข้อมูลต้องตรวจสอบและเปลี่ยนเป็นข้อมูลจาก FACEWALL ก่อนเปิดใช้งานเว็บไซต์จริง
