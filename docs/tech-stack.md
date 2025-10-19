# Tech Stack - Sistem Kasir & Stok Multi-Toko

## 1. Frontend

- **Framework:** React.js
- **UI Library:** Material-UI (MUI)
- **State Management:** React Context / Redux (opsional)
- **Charting / Visualization:** MUI Charts, Recharts
- **Form & Validation:** React Hook Form, Yup
- **Routing:** React Router DOM
- **Build Tool:** Vite
- **PDF / Print:** jsPDF, print-js untuk cetak struk
- **PWA / Mobile Friendly:** optional, service worker untuk offline mode

## 2. Backend

- **Runtime Environment:** Node.js
- **Framework:** Express.js
- **Authentication:** JWT (Access Token + Refresh Token)
- **Database ORM:** Sequelize (untuk PostgreSQL)
- **Logging:** Winston / Morgan
- **File Upload / Excel Handling:** Multer, ExcelJS
- **Task Scheduling / Cron:** node-cron
- **API Documentation:** Swagger (opsional)

## 3. Database

- **Primary Database:** PostgreSQL
- **Design / Diagram:** DBML untuk desain, ERD konseptual untuk referensi
- **Backup & Restore:** Manual via DB tools / script, optional auto backup cron job

## 4. DevOps / Tools (untuk deployment di Render)

- **Version Control:** GitHub (Render langsung integrasi dengan repo GitHub)
- **Package Manager:** npm / yarn
- **Build & Deployment:**
  - Frontend: build React → deploy ke Static Site di Render
  - Backend: deploy Express server di Render Web Service
  - Gunakan environment variables di dashboard Render
- **Process Management:** Render menangani auto-restart & scaling, jadi PM2 opsional
- **Testing:** Jest / React Testing Library / Supertest untuk API sebelum deploy
- **Environment Variables:** diset di dashboard Render (`.env` tidak di-push ke repo)
- **Editor / IDE:** VS Code

## 5. Optional Integrations

- **Payment Gateway:** QRIS / Midtrans / Stripe (opsional)
- **Marketplace / API Integrations:** optional untuk fitur ekspansi
- **Notifications:** Email (Nodemailer) / WhatsApp API
