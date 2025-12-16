# 🧾 Payment Collection Backend API

A **production-ready backend service** built using **Node.js, Express, TypeScript, and PostgreSQL** for managing loan customers and EMI payments.

This backend supports:
- Customer creation & retrieval
- Secure EMI payment processing using database transactions
- Payment history tracking
- Input validation using Zod
- Automated testing
- CI/CD deployment to AWS EC2
- Public API access using **ngrok** for mobile & APK testing

This project is submitted as part of a **technical assessment**.

---

## 🚀 Features

- RESTful APIs for Customers & Payments
- PostgreSQL transactions (`BEGIN / COMMIT / ROLLBACK`)
- Row-level locking using `SELECT ... FOR UPDATE`
- Zod-based request validation
- Centralized error handling
- Database seeding support
- Jest + Supertest test cases
- CI/CD using GitHub Actions
- Deployment on AWS EC2 with PM2
- Ngrok for public HTTPS API access

---

## 🧱 Tech Stack

### Backend
- Node.js (v20)
- Express.js
- TypeScript
- PostgreSQL
- pg (node-postgres)

### Security & Middleware
- Helmet
- CORS
- Zod validation

### Testing
- Jest
- Supertest

### DevOps
- PM2
- GitHub Actions
- AWS EC2
- Ngrok (public API access)

---

## 📂 Project Structure

```

src/
├── app.ts                     # Express app configuration
├── server.ts                  # Server bootstrap
│
├── config/
│   └── db.ts                  # PostgreSQL connection pool
│
├── controllers/
│   ├── customerController.ts
│   └── paymentController.ts
│
├── routes/
│   ├── customerRoutes.ts
│   └── paymentRoutes.ts
│
├── schemas/
│   ├── customerSchema.ts
│   └── paymentSchema.ts
│
├── middleware/
│   └── validate.ts            # Zod validation middleware
│
├── types/
│   └── index.ts
│
├── tests/
│   └── api.test.ts            # Jest + Supertest tests
│
├── seed.ts                    # Database seed script
└── ...

````

---

## 🌐 API Endpoints

### Customers
```http
GET    /api/customers
POST   /api/customers
````

### Payments

```http
POST   /api/payments
GET    /api/payments/:account_number
```

---

## 🧪 Sample API Requests

### Create Customer

```json
{
  "customer_name": "John Doe",
  "issue_date": "12-01-2024",
  "interest_rate": 8.5,
  "tenure_months": 60,
  "emi_due_amount": 5000,
  "outstanding_balance": 250000
}
```

### Make Payment

```json
{
  "account_number": "ACC001",
  "amount": 2000
}
```

---

## 🔒 Transaction Safety (Important)

EMI payments are handled using **PostgreSQL transactions**:

* `BEGIN`
* `SELECT ... FOR UPDATE`
* Insert payment record
* Update customer balance
* `COMMIT`
* Automatic `ROLLBACK` on failure

This guarantees:

* Atomic operations
* No race conditions
* Consistent loan balances

---

## 🌍 Ngrok Usage (Public API Access)

Ngrok is used to expose the locally running backend to the internet for:

* Expo mobile app testing
* APK testing on real devices
* Assessment review without full deployment

---

### ▶️ How to Use Ngrok

1. Start the backend server:

```bash
npm run dev
```

2. Expose port `3000` using ngrok:

```bash
ngrok http 3000
```

3. Ngrok generates a public HTTPS URL:

```
https://uncerebric-karma-nonnitric.ngrok-free.dev/api'
```

4. Use this URL in the frontend / APK:

```env
EXPO_PUBLIC_API_BASE_URL=https://uncerebric-karma-nonnitric.ngrok-free.dev/api'
```

---

### 🔒 Why Ngrok is Required

* Mobile apps cannot access `localhost`
* Ngrok provides HTTPS by default
* Required for Expo Go & APK testing

---

### ⚠️ Notes on Ngrok

* Free ngrok URLs change on restart
* Suitable for development & assessment
* Production uses AWS EC2 deployment

---

## ⚙️ Environment Variables

Create a `.env` file in the root directory:

```env
PORT=3000

DB_HOST=your-db-host
DB_USER=your-db-user
DB_PASSWORD=your-db-password
DB_NAME=your-db-name
DB_PORT=5432
```

> SSL is enabled for cloud databases (Neon / managed Postgres)

---

## ▶️ Installation & Setup (For Interviewer)

### Prerequisites

* Node.js v16+
* PostgreSQL
* npm

---

### Step 1️⃣ Clone Repository

```bash
git clone <backend-repository-url>
cd backendPaymentApp
```

---

### Step 2️⃣ Install Dependencies

```bash
npm install
```

---

### Step 3️⃣ Seed Database (First Time Only)

```bash
npm run seed
```

This will:

* Create `customers` table
* Create `payments` table
* Insert sample data

---

### Step 4️⃣ Start Server

```bash
npm run dev
```

Server runs on:

```
http://localhost:3000
```

---

## 🧪 Testing

Run automated tests:

```bash
npm test
```

### Test Coverage Includes

* Fetch customers
* Payment validation
* Successful payment transaction
* Transaction rollback on failure

---

## 🔄 CI/CD Pipeline (GitHub Actions)

### Trigger

* Runs on every push to `main` branch

### Workflow Steps

1. Checkout repository
2. Setup Node.js
3. Install dependencies
4. Build application
5. SSH into EC2
6. Pull latest code
7. Install dependencies
8. Restart app using PM2

Workflow file:

```
.github/workflows/deploy.yml
```

---

## 🚀 Deployment (AWS EC2)

* Ubuntu EC2 instance
* PM2 for process management
* SSH-based deployment
* GitHub Secrets used:

  * `EC2_HOST`
  * `EC2_USERNAME`
  * `EC2_SSH_KEY`

---

## 🛡 Security Measures

* Helmet for HTTP headers
* CORS enabled
* Zod schema validation
* Parameterized SQL queries

---

## 📈 Future Improvements

* Authentication & authorization
* Rate limiting
* Pagination support
* Swagger / OpenAPI docs
* Payment modes (UPI / Card)

---

## 👨‍💻 Author

**Harsh Singh**
