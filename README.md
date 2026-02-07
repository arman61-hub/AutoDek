# 🚗 AutoDek – AI-Powered Car Marketplace 🚀

**AutoDek** is a modern, full-stack **AI-driven car marketplace** that enables users to intelligently explore, search, save, and book cars online. It combines **AI-based image search**, a robust backend, and a clean, responsive UI to deliver a production-ready automobile marketplace experience.

Built with **Next.js**, **Tailwind CSS**, **Prisma**, and **Gemini AI**, AutoDek showcases real-world full-stack engineering, including authentication, admin workflows, database modeling, and AI integrations.

---

## 🌐 Live Demo 
> 🔗 [AutoDek](https://autodek.vercel.app/)

---

## 📚 Table of Contents
- [✨ Features](#-features)
- [📦 Project Structure](#-project-structure)
- [🗄️ Database Schema](#️-database-schema-prisma)
- [🛠 Technologies Used](#-technologies-used)
- [🚀 Installation](#-installation)
- [🕹 Usage Guide](#-usage-guide)
- [📢 API Routes](#-api-routes)
- [🤝 Contributing](#-contributing)
- [⭐ Motivation](#-motivation)

---

## ✨ Features

### 🚘 Car Marketplace
- Browse curated car listings with rich specifications
- View pricing, availability, and detailed car information
- Save favorite cars and manage reservations
- Seamlessly book test drives

### 🧠 AI Image Search
- Upload a car image to discover visually similar cars
- Powered by **Gemini AI** for image understanding and matching

### 🛠 Admin Dashboard
- Add, update, and delete car listings
- Manage test-drive bookings and schedules
- Monitor users and overall platform activity

### 🔐 Authentication & Security
- Secure authentication using **Clerk**
- Role-based access control (**Admin / User**)
- Protected routes and server actions

### ⚡ Performance & UX
- Built with **Next.js App Router**
- **Shadcn UI** for accessible, modern components
- Fully responsive and mobile-friendly design

---

## 📦 Project Structure

```bash
📁 AutoDek/
├── 📁 actions/                       # Server Actions
│   ├── admin.js
│   ├── car-listing.js
│   ├── cars.js
│   ├── home.js
│   ├── settings.js
│   └── test-drive.js
│
├── 📁 app/                           # Next.js App Router
│   ├── 📁 (admin)/                   # Admin Dashboard
│   │   └── 📁 admin/
│   │       ├── 📁 cars/
│   │       ├── 📁 settings/
│   │       ├── 📁 test-drives/
│   │       ├── 📁 _components/
│   │       ├── layout.js
│   │       └── page.jsx
│   │
│   ├── 📁 (auth)/                    # Authentication (Clerk)
│   │   ├── 📁 sign-in/
│   │   ├── 📁 sign-up/
│   │   └── layout.jsx
│   │
│   ├── 📁 (main)/                    # User-facing Pages
│   │   ├── 📁 cars/
│   │   ├── 📁 reservations/
│   │   ├── 📁 saved-cars/
│   │   ├── 📁 test-drive/
│   │   └── layout.js
│   │
│   ├── layout.js
│   ├── not-found.jsx
│   └── page.js
│
├── 📁 components/                    # Reusable UI Components
│   ├── 📁 ui/                        # Shadcn UI components
│   ├── car-card.jsx
│   ├── header.jsx
│   ├── home-search.jsx
│   └── test-drive-card.jsx
│
├── 📁 hooks/
│   └── use-fetch.js
│
├── 📁 lib/                           # Utilities & Configs
│   ├── arcjet.js
│   ├── checkUser.js
│   ├── data.js
│   ├── helpers.js
│   ├── prisma.js
│   ├── supabase.js
│   └── utils.js
│
├── 📁 prisma/                        # Database Layer
│   ├── 📁 migrations/
│   └── schema.prisma
│
├── 📁 public/                        # Static Assets
│   ├── 📁 body/
│   ├── 📁 make/
│   └── logo.png
│
├── .env
├── prisma.config.ts
├── proxy.js
└── README.md
```

---

## 🗄️ Database Schema (Prisma)

AutoDek uses **Prisma ORM** with **PostgreSQL (Supabase)** for scalable and relational data management.

### 👤 User
| Field        | Type      | Description |
|-------------|-----------|-------------|
| `id`        | String (UUID) | Primary key |
| `clerkUserId` | String | Unique Clerk user ID |
| `email`     | String | User email (unique) |
| `name`      | String | User full name |
| `imageUrl`  | String | Profile image |
| `phone`     | String | Contact number |
| `role`      | Enum (`USER`, `ADMIN`) | User role |
| `createdAt` | DateTime | Account creation time |
| `updatedAt` | DateTime | Last update time |

### 🚘 Car
| Field        | Type | Description |
|-------------|------|-------------|
| `id`        | String (UUID) | Primary key |
| `make`      | String | Car manufacturer |
| `model`     | String | Car model |
| `year`      | Int | Manufacturing year |
| `price`     | Decimal | Car price |
| `mileage`   | Int | Mileage |
| `color`     | String | Car color |
| `fuelType`  | String | Petrol / Diesel / EV |
| `transmission` | String | Manual / Automatic |
| `bodyType`  | String | Sedan / SUV / Hatchback |
| `seats`     | Int | Number of seats |
| `description` | String | Car description |
| `status`    | Enum (`AVAILABLE`, `UNAVAILABLE`, `SOLD`) | Availability |
| `featured`  | Boolean | Highlighted car |
| `images`    | String[] | Supabase image URLs |
| `createdAt` | DateTime | Created time |
| `updatedAt` | DateTime | Updated time |

### ⭐ UserSavedCar
| Field | Type | Description |
|------|------|-------------|
| `id` | String (UUID) | Primary key |
| `userId` | String | User reference |
| `carId` | String | Car reference |
| `savedAt` | DateTime | Saved timestamp |
> Enforces **unique saved cars per user**

### 📅 TestDriveBooking
| Field | Type | Description |
|------|------|-------------|
| `id` | String (UUID) | Primary key |
| `userId` | String | User reference |
| `carId` | String | Car reference |
| `bookingDate` | Date | Test drive date |
| `startTime` | String | Start time |
| `endTime` | String | End time |
| `status` | Enum (`PENDING`, `CONFIRMED`, `COMPLETED`, `CANCELLED`, `NO_SHOW`) | Booking state |
| `notes` | String | Optional notes |
| `createdAt` | DateTime | Created time |
| `updatedAt` | DateTime | Updated time |

---

### 🏢 DealershipInfo Table

| Field | Type | Description |
|------|------|-------------|
| `id` | String (UUID) | Primary key |
| `name` | String | Dealership name |
| `address` | String | Dealership address |
| `phone` | String | Contact number |
| `email` | String | Contact email |
| `createdAt` | DateTime | Created time |
| `updatedAt` | DateTime | Updated time |

---

### 🕒 WorkingHour Table

| Field | Type | Description |
|------|------|-------------|
| `id` | String (UUID) | Primary key |
| `dealershipId` | String | Linked dealership |
| `dayOfWeek` | Enum (`MONDAY` → `SUNDAY`) | Day (Mon–Sun) |
| `openTime` | String | Opening time (HH:MM) |
| `closeTime` | String | Closing time (HH:MM) |
| `isOpen` | Boolean | Open/Closed |
| `createdAt` | DateTime | Created time |
| `updatedAt` | DateTime | Updated time |

---

## 🛠 Technologies Used

### 🔧 Backend
- Next.js (App Router)
- Prisma ORM
- Supabase (PostgreSQL)
- Gemini AI API
- Server Actions
- Arcjet (Rate Limiting)

### 🎨 Frontend
- React 19
- Next.js 15
- Tailwind CSS
- Shadcn UI
- Lucide Icons
- Clerk Authentication

---

## 🚀 Installation

### 1️⃣ Clone the Repository
```bash
git clone https://github.com/arman61-hub/AutoDek.git
cd AutoDek
```

### 2️⃣ Install Dependencies
```bash
npm install
```

### 3️⃣ Environment Variables
Create a `.env` file and configure the required keys:
```env
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=''
CLERK_SECRET_KEY=''
NEXT_PUBLIC_CLERK_SIGN_IN_URL=/sign-in
NEXT_PUBLIC_CLERK_SIGN_UP_URL=/sign-up
ARCJET_KEY=''
GEMINI_API_KEY=''
NEXT_PUBLIC_SUPABASE_URL=''
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_DEFAULT_KEY=''
# Connect to Supabase via connection pooling
DATABASE_URL=''
# Direct connection to the database. Used for migrations
DIRECT_URL=''
```

### 4️⃣ Prisma Setup
```bash
npx prisma generate
npx prisma db push
```

### 5️⃣ Run the App
```bash
npm run dev
```

➡️ App runs on **http://localhost:3000**

---

## 🕹 Usage Guide

### 👤 User
- Sign up / log in using Clerk
- Browse and save cars
- Upload images for AI-based search
- Book test drives

### 🛠 Admin
- Access admin dashboard
- Manage car listings
- Handle test drive bookings
- Monitor users and activity

---

## 📢 API Routes

### 🚗 Cars
- `GET /api/cars`  
  Fetch all available cars

- `POST /api/cars`  
  Add a new car listing (**Admin only**)

- `DELETE /api/cars/:id`  
  Remove a car listing (**Admin only**)

### 🧠 AI
- `POST /api/ai/image-search`  
  Upload a car image and receive similar car listings powered by **Gemini AI**

### 📅 Bookings
- `POST /api/book-test-drive`  
  Book a test drive for a selected car

- `GET /api/bookings`  
  Fetch all test drive bookings (**Admin only**)

---

## 🤝 Contributing

Contributions are always welcome 🚀  
Whether it’s a bug fix, feature enhancement, or UI improvement — feel free to contribute!

### 🧩 How to Contribute

#### 1. Fork the Repository  
   Click the **Fork** button on the top right of this page.

#### 2. Clone Your Fork 
   Open terminal and run:
   ```bash
   git clone  https://github.com/arman61-hub/AutoDek.git
   cd AutoDek
   ```

#### 3. Create a feature branch:
   Use a clear naming convention:
   ```bash
   git checkout -b feature/new-feature
   ```
   
#### 4. Make & Commit Your Changes
   Write clean, documented code and commit:
   ```bash
   git add .
   git commit -m "✨ Added: your change description"
   ```
   
#### 5. Push to GitHub & Submit PR
   ```bash
   git push origin feature/your-feature-name
   ```
#### 6. Then go to your forked repo on GitHub and open a Pull Request.

---

## ⭐ Motivation

> 💡**PS:** If you found this project helpful or inspiring, please **[⭐ star the repository](https://github.com/arman61-hub/AutoDek)** — it keeps me motivated to build and share more awesome projects like this one!