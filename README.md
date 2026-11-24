# ละมุน Soap Studio — Landing Page

เว็บไซต์ร้านสบู่ตัวอย่าง 2 SKUs พร้อมตะกร้า, checkout, หน้าจัดการหยิบ/แพ็ค, และพิมพ์ใบปะหน้าพัสดุ

## โครงสร้าง
- `index.html`, `styles.css`, `app.js` — เว็บไซต์
- `assets/images/` — รูปสินค้าแยกโฟลเดอร์
- `google-apps-script/Code.gs` — API เชื่อม Google Sheets
- `vercel.json` — ตั้งค่า deploy

## ทดลองทันที
เปิด `index.html` หรือ deploy ขึ้น Vercel ได้เลย โดยยังไม่ต้องตั้งค่า API ระบบจะใช้ localStorage ในเบราว์เซอร์เพื่อสาธิตคำสั่งซื้อ (ข้อมูลนี้ไม่ใช่ฐานข้อมูลกลาง และไม่ซิงก์ข้ามเครื่อง)

## เชื่อม Google Sheets
1. สร้าง Google Sheet ใหม่ ตั้งชื่อ `Lamoon Orders`
2. ไปที่ Extensions → Apps Script
3. วางโค้ดจาก `google-apps-script/Code.gs`
4. แก้ `ADMIN_KEY` เป็นรหัสลับที่คาดเดายาก และแก้ `SHEET_ID` เป็น ID จาก URL ของชีต
5. Deploy → New deployment → Web app
6. Execute as: Me; Who has access: Anyone (จำเป็นสำหรับหน้าเว็บสาธารณะ) แล้วกด Deploy
7. คัดลอก Web app URL ไปใส่ใน `API_URL` ที่บรรทัดต้น ๆ ของ `app.js`
8. Commit และ push ไป GitHub อีกครั้ง เพื่อให้ Vercel deploy เวอร์ชันใหม่

> ข้อควรระวัง: ตัวอย่างนี้เป็นงานสาธิต อย่าเก็บข้อมูลอ่อนไหวเกินจำเป็น และอย่าเผยแพร่ ADMIN_KEY ในเว็บไซต์จริง เพราะ JavaScript ฝั่ง browser อ่านได้ ควรย้ายงานผู้ดูแลไปใช้ระบบล็อกอิน/เซิร์ฟเวอร์ที่ตรวจสิทธิ์จริงก่อนใช้งานจริง

## Deploy GitHub + Vercel
1. สร้าง repository ใหม่บน GitHub เช่น `lamoon-soap-store`
2. อัปโหลดไฟล์และโฟลเดอร์ทั้งหมดในโปรเจกต์นี้ (อย่าอัปโหลดไฟล์ ZIP อย่างเดียว)
3. เข้า Vercel → Add New → Project → Import Git Repository
4. เลือก repo นี้; Framework Preset = Other; Build Command เว้นว่าง; Output Directory = `.`; กด Deploy
5. ส่ง URL ที่ลงท้าย `.vercel.app`

## SKU ตัวอย่าง
- SOAP-001 สบู่ข้าวโอ๊ต & น้ำนม ราคา 89 บาท
- SOAP-002 สบู่ชาเขียว & มินต์ ราคา 99 บาท

## ฟังก์ชัน
- เพิ่ม/ลดจำนวนสินค้าในตะกร้า
- บันทึกคำสั่งซื้อไป Google Sheets เมื่อเชื่อม API
- แสดงรายการออเดอร์และเปลี่ยนสถานะหยิบ/แพ็ค
- สร้างใบปะหน้าพัสดุสำหรับพิมพ์

ใบปะหน้าเป็นเอกสารที่อยู่ผู้รับ ไม่ใช่ใบขนส่ง/เลข Tracking จากบริษัทขนส่ง ต้องนำข้อมูลไปสร้าง shipment ในระบบขนส่งอีกครั้ง
