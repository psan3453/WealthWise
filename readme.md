<div align="center">

# 💎 WealthWise

Understand your finances, plan for the future, and make informed financial decisions, all in one place.

![React](https://img.shields.io/badge/React-Vite-61DAFB?logo=react&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-CSS-38BDF8?logo=tailwindcss&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-Express-339933?logo=nodedotjs&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-Atlas-47A248?logo=mongodb&logoColor=white)
![JWT](https://img.shields.io/badge/Auth-JWT-000000?logo=jsonwebtokens&logoColor=white)
![Mistral AI](https://img.shields.io/badge/AI-Mistral-FF7000)

[Features](#-features) · [Tech Stack](#-technology-stack) · [Architecture](#-architecture) · [Getting Started](#-getting-started) · [Deployment](#-deployment) · [Security](#-security-practices)

</div>

---

WealthWise is a full-stack personal finance and wealth management application. It brings **financial tracking**, **wealth projections**, **goal planning**, and **AI-assisted insights** together in a single dashboard.

---

## ✨ Features

<table>
<tr>
<td width="50%" valign="top">

### 🏦 Financial Management
- Manage personal financial information and accounts
- Track savings, investments, and other assets
- Store data securely in MongoDB
- Organize financial data for analysis and planning

</td>
<td width="50%" valign="top">

### 📈 Projections & Planning
- Project future wealth using growth assumptions
- Explore different financial scenarios
- Estimate progress toward long-term goals
- Support FIRE (financial independence, retire early) planning

</td>
</tr>
<tr>
<td width="50%" valign="top">

### 🔍 Financial Analysis
- Scenario planning to see how decisions affect outcomes
- Monte Carlo simulation for outcomes under uncertainty
- Debt repayment strategy comparison

</td>
<td width="50%" valign="top">

### 🤖 AI-Assisted Insights
- AI assistant for financial questions and insights
- Helps explain scenarios and planning concepts
- Requires AI provider configuration

</td>
</tr>
</table>

### 📄 Reporting & External Data
- PDF report generation
- Exchange-rate data integration
- Cryptocurrency market data via CoinGecko

> [!NOTE]
> Features that depend on external APIs require valid configuration and may be unavailable when credentials or provider access are missing.

---

## 🧰 Technology Stack

| Layer | Technologies |
|---|---|
| 🖥 **Frontend** | React, Vite, JavaScript |
| 🎨 **Styling** | Tailwind CSS |
| ⚙️ **Backend** | Node.js, Express.js |
| 🗄 **Database** | MongoDB Atlas, MongoDB, Mongoose |
| 🔐 **Authentication** | JSON Web Tokens (JWT), bcryptjs |
| 🔌 **API communication** | Axios, REST APIs |
| 📊 **Data visualization** | Recharts |
| 🧮 **Financial calculations** | JavaScript, simple-statistics |
| 📑 **PDF reports** | jsPDF, html2canvas |
| 🛡 **Security** | Helmet, CORS, Express Rate Limit |
| 🛠 **Development** | Git, npm, Nodemon |

---

## 🏗 Architecture

The React frontend communicates with the Express backend over HTTP APIs. The backend uses Mongoose to store and retrieve financial records in MongoDB Atlas, and calls external services for exchange rates, crypto prices, and AI chat.

```text
┌─────────────────────┐         ┌─────────────────────┐
│                     │  HTTP   │                     │
│   React Frontend    │◄──────► │  Express Backend    │
│   (Vite + Tailwind) │  :5173  │  (REST API)  :5000  │
│                     │         │                     │
└─────────────────────┘         └────────┬────────────┘
                                         │
                                         ▼
                                ┌─────────────────────┐
                                │   MongoDB Database   │
                                │   (Atlas / :27017)   │
                                └─────────────────────┘
                                         │
                                         ▼
                                ┌─────────────────────┐
                                │  External APIs       │
                                │  • ExchangeRate-API  │
                                │  • CoinGecko         │
                                │  • Mistral AI        │
                                └─────────────────────┘
```

### 📁 Project Structure

```text
WealthWise/
│
├── BACKEND/                          # Express.js REST API
│   ├── server.js                     # Entry point, Express app setup
│   ├── .env                          # Environment variables (never commit)
│   ├── package.json                  # Backend dependencies
│   │
│   ├── controllers/
│   │   ├── authController.js         # Signup, login, JWT token generation
│   │   ├── financialsController.js   # CRUD for accounts & scenarios
│   │   └── aiController.js           # AI chat integration
│   │
│   ├── middleware/
│   │   └── auth.js                   # JWT authentication middleware
│   │
│   ├── models/
│   │   ├── User.js                   # Mongoose user schema
│   │   └── UserFinancials.js         # Mongoose schema for accounts & scenarios
│   │
│   └── routes/
│       ├── authRoutes.js             # /api/auth/*
│       ├── financialsRoutes.js       # /api/financials/*
│       └── aiRoutes.js               # /api/ai/*
│
├── FRONTEND/                         # React + Vite SPA
│   ├── index.html                    # HTML entry point
│   ├── package.json                  # Frontend dependencies
│   ├── vite.config.js                # Vite configuration
│   ├── tailwind.config.js            # Tailwind CSS configuration
│   ├── .env                          # If required (never commit)
│   │
│   └── src/
│       ├── main.jsx                  # App entry: routing & providers
│       ├── App.jsx                   # Main dashboard page
│       ├── App.css                   # Global styles
│       │
│       ├── components/
│       │   ├── AccountList.jsx       # Displays account cards
│       │   ├── AiChat.jsx            # Floating AI chat widget
│       │   ├── FireInsights.jsx      # FIRE number & freedom date
│       │   ├── ScenarioToggle.jsx    # Scenario on/off toggles
│       │   ├── StatCards.jsx         # Summary stat cards
│       │   └── WealthChart.jsx       # Net worth projection chart
│       │
│       ├── pages/
│       │   ├── LoginPage.jsx         # User login
│       │   ├── SignupPage.jsx        # User registration
│       │   ├── ManageAccountsPage.jsx    # Add/edit/delete accounts
│       │   ├── ManageScenariosPage.jsx   # Add/edit/delete scenarios
│       │   ├── AiChatPage.jsx        # Full-page AI chat
│       │   ├── TaxSimulatorPage.jsx  # State migration tax comparison
│       │   └── BlackSwanPage.jsx     # Crisis stress test
│       │
│       ├── context/
│       │   ├── AuthContext.jsx       # Authentication state provider
│       │   └── ThemeContext.jsx      # Dark/light mode provider
│       │
│       └── utils/
│           ├── financeHelpers.js     # Projection, Monte Carlo, debt math
│           ├── currencyHelper.js     # Exchange rates & currency formatting
│           └── exportHelper.js       # PDF export functionality
│
├── .gitignore
└── readme.md                         # ← You are here
```

> [!TIP]
> The directory listing is an overview; individual source files may vary.

---

## ✅ Prerequisites

- **Node.js** and **npm**
- **Git**
- A **MongoDB Atlas** account and database
- A modern web browser

---

## 🚀 Getting Started

### 1️⃣ Clone the repository

```bash
git clone https://github.com/psan3453/WealthWise.git
cd WealthWise
```

### 2️⃣ Set up the backend

```bash
cd BACKEND
npm install
```

Create `BACKEND/.env`:

```dotenv
PORT=5000
FRONTEND_URL=http://localhost:5173
MONGODB_URI=your_mongodb_atlas_connection_string
JWT_SECRET=your_long_random_secret
MISTRAL_API_KEY=
NODE_ENV=development
```

Replace the MongoDB URI and JWT secret with your own values, and configure the AI API key for the provider your AI implementation uses.

> [!WARNING]
> **Never publish real database credentials, JWT secrets, or API keys.** Do not commit your `.env` file.

### 3️⃣ Start the backend

```bash
npm run dev
```

The API runs at **http://localhost:5000**. Visit the root endpoint (`http://localhost:5000/`) to confirm it is up.

### 4️⃣ Set up the frontend

Open a **second terminal**:

```bash
cd FRONTEND
npm install
```

### 5️⃣ Start the frontend

```bash
npm run dev
```

Open the URL printed by Vite, normally **http://localhost:5173**.

> Keep both development servers running while you use the app.

---

## ⚙️ Environment Configuration

| Variable | Purpose |
|---|---|
| `PORT` | Port used by the backend |
| `FRONTEND_URL` | Allowed frontend origin for CORS |
| `MONGODB_URI` | MongoDB Atlas connection string |
| `JWT_SECRET` | Secret used for signing authentication tokens |
| `MISTRAL_API_KEY` | Intended AI provider configuration; verify compatibility with the implementation |
| `NODE_ENV` | Application environment |

The frontend may need extra environment variables depending on how API URLs and third-party integrations are configured in the source code.

---

## 🗄 Database

WealthWise uses **MongoDB Atlas**, a managed cloud database service.

MongoDB is a NoSQL document database. Records are stored as BSON documents, a binary representation of JSON-like data, and the application uses **Mongoose** to model and interact with them.

- Collections for users and financial information, depending on the implemented schemas
- Each user should only access **their own** financial information
- Authentication and authorization checks are enforced by the backend

---

## 🧑‍💻 Development Commands

<table>
<tr>
<td width="50%" valign="top">

**Backend** (`BACKEND/`)
```bash
npm install
npm run dev
```

</td>
<td width="50%" valign="top">

**Frontend** (`FRONTEND/`)
```bash
npm install
npm run dev
npm run build
npm run lint
```

</td>
</tr>
</table>

Available scripts depend on the corresponding `package.json`.

---

## ☁️ Deployment

| Part | Intended host |
|---|---|
| Frontend | Vercel |
| Backend | Render or another Node.js host |
| Database | MongoDB Atlas |

**Before deploying:**

1. Deploy the backend and set its environment variables on the hosting provider.
2. Confirm the production MongoDB URI and database access rules.
3. Deploy the frontend and set its production API base URL.
4. Set the backend's allowed CORS origin to the deployed frontend URL.
5. Configure all external API credentials in the host's environment-variable settings.
6. Test registration, login, financial data operations, and external integrations in production.

> [!IMPORTANT]
> Don't assume the app is production-ready just because it runs locally. Test authentication, ownership checks, error handling, external API integrations, and deployment configuration.

> [!NOTE]
> On Render's free tier the backend may take **30-50 seconds** to wake up on the first request after being idle.

---

## 🔒 Security Practices

- ✅ Keep `.env` files out of version control
- ✅ Never hardcode private API keys or database credentials
- ✅ Use a strong, randomly generated JWT secret
- ✅ Use HTTPS in production
- ✅ Restrict MongoDB network access and use a least-privilege database account
- ✅ Validate and sanitize user input
- ✅ Enforce user-specific access controls for financial records
- ✅ Avoid logging passwords, tokens, or sensitive financial information

---

## 🛣 Future Improvements

- [ ] Automated testing and CI/CD
- [ ] Improved financial dashboards and reporting
- [ ] More comprehensive validation of financial calculations
- [ ] Stronger access controls and security auditing
- [ ] Better performance for large datasets and complex charts
- [ ] Expanded goal tracking and scenario comparisons

---

## ⚖️ Disclaimer

WealthWise is a personal finance planning and analysis application. Its projections and simulations are estimates based on their assumptions and inputs. They are **not** guarantees of future returns or personalized professional financial advice.

---

<div align="center">

Made using React, Express, and MongoDB

</div>