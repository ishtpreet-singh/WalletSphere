# 🌐 WalletSphere

> **Smart Personal Finance Management & AI-Powered Financial Analytics**

WalletSphere is a full-stack personal finance platform designed to give you complete visibility and control over your financial health. Built with **React**, **Node.js/Express**, and **MongoDB**, WalletSphere combines automated bank transaction parsing, budget tracking, real-time analytics, and an integrated AI financial copilot.

---

## 🚀 Key Features

### 📊 Financial Dashboard & Analytics
- **Live Summary Cards**: Real-time Net Balance, Total Monthly Income, and Total Monthly Expenses.
- **Interactive Visualizations**: Expense category breakdowns and monthly income vs. expense trends powered by Recharts.
- **Multi-Currency Support**: Native support for ₹ (INR), $ (USD), € (EUR), and £ (GBP).

### 💳 Transaction Management & Bank Sync
- **Workspace Filtering**: Instant search, category filters, type filters (Income / Expense), and pagination.
- **Statement Import Engine**: Bulk import bank transactions directly from **CSV**, **Excel (.xlsx)**, and **PDF** bank statements.
- **Gmail Bank Alert Sync**: Automated integration using Google Identity Services to sync real-time debit/credit transaction alerts from bank notification emails.
- **Custom Categorization**: Automatic rule-based and manual expense tagging.

### 🎯 Budgets & Bills Tracking
- **Category Budgets**: Set spending limits per category with visual progress tracking and threshold warnings.
- **Upcoming Bills**: Recurring bill reminders and due-date trackers to avoid late fees.

### 🤖 AI Financial Copilot
- **AI Chat Workspace**: Conversational financial intelligence built into your dashboard.
- **Affordability Engine**: Ask before you buy — the AI evaluates your budget, savings rate, and upcoming bills to provide actionable purchase advice.
- **Scenario Planning**: Test what-if financial scenarios (e.g., career moves, big-ticket investments, expense cuts).

### 🔐 Secure Authentication & Data Privacy
- **Google OAuth 2.0**: One-click Sign-in with Google via Google Identity Services (`@react-oauth/google`).
- **Email & Password**: Secure salted password hashing with bcrypt, JWT session management, and email verification.
- **Self-Service Recovery**: Password reset flows via email tokens.
- **Data Export & Backup**: One-click complete JSON backup export of all personal transactions, budgets, and bills.

---

## 🛠️ Tech Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 18, Vite 5, Tailwind CSS, Lucide React, Framer Motion, Recharts, Axios |
| **Backend** | Node.js, Express 4, MongoDB, Mongoose 8, JWT, bcryptjs |
| **Authentication** | Google OAuth 2.0 (`@react-oauth/google` / `google-auth-library`), JWT |
| **Parsing & Media** | `pdf-parse`, `xlsx`, `csv-parser`, `multer`, `nodemailer` |
| **AI Integration** | OpenAI / NVIDIA AI API Engine |

---

## 📁 Project Architecture

```text
WalletSphere/
├── client/                     # Vite + React Frontend
│   ├── src/
│   │   ├── components/         # Modular UI & Feature Components
│   │   │   ├── ai/             # AI Copilot Workspace
│   │   │   ├── auth/           # OAuth & Route Guards
│   │   │   ├── budgets/        # Budget modals and widgets
│   │   │   ├── dashboard/      # Overview cards & bank sync
│   │   │   ├── reports/        # Analytics & charts
│   │   │   ├── settings/       # Profile & backup modals
│   │   │   └── transactions/   # Transaction list & importers
│   │   ├── context/            # Global Auth & State Context
│   │   ├── pages/              # Landing, Login, Register, Dashboard
│   │   ├── services/           # Axios API configuration & interceptors
│   │   └── utils/              # Client helpers & AI generators
│   ├── package.json
│   └── vite.config.js
│
├── server/                     # Node.js + Express Backend API
│   ├── src/
│   │   ├── config/             # MongoDB database connection
│   │   ├── controllers/        # Auth, Transaction, Budget, BankSync, AI
│   │   ├── middleware/         # JWT auth middleware
│   │   ├── models/             # Mongoose schemas (User, Transaction, Budget, etc.)
│   │   ├── routes/             # RESTful API Route definitions
│   │   ├── utils/              # Parsers (PDF, XLSX, CSV), AI tools, Emailer
│   │   ├── app.js              # Express app setup & CORS configuration
│   │   └── server.js           # Server entry point
│   └── package.json
│
├── .gitignore
├── package.json                # Monorepo root scripts
└── README.md
```

---

## ⚙️ Getting Started

### 1. Prerequisites
- [Node.js](https://nodejs.org/) (v18.x or later)
- [MongoDB](https://www.mongodb.com/) (Local instance or MongoDB Atlas cluster)
- [Google Cloud Console](https://console.cloud.google.com/) Project (for Google OAuth)

### 2. Clone the Repository
```bash
git clone https://github.com/ishtpreet-singh/WalletSphere.git
cd WalletSphere
```

### 3. Install Dependencies
Install dependencies for both frontend and backend using the root helper:
```bash
npm run install:all
```
*Or install manually:*
```bash
npm install
cd server && npm install
cd ../client && npm install
cd ..
```

---

## 🔐 Environment Configuration

Create `.env` files in both `server/` and `client/` directories:

### Backend (`server/.env`)
```env
PORT=5001
NODE_ENV=development
MONGODB_URI=your_mongodb_connection_string
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRE=30d
CLIENT_URL=http://localhost:5175

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id.apps.googleusercontent.com

# AI Engine (Optional / If using AI Copilot)
NVIDIA_API_KEY=your_nvidia_api_key
# or
OPENAI_API_KEY=your_openai_api_key

# Email Service (Optional / For verification & password resets)
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email@gmail.com
SMTP_PASS=your_email_app_password
```

### Frontend (`client/.env`)
```env
# Must start with VITE_
VITE_GOOGLE_CLIENT_ID=your_google_client_id.apps.googleusercontent.com
```

> **Note on Google Cloud Console Configuration:**
> In your Google Cloud OAuth Client settings, ensure:
> - **Authorized JavaScript origins**: `http://localhost:5175` (or your client port)
> - **Authorized redirect URIs**: `http://localhost:5175/login`

---

## 🏃 Running the Application

### Development Mode (Both Frontend & Backend)
From the root directory, run:
```bash
npm run dev
```
*(This starts both the backend API server and the Vite dev server concurrently.)*

### Running Individually:
- **Backend API**:
  ```bash
  cd server
  npm run dev
  # Server runs on http://localhost:5001
  ```
- **Frontend App**:
  ```bash
  cd client
  npm run dev
  # Client runs on http://localhost:5174 or http://localhost:5175
  ```

---

## 📡 API Reference Overview

| Endpoint | Method | Description | Access |
|---|---|---|---|
| `/api/auth/register` | `POST` | Register a new user | Public |
| `/api/auth/login` | `POST` | Authenticate user & return JWT | Public |
| `/api/auth/google` | `POST` | Google OAuth token verification & login | Public |
| `/api/auth/profile` | `GET` / `PUT` | Fetch or update user profile & persona | Private |
| `/api/auth/export-backup` | `GET` | Export all user data as JSON | Private |
| `/api/transactions` | `GET` / `POST` | List (with pagination/filters) or create transaction | Private |
| `/api/transactions/:id` | `PUT` / `DELETE` | Edit or delete a transaction | Private |
| `/api/budgets` | `GET` / `POST` | Manage spending budgets | Private |
| `/api/bills` | `GET` / `POST` | Manage recurring bills & subscriptions | Private |
| `/api/ai/chat` | `POST` | AI assistant insights & recommendations | Private |
| `/api/bank-sync/upload` | `POST` | Upload and parse bank statement (CSV/XLSX/PDF) | Private |

---

## 🛡️ License

This project is licensed under the [ISC License](LICENSE).
