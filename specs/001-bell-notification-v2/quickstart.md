# Quick Start Guide: Bell Notification App

**Project**: React Native + Rust Bell Notification App
**Branch**: 001-bell-notification-v2
**Updated**: 2025-01-24

## คำอธิบายโครงการ (Project Overview)

สร้างแอปพลิเคชันแจ้งเตือนเสียงระฆังบนมือถือ Android โดยใช้ React Native กับ Expo สำหรับฟรอนต์เอนด์ และ Rust สำหรับแบ็คเอนด์เพื่อประมวลผลเสียง มีเป้าหมายเพื่อประสิทธิภาพสูง ใช้ทรัพยากรน้อย พร้อมส่วนติดต่อผู้ใช้ที่สวยงามด้วย Tailwind CSS

### คุณสมบัติหลัก (Key Features)
- 🔔 **เล่นเสียงระฆังทันที** พร้อมเวลาหน่วง <100ms
- ⏰ **ตารางเวลาอัตโนมัติ** รองรับการตั้งเวลาหลายครั้ง
- 🌙 **โหมดการทำงานในพื้นหลัง** ประหยัดแบตเตอรี่ <1% ต่อวัน
- 📱 **รองรับทุกรุ่น Android** ตั้งแต่ Android 6.0+
- 🎨 **UI สวยงาม** ด้วย Tailwind CSS และ NativeWind
- 🛠️ **การพัฒนาง่าย** ผ่าน Expo QR Code

## การติดตั้ง (Installation)

### ข้อกำหนดเบื้องต้น (Prerequisites)

```bash
# Node.js 18+ และ npm
node --version  # ควรเป็น 18.x หรือใหม่กว่า
npm --version   # ควรเป็น 9.x หรือใหม่กว่า

# Rust 1.75+ สำหรับ backend
rustc --version  # ควรเป็น 1.75+ หรือใหม่กว่า
cargo --version

# Git
git --version

# Expo CLI
npm install -g @expo/cli
```

### 1. Clone Repository

```bash
git clone https://github.com/your-username/bell-notification-app.git
cd bell-notification-app
```

### 2. Setup Frontend (React Native + Expo)

```bash
# เข้าโฟลเดอร์ frontend
cd frontend

# ติดตั้ง dependencies
npm install

# สร้างไฟล์ .env จาก template
cp .env.example .env

# แก้ไข .env ตามความเหมาะสม
# API_BASE_URL=http://localhost:8080
# API_KEY=your-api-key-here
```

### 3. Setup Backend (Rust)

```bash
# กลับไปที่ root แล้วเข้าโฟลเดอร์ backend
cd ../backend

# ตรวจสอบ Rust toolchain
rustup update stable

# สร้างไฟล์ .env
echo "DATABASE_URL=sqlite:///./bell_app.db" > .env
echo "RUST_LOG=info" >> .env
echo "PORT=8080" >> .env
```

### 4. Setup Audio Files

```bash
# สร้างโฟลเดอร์สำหรับไฟล์เสียง
mkdir -p frontend/assets/audio
mkdir -p backend/assets/audio

# คัดลอกไฟล์เสียงตัวอย่าง (จาก assets หรือดาวน์โหลด)
# ควรมีไฟล์:
# - bell_default.wav (เสียงระฆังปกติ)
# - bell_gentle.wav (เสียงเบาๆ)
# - bell_loud.wav (เสียงดัง)
# - temple_bell.wav (เสียงระฆังวัด)
```

## การรันแอปพลิเคชัน (Running the Application)

### 1. Start Rust Backend

```bash
# ในโฟลเดอร์ backend
cargo run

# หรือสำหรับ development พร้อม auto-reload
cargo install cargo-watch
cargo watch -x run
```

Backend จะทำงานที่ `http://localhost:8080`

### 2. Start React Native Frontend

```bash
# ในโฟลเดอร์ frontend (terminal ใหม่)
npm start

# หรือ
expo start
```

Expo จะแสดง QR code สำหรับติดตั้งบนมือถือ

### 3. Test on Mobile Device

```bash
# ติดตั้ง Expo Go บนมือถือ Android
# แล้วแสกน QR code จาก terminal

# หรือสำหรับ emulator
npm run android
```

## โครงสร้างโปรเจค (Project Structure)

```
bell-notification-app/
├── frontend/                    # React Native Expo app
│   ├── src/
│   │   ├── components/         # UI components พร้อม Tailwind CSS
│   │   │   ├── BellButton/
│   │   │   ├── ScheduleCard/
│   │   │   └── SettingsScreen/
│   │   ├── screens/            # Main screens
│   │   │   ├── HomeScreen.tsx
│   │   │   └── SettingsScreen.tsx
│   │   ├── services/           # API services
│   │   │   ├── AudioService.ts
│   │   │   ├── ScheduleService.ts
│   │   │   └── StorageService.ts
│   │   ├── types/              # TypeScript definitions
│   │   ├── hooks/              # Custom React hooks
│   │   └── context/            # React Context providers
│   ├── assets/
│   │   ├── audio/              # Bell sound files
│   │   └── icons/              # App icons
│   ├── __tests__/              # Jest tests
│   ├── app.json               # Expo configuration
│   ├── package.json           # Dependencies
│   ├── tailwind.config.js     # Tailwind CSS config
│   └── metro.config.js        # Metro bundler config
│
├── backend/                     # Rust backend service
│   ├── src/
│   │   ├── main.rs             # Entry point
│   │   ├── audio/              # Audio processing modules
│   │   │   ├── player.rs       # เล่นเสียงระฆัง
│   │   │   └── scheduler.rs    # จัดการตารางเวลา
│   │   ├── api/                # HTTP API endpoints
│   │   │   └── handlers.rs     # API handlers
│   │   ├── database/           # Database operations
│   │   │   ├── models.rs       # Data models
│   │   │   └── repositories/   # Data access layer
│   │   └── utils/              # Utility modules
│   ├── assets/audio/           # Audio files for backend
│   ├── tests/                  # Rust tests
│   └── Cargo.toml              # Rust dependencies
│
└── specs/                       #  Documentation and contracts
    └── 001-bell-notification-v2/
        ├── spec.md              # Feature specification
        ├── plan.md              # Implementation plan
        ├── research.md          # Research findings
        ├── data-model.md        # Data model definitions
        ├── contracts/           # API contracts
        └── quickstart.md        # This file
```

## API Endpoints หลัก (Main API Endpoints)

### Audio Management
```bash
# เล่นเสียงระฆัง
POST /audio/play
{
  "bellTypeId": "default",
  "volume": 0.8,
  "loop": false
}

# หยุดการเล่นเสียง
POST /audio/stop

# ดึงประเภทเสียงระฆังทั้งหมด
GET /audio/bell-types
```

### Schedule Management
```bash
# สร้างตารางเวลาใหม่
POST /schedules
{
  "name": "Morning Bell",
  "triggerTime": "07:00",
  "daysOfWeek": [1,2,3,4,5],  # Monday-Friday
  "bellTypeId": "default"
}

# ดึงตารางเวลาทั้งหมด
GET /schedules?active_only=true

# อัพเดทตารางเวลา
PUT /schedules/{id}
{
  "name": "Updated Bell",
  "isActive": false
}

# ลบตารางเวลา
DELETE /schedules/{id}
```

### User Preferences
```bash
# ดึงการตั้งค่าผู้ใช้
GET /preferences

# อัพเดทการตั้งค่า
PUT /preferences
{
  "silentModeBehavior": "respect",
  "defaultVolume": 0.9,
  "themeMode": "dark"
}
```

## การตั้งค่า (Configuration)

### Frontend Configuration

```javascript
// frontend/app.json
{
  "expo": {
    "name": "Bell Notification",
    "slug": "bell-notification",
    "version": "1.0.0",
    "orientation": "portrait",
    "icon": "./assets/icon.png",
    "userInterfaceStyle": "automatic",
    "plugins": [
      "expo-font",
      "expo-splash-screen",
      "expo-status-bar",
      ["react-native-reanimated/plugin"]
    ],
    "android": {
      "package": "com.bellnotification.app",
      "adaptiveIcon": {
        "foregroundImage": "./assets/adaptive-icon.png",
        "backgroundColor": "#FFFFFF"
      }
    }
  }
}
```

```javascript
// frontend/tailwind.config.js
module.exports = {
  content: ["./App.tsx", "./src/**/*.{js,jsx,ts,tsx}"],
  presets: [require("nativewind/preset")],
  theme: {
    extend: {
      colors: {
        bell: {
          primary: '#2563eb',
          secondary: '#3b82f6',
          accent: '#60a5fa',
        }
      },
      animation: {
        'bell-ring': 'bellRing 0.6s ease-in-out',
      },
      keyframes: {
        bellRing: {
          '0%': { transform: 'rotate(0deg)' },
          '25%': { transform: 'rotate(15deg)' },
          '75%': { transform: 'rotate(-15deg)' },
          '100%': { transform: 'rotate(0deg)' },
        }
      }
    },
  },
}
```

### Backend Configuration

```toml
# backend/Cargo.toml
[package]
name = "bell-notification-backend"
version = "1.0.0"
edition = "2021"

[dependencies]
tokio = { version = "1.0", features = ["full"] }
axum = "0.7"
sqlx = { version = "0.7", features = ["runtime-tokio-rustls", "sqlite", "chrono"] }
serde = { version = "1.0", features = ["derive"] }
chrono = { version = "0.4", features = ["serde"] }
uuid = { version = "1.0", features = ["v4"] }
cpal = "0.15"
rodio = "0.17"
tracing = "0.1"
tracing-subscriber = { version = "0.3", features = ["env-filter"] }
dotenv = "0.15"
```

## การทดสอบ (Testing)

### Frontend Tests

```bash
# ในโฟลเดอร์ frontend
npm test

# ทดสอบพร้อม coverage
npm run test:coverage

# ทดสอบบน emulator
npm run test:e2e
```

### Backend Tests

```bash
# ในโฟลเดอร์ backend
cargo test

# ทดสอบพร้อม coverage
cargo install cargo-tarpaulin
cargo tarpaulin --out Html
```

### API Testing

```bash
# ติดตั้ง httpie หรือใช้ curl
pip install httpie

# ทดสอบ health check
http GET localhost:8080/health

# ทดสอบเล่นเสียงระฆัง
http POST localhost:8080/audio/play bellTypeId=default volume:=0.8

# ทดสอบสร้างตารางเวลา
http POST localhost:8080/schedules name="Test Bell" triggerTime="14:30" daysOfWeek:='[1,2,3,4,5]' bellTypeId=default
```

## การสร้าง Production Build

### Frontend (Expo)

```bash
# ในโฟลเดอร์ frontend
# สร้าง APK สำหรับ Android
npm run build:android

# หรือใช้ EAS (Expo Application Services)
npm install -g eas-cli
eas build --platform android

# สร้าง preview build
eas build --platform android --profile preview
```

### Backend (Rust)

```bash
# ในโฟลเดอร์ backend
# สร้าง optimized binary
cargo build --release

# Binary จะอยู่ที่ target/release/bell-notification-backend

# สร้าง Docker image (ถ้าต้องการ)
docker build -t bell-notification-backend .

# รัน container
docker run -p 8080:8080 bell-notification-backend
```

## การแก้ไขปัญหา (Troubleshooting)

### ปัญหาที่พบบ่อย

#### 1. เชื่อมต่อ Backend ไม่ได้
```bash
# ตรวจสอบว่า backend ทำงานอยู่
curl http://localhost:8080/health

# ตรวจสอบการตั้งค่าใน .env
cat frontend/.env

# ตรวจสอบ firewall หรือ antivirus
```

#### 2. เสียงไม่เล่นบนมือถือ
```bash
# ตรวจสอบ permission ใน Android
# Settings > Apps > Bell Notification > Permissions > Audio

# ตรวจสอบไฟล์เสียง
ls -la frontend/assets/audio/

# ตรวจสอบว่าระบบอยู่ในโหมดเงียบหรือไม่
```

#### 3. ปัญหา Memory หรือ Performance
```bash
# ตรวจสอบ memory usage บน backend
top | grep bell-notification

# ตรวจสอบ performance metrics
curl http://localhost:8080/metrics

# ลดจำนวน schedule หรือปรับปรุง algorithm
```

#### 4. ปัญหา Expo QR Code
```bash
# ตรวจสอบว่าอยู่ใน network เดียวกัน
ipconfig  # Windows
ifconfig  # macOS/Linux

# รีสตาร์ท Expo server
npm start -- --clear

# ลบ cache ของ Expo
expo r -c
```

### Log Files Location

```bash
# Frontend logs
# ใน Expo Go app: Menu > Device Logs
# หรือใน terminal ขณะรัน npm start

# Backend logs
# แสดงใน terminal ขณะรัน cargo run
# หรือตรวจสอบใน backend/logs/ (ถ้ามีการตั้งค่า)

# Android device logs
adb logcat | grep BellNotification
```

## Best Practices

### Performance Optimization
- ใช้ React.memo สำหรับ components ที่ไม่เปลี่ยนบ่อย
- ใช้ useCallback และ useMemo อย่างเหมาะสม
- จัดการ state ด้วย Context API และ useReducer
- Optimize audio buffer size สำหรับ latency <100ms

### Battery Optimization
- ใช้ background jobs อย่างมีประสิทธิภาพ
- จัดการ wake locks อย่างระมัดระวัง
- ตรวจสอบ Doze mode ของ Android
- ใช้ work constraints สำหรับ background tasks

### Code Quality
- เขียน comments เป็นภาษาไทยสำหรับฟังก์ชันที่ซับซ้อน
- ใช้ TypeScript สำหรับ type safety
- เขียน tests สำหรับ functions ที่สำคัญ
- ใช้ ESLint และ Prettier สำหรับ code formatting

### Security
- Validate input ทั้งฝั่ง frontend และ backend
- ใช้ HTTPS สำหรับ production
- จัดการ API keys อย่างปลอดภัย
- Sanitize user input ก่อนบันทึกลับฐานข้อมูล

## ข้อมูลติดต่อ (Contact)

- **Project Repository**: https://github.com/your-username/bell-notification-app
- **Documentation**: ดูในโฟลเดอร์ `specs/`
- **Issues**: https://github.com/your-username/bell-notification-app/issues
- **Email**: dev@uncle-codeing.com

## License

MIT License - ดูไฟล์ LICENSE สำหรับรายละเอียด

---

**Note**: คู่มือนี้เป็นเวอร์ชันเริ่มต้น สำหรับข้อมูลเพิ่มเติมและการอัพเดท กรุณาดูที่ `specs/001-bell-notification-v2/` ครับ 🚀