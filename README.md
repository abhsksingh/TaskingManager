# 🚀 Taskman — Team Task Manager

**Live Demo:** [https://taskingmanager-production.up.railway.app](https://taskingmanager-production.up.railway.app)

A full-stack team task management application with role-based access control, project tracking, Kanban board, and real-time dashboards.

## ✨ Features

- **Authentication** — JWT-based signup/login with secure bcrypt password hashing
- **Role-Based Access Control** — Admin and Member roles with enforced permissions
- **Project Management** — Create, edit, delete projects with color coding and priority levels
- **Task Tracking** — Full CRUD with status pipeline: To Do → In Progress → Review → Done
- **Kanban Board** — Visual drag-free kanban with quick status updates
- **Dashboard** — Real-time stats, overdue alerts, activity feed, team performance
- **Team Management** — Admin-only view with member performance metrics
- **Comments** — Per-task threaded comments
- **Activity Log** — Full audit trail of all actions

## 🛠 Tech Stack

| Layer | Technology | Details |
|-------|------------|---------|
| **Backend** | Node.js + Express.js | Core server framework |
| **Database** | SQLite | Persistent relational storage |
| **Authentication** | JWT + bcryptjs | Secure token-based auth & password hashing |
| **Security** | Express Rate Limit | Protection against brute-force attacks |
| **Validation** | Express Validator | Server-side input sanitization & validation |
| **Frontend** | Vanilla JS, HTML5, CSS3 | Modern, responsive, dependency-free UI |
| **Deployment** | Railway | Cloud hosting & continuous deployment |

## 🔐 API Endpoints

### Auth
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| POST | `/api/auth/signup` | Public | Register new user |
| POST | `/api/auth/login` | Public | Login |
| GET | `/api/auth/profile` | Auth | Get own profile |
| PUT | `/api/auth/profile` | Auth | Update profile |
| PUT | `/api/auth/change-password` | Auth | Change password |
| GET | `/api/auth/users` | Auth | List all users |

### Projects
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/api/projects` | Auth | List projects |
| POST | `/api/projects` | Auth | Create project |
| GET | `/api/projects/:id` | Member+ | Get project detail |
| PUT | `/api/projects/:id` | Project Admin | Update project |
| DELETE | `/api/projects/:id` | Admin | Delete project |
| POST | `/api/projects/:id/members` | Project Admin | Add member |
| DELETE | `/api/projects/:id/members/:userId` | Project Admin | Remove member |

### Tasks
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/api/tasks` | Auth | List tasks (filtered) |
| POST | `/api/tasks` | Auth | Create task |
| GET | `/api/tasks/:id` | Auth | Get task detail |
| PUT | `/api/tasks/:id` | Auth | Update task |
| PATCH | `/api/tasks/:id/status` | Auth | Quick status update |
| DELETE | `/api/tasks/:id` | Auth | Delete task |
| POST | `/api/tasks/:id/comments` | Auth | Add comment |
| DELETE | `/api/tasks/:id/comments/:commentId` | Auth | Delete comment |

### Dashboard
| Method | Endpoint | Access | Description |
|--------|----------|--------|-------------|
| GET | `/api/dashboard` | Auth | Dashboard stats & data |

## 🏃 Running Locally

```bash
# Clone the repo
git clone <your-repo-url>
cd team-task-manager

# Install dependencies
npm install

# Set up environment
cp .env.example .env
# Edit .env and set JWT_SECRET

# Start the server (auto-seeds demo data)
npm start

# Or for development with auto-reload
npm run dev
```

Open [http://localhost:3000](http://localhost:3000)

### Demo Accounts

| Role | Email | Password |
|------|-------|----------|
| **Admin** | dexter@taskmanager.io | Admin@123 |
| **Member** | bob@taskmanager.io | Member@123 |
| **Member** | carol@taskmanager.io | Member@123 |

## 🚂 Deploying to Railway

1. Push code to GitHub
2. Go to [railway.app](https://railway.app) → **New Project** → **Deploy from GitHub Repo**
3. Select your repository
4. Add environment variables in Railway dashboard:
   - `JWT_SECRET` — a long random string
   - `NODE_ENV` — `production`
5. Railway auto-detects Node.js and deploys!

> **Note:** The SQLite database persists on Railway's filesystem. For production scale, consider migrating to PostgreSQL using Railway's managed Postgres service.

## 📁 Project Structure

```
├── src/
│   ├── app.js                 # Express app entry point
│   ├── database/
│   │   ├── migrate.js         # Schema & DB init
│   │   └── seed.js            # Demo data
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── projectController.js
│   │   ├── taskController.js
│   │   └── dashboardController.js
│   ├── middleware/
│   │   └── auth.js            # JWT + RBAC middleware
│   └── routes/
│       ├── auth.js
│       ├── projects.js
│       ├── tasks.js
│       └── dashboard.js
├── public/                    # Frontend (served as static)
│   ├── index.html             # Auth page (Login/Signup)
│   ├── dashboard.html
│   ├── projects.html
│   ├── tasks.html
│   ├── team.html
│   ├── css/
│   │   ├── style.css          # Design system
│   │   ├── auth.css
│   │   └── app.css
│   └── js/
│       ├── app.js             # Shared utilities
│       ├── auth.js
│       ├── dashboard.js
│       ├── projects.js
│       ├── tasks.js
│       └── team.js
├── data/                      # SQLite database (auto-created)
├── .env                       # Environment variables
├── railway.toml               # Railway deployment config
└── package.json
```

## 🔒 Role-Based Access Control

| Feature | Admin | Member |
|---------|-------|--------|
| View all projects | ✅ | ❌ (own only) |
| Create projects | ✅ | ✅ |
| Delete any project | ✅ | ❌ |
| Add project members | ✅ | Project Admin only |
| View all tasks | ✅ | ❌ (own only) |
| Create/edit tasks | ✅ | ✅ |
| Delete tasks | ✅ | ✅ |
| View team page | ✅ | ❌ |
| View all activity | ✅ | ❌ |

## 📝 License

MIT
