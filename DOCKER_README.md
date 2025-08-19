# E-Borrow System - Docker Setup

## การติดตั้งและใช้งานด้วย Docker

### ข้อกำหนดเบื้องต้น
- Docker Desktop (เวอร์ชันล่าสุด)
- Docker Compose
- Git

### ขั้นตอนการติดตั้ง

#### 1. Clone โปรเจค
```bash
git clone <repository-url>
cd E-borrow-system
```

#### 2. ตั้งค่า Environment Variables (ถ้าจำเป็น)
โปรเจคนี้มาพร้อมกับ environment variables ที่ตั้งค่าไว้แล้วใน `docker-compose.yml` แต่ถ้าต้องการเปลี่ยนค่า ให้สร้างไฟล์ `.env` ในโฟลเดอร์หลัก:

```bash
# คัดลอกไฟล์ตัวอย่าง
cp env.example .env

# แก้ไขไฟล์ .env ตามต้องการ
```

**หมายเหตุ**: โปรเจคนี้ใช้ remote MySQL database ที่ตั้งค่าไว้แล้ว จึงไม่จำเป็นต้องตั้งค่า database ใหม่

#### 3. รัน Docker Compose
```bash
# Build และรัน containers
docker-compose up --build

# หรือรันใน background
docker-compose up -d --build
```

#### 4. เข้าถึงแอปพลิเคชัน
- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:5000
- **Database**: localhost:3306 (ถ้าใช้ local MySQL)

### คำสั่งที่มีประโยชน์

#### ดูสถานะ containers
```bash
docker-compose ps
```

#### ดู logs
```bash
# ทั้งหมด
docker-compose logs

# เฉพาะ service
docker-compose logs backend
docker-compose logs frontend
```

#### หยุดการทำงาน
```bash
docker-compose down
```

#### ลบ containers และ volumes
```bash
docker-compose down -v
```

#### Rebuild containers
```bash
docker-compose up --build
```

### การแก้ไขปัญหา

#### 1. Port ถูกใช้งานอยู่
```bash
# ตรวจสอบ port ที่ใช้งาน
netstat -ano | findstr :5173
netstat -ano | findstr :5000

# หยุด process ที่ใช้ port
taskkill /PID <process_id> /F
```

#### 2. Build ล้มเหลว
```bash
# ลบ images เก่า
docker-compose down
docker system prune -a

# Build ใหม่
docker-compose up --build
```

#### 3. Database Connection Error
- ตรวจสอบว่า MySQL container รันอยู่
- ตรวจสอบ environment variables ใน docker-compose.yml

#### 4. Frontend ไม่สามารถเชื่อมต่อ Backend
- ตรวจสอบว่า Backend container รันอยู่
- ตรวจสอบ CORS settings ใน Backend
- ตรวจสอบ API URL ใน Frontend environment variables

### โครงสร้างไฟล์
```
E-borrow-system/
├── docker-compose.yml          # Docker Compose configuration
├── env.example                 # Environment variables example
├── E-borrow-System_Backend/
│   ├── Dockerfile              # Backend Docker configuration
│   └── ...
├── E-borrow-System_Frontend-/
│   ├── Dockerfile              # Frontend Docker configuration
│   └── ...
└── DOCKER_README.md            # ไฟล์นี้
```

### หมายเหตุ
- โปรเจคนี้ใช้ remote MySQL database (nozomi.proxy.rlwy.net)
- ถ้าต้องการใช้ local MySQL ให้ uncomment ส่วน MySQL ใน docker-compose.yml
- Frontend ใช้ Vite development server
- Backend ใช้ Node.js Express server

### การพัฒนา
สำหรับการพัฒนา ให้ใช้ volume mounts เพื่อให้การเปลี่ยนแปลงโค้ดมีผลทันที:
```yaml
volumes:
  - ./E-borrow-System_Backend:/app
  - /app/node_modules
```

### การ Deploy
สำหรับ production deployment:
1. เปลี่ยน NODE_ENV เป็น production
2. ใช้ production build สำหรับ Frontend
3. ตั้งค่า environment variables ที่เหมาะสม
4. ใช้ reverse proxy (nginx) สำหรับ production
