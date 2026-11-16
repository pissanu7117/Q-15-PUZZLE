15 PUZZLE V2.0 — สถิติส่วนตัว + จัดอันดับออนไลน์ (ทดลอง)

ไฟล์:
1) index.html เกมเดิมธีม 3D 5 สี พร้อมเมนูใหม่
2) firebase-config.js ไฟล์ตั้งค่าระบบออนไลน์ (เริ่มต้นยังไม่เชื่อม)
3) firestore.rules กฎที่ต้องคัดลอกไปยัง Firebase Console
4) firestore.indexes.json แผนผังดัชนีที่ใช้เรียงอันดับ (ต้องสร้าง Composite Index ใน Firestore Console หรือใช้ Firebase CLI)

การทดลองแบบส่วนตัว:
- อัปโหลด index.html และ firebase-config.js เข้า GitHub Pages (หรือเปิด index.html ในเบราว์เซอร์)
- เล่นชนะแล้วดูสถิติในเมนู 'สถิติของฉัน'
- ส่งออก / นำเข้าไฟล์ JSON เพื่อสำรองประวัติ

การเปิดอันดับออนไลน์:
1. เข้า https://console.firebase.google.com/ แล้วสร้างโปรเจกต์
2. เพิ่มแอป Web (ไอคอน </>) คัดลอก firebaseConfig
3. เปิด Authentication > Sign-in method > Anonymous > Enable
4. เปิด Firestore Database (เลือก region ที่ต้องการ; แนะนำเริ่มใน production mode)
5. เปิด Firestore Database > Rules แล้วแทนที่ด้วยข้อความใน firestore.rules กด Publish
6. ใน Firestore > Indexes สร้าง Composite Index สำหรับ collection leaderboard: moves Ascending, seconds Ascending (หรือใช้ไฟล์ firestore.indexes.json ผ่าน Firebase CLI)
7. แก้ firebase-config.js จาก null เป็น object ตามตัวอย่างพร้อมค่าจริงของคุณ
8. อัปโหลด index.html กับ firebase-config.js ไป repo GitHub Pages เดิม
9. เปิดเกม ตั้งชื่อผู้เล่น กดบันทึกชื่อ แล้วเล่นจบเพื่อส่งสถิติ

ข้อควรทราบ:
- ส่วนตัวเล่นแบบไม่เชื่อมอินเทอร์เน็ตได้ (หากโหลดหน้าเว็บได้แล้ว); คะแนนส่วนตัวเก็บเฉพาะเบราว์เซอร์และโดเมนนั้น
- อย่าเปิดหน้าเว็บผ่าน file:// เพื่อทดสอบ Firebase; ใช้ GitHub Pages / HTTPS
- Firebase web config ไม่ใช่รหัสผ่านลับ แต่ต้องใช้ Security Rules ให้ถูกต้อง
- ต้องตั้งค่า Authorized domains หากโดเมน GitHub Pages ของคุณไม่ได้รับอนุญาต
- คะแนนออนไลน์ในเวอร์ชันนี้ยังตรวจความถูกต้องฝั่งเซิร์ฟเวอร์ไม่ได้ จึงเหมาะสำหรับการแข่งขันระหว่างเพื่อนแบบไม่เป็นทางการ
- ฐานข้อมูลอาจปฏิเสธการส่งคะแนนที่แย่ลง แม้ผู้เล่นกดปุ่มส่งซ้ำ; เล่นต่อได้ตามปกติ
- ระบบไม่ได้ส่งข้อมูลประวัติส่วนตัวทั้งหมดขึ้นออนไลน์ ส่งเฉพาะคะแนนที่ดีที่สุดและชื่อผู้เล่น
- หน้าอันดับจำกัด 10 คนและดึงใหม่ตอนเปิด/กดรีเฟรช เพื่อประหยัดโควตา
