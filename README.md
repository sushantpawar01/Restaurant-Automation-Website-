# 🍔 Food Delivery - Full-Stack Restaurant Automation Web Application

A full-stack, responsive food delivery and restaurant automation application built using **Node.js, Express, MongoDB, React, and Vite**, featuring **Stripe Payment Gateway** integration and an **Admin Control Panel**.

---

## 🚀 Features

### 🛒 Customer Storefront (Frontend)
- **Interactive Food Catalog**: Filter food items by categories (Salad, Rolls, Deserts, Sandwich, Cake, Pure Veg, Pasta, Noodles).
- **Cart Management**: Add/remove food items dynamically with realtime price updates.
- **User Authentication**: Secure user Signup & Login using JSON Web Tokens (JWT) and encrypted passwords (bcrypt).
- **Stripe Payment Integration**: Seamless online payment checkout session via Stripe.
- **My Orders Page**: Track placed order status and order history in real-time.

### ⚙️ Admin Control Panel (Admin Dashboard)
- **Add Food Items**: Upload new dishes with images, categories, and pricing.
- **Manage Menu**: View and remove existing items from the food database.
- **Order Management**: Monitor customer orders and update status (Food Processing -> Out for delivery -> Delivered).

### ⚡ Backend API (REST API)
- **Database Connection**: MongoDB object mapping using Mongoose.
- **File Uploads**: Image handling via `multer` serving static assets.
- **Secure Endpoints**: Cart & Order endpoints protected by JWT authentication middleware.

---

## 🛠️ Tech Stack

| Domain | Technology |
| :--- | :--- |
| **Frontend** | React 18, Vite, React Router DOM, React Toastify, Axios |
| **Admin** | React 18, Vite, React Router DOM, React Toastify |
| **Backend** | Node.js, Express.js |
| **Database** | MongoDB & Mongoose ORM |
| **Authentication** | JSON Web Tokens (JWT) & bcrypt |
| **Payment Gateway** | Stripe API (`stripe`, `@stripe/stripe-js`) |
| **File Storage** | Multer (Local static file hosting) |

---

## 📁 Project Architecture

```text
Restaurant-Automation-Website/
├── food-del/
│   ├── backend/               # Express REST API Server
│   │   ├── config/            # DB connection setup
│   │   ├── controllers/       # User, Food, Cart & Order controllers
│   │   ├── middleware/        # Auth middleware (JWT verification)
│   │   ├── models/            # Mongoose Schemas (User, Food, Order)
│   │   ├── routes/            # Express API Routes
│   │   ├── uploads/           # Static food item images
│   │   ├── server.js          # Express app entry point
│   │   └── seed.js            # Initial database seeder script
│   │
│   ├── frontend/              # Customer React App (Vite)
│   │   ├── src/
│   │   │   ├── assets/        # UI icons, images & sample food list
│   │   │   ├── components/    # Navbar, Header, FoodDisplay, Footer, LoginPopup
│   │   │   ├── Context/       # Global StoreContext for cart state & user token
│   │   │   └── pages/         # Home, Cart, PlaceOrder, Verify, MyOrders
│   │   └── index.html
│   │
│   └── admin/                 # Admin Dashboard React App (Vite)
│       ├── src/
│       │   ├── components/    # Sidebar & Navbar
│       │   └── pages/         # Add, List, Orders
│       └── index.html
└── README.md
```

---

## ⚙️ Environment Configuration

Create a `.env` file in the `food-del/backend` directory with the following variables:

```env
JWT_SECRET="your_jwt_secret_key"
STRIPE_SECRET_KEY="your_stripe_secret_key"
MONGODB_URI="mongodb://127.0.0.1:27017/food-del"
```

---

## 💻 Quick Start & Running Locally

### 1. Prerequisites
- **Node.js**: v18.x or higher
- **MongoDB**: Installed locally on port `27017` or a MongoDB Atlas URI.

---

### 2. Backend Setup & Data Seeding

```bash
cd food-del/backend

# Install dependencies
npm install

# Seed the database with 32 initial food items & images
node seed.js

# Start the Express backend server (Runs on http://localhost:4000)
npm run server
```

---

### 3. Frontend Customer App

```bash
cd food-del/frontend

# Install dependencies
npm install

# Start the Vite development server (Runs on http://localhost:5173)
npm run dev
```

---

### 4. Admin Dashboard

```bash
cd food-del/admin

# Install dependencies
npm install

# Start the Admin development server (Runs on http://localhost:5174)
npx vite --port 5174
```

---

## 🔌 API Endpoints Summary

### 👤 User Endpoints (`/api/user`)
- `POST /api/user/register` - Register a new user account
- `POST /api/user/login` - Authenticate user & receive JWT token

### 🥗 Food Endpoints (`/api/food`)
- `GET /api/food/list` - Fetch all food items
- `POST /api/food/add` - Add new food item (Multipart form data with image)
- `POST /api/food/remove` - Remove food item by ID

### 🛒 Cart Endpoints (`/api/cart`) - *Requires Auth Token*
- `POST /api/cart/get` - Get current user cart items
- `POST /api/cart/add` - Increment item quantity in cart
- `POST /api/cart/remove` - Decrement item quantity in cart

### 📦 Order Endpoints (`/api/order`)
- `POST /api/order/place` - Create order & Stripe checkout session
- `POST /api/order/verify` - Verify Stripe checkout payment status
- `POST /api/order/userorders` - Get user order history
- `GET /api/order/list` - Fetch all customer orders (Admin)
- `POST /api/order/status` - Update order delivery status (Admin)

---

## 📝 License

This project is open source under the [ISC License](LICENSE).
