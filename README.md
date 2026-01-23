# Task Management System

A full-stack task management application built with **Node.js, TypeScript, Next.js, and PostgreSQL** that allows users to securely manage their personal tasks.

---

## 📸 Screenshots

### Registration Page
![Registration Page](./screenshots/register.png)
*User registration with validation*

### Login Page
![Login Page](./screenshots/login.png)
*Secure user authentication*

### Dashboard
![Dashboard](./screenshots/dashboard.png)
*Main task dashboard with filter and search functionality*

---

## 🚀 Features

- ✅ User authentication (Register, Login, Logout)
- ✅ JWT-based authentication with access & refresh tokens
- ✅ Create, read, update, delete (CRUD) tasks
- ✅ Toggle task status (pending / in-progress / completed)
- ✅ Filter tasks by status
- ✅ Search tasks by title
- ✅ Pagination for large task lists
- ✅ Responsive UI (mobile & desktop)
- ✅ Toast notifications for user actions
- ✅ Automatic token refresh mechanism

---

## 🛠️ Tech Stack

### Backend
- **Node.js** - Runtime environment
- **TypeScript** - Type safety
- **Express.js** - Web framework
- **Prisma ORM** - Database toolkit
- **PostgreSQL** - Database
- **JWT** - Authentication
- **Bcrypt** - Password hashing

### Frontend
- **Next.js 14** - React framework (App Router)
- **TypeScript** - Type safety
- **Tailwind CSS** - Styling
- **Zustand** - State management
- **Axios** - HTTP client
- **React Hot Toast** - Notifications

---

## 📦 Installation

### Prerequisites
- Node.js (v18 or higher)
- PostgreSQL (v14 or higher)
- npm or yarn

### Backend Setup

```bash
# Navigate to backend directory
cd backend

# Install dependencies
npm install

# Set up environment variables
# Create .env file and add:
# DATABASE_URL="postgresql://postgres:yourpassword@localhost:5432/taskmanagement?schema=public"
# JWT_ACCESS_SECRET="your-access-secret"
# JWT_REFRESH_SECRET="your-refresh-secret"
# JWT_ACCESS_EXPIRY="15m"
# JWT_REFRESH_EXPIRY="7d"
# PORT=5000

# Generate Prisma client
npx prisma generate

# Run database migrations
npx prisma migrate dev --name init

# Start development server
npm run dev
```

### Frontend Setup

```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Set up environment variables
# Create .env.local file and add:
# NEXT_PUBLIC_API_URL=http://localhost:5000/api

# Start development server
npm run dev
```

---

## 🚀 Running the Application

### Development Mode

**Terminal 1 - Backend:**
```bash
cd backend
npm run dev
```
Server runs on `http://localhost:5000`

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```
Application runs on `http://localhost:3000`

### Production Build

**Backend:**
```bash
cd backend
npm run build
npm start
```

**Frontend:**
```bash
cd frontend
npm run build
npm start
```

---

## 📁 Project Structure

```
task-management-system/
├── backend/
│   ├── prisma/
│   │   ├── migrations/
│   │   └── schema.prisma
│   ├── src/
│   │   ├── controllers/
│   │   │   ├── auth.controller.ts
│   │   │   └── task.controller.ts
│   │   ├── middleware/
│   │   │   ├── auth.middleware.ts
│   │   │   └── errorHandler.ts
│   │   ├── routes/
│   │   │   ├── auth.routes.ts
│   │   │   └── task.routes.ts
│   │   └── index.ts
│   ├── .env
│   ├── package.json
│   └── tsconfig.json
│
└── frontend/
    ├── src/
    │   ├── app/
    │   │   ├── dashboard/
    │   │   ├── login/
    │   │   ├── register/
    │   │   └── layout.tsx
    │   ├── components/
    │   │   ├── Pagination.tsx
    │   │   ├── SearchAndFilter.tsx
    │   │   ├── TaskCard.tsx
    │   │   ├── TaskList.tsx
    │   │   └── TaskModal.tsx
    │   ├── lib/
    │   │   └── api.ts
    │   └── store/
    │       ├── authStore.ts
    │       └── taskStore.ts
    ├── .env.local
    ├── package.json
    └── tsconfig.json
```

---

## 🔌 API Endpoints

### Authentication

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| POST | `/api/auth/register` | Register new user | No |
| POST | `/api/auth/login` | Login user | No |
| POST | `/api/auth/refresh` | Refresh access token | No |
| POST | `/api/auth/logout` | Logout user | Yes |

### Tasks

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| GET | `/api/tasks` | Get all tasks (paginated) | Yes |
| POST | `/api/tasks` | Create new task | Yes |
| GET | `/api/tasks/:id` | Get single task | Yes |
| PATCH | `/api/tasks/:id` | Update task | Yes |
| DELETE | `/api/tasks/:id` | Delete task | Yes |
| PATCH | `/api/tasks/:id/toggle` | Toggle task status | Yes |

### Query Parameters for GET /api/tasks

- `page` - Page number (default: 1)
- `limit` - Items per page (default: 10)
- `status` - Filter by status: `all`, `pending`, `in-progress`, `completed`
- `search` - Search by title

**Example:**
```
GET /api/tasks?page=1&limit=10&status=pending&search=homework
```

---

## 🧪 Testing the API

### Using cURL

**Register User:**
```bash
curl -X POST http://localhost:5000/api/auth/register \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "password123",
    "name": "Test User"
  }'
```

**Login:**
```bash
curl -X POST http://localhost:5000/api/auth/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "test@example.com",
    "password": "password123"
  }'
```

**Create Task:**
```bash
curl -X POST http://localhost:5000/api/tasks \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -d '{
    "title": "Complete assignment",
    "description": "Finish the coding project",
    "status": "pending"
  }'
```

---

## 🔐 Environment Variables

### Backend (.env)

```env
DATABASE_URL="postgresql://postgres:yourpassword@localhost:5432/taskmanagement?schema=public"
JWT_ACCESS_SECRET="your-super-secret-access-key"
JWT_REFRESH_SECRET="your-super-secret-refresh-key"
JWT_ACCESS_EXPIRY="15m"
JWT_REFRESH_EXPIRY="7d"
PORT=5000
```

### Frontend (.env.local)

```env
NEXT_PUBLIC_API_URL=http://localhost:5000/api
```

---

## 🎯 Key Features Implementation

### Authentication Flow
1. User registers with email, password, and name
2. Password is hashed using bcrypt before storage
3. Upon login, user receives access token (15min) and refresh token (7 days)
4. Access token is used for API requests
5. When access token expires, refresh token is used to get a new one
6. Tokens are stored in localStorage on the client

### Task Management
1. Users can only view and manage their own tasks
2. Tasks have three statuses: pending, in-progress, completed
3. Tasks can be filtered by status and searched by title
4. Tasks are paginated (10 per page)
5. Toggle feature quickly marks tasks as completed/pending

---

## 🐛 Troubleshooting

### Common Issues

**Backend won't start:**
- Check if PostgreSQL is running
- Verify DATABASE_URL in .env is correct
- Run `npx prisma generate` and `npx prisma migrate dev`

**Frontend API calls failing:**
- Ensure backend is running on port 5000
- Check NEXT_PUBLIC_API_URL in .env.local
- Verify CORS is enabled in backend

**Database connection errors:**
- Confirm PostgreSQL credentials
- Check if database exists: `psql -U postgres -l`
- Verify port 5432 is not blocked

---

## 📝 License

This project is open source and available under the [MIT License]([LICENSE]).

---

## 👨‍💻 Author

Built as a demonstration of full-stack development skills using modern web technologies.

---

## 🙏 Acknowledgments

- Next.js team for the amazing framework
- Prisma team for the excellent ORM
- Tailwind CSS for the utility-first CSS framework
