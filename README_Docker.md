# E-Borrow System Docker Setup

## 🚀 Quick Start

### 1. เปิด Docker Desktop
- เปิดโปรแกรม Docker Desktop
- รอให้สถานะเป็น "Docker Desktop is running"

### 2. รันระบบ
```bash
docker-compose up -d
```

### 3. เข้าถึงแอปพลิเคชัน
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:5000
- **MySQL Database**: localhost:3306

## 📋 คำสั่งที่ใช้บ่อย

```bash
# เริ่มต้นระบบ
docker-compose up -d

# ดูสถานะ
docker-compose ps

# ดู logs
docker-compose logs -f

# หยุดระบบ
docker-compose down

# รีสตาร์ท
docker-compose restart
```

## ⚙️ การตั้งค่า

แก้ไขไฟล์ `docker-compose.yml` เพื่อเปลี่ยนค่า environment variables ตามความต้องการ

## 🔧 การแก้ไขปัญหา

```bash
# ลบและ rebuild
docker-compose down
docker-compose up --build -d
```
