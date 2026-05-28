# 🛒 SmartPantry — Grocery & Inventory Manager

> A full-featured Smart Grocery List & Inventory Management web app — built as a proof-of-work student project for Full Stack Development portfolios.

![SmartPantry Screenshot](docs/screenshot-placeholder.png)

---

## 📌 Problem Statement

Households waste money and food because of:
- Forgotten items (no stock tracking)
- Expired products (no expiry alerts)
- Repeated over-purchasing or stockouts
- No shared family grocery planning

**SmartPantry** solves all of this in one app.

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔐 Auth | Login / Register with session persistence |
| 📦 Inventory Manager | Add items with qty, unit, category, expiry, price |
| ➕/➖ Quantity Control | Increment/decrement stock inline |
| ⚠️ Low Stock Alerts | Auto-detect items below minimum threshold |
| 📅 Expiry Alerts | Color-coded badges — expired / expiring soon |
| 🛒 Grocery List | Manual add, auto-generate from alerts |
| ⚡ Auto-Generate List | One click — adds all low/expired items |
| 📖 Recipe Planner | Add recipes, push ingredients to shopping list |
| 🔍 Search & Filter | Filter by category, search by name |
| 📊 Dashboard | Stats cards + category chart overview |
| 💾 Offline Storage | localStorage persistence — no server needed |
| 📱 Responsive | Works on mobile, tablet, desktop |

---

## 🏗️ Tech Stack

**This demo version (Frontend-only):**
- HTML5, CSS3 (custom design system)
- Vanilla JavaScript (ES6+)
- Google Fonts (Syne + DM Sans)
- localStorage for data persistence

**Full MERN Stack version (see `/docs/FULLSTACK.md`):**
- **Frontend:** React.js, Tailwind CSS, Axios, React Router
- **Backend:** Node.js, Express.js
- **Database:** MongoDB, Mongoose
- **Auth:** JWT (JSON Web Tokens), bcrypt
- **Charts:** Recharts / Chart.js
- **PWA:** Service Workers, Manifest

---

## 📁 Folder Structure

```
Smart-Grocery-Inventory-Manager/
│
├── index.html              ← Main app (standalone demo)
│
├── client/                 ← React frontend (full version)
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx
│   │   │   ├── ItemCard.jsx
│   │   │   ├── AlertBadge.jsx
│   │   │   └── StockBar.jsx
│   │   ├── pages/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Inventory.jsx
│   │   │   ├── GroceryList.jsx
│   │   │   ├── Alerts.jsx
│   │   │   ├── Recipes.jsx
│   │   │   ├── Login.jsx
│   │   │   └── Register.jsx
│   │   ├── services/
│   │   │   ├── api.js          ← Axios instance
│   │   │   ├── authService.js
│   │   │   └── itemService.js
│   │   ├── App.jsx
│   │   └── main.jsx
│   └── package.json
│
├── server/                 ← Express backend (full version)
│   ├── models/
│   │   ├── User.js
│   │   ├── GroceryItem.js
│   │   └── GroceryList.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── items.js
│   │   ├── grocery.js
│   │   └── dashboard.js
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── itemController.js
│   │   └── groceryController.js
│   ├── middleware/
│   │   ├── auth.js             ← JWT verification
│   │   └── validate.js
│   ├── config/
│   │   └── db.js               ← MongoDB connection
│   ├── utils/
│   │   └── alertHelper.js
│   └── package.json
│
├── docs/
│   ├── FULLSTACK.md
│   ├── API.md
│   ├── ARCHITECTURE.md
│   └── INTERVIEW_PREP.md
│
├── README.md
├── .gitignore
└── .env.example
```

---

## 🚀 How to Run (Demo Version)

1. **Download or clone this repo**
2. **Open `index.html` in any browser**
3. **Login with demo credentials:**
   - Email: `demo@smartpantry.app`
   - Password: `password123`
4. **Explore all features!**

No server, no database, no installation required.

---

## 🔧 Full Stack Setup (MERN)

### Prerequisites
- Node.js v18+
- MongoDB (local or Atlas)
- npm or yarn

### Backend
```bash
cd server
npm install
cp .env.example .env   # Edit with your values
npm run dev
```

### Frontend
```bash
cd client
npm install
npm run dev
```

### Environment Variables (`.env`)
```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/smartpantry
JWT_SECRET=your_super_secret_key_here
JWT_EXPIRES_IN=7d
```

---

## 📡 API Endpoints

### Auth
| Method | Route | Description |
|---|---|---|
| POST | `/api/auth/register` | Register user |
| POST | `/api/auth/login` | Login, get JWT |
| GET | `/api/auth/me` | Get current user |

### Inventory Items
| Method | Route | Description |
|---|---|---|
| GET | `/api/items` | Get all items |
| POST | `/api/items` | Add new item |
| PUT | `/api/items/:id` | Update item |
| DELETE | `/api/items/:id` | Delete item |
| PATCH | `/api/items/:id/qty` | Update quantity |

### Grocery List
| Method | Route | Description |
|---|---|---|
| GET | `/api/grocery` | Get grocery list |
| POST | `/api/grocery` | Add to list |
| PATCH | `/api/grocery/:id/check` | Toggle checked |
| DELETE | `/api/grocery/:id` | Remove entry |
| POST | `/api/grocery/generate` | Auto-generate |

### Dashboard
| Method | Route | Description |
|---|---|---|
| GET | `/api/dashboard/stats` | Summary stats |
| GET | `/api/dashboard/alerts` | All alerts |

---

## 📸 Screenshots to Capture for GitHub

1. ✅ Login / Register page
2. ✅ Dashboard with stats cards
3. ✅ Inventory table with stock bars
4. ✅ Low stock alert section
5. ✅ Expiry alert section
6. ✅ Grocery list with checkboxes
7. ✅ Add item modal
8. ✅ Recipe planner

---

## 🎓 Learning Outcomes

- Full-stack application architecture
- React component design and state management
- RESTful API design with Express.js
- MongoDB schema design with Mongoose
- JWT authentication flow
- UI/UX design for data-heavy apps
- CRUD operations end-to-end
- Alert/notification logic
- Responsive design

---

## 💼 Interview Prep

See [docs/INTERVIEW_PREP.md](docs/INTERVIEW_PREP.md) for 10 detailed Q&A pairs.

---

## 🤝 Contributing

Pull requests welcome! See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## 📄 License

MIT License — free to use for educational and portfolio purposes.

---

**Built with ❤️ as a Full Stack Development portfolio project.**

> ⭐ Star this repo if it helped you!
