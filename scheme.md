
---

## 🏗️ System Overview

### 🖥️ Frontend — React + Vite

| Component | Description | Tag |
|-----------|-------------|-----|
| **🔐 Auth Layer** | AuthContext, ProtectedRoute, firebase.js · JWT token handling | `auth/` |
| **🌍 Context Providers** | DataContext (dataset state) · ThemeContext (dark/light) | `context/` |
| **📡 API Client** | Axios instance · api.js, contact.js, gemini.js | `api/` |
| **🪝 Custom Hooks** | useAIAnalysis · useSmartCleaning | `hooks/` |
| **⚙️ Client Services** | aiAdvisorService · ruleEngine (data-cleaning rules) | `services/` |

### 🐍 Backend — FastAPI v3.0

| Component | Description | Tag |
|-----------|-------------|-----|
| **🗄️ App Core** | models, database, user_store, data_context, dataset_manager, cache | `app/` |
| **🔀 Routers** | auth · admin · stats · analyze · charts · ai_advisor · firebase_auth · gemini · profiling · contact | `routers/` |
| **🧩 Services** | engine · anomaly · quality_score · stats_service · chart_service · analyzer_service · main | `services/` |
| **🛡️ Utils** | security (bcrypt, JWT) · file_utils | `utils/` |
| **🔧 Core Config** | config · firebase_config · supabase_client | `core/` |

### ☁️ External Services

| Service | Description |
|---------|-------------|
| **🔥 Firebase Auth** | Google OAuth · email/password · firebase-admin SDK |
| **🤖 Google Gemini AI** | AI chat assistant · AI advisor · data insights generation |
| **📦 Supabase** | Remote PostgreSQL backend · file storage (optional) |
| **⚡ Redis Cache** | In-memory dataset cache · session TTL |

---

## 📄 Frontend Pages & Routes

| Route | Type | Description |
|-------|------|-------------|
| `/` | Public | Home Page |
| `/about` | Public | About |
| `/login` | Public | Auth (Login / Register) |
| `/forgot-password` | Public | Password Recovery |
| `/features` | Public | Features |
| `/pricing` | Public | Pricing |
| `/faq`, `/contact` | Public | FAQ & Contact |
| `/privacy`, `/terms`, `/cookies` | Public | Legal Pages |
| `/upload` | Auth | File Upload |
| `/dashboard` | Auth | Main Dashboard |
| `/analytics` | Auth | Analytics |
| `/stats` | Auth | CSV Stats |
| `/data-quality` | Auth | Data Quality |
| `/3d-visualizations` | Auth | 3D Charts |
| `/model` | Auth | ML Model Builder |
| `/user` | Auth | Profile |
| `/admin` | Admin | Admin Panel |
| `*` | Public | 404 Not Found |

---

## 🧱 Key Frontend Components

### 🤖 AIAdvisor
- AIChatAssistant
- AIAdvisorPanel
- IssueCard
- MLReadinessScore
- SmartFixButton

### 📊 DataQuality
- ColumnProfiler
- QualityMetrics
- RecommendationEngine

### 📉 Charts & Viz
- ChartBuilder
- ChartContainer
- MatplotlibChart
- HeatmapDisplay

### 🧹 Data Tools
- CleaningToolbar
- AutoCleanAgent
- ExcelGrid
- FileUploader

### 🧮 Stats & Models
- StatsPanel
- CsvStatsTable
- DescriptiveStatsTable
- ModelBuilderSection
- PredictionSection

---

## 🔌 Backend API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/auth/login` | User login |
| `POST` | `/api/auth/register` | User registration |
| `POST` | `/api/auth/refresh` | Token refresh |
| `POST` | `/api/auth/firebase` | Firebase authentication |
| `POST` | `/api/analyze/upload` | File upload |
| `GET` | `/api/analyze/info` | Analysis info |
| `GET` | `/api/analyze/preview` | Data preview |
| `POST` | `/api/analyze/reset` | Reset analysis |
| `GET` | `/api/stats/describe` | Descriptive stats |
| `GET` | `/api/stats/correlation` | Correlation matrix |
| `GET` | `/api/stats/distribution` | Distribution data |
| `GET` | `/api/stats/outliers` | Outlier detection |
| `POST` | `/api/charts/build` | Build chart |
| `POST` | `/api/charts/matplotlib` | Matplotlib chart |
| `POST` | `/api/ai-advisor/analyze` | AI analysis |
| `POST` | `/api/ai-advisor/chat` | AI chat |
| `POST` | `/api/ai-advisor/fix` | Auto-fix data |
| `POST` | `/api/gemini/chat` | Gemini chat |
| `GET` | `/api/profiling/report` | Profiling report |
| `GET` | `/api/admin/users` | List users |
| `DEL` | `/api/admin/users/{id}` | Delete user |
| `GET` | `/api/admin/metrics` | System metrics |
| `GET` | `/api/health` | Health check |
| `POST` | `/api/contact` | Contact form |

---

## 🗄️ Database Schema

### 👤 users
| Field | Type |
|-------|------|
| `id` | UUID PK |
| `firebase_uid` | VARCHAR? |
| `name` | VARCHAR |
| `email` | VARCHAR UNIQUE |
| `password_hash` | VARCHAR? |
| `role` | user/admin |
| `is_active` | BOOL |
| `uploads` | INT |
| `api_calls_count` | INT |
| `last_login` | DATETIME |

### 📁 datasets
| Field | Type |
|-------|------|
| `id` | UUID PK |
| `user_id` | FK→users |
| `filename` | VARCHAR |
| `file_path` | TEXT |
| `rows` | INT |
| `columns` | INT |
| `file_size` | BIGINT |
| `created_at` | DATETIME |

### 🔑 sessions
| Field | Type |
|-------|------|
| `id` | UUID PK |
| `user_id` | FK→users |
| `token` | TEXT |
| `expires_at` | DATETIME |
| `is_revoked` | BOOL |
| `created_at` | DATETIME |

### 📋 activity_logs
| Field | Type |
|-------|------|
| `id` | INT PK |
| `user_id` | FK→users |
| `action` | VARCHAR |
| `resource` | VARCHAR |
| `details` | JSON |
| `ip_address` | VARCHAR |
| `created_at` | DATETIME |

---

## 🧠 Backend Services Layer

### ⚙️ Analysis Engine
- **engine.py**: Core data processing pipeline · Pandas/Polars
- **analyzer_service.py**: Column type inference · data profiling
- **stats_service.py**: Descriptive stats · correlation · distribution
- **chart_service.py**: Plotly / Matplotlib chart generation

### 🔬 Quality & AI
- **quality_score.py**: Data quality scoring · completeness · consistency
- **anomaly.py**: Anomaly detection · outlier flagging
- **ai_advisor.py**: Gemini-powered analysis · chat · auto-fix
- **stats.py**: 87 KB · Comprehensive statistics module

### 🔐 Auth & Admin
- **routers/auth.py**: Register / login / refresh · bcrypt + PyJWT
- **firebase_auth.py**: Firebase token verify · user sync
- **admin.py**: User management · metrics · activity logs
- **utils/security.py**: Password hashing · JWT encode/decode

---

## 🏛️ Infrastructure & Security

| Technology | Purpose |
|------------|---------|
| 🔄 CORS Middleware | Cross-origin resource sharing |
| 🔒 HTTPS Redirect (prod) | Secure connections |
| 🛡️ XSS / CSRF Headers | Security headers |
| ⏱️ Request Logging | API monitoring |
| 🚫 Global Exception Handler | Error handling |
| 🔑 JWT Auth (PyJWT) | Authentication |
| 🔐 bcrypt Password Hashing | Password security |
| 🔥 Firebase Admin SDK | Firebase integration |
| ⚡ Redis In-Memory Cache | Caching |
| 📄 SQLAlchemy ORM | Database ORM |
| 🐘 PostgreSQL (prod) | Production database |
| 🗂️ SQLite (dev) | Development database |
| 🔢 Pagination Headers | API pagination |
| 📋 OpenAPI / Swagger Docs | API documentation |
| 🌐 Uvicorn ASGI | ASGI server |
| 🌱 dotenv Config | Environment variables |

---

## 📦 Technology Stack

### 🖥️ Frontend Stack
- ⚛️ React 18
- ⚡ Vite
- 🎨 TailwindCSS
- 🔀 React Router v6
- 📡 Axios
- 🔥 Firebase SDK
- 📊 Plotly.js
- 🌙 Dark/Light Theme

### 🐍 Backend Stack
- 🚀 FastAPI
- 🌐 Uvicorn
- 🐼 Pandas
- 🔢 NumPy
- ⚡ Polars
- 📊 Plotly
- 🐍 Matplotlib
- 🧬 SciPy
- 🤖 scikit-learn
- 🔍 rapidfuzz

### ☁️ External / AI
- 🤖 Google Gemini AI
- 🔥 Firebase Auth
- 📦 Supabase
- ⚡ Redis
- 🐘 PostgreSQL

---

*DataViz Architecture Scheme · FastAPI v3.0.0 + React 18 + Vite*
