# ระบบจัดการสินค้าคงคลัง Golang (CRUD)

[![Go Version](https://img.shields.io/badge/Go-1.21+-blue.svg)](https://golang.org)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Active-brightgreen.svg)]()

> ระบบบริหารสินค้าคงคลังผ่านเว็บ ที่พัฒนาด้วย Go พร้อมระบบตรวจสอบสิทธิ์ การจัดการสินค้า และการควบคุมสต็อก

**For English Version:** [README_EN.md](README_EN.md)

## ✨ ฟีเจอร์หลัก

### 🔐 ระบบการตรวจสอบสิทธิ์
- เข้าสู่ระบบด้วย Username/Password
- จัดการเซสชั่นโดยใช้ Gorilla Sessions
- ควบคุมสิทธิ์ตามบทบาท (Admin/Staff)
- การออกจากระบบที่ปลอดภัย
- Middleware สำหรับตรวจสอบการเข้าสู่ระบบ

### 📦 การจัดการสินค้า
- สร้าง อ่าน แก้ไข ลบ สินค้า
- จำแนกสินค้าตามหมวดหมู่
- ติดตามระดับสต็อก (ขั้นต่ำ/สูงสุด)
- รองรับหน่วยวัดต่างๆ
- ติดตามต้นทุนและราคาขาย
- จัดการสถานะสินค้า
- รองรับบาร์โค้ด

### 🏷️ การจัดการหมวดหมู่
- ดำเนินการหมวดหมู่สินค้า
- จัดระเบียบสินค้าตามหมวดหมู่
- กรองตามหมวดหมู่อย่างรวดเร็ว

### 📊 การจัดการสต็อก
- **รับสินค้าเข้า**: บันทึกสินค้าเข้าคลัง
- **เบิกออก**: บันทึกการเบิกสินค้า
- **ติดตามการเคลื่อนย้าย**: ติดตามธุรกรรมสต็อกทั้งหมด
- อัปเดตระดับสต็อกโดยอัตโนมัติ
- เตือนเมื่อสต็อกต่ำ

### 🔍 ค้นหาและกรอง
- ค้นหาตามชื่อสินค้า
- ค้นหาตามรหัสสินค้า
- กรองตามหมวดหมู่
- กรองตามสถานะ
- กรองแบบไดนามิก

### 📈 แดชบอร์ด
- ภาพรวมสินค้าคงคลัง
- แสดงสถานะสต็อกด้วยภาพ
- ธุรกรรมล่าสุด
- สถานะระบบ

## 🛠️ สแต็กเทคโนโลยี

| องค์ประกอบ | เทคโนโลยี |
|-----------|-----------|
| **Backend** | Go (1.21+) |
| **ฐานข้อมูล** | MySQL |
| **Frontend** | HTML5, CSS3, JavaScript |
| **Templates** | Go html/template |
| **Session Management** | Gorilla Sessions |
| **HTTP Framework** | Go net/http |

## 📋 ข้อกำหนดเบื้องต้น

ก่อนเริ่มต้น โปรดติดตั้งสิ่งต่อไปนี้:

- **Go 1.21** ขึ้นไป - [ดาวน์โหลด](https://golang.org/dl/)
- **MySQL 5.7** ขึ้นไป - [ดาวน์โหลด](https://www.mysql.com/downloads/)
- **Git** - [ดาวน์โหลด](https://git-scm.com/)
- **PowerShell** (สำหรับผู้ใช้ Windows)

## ⚙️ การติดตั้ง

### ขั้นที่ 1: Clone Repository

```bash
# Clone จาก git
git clone https://github.com/Punyawit1/Dashboard-CRUD-Golang.git
cd golang-crud
```

### ขั้นที่ 2: ตั้งค่าฐานข้อมูล

```bash
# เปิด MySQL Command Line
mysql -u root -p

# สร้างฐานข้อมูล
CREATE DATABASE golang_crud;
USE golang_crud;

# นำเข้าโครงสร้างตาราง
SOURCE Readme/database.sql;

# ออกจาก MySQL
EXIT;
```

**ข้อมูลเข้าสู่ระบบเริ่มต้น:**
- Username: `admin`
- Password: `admin123`

### ขั้นที่ 3: ติดตั้ง Go Dependencies

```bash
go mod download
go mod tidy
```

Package ที่ต้องใช้:
- `github.com/go-sql-driver/mysql` - MySQL database driver
- `github.com/gorilla/sessions` - Session management
- `github.com/gorilla/securecookie` - Secure cookies

### ขั้นที่ 4: อัปเดตการเชื่อมต่อฐานข้อมูล

แก้ไข `main.go` และอัปเดต connection string (ประมาณบรรทัด 50):

```go
// อัปเดตข้อมูล MySQL ของคุณ
dsn := "username:password@tcp(localhost:3306)/golang_crud?parseTime=true"
```

### ขั้นที่ 5: รันแอปพลิเคชัน

**วิธีที่ 1: ใช้ PowerShell Script (Windows)**
```powershell
.\Readme\start.ps1
```

**วิธีที่ 2: ใช้ Go โดยตรง**
```bash
go run main.go
```

แอปพลิเคชันจะเริ่มบนที่อยู่: **http://localhost:8080**

## 🚀 เริ่มต้นอย่างรวดเร็ว

1. **เข้าถึงแอปพลิเคชัน**
   - เปิดเว็บเบราว์เซอร์ของคุณ
   - ไปที่: http://localhost:8080

2. **เข้าสู่ระบบ**
   - Username: `admin`
   - Password: `admin123`

3. **การตั้งค่าครั้งแรก**
   - คลิก "สินค้า" เพื่อเพิ่มสินค้าชิ้นแรก
   - กรอกรายละเอียดสินค้า (ชื่อ รหัส ราคา สต็อก)
   - บันทึกสินค้า
   - ทดสอบการเคลื่อนย้ายสต็อกโดยใช้ "รับสินค้าเข้า"

## 📁 โครงสร้างโปรเจค

```
golang-crud/
├── main.go                 # ไฟล์แอปพลิเคชันหลัก
├── go.mod                  # Go module definition
├── README.md              # เอกสารภาษาไทย (ไฟล์นี้)
├── README_EN.md           # เอกสารภาษาอังกฤษ
├── Readme/                # โฟลเดอร์เอกสาร
│   ├── QUICKSTART.md      # คู่มือเริ่มต้นอย่างรวดเร็ว
│   ├── FEATURES.md        # รายการฟีเจอร์โดยละเอียด
│   ├── SETUP.md           # คำแนะนำการตั้งค่า
│   ├── USAGE_GUIDE.md     # คู่มือการใช้งาน
│   ├── USER_MANUAL.md     # คู่มือผู้ใช้
│   ├── CATEGORY_MANAGEMENT.md
│   ├── README_INVENTORY.md
│   ├── README_TH.md       # เอกสารภาษาไทย
│   ├── database.sql       # โครงสร้างฐานข้อมูล
│   └── start.ps1          # PowerShell startup script
└── templates/             # HTML templates
    ├── layout.html        # Base layout template
    ├── login.html         # หน้าเข้าสู่ระบบ
    ├── dashboard.html     # แดชบอร์ด
    ├── product_list.html  # รายการสินค้า
    ├── product_form.html  # ฟอร์มสินค้า
    ├── category_list.html # รายการหมวดหมู่
    ├── category_form.html # ฟอร์มหมวดหมู่
    ├── stock_in.html      # ฟอร์มรับสินค้าเข้า
    ├── stock_out.html     # ฟอร์มเบิกออก
    ├── stock_movements.html # การเคลื่อนย้ายสต็อก
    ├── form.html          # ฟอร์มทั่วไป
    └── list.html          # รายการทั่วไป
```

## 📖 โครงสร้างข้อมูลหลัก

### ผู้ใช้
```go
type User struct {
    ID        int
    Name      string
    Email     string
    Phone     string
    Address   string
    CreatedAt time.Time
}
```

### สินค้า
```go
type Product struct {
    ID            int
    Code          string
    Name          string
    CategoryID    int
    CategoryName  string
    Description   string
    Unit          string
    Price         float64
    Cost          float64
    StockQuantity int
    MinStock      int
    MaxStock      int
}
```

### หมวดหมู่
```go
type Category struct {
    ID          int
    Name        string
    Description string
    CreatedAt   time.Time
}
```

## 🔧 การตั้งค่า

### การเชื่อมต่อฐานข้อมูล
อัปเดต DSN (Data Source Name) ใน `main.go`:

```go
dsn := "username:password@tcp(localhost:3306)/golang_crud?parseTime=true"
```

### Secret Key ของเซสชั่น
เปลี่ยน secret key ของเซสชั่นในการใช้งานจริง:

```go
var store = sessions.NewCookieStore([]byte("change-this-secret-key-in-production"))
```

### พอร์ตเซิร์ฟเวอร์
พอร์ตเริ่มต้นคือ `:8080` ในการแปลง แก้ไขการตั้งค่าเซิร์ฟเวอร์ใน `main.go`

## 🧪 รายการตรวจสอบการทดสอบ

- [ ] เข้าออกระบบได้อย่างถูกต้อง
- [ ] เพิ่มสินค้าใหม่
- [ ] แก้ไขสินค้า
- [ ] ลบสินค้า (soft delete)
- [ ] เพิ่มหมวดหมู่
- [ ] รับสินค้าเข้า
- [ ] เบิกออก
- [ ] ฟังก์ชันค้นหา
- [ ] ฟังก์ชันกรอง
- [ ] แดชบอร์ดแสดงอย่างถูกต้อง

## 📝 ตารางฐานข้อมูล

แอปพลิเคชันใช้ตารางหลักดังต่อไปนี้:

- `users` - การตรวจสอบสิทธิ์และรายละเอียดผู้ใช้
- `products` - สินค้าคงคลัง
- `categories` - หมวดหมู่สินค้า
- `stock_movements` - ประวัติธุรกรรมสต็อก
- `stock_in` - บันทึกสินค้าเข้า
- `stock_out` - บันทึกสินค้าออก

ดูที่ [database.sql](Readme/database.sql) สำหรับโครงสร้างที่สมบูรณ์

## 🐛 การแก้ไขปัญหา

### ปฏิเสธการเชื่อมต่อ
```
Error: Connection refused
```
**วิธีแก้ไข**: ตรวจสอบว่า MySQL กำลังทำงานและการเชื่อมต่อถูกต้อง

### ไม่พบ Module
```
Error: cannot find module
```
**วิธีแก้ไข**: รัน `go mod download` และ `go mod tidy`

### พอร์ตกำลังใช้งานแล้ว
```
Error: Address already in use
```
**วิธีแก้ไข**: เปลี่ยนพอร์ตใน main.go หรือหยุดกระบวนการที่ใช้พอร์ต 8080

### ข้อผิดพลาดของเซสชั่น
ตรวจสอบว่า secret key ของเซสชั่นตั้งค่าถูกต้องและไม่เปลี่ยนแปลงระหว่างการเริ่มการทำงาน

## 📚 เอกสารประกอบ

สำหรับข้อมูลที่ละเอียดมากขึ้น ดูที่:
- [คู่มือเริ่มต้นอย่างรวดเร็ว](Readme/QUICKSTART.md)
- [รายการฟีเจอร์ที่สมบูรณ์](Readme/FEATURES.md)
- [คำแนะนำการตั้งค่า](Readme/SETUP.md)
- [คู่มือการใช้งาน](Readme/USAGE_GUIDE.md)
- [คู่มือผู้ใช้](Readme/USER_MANUAL.md)

## 🎯 การปรับปรุงในอนาคต

- [ ] ปรับปรุง Role-based access control
- [ ] API endpoints (REST)
- [ ] รายงานขั้นสูง
- [ ] การแจ้งเตือนทางอีเมล
- [ ] แอปพลิเคชันมือถือ
- [ ] รองรับคลังสินค้าหลายแห่ง
- [ ] การสแกนบาร์โค้ด
- [ ] ส่งออก Excel/PDF

## 🤝 การมีส่วนร่วม

ยินดีต้อนรับการมีส่วนร่วม! โปรดส่ง Pull Request

## 📄 ใบอนุญาต

โปรเจคนี้อยู่ภายใต้ใบอนุญาต MIT - ดูไฟล์ LICENSE สำหรับรายละเอียด

## 👤 ผู้เขียน

**Punyawit**
- GitHub: [@Punyawit1](https://github.com/Punyawit1)
- Facebook: [Punyawit](https://www.facebook.com/punyawit.richut/)

## 📞 การสนับสนุน

หากคุณพบปัญหา โปรดสือ:
1. ตรวจสอบส่วน [การแก้ไขปัญหา](#-การแก้ไขปัญหา)
2. ตรวจสอบ [เอกสารประกอบ](Readme/)
3. เปิด issue บน GitHub

---

