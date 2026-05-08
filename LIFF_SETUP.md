# MyWay LIFF Setup

คู่มือนี้สำหรับทำให้ MyWay เปิดใน LINE OA แบบเชื่อม LIFF จริง ไม่ใช่แค่เปิดเว็บใน browser ของ LINE

## หลักสำคัญ

ถ้าส่งลิงก์ GitHub Pages ตรง ๆ เช่น

```text
https://your-username.github.io/myway-liff/
```

เว็บจะเปิดได้ แต่จะไม่ถือว่าเป็น LIFF เต็มรูปแบบในหลายกรณี และอาจไม่เชื่อมกับ LINE profile ตามที่ต้องการ

ให้ใช้ลิงก์ LIFF แบบนี้ใน LINE OA:

```text
https://liff.line.me/YOUR_LIFF_ID
```

## 1. Deploy ด้วย GitHub Pages

อัปโหลดไฟล์เหล่านี้ไปที่ GitHub repo:

- `index.html`
- `LIFF_SETUP.md`

จากนั้นเปิด GitHub Pages จะได้ URL ประมาณนี้:

```text
https://your-username.github.io/myway-liff/
```

URL นี้คือ Endpoint URL สำหรับตั้งค่าใน LINE Developers

## 2. สร้าง LIFF App ใน LINE Developers

1. เข้า LINE Developers Console
2. เลือก Provider
3. เลือก Channel ประเภท LINE Login
4. ไปที่แท็บ LIFF
5. กด Add
6. ตั้งค่า:
   - LIFF app name: `MyWay`
   - Size: `Full`
   - Endpoint URL: ใส่ GitHub Pages URL เช่น

```text
https://your-username.github.io/myway-liff/
```

7. เปิด Scope:
   - `profile`
8. Save
9. Copy `LIFF ID`

## 3. ใส่ LIFF ID ในไฟล์ index.html

เปิดไฟล์ `index.html` แล้วค้นหาบรรทัดนี้:

```js
const MYWAY_LIFF_ID = "";
```

ใส่ LIFF ID จริง เช่น:

```js
const MYWAY_LIFF_ID = "2000000000-AbCdEfGh";
```

จากนั้น commit / upload ไฟล์ `index.html` กลับขึ้น GitHub อีกครั้ง แล้วรอ GitHub Pages อัปเดตประมาณ 1-5 นาที

## 4. ใส่ลิงก์ใน LINE OA

อย่าใช้ GitHub Pages URL ตรง ๆ เป็นปุ่มใน LINE OA หากต้องการเปิดเป็น LIFF

ให้ใช้:

```text
https://liff.line.me/YOUR_LIFF_ID
```

ตัวอย่าง:

```text
https://liff.line.me/2000000000-AbCdEfGh
```

นำลิงก์นี้ไปใส่ใน:

- Rich Menu
- Broadcast message
- Auto response
- Flex Message button
- Card Message button

## 5. การทำงานที่แอปรองรับแล้ว

- Init LIFF อัตโนมัติจาก `MYWAY_LIFF_ID`
- ไม่มีช่องกรอก LIFF ID บนหน้า Interface แล้ว
- ดึงชื่อ LINE profile มาเติมเป็นผู้กรอกข้อมูลอัตโนมัติ เมื่อผู้ใช้ login แล้วและช่องยังว่าง
- ตรวจได้ว่าเปิดอยู่ใน LINE หรือ Browser
- แชร์สรุปรายงานเข้า LINE ผ่าน Share Target Picker

## 6. ถ้ายังไม่เชื่อม LINE

ตรวจ 4 จุดนี้:

1. เปิดจากลิงก์ `https://liff.line.me/YOUR_LIFF_ID`
2. ใน LINE Developers ตั้ง Endpoint URL เป็น GitHub Pages URL ที่ถูกต้อง
3. ในไฟล์ `index.html` ใส่ `MYWAY_LIFF_ID` แล้ว
4. GitHub Pages อัปเดตไฟล์ล่าสุดแล้ว

## 7. หมายเหตุเรื่องข้อมูล

ข้อมูลลูกค้ายังเก็บใน `localStorage` ของเครื่อง/LINE browser นั้น ๆ หากต้องการให้โค้ชหลายคนเห็นข้อมูลเดียวกัน ต้องเพิ่ม backend/database ภายหลัง เช่น Firebase, Supabase หรือ API server
