# MyWay LIFF Setup

วิธีนำ MyWay ไปใช้เป็นลิงก์ใน LINE OA

## 1. Deploy Web App

LIFF ต้องใช้ URL แบบ HTTPS เท่านั้น เช่น

```text
https://your-domain.com/
```

สามารถ deploy ไฟล์ `index.html` ไปที่บริการ static hosting เช่น Vercel, Netlify, Firebase Hosting, Cloudflare Pages หรือ hosting ของคุณเอง

## 2. สร้าง LIFF App

1. เข้า LINE Developers Console
2. เลือก Provider และ Channel ประเภท LINE Login
3. ไปที่แท็บ LIFF
4. กด Add
5. ตั้งค่า Endpoint URL เป็น URL ที่ deploy แล้ว เช่น

```text
https://your-domain.com/
```

6. เลือก Size ตามการใช้งาน
   - Full เหมาะกับ Dashboard
   - Tall เหมาะกับมือถือและฟอร์มสั้น
7. เปิด Scope `profile` เพื่อให้แอปอ่านชื่อ LINE ของผู้เปิดได้
8. Copy LIFF ID

## 3. ใช้ลิงก์ใน LINE OA

ใช้ลิงก์รูปแบบนี้:

```text
https://your-domain.com/?liffId=YOUR_LIFF_ID
```

นำลิงก์นี้ไปใส่ใน:

- Rich Menu
- Broadcast message
- Auto response
- Card message button
- Flex message action

## 4. สิ่งที่แอปรองรับแล้ว

- โหลด LINE LIFF SDK
- Init LIFF จาก `?liffId=...`
- บันทึก LIFF ID ในเครื่องได้
- Login LINE
- ดึงชื่อ LINE Profile แล้วเติมเป็นชื่อผู้กรอกข้อมูลอัตโนมัติเมื่อยังว่าง
- แชร์สรุปรายงานกลับเข้า LINE ผ่าน Share Target Picker ถ้าเปิดใน LIFF
- ถ้าไม่ได้เปิดใน LIFF จะ fallback เป็น native share หรือ copy text

## 5. หมายเหตุ

ข้อมูลลูกค้ายังเก็บใน `localStorage` ของเครื่อง/LINE browser นั้น ๆ หากต้องการให้โค้ชหลายคนเห็นข้อมูลเดียวกัน ต้องเพิ่ม backend/database ภายหลัง เช่น Supabase, Firebase หรือ API server
