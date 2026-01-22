# Task Management System

A full-stack task management application built with Node.js, TypeScript, Next.js, and PostgreSQL.

---

## 🚀 Features

- User authentication (Register, Login, Logout)
- JWT-based authentication with access and refresh tokens
- Full CRUD operations for tasks
- Toggle task status (pending / completed)
- Task filtering by status
- Task searching by title
- Responsive UI
- Toast notifications

---

## 🛠️ Tech Stack

### Backend
- Node.js
- TypeScript
- Express.js
- Prisma ORM
- PostgreSQL
- JWT Authentication
- Bcrypt

### Frontend
- Next.js 14
- TypeScript
- Tailwind CSS
- Axios
- React Hot Toast

---

## 📦 Installation

### Prerequisites
- Node.js (v18+)
- PostgreSQL

### Backend Setup
```bash
cd backend
npm install
npx prisma generate
npx prisma migrate dev --name init
npm run dev


