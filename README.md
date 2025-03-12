# **Internal Time Tracking Application – System Design & Implementation**

## **Disclaimer**
This document serves as a reference draft for resume purposes, as the original repository remains proprietary to the previous employer, and the author's tenure concluded before full project execution.

---

## **Overview**
An internal time tracking application was proposed and designed using **Next.js, React, Node.js, and PostgreSQL**. The architecture was structured to define how the **frontend (React)** would interact with the **backend (Node.js with Next.js API routes)** and how data would be stored in a **PostgreSQL database using Prisma ORM**.

Key **API routes** were outlined for logging work hours, retrieving reports, and managing user roles. For **authentication**, **NextAuth.js** was considered with OAuth or JWT for secure access. The frontend design prioritized a **responsive UI with React components**, enabling employees to log hours efficiently while allowing managers to track productivity.

Additionally, the **data flow** was planned to ensure efficient **state management** through React hooks and caching strategies to minimize load times. The system was designed to be **scalable and maintainable**, integrating seamlessly with existing company workflows.

---

## **State Management**
- **React Hooks**: Utilized `useState` and `useEffect` for local state management.
- **Context API**: Employed for global state management, particularly for user authentication and role-based access.
- **NextAuth.js**: Implemented to store session details in secure JWT tokens for authentication.
- **React Query (TanStack Query)**: Integrated for data fetching, caching, and background synchronization.
- **Optimistic Updates**: Applied to enhance UI responsiveness, with rollback mechanisms in case of errors.

---

## **Data Flow & System Architecture**
### **1. Frontend (React + Next.js)**
- User authentication handled via **NextAuth.js**, with session state stored in **JWT tokens**.
- Upon submission of a **time log**, the UI updates **optimistically** before sending the request to the backend.
- **React Query** manages data fetching, caching, and synchronization to keep UI state updated.

### **2. Backend (Next.js API Routes + Node.js + PostgreSQL)**
- **Next.js API routes** handle RESTful API requests (e.g., `POST /api/log-time`, `GET /api/user-logs`).
- **Middleware** validates authentication, role-based access, and request payloads before processing.
- **PostgreSQL**, managed with **Prisma ORM**, is used for structured queries and efficient data handling.
- **Webhooks or CRON jobs** automate periodic reports and notifications.

### **3. Database Layer (PostgreSQL + Prisma)**
- Time logs are stored with **timestamps, user IDs, and project tags** for filtering and reporting.
- **Optimized queries** ensure fast retrieval for reports and dashboards.

### **4. Notifications & Reports**
- **Next.js API** generates **weekly reports (CSV/PDF exports)** and distributes them via **Nodemailer**.
- **Managers receive notifications** (via **WebSockets or polling**) upon employee log submissions.

---

## **Tech Stack**
- **Frontend**: React, Next.js
- **Backend**: Next.js API Routes, Node.js
- **Database**: PostgreSQL, Prisma ORM
- **State Management**: React Query, Context API
- **Authentication**: NextAuth.js (JWT, OAuth)
- **Deployment**: Docker, Vercel (Frontend), Railway/Heroku (Backend & DB)

---

## **Installation & Setup**
### **1. Clone the repository**
```sh
git clone https://github.com/company/time-tracking-app.git
cd time-tracking-app
```

### **2. Install dependencies**
```sh
npm install
```

### **3. Set up environment variables**
Create a `.env.local` file and add:
```
DATABASE_URL=postgresql://user:password@localhost:5432/timetracking
NEXTAUTH_SECRET=your_secret_key
NEXTAUTH_URL=http://localhost:3000
```

### **4. Run the development server**
```sh
npm run dev
```
Access the app at `http://localhost:3000`

---

## **API Endpoints**
| Method | Endpoint         | Description                     |
|--------|----------------|---------------------------------|
| POST   | `/api/log-time` | Log a new time entry           |
| GET    | `/api/time-logs` | Retrieve all time logs         |
| DELETE | `/api/time-logs/:id` | Delete a time entry          |
| GET    | `/api/reports` | Generate and download reports  |

---

## **Future Improvements**
- WebSocket support for real-time updates
- Mobile app integration
- AI-powered time suggestions

---

## **License**
This project is proprietary and managed by **[Company Name]**. Unauthorized distribution is prohibited.

---

**Author:** Timmy Ifidon

