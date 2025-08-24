# 🏭 Warehouse Management System with IoT Integration

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Node.js](https://img.shields.io/badge/Node.js-18.x-green.svg)](https://nodejs.org/)
[![Flutter](https://img.shields.io/badge/Flutter-3.x-blue.svg)](https://flutter.dev/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-14.x-blue.svg)](https://www.postgresql.org/)

## 📋 Mục lục
- [🎯 Tổng quan dự án](#-tổng-quan-dự-án)
- [🏗️ Kiến trúc hệ thống](#%EF%B8%8F-kiến-trúc-hệ-thống)
- [✨ Tính năng chính](#-tính-năng-chính)
- [💻 Công nghệ sử dụng](#-công-nghệ-sử-dụng)
- [🗄️ Cơ sở dữ liệu](#%EF%B8%8F-cơ-sở-dữ-liệu)
- [🤖 Tích hợp IoT](#-tích-hợp-iot)
- [📡 API Documentation](#-api-documentation)
- [🚀 Lộ trình phát triển](#-lộ-trình-phát-triển)
- [🛠️ Cài đặt và triển khai](#%EF%B8%8F-cài-đặt-và-triển-khai)

## 🎯 Tổng quan dự án

### Mục tiêu
Xây dựng hệ thống quản lý kho hàng thông minh tích hợp IoT, cung cấp giải pháp toàn diện cho việc quản lý sản phẩm, theo dõi tồn kho và tự động hóa quy trình nhập xuất hàng.

### Đặc điểm nổi bật
- 📱 **Giao diện di động**: Ứng dụng mobile thân thiện với người dùng
- 🔄 **Real-time monitoring**: Theo dõi tồn kho theo thời gian thực
- 🤖 **IoT Integration**: Tự động hóa với RFID, cảm biến siêu âm và cân điện tử
- 📊 **Analytics**: Báo cáo và thống kê chi tiết
- 🔐 **Security**: Xác thực và phân quyền người dùng
- ⚡ **Performance**: Tìm kiếm nâng cao và xử lý dữ liệu nhanh chóng

## 🏗️ Kiến trúc hệ thống

### Sơ đồ kiến trúc tổng quan

```mermaid
graph TB
    subgraph "Client Layer"
        A[Mobile App - Flutter]
        B[Web Dashboard]
    end
    
    subgraph "API Gateway"
        C[Load Balancer]
        D[Authentication Service]
    end
    
    subgraph "Application Layer"
        E[Product Service]
        F[Inventory Service]
        G[Analytics Service]
        H[IoT Service]
        I[Notification Service]
    end
    
    subgraph "Data Layer"
        J[(PostgreSQL Database)]
        K[Redis Cache]
        L[File Storage]
    end
    
    subgraph "IoT Layer"
        M[MQTT Broker]
        N[ESP32/Raspberry Pi]
        O[RFID Readers]
        P[Load Cells]
        Q[Ultrasonic Sensors]
    end
    
    subgraph "External Services"
        R[Push Notifications]
        S[Email Service]
        T[SMS Gateway]
    end
    
    A --> C
    B --> C
    C --> D
    D --> E
    D --> F
    D --> G
    D --> H
    D --> I
    
    E --> J
    F --> J
    G --> J
    H --> J
    I --> J
    
    E --> K
    F --> K
    G --> K
    
    H --> M
    M --> N
    N --> O
    N --> P
    N --> Q
    
    I --> R
    I --> S
    I --> T
    
    F --> L
```

### Luồng dữ liệu IoT

```mermaid
sequenceDiagram
    participant S as Sensors
    participant E as ESP32/RPi
    participant M as MQTT Broker
    participant B as Backend API
    participant D as Database
    participant A as Mobile App
    
    S->>E: Đọc dữ liệu cảm biến
    E->>M: Publish data via MQTT
    M->>B: Subscribe và nhận data
    B->>D: Lưu dữ liệu IoT
    B->>B: Xử lý logic nghiệp vụ
    B->>A: Push notification (WebSocket)
    B->>A: Cập nhật real-time data
```

## ✨ Tính năng chính

### 🔐 Authentication & Authorization
- Đăng nhập bảo mật với JWT
- Phân quyền người dùng (Admin, Manager, Staff)
- Session management

### 📦 Quản lý sản phẩm
- **CRUD Operations**: Thêm, sửa, xóa, xem sản phẩm
- **Categorization**: Phân loại sản phẩm theo danh mục
- **Product Tracking**: Mã vạch, QR code, RFID tags
- **Image Management**: Upload và quản lý hình ảnh sản phẩm

### 📊 Quản lý tồn kho
- **Real-time Inventory**: Cập nhật tồn kho theo thời gian thực
- **Stock Alerts**: Cảnh báo sắp hết hàng, tồn kho thấp
- **Batch Tracking**: Theo dõi lô hàng và hạn sử dụng
- **Location Management**: Quản lý vị trí lưu trữ

### 📈 Nhập xuất hàng
- **Import Management**: Quản lý phiếu nhập hàng
- **Export Management**: Quản lý phiếu xuất hàng
- **Automatic Updates**: Tự động cập nhật tồn kho
- **Document Generation**: Tạo phiếu nhập/xuất tự động

### 📊 Báo cáo & Thống kê
- **Dashboard Analytics**: Biểu đồ tổng quan
- **Inventory Reports**: Báo cáo tồn kho
- **Transaction History**: Lịch sử giao dịch
- **Export Options**: Xuất báo cáo PDF, Excel

### 🔍 Tìm kiếm nâng cao
- **Multi-field Search**: Tìm kiếm đa tiêu chí
- **Filter Options**: Bộ lọc nâng cao
- **Barcode Scanning**: Quét mã vạch để tìm kiếm
- **Voice Search**: Tìm kiếm bằng giọng nói

## 💻 Công nghệ sử dụng

### Frontend
```
📱 Mobile App
├── Flutter (Dart)
├── Provider/Bloc (State Management)
├── HTTP Client (API Integration)
└── SQLite (Local Storage)

🌐 Web Dashboard
├── React.js (TypeScript)
├── Redux Toolkit (State Management)
├── Material-UI (Component Library)
└── Chart.js (Data Visualization)
```

### Backend
```
🔧 API Server
├── Node.js + Express.js
├── TypeScript
├── JWT Authentication
├── Helmet (Security)
├── Rate Limiting
└── API Documentation (Swagger)

📡 Real-time Services
├── Socket.io (WebSocket)
├── MQTT.js (IoT Communication)
└── Redis (Pub/Sub)
```

### Database & Storage
```
🗄️ Primary Database
├── PostgreSQL 14+
├── Connection Pooling
└── Database Migrations

⚡ Caching & Session
├── Redis
└── Session Storage

📁 File Storage
├── Local Storage
└── AWS S3 (Production)
```

### IoT & Hardware
```
🔌 Microcontrollers
├── ESP32 (WiFi/Bluetooth)
└── Raspberry Pi 4

📡 Communication
├── MQTT Protocol
├── WiFi/Ethernet
└── Bluetooth LE

🔧 Sensors
├── RFID/NFC Readers
├── Load Cells (Weight)
├── Ultrasonic Sensors
└── Temperature/Humidity
```

## 🗄️ Cơ sở dữ liệu

### Entity Relationship Diagram

```mermaid
erDiagram
    USERS {
        uuid id PK
        string username UK
        string email UK
        string password_hash
        enum role
        timestamp created_at
        timestamp updated_at
        boolean is_active
    }
    
    CATEGORIES {
        uuid id PK
        string name UK
        string description
        string code UK
        timestamp created_at
        timestamp updated_at
    }
    
    PRODUCTS {
        uuid id PK
        string code UK
        string name
        string description
        uuid category_id FK
        decimal price
        integer quantity
        integer min_stock_level
        string unit
        string image_url
        json metadata
        timestamp created_at
        timestamp updated_at
        boolean is_active
    }
    
    LOCATIONS {
        uuid id PK
        string name UK
        string code UK
        string description
        string zone
        integer capacity
        timestamp created_at
        timestamp updated_at
    }
    
    PRODUCT_LOCATIONS {
        uuid id PK
        uuid product_id FK
        uuid location_id FK
        integer quantity
        timestamp updated_at
    }
    
    IMPORTS {
        uuid id PK
        string import_number UK
        uuid supplier_id FK
        decimal total_amount
        enum status
        text notes
        timestamp import_date
        timestamp created_at
        timestamp updated_at
        uuid created_by FK
    }
    
    IMPORT_DETAILS {
        uuid id PK
        uuid import_id FK
        uuid product_id FK
        integer quantity
        decimal unit_price
        decimal total_price
        date expiry_date
        string batch_number
        timestamp created_at
    }
    
    EXPORTS {
        uuid id PK
        string export_number UK
        uuid customer_id FK
        decimal total_amount
        enum status
        text reason
        text notes
        timestamp export_date
        timestamp created_at
        timestamp updated_at
        uuid created_by FK
    }
    
    EXPORT_DETAILS {
        uuid id PK
        uuid export_id FK
        uuid product_id FK
        integer quantity
        decimal unit_price
        decimal total_price
        timestamp created_at
    }
    
    SUPPLIERS {
        uuid id PK
        string name
        string code UK
        string contact_person
        string phone
        string email
        text address
        timestamp created_at
        timestamp updated_at
        boolean is_active
    }
    
    CUSTOMERS {
        uuid id PK
        string name
        string code UK
        string contact_person
        string phone
        string email
        text address
        timestamp created_at
        timestamp updated_at
        boolean is_active
    }
    
    IOT_DEVICES {
        uuid id PK
        string device_id UK
        string name
        enum device_type
        uuid location_id FK
        json configuration
        enum status
        timestamp last_seen
        timestamp created_at
        timestamp updated_at
    }
    
    IOT_LOGS {
        uuid id PK
        uuid device_id FK
        uuid product_id FK
        string sensor_type
        json sensor_data
        decimal value
        timestamp recorded_at
        timestamp created_at
    }
    
    STOCK_MOVEMENTS {
        uuid id PK
        uuid product_id FK
        enum movement_type
        integer quantity_change
        integer quantity_before
        integer quantity_after
        string reference_type
        uuid reference_id
        text notes
        timestamp created_at
        uuid created_by FK
    }
    
    NOTIFICATIONS {
        uuid id PK
        uuid user_id FK
        string title
        text message
        enum type
        json data
        boolean is_read
        timestamp created_at
        timestamp read_at
    }
    
    USERS ||--o{ IMPORTS : creates
    USERS ||--o{ EXPORTS : creates
    USERS ||--o{ STOCK_MOVEMENTS : creates
    USERS ||--o{ NOTIFICATIONS : receives
    
    CATEGORIES ||--o{ PRODUCTS : contains
    
    PRODUCTS ||--o{ PRODUCT_LOCATIONS : "stored at"
    PRODUCTS ||--o{ IMPORT_DETAILS : "imported in"
    PRODUCTS ||--o{ EXPORT_DETAILS : "exported in"
    PRODUCTS ||--o{ IOT_LOGS : "monitored by"
    PRODUCTS ||--o{ STOCK_MOVEMENTS : "has movements"
    
    LOCATIONS ||--o{ PRODUCT_LOCATIONS : stores
    LOCATIONS ||--o{ IOT_DEVICES : "has devices"
    
    SUPPLIERS ||--o{ IMPORTS : supplies
    CUSTOMERS ||--o{ EXPORTS : receives
    
    IMPORTS ||--o{ IMPORT_DETAILS : contains
    EXPORTS ||--o{ EXPORT_DETAILS : contains
    
    IOT_DEVICES ||--o{ IOT_LOGS : generates
```

### Chỉ mục và Tối ưu hóa
```sql
-- Indexes for performance optimization
CREATE INDEX idx_products_code ON products(code);
CREATE INDEX idx_products_category ON products(category_id);
CREATE INDEX idx_products_quantity ON products(quantity);
CREATE INDEX idx_stock_movements_product_date ON stock_movements(product_id, created_at);
CREATE INDEX idx_iot_logs_device_time ON iot_logs(device_id, recorded_at);
CREATE INDEX idx_notifications_user_unread ON notifications(user_id, is_read);
```

## 🤖 Tích hợp IoT

### Kiến trúc IoT

```mermaid
graph LR
    subgraph "Physical Layer"
        A[RFID Tags]
        B[Load Cells]
        C[Ultrasonic Sensors]
        D[Temperature Sensors]
    end
    
    subgraph "Edge Computing"
        E[ESP32 Controllers]
        F[Raspberry Pi Gateway]
    end
    
    subgraph "Communication"
        G[MQTT Broker]
        H[WebSocket Server]
    end
    
    subgraph "Processing"
        I[IoT Service]
        J[Rule Engine]
        K[Alert System]
    end
    
    subgraph "Storage"
        L[(Time Series DB)]
        M[(Main Database)]
    end
    
    A --> E
    B --> E
    C --> E
    D --> E
    
    E --> F
    F --> G
    G --> H
    H --> I
    
    I --> J
    J --> K
    I --> L
    I --> M
```

### Các loại cảm biến và ứng dụng

| Cảm biến | Ứng dụng | Dữ liệu thu thập |
|----------|----------|------------------|
| **RFID/NFC** | Định danh sản phẩm, tracking | Product ID, Location, Timestamp |
| **Load Cell** | Đo khối lượng tồn kho | Weight, Product quantity estimation |
| **Ultrasonic** | Đo mức độ đầy của kệ hàng | Distance, Stock level percentage |
| **Temperature** | Giám sát điều kiện bảo quản | Temperature, Humidity |
| **Motion** | Phát hiện hoạt động | Movement detection, Security |

### MQTT Topics Structure
```
warehouse/
├── devices/
│   ├── {device_id}/status
│   ├── {device_id}/data
│   └── {device_id}/config
├── alerts/
│   ├── low_stock
│   ├── temperature
│   └── security
└── commands/
    ├── calibrate
    └── reset
```

## 📡 API Documentation

### Authentication Endpoints
```
POST /api/auth/login
POST /api/auth/logout
POST /api/auth/refresh
GET  /api/auth/profile
PUT  /api/auth/profile
```

### Product Management
```
GET    /api/products              # Lấy danh sách sản phẩm
POST   /api/products              # Tạo sản phẩm mới
GET    /api/products/:id          # Lấy chi tiết sản phẩm
PUT    /api/products/:id          # Cập nhật sản phẩm
DELETE /api/products/:id          # Xóa sản phẩm
GET    /api/products/search       # Tìm kiếm sản phẩm
GET    /api/products/barcode/:code # Tìm theo mã vạch
```

### Inventory Management
```
GET  /api/inventory               # Tổng quan tồn kho
GET  /api/inventory/low-stock     # Sản phẩm sắp hết
GET  /api/inventory/movements     # Lịch sử biến động
POST /api/inventory/adjust        # Điều chỉnh tồn kho
```

### Import/Export Operations
```
GET  /api/imports                 # Danh sách phiếu nhập
POST /api/imports                 # Tạo phiếu nhập
GET  /api/imports/:id             # Chi tiết phiếu nhập
PUT  /api/imports/:id/status      # Cập nhật trạng thái

GET  /api/exports                 # Danh sách phiếu xuất
POST /api/exports                 # Tạo phiếu xuất
GET  /api/exports/:id             # Chi tiết phiếu xuất
PUT  /api/exports/:id/status      # Cập nhật trạng thái
```

### IoT & Analytics
```
GET  /api/iot/devices             # Danh sách thiết bị IoT
GET  /api/iot/devices/:id/data    # Dữ liệu cảm biến
POST /api/iot/data                # Nhận dữ liệu từ thiết bị

GET  /api/analytics/dashboard     # Dữ liệu dashboard
GET  /api/analytics/reports       # Báo cáo tùy chỉnh
GET  /api/analytics/alerts        # Cảnh báo hệ thống
```

### WebSocket Events
```javascript
// Client to Server
socket.emit('join_room', { userId, role });
socket.emit('get_realtime_data');

// Server to Client
socket.on('inventory_update', data);
socket.on('low_stock_alert', data);
socket.on('device_status_change', data);
socket.on('new_transaction', data);
```

## 🚀 Lộ trình phát triển

### Timeline Dự án

```mermaid
gantt
    title Warehouse Management System - Development Timeline
    dateFormat  YYYY-MM-DD
    section Phase 1 Foundation
    Database Design & Setup    :done, db, 2024-01-01, 2024-01-07
    Backend API Core          :done, api, 2024-01-08, 2024-01-15
    Authentication System     :done, auth, 2024-01-16, 2024-01-21
    
    section Phase 2 Core Features
    Product Management        :active, products, 2024-01-22, 2024-02-05
    Inventory System         :inventory, 2024-02-06, 2024-02-19
    Import Export Features   :import, 2024-02-20, 2024-03-05
    
    section Phase 3 Frontend
    Mobile App Development   :mobile, 2024-03-06, 2024-03-26
    Web Dashboard           :web, 2024-03-27, 2024-04-09
    UI UX Refinement        :ui, 2024-04-10, 2024-04-16
    
    section Phase 4 IoT Integration
    IoT Device Setup        :iot, 2024-04-17, 2024-04-30
    MQTT Integration        :mqtt, 2024-05-01, 2024-05-07
    Real-time Features      :realtime, 2024-05-08, 2024-05-14
    
    section Phase 5 Advanced Features
    Analytics Reporting   :analytics, 2024-05-15, 2024-05-28
    Advanced Search         :search, 2024-05-29, 2024-06-04
    Performance Optimization :perf, 2024-06-05, 2024-06-11
    
    section Phase 6 Deployment
    Testing QA           :testing, 2024-06-12, 2024-06-18
    Production Deployment  :deploy, 2024-06-19, 2024-06-25
    Documentation Training :docs, 2024-06-26, 2024-06-30
```

### Chi tiết từng giai đoạn

#### 🏗️ Phase 1: Foundation (3 tuần)
- **Week 1**: Thiết kế database, setup môi trường phát triển
- **Week 2**: Xây dựng API core, middleware, error handling
- **Week 3**: Implement authentication, authorization, JWT

#### 🔧 Phase 2: Core Features (6 tuần)
- **Week 4-5**: Product management CRUD, categories
- **Week 6-7**: Inventory tracking, stock movements
- **Week 8-9**: Import/Export functionality, document generation

#### 📱 Phase 3: Frontend Development (4 tuần)
- **Week 10-12**: Flutter mobile app development
- **Week 13**: Web dashboard với React
- **Week 14**: UI/UX improvements, responsive design

#### 🤖 Phase 4: IoT Integration (4 tuần)
- **Week 15-16**: Setup IoT devices, sensors
- **Week 17**: MQTT broker, communication protocols
- **Week 18**: Real-time data processing, WebSocket

#### 📊 Phase 5: Advanced Features (3 tuần)
- **Week 19-20**: Analytics, reporting, charts
- **Week 21**: Advanced search, filters
- **Week 22**: Performance optimization, caching

#### 🚀 Phase 6: Deployment (2 tuần)
- **Week 23**: Testing, bug fixes, QA
- **Week 24**: Production deployment, documentation

## 🛠️ Cài đặt và triển khai

### Yêu cầu hệ thống

#### Development Environment
```
Node.js: >= 18.0.0
PostgreSQL: >= 14.0
Redis: >= 6.0
Flutter: >= 3.0.0
Docker: >= 20.0.0
```

#### Hardware Requirements (IoT)
```
ESP32 Development Board
RFID/NFC Reader Module
Load Cell + HX711 Amplifier
Ultrasonic Sensor (HC-SR04)
Raspberry Pi 4 (Optional gateway)
```

### Quick Start

#### 1. Clone Repository
```bash
git clone https://github.com/your-username/warehouse-management-app.git
cd warehouse-management-app
```

#### 2. Backend Setup
```bash
cd warehouse-management-backend
npm install
cp .env.example .env
# Configure environment variables
npm run db:migrate
npm run db:seed
npm run dev
```

#### 3. Database Setup
```bash
# PostgreSQL
createdb warehouse_management
psql warehouse_management < database/schema.sql

# Redis
redis-server
```

#### 4. Frontend Setup
```bash
# Flutter Mobile App
cd warehouse-management-mobile
flutter pub get
flutter run

# React Web Dashboard
cd warehouse-management-web
npm install
npm start
```

#### 5. IoT Setup
```bash
# MQTT Broker
docker run -p 1883:1883 -p 9001:9001 eclipse-mosquitto

# Upload code to ESP32
cd iot-devices/esp32
# Configure WiFi and MQTT settings
# Upload using Arduino IDE or PlatformIO
```

### Docker Deployment

#### Development
```bash
docker-compose up -d
```

#### Production
```bash
docker-compose -f docker-compose.prod.yml up -d
```

### Environment Variables
```bash
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/warehouse_management
REDIS_URL=redis://localhost:6379

# Authentication
JWT_SECRET=your-super-secret-key
JWT_EXPIRES_IN=7d

# IoT
MQTT_BROKER_URL=mqtt://localhost:1883
MQTT_USERNAME=warehouse_user
MQTT_PASSWORD=secure_password

# Storage
UPLOAD_PATH=./uploads
AWS_S3_BUCKET=warehouse-files

# Notifications
SMTP_HOST=smtp.gmail.com
SMTP_USER=your-email@gmail.com
SMTP_PASS=your-app-password
```

## 📈 Performance & Scaling

### Database Optimization
- Connection pooling
- Query optimization với indexes
- Read replicas cho reporting
- Partitioning cho bảng lớn

### Caching Strategy
- Redis cho session storage
- API response caching
- Static file CDN

### Load Balancing
- Nginx reverse proxy
- Application server clustering
- Database load balancing

## 🔒 Security Measures

### Authentication & Authorization
- JWT với refresh tokens
- Role-based access control (RBAC)
- API rate limiting
- Password hashing với bcrypt

### Data Protection
- HTTPS/TLS encryption
- Database encryption at rest
- Input validation & sanitization
- SQL injection prevention

### IoT Security
- Device authentication
- Encrypted MQTT communication
- Secure device provisioning
- Regular security updates

## 🧪 Testing Strategy

### Unit Testing
```bash
# Backend
npm run test
npm run test:coverage

# Frontend
flutter test
npm run test # React
```

### Integration Testing
```bash
npm run test:integration
```

### Load Testing
```bash
# API load testing
npm run test:load

# Database performance testing
npm run test:db-performance
```

## 📚 Documentation

### API Documentation
- Swagger/OpenAPI specifications
- Postman collections
- Code examples

### User Manuals
- Admin user guide
- Staff user guide
- Mobile app tutorial
- IoT device setup guide

### Developer Documentation
- Architecture overview
- Database schema
- API reference
- Deployment guide

## 🤝 Contributing

### Development Workflow
1. Fork repository
2. Create feature branch
3. Make changes với proper testing
4. Submit pull request
5. Code review process

### Code Standards
- ESLint + Prettier for JavaScript/TypeScript
- Dart formatter for Flutter
- Conventional commits
- Code documentation

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Team & Contact

### Development Team
- **Project Manager**: [Tên]
- **Backend Developer**: [Tên]
- **Frontend Developer**: [Tên]
- **IoT Engineer**: [Tên]
- **UI/UX Designer**: [Tên]

### Contact Information
- Email: contact@warehouse-management.com
- GitHub: https://github.com/your-username/warehouse-management-app
- Documentation: https://docs.warehouse-management.com

---

> 🚀 **Ready to revolutionize warehouse management with IoT integration!**
