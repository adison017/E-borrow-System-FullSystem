# Environment Variables Setup Guide

## การตั้งค่า Environment Variables

### 1. สร้างไฟล์ `.env`

สร้างไฟล์ `.env` ในโฟลเดอร์หลักของโปรเจค และใส่ค่าต่อไปนี้:

```env
# MySQL Database Configuration
MYSQL_ROOT_PASSWORD=rootpassword
MYSQL_DATABASE=eborrow_db
MYSQL_USER=root
MYSQL_PASSWORD=rootpassword

# Backend Environment Variables
NODE_ENV=production
DB_HOST=mysql
DB_USER=root
DB_PASS=rootpassword
DB_NAME=eborrow_db
DB_PORT=3306

# JWT Configuration
JWT_SECRET=your_jwt_secret_key_here

# Cloudinary Configuration
CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

# Line Notify Configuration
LINE_NOTIFY_TOKEN=your_line_notify_token

# Email Configuration
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_email_app_password

# Frontend URLs
FRONTEND_URLS=http://localhost:5173,http://frontend:5173

# Frontend Environment Variables
REACT_APP_API_URL=http://localhost:5000
REACT_APP_SOCKET_URL=http://localhost:5000
```

### 2. แก้ไขค่าตามความต้องการ

**สำคัญ**: เปลี่ยนค่าต่อไปนี้เป็นค่าจริงของคุณ:

- `JWT_SECRET`: สร้างรหัสลับสำหรับ JWT
- `CLOUDINARY_CLOUD_NAME`: ชื่อ cloud ของ Cloudinary
- `CLOUDINARY_API_KEY`: API Key ของ Cloudinary
- `CLOUDINARY_API_SECRET`: API Secret ของ Cloudinary
- `LINE_NOTIFY_TOKEN`: Token สำหรับ Line Notify
- `EMAIL_USER`: อีเมล Gmail ของคุณ
- `EMAIL_PASS`: App Password ของ Gmail

### 3. ความปลอดภัย

- **อย่า commit ไฟล์ `.env` ไปยัง Git**
- ไฟล์ `.env` ควรอยู่ใน `.gitignore`
- ใช้ `.env.example` เป็นเทมเพลตสำหรับทีม

### 4. การใช้งาน

หลังจากสร้างไฟล์ `.env` แล้ว ให้รันคำสั่ง:

```bash
docker-compose up -d
```

## ข้อดีของการใช้ .env file

✅ **ความปลอดภัย**: ไม่มีข้อมูลลับในโค้ด
✅ **ความยืดหยุ่น**: เปลี่ยนค่าได้ง่าย
✅ **การทำงานเป็นทีม**: ทุกคนใช้การตั้งค่าของตัวเอง
✅ **การ deploy**: ใช้ค่าต่างกันในแต่ละ environment
