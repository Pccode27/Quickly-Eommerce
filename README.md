# 🛒 Quickly Commerce

**Quickly Commerce** is a full-stack, multi-vendor e-commerce (grocery-focused) platform where **customers, sellers, and administrators** operate on a single unified system.  
The frontend is built as a **Vite + React Single Page Application**, while the backend is a **modular Express.js API** powered by **MongoDB**.

The platform supports **OTP-based authentication**, **Cloudinary-powered media uploads**, **Razorpay payments**, and **role-based dashboards** for sellers and admins.

🚀 **Live Demo**: https://quick-kart-lilac.vercel.app/

---

## ✨ Features

### 👤 Shoppers (Customers)
- OTP-based registration & login
- Profile photo upload
- Cart synchronization (server-side)
- Saved delivery addresses
- Cash on Delivery (COD) & Razorpay checkout
- Product reviews & ratings
- Complete order history

### 🛍️ Sellers
- Dedicated seller authentication
- Product submission with multiple images
- Admin approval workflow
- Inventory (stock) management
- Seller-specific order visibility

### 🛠️ Admins
- Secure admin authentication (JWT cookies)
- Product approval & rejection
- Order inspection & status updates
- Platform-wide catalog management

### ⚙️ Platform Services
- Cloudinary image uploads
- Razorpay payment gateway integration
- Email-based OTP verification (Nodemailer)
- Secure JWT authentication (HTTP-only cookies)
- Production-ready CORS, timeouts & DNS handling

---

## 🧰 Tech Stack

### Frontend
- React 19
- Vite
- React Router 7
- Tailwind CSS
- Axios
- React Hot Toast

### Backend
- Node.js 18+
- Express.js
- MongoDB & Mongoose
- JWT Authentication
- Multer (file handling)
- Cloudinary SDK
- Nodemailer
- Razorpay SDK

### Infrastructure
- MongoDB Atlas (or local)
- Cloudinary
- Razorpay
- SMTP provider
- Vercel (deployment)

---

## 📁 Project Structure

```

Quickly-Commerce/
├── backend/
│   ├── models/                # Mongoose schemas (User, Product, Order, Address, Review)
│   ├── routes/                # Express API routes
│   │   ├── address.routes.js
│   │   ├── admin.routes.js
│   │   ├── cart.routes.js
│   │   ├── order.routes.js
│   │   ├── product.routes.js
│   │   ├── review.routes.js
│   │   └── user.routes.js
│   ├── services/
│   │   └── emailService.js    # OTP & email handling
│   ├── uploads/               # Temporary local file storage
│   ├── utils/
│   │   ├── cloudinary.js
│   │   ├── db.js
│   │   └── multer.js
│   ├── index.js               # Express application entry point
│   ├── vercel.json
│   ├── DEPLOYMENT.md
│   └── package.json
│
├── frontend/
│   ├── public/
│   │   └── vite.svg
│   ├── src/
│   │   ├── assets/            # Images & static assets
│   │   ├── components/        # Reusable UI components
│   │   │   ├── Admin/
│   │   │   ├── BestSeller.jsx
│   │   │   ├── Categories.jsx
│   │   │   ├── Footer.jsx
│   │   │   ├── Login.jsx
│   │   │   ├── MainBanner.jsx
│   │   │   ├── Navbar.jsx
│   │   │   ├── SellerLogin.jsx
│   │   │   └── SellerSignup.jsx
│   │   ├── context/
│   │   │   └── AppContext.jsx # Global state management
│   │   ├── pages/             # Page-level components
│   │   ├── utils/             # Frontend helpers (Razorpay loader)
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── index.html
│   └── package.json
│
└── README.md

```

---

## 🖥️ Local Setup

### Prerequisites
- Node.js 18+
- MongoDB (local or Atlas)
- Cloudinary account
- Razorpay account *(optional for COD testing)*
- SMTP credentials for OTP emails

---

## 🔐 Environment Variables

### `backend/.env`
```

PORT=5000
MONGO_URI=your_mongodb_uri
SECRET_KEY=your_jwt_secret
FRONTEND_URL=[http://localhost:5173](http://localhost:5173)

ADMIN_EMAIL=[admin@example.com](mailto:admin@example.com)
ADMIN_PASSWORD=adminpassword

CLOUD_NAME=cloudinary_name
API_KEY=cloudinary_key
API_SECRET=cloudinary_secret

RAZORPAY_KEY=your_key
RAZORPAY_SECRET=your_secret

MAIL_HOST=smtp_host
MAIL_USER=your_email
MAIL_PASS=email_password

NODE_ENV=development

```

### `frontend/.env`
```

VITE_BACKEND_URL=[http://localhost:5000](http://localhost:5000)
VITE_RAZORPAY_KEY_ID=rzp_test_xxx
VITE_CURRENCY=₹

````

---

## ▶️ Install & Run

```bash
git clone https://github.com/Pccode27/Quickly-Eommerce.git
cd Quickly-Commerce

# Backend
cd backend
npm install
npm run dev

# Frontend
cd ../frontend
npm install
npm run dev
````

---

## 🔁 Core Application Flows

* **Authentication & Profiles**: OTP-based signup/login with HTTP-only JWT cookies and Cloudinary profile uploads
* **Product Catalog**: Seller uploads → Admin approval → Public storefront listing
* **Cart & Checkout**: Server-synced cart with COD or Razorpay payment
* **Orders**: User, seller, and admin order views with lifecycle management
* **Reviews**: One review per user per product with aggregated ratings

---

## 📡 API Highlights

| Module   | Endpoint                       | Description           |
| -------- | ------------------------------ | --------------------- |
| Auth     | `POST /api/v1/user/register`   | Register & send OTP   |
| Auth     | `POST /api/v1/user/verify-otp` | Verify OTP            |
| Auth     | `POST /api/v1/user/login`      | Login                 |
| Products | `POST /api/v1/product/add`     | Seller product upload |
| Products | `GET /api/v1/product/list`     | Public product list   |
| Orders   | `POST /api/v1/order/cod`       | COD order             |
| Orders   | `POST /api/v1/order/razor`     | Razorpay order        |
| Cart     | `POST /api/v1/cart/update`     | Sync cart             |
| Reviews  | `POST /api/v1/review`          | Add/update review     |

All endpoints are mounted under `/api/v1/*` in `backend/index.js`.

---

## 🚀 Deployment

### Backend (Vercel)

```bash
cd backend
vercel
```

Add all backend environment variables in the **Vercel Dashboard**.

### Frontend (Vercel)

* Set `VITE_BACKEND_URL` to backend Vercel URL
* Deploy using Vercel UI or CLI

⚠️ Ensure `FRONTEND_URL` matches the deployed frontend domain for cookies & CORS.

---

## 📌 Useful Commands

| Location | Command           | Purpose              |
| -------- | ----------------- | -------------------- |
| backend  | `npm run dev`     | Start backend (dev)  |
| backend  | `npm start`       | Start backend (prod) |
| frontend | `npm run dev`     | Start frontend       |
| frontend | `npm run build`   | Production build     |
| frontend | `npm run preview` | Preview build        |

---

## 📈 Future Enhancements

* Role-based middleware refactor
* Redis-based cart caching
* Advanced product search & filters
* Admin analytics dashboard

---

### ⭐ If you like this project, don’t forget to star the repository!

