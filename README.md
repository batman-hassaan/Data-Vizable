<div align="center">

# ✦ Data Vizable™

### **The AI-Powered Data Analytics & Machine Learning Platform**

*Upload. Clean. Visualize. Predict. — All from your browser.*

<br/>

[![Live Platform](https://img.shields.io/badge/🌐_Live_Platform-data--vizable.vercel.app-6366f1?style=for-the-badge&labelColor=1e1b4b)](https://data-vizable.vercel.app/)
&nbsp;&nbsp;
[![API Status](https://img.shields.io/badge/API-Operational-10b981?style=for-the-badge&labelColor=064e3b)](https://data-vizable.vercel.app/)

<br/>

[![React 19](https://img.shields.io/badge/React-19-61DAFB?style=flat-square&logo=react&logoColor=white)](https://react.dev/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.115+-009688?style=flat-square&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Scikit Learn](https://img.shields.io/badge/Scikit--Learn-ML_Engine-F7931E?style=flat-square&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
[![Plotly](https://img.shields.io/badge/Plotly-3D_Studio-3F4F75?style=flat-square&logo=plotly&logoColor=white)](https://plotly.com/)
[![Firebase](https://img.shields.io/badge/Firebase-Auth-FFCA28?style=flat-square&logo=firebase&logoColor=black)](https://firebase.google.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-4.0-06B6D4?style=flat-square&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)

<br/>

> **Data Vizable** is a production-grade SaaS platform that transforms raw data files into actionable intelligence. Upload any dataset, clean it with surgical precision, generate publication-ready 2D and 3D visualizations, compute deep statistical profiles, and train machine learning models — all without writing a single line of code.

</div>

---

<br/>

## 🔗 Live Platform

<div align="center">

### **[→ Launch Data Vizable](https://data-vizable.vercel.app/)**

*Publicly available. Create a free account and start analyzing data in seconds.*

</div>

<br/>

---

## 🏗️ How It Works

Data Vizable follows a streamlined four-stage pipeline that takes users from raw data to trained ML models:

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   UPLOAD    │ ──▶ │    CLEAN    │ ──▶ │  VISUALIZE  │ ──▶ │   PREDICT   │
│             │     │             │     │             │     │             │
│ CSV · XLSX  │     │ Fill Nulls  │     │ 2D Charts   │     │ Train ML    │
│ XLS · JSON  │     │ Drop Dupes  │     │ 3D Plotly   │     │ Evaluate    │
│ Drag & Drop │     │ Fix Types   │     │ Heatmaps    │     │ Predict     │
│ Up to 100MB │     │ Regex Ops   │     │ Correlation │     │ Export      │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
```

**1. Upload** — Drag-and-drop any `.csv`, `.xlsx`, `.xls`, or `.json` file. The backend parses it with Pandas, generates a UUID-keyed session, caches the dataframe in-memory, and returns a lightweight 100-row preview instantly.

**2. Clean** — Use the Data Surgery toolbar to impute missing values (mean / median / mode / custom), remove duplicates, convert column types, apply text transformations (uppercase, lowercase, trim, regex replace), and detect + remove outliers. Every operation is non-destructive — the original dataset is preserved and can be restored at any time.

**3. Visualize** — Build interactive 2D charts (Bar, Line, Pie, Scatter, Area, Box, Histogram) powered by Recharts, Chart.js, and ApexCharts. Switch to the 3D Plotly Studio for Scatter3D, Line3D, and Surface plots. Generate Pearson correlation heatmaps to uncover hidden relationships between numeric columns.

**4. Predict** — Select a target column, pick your features, choose an algorithm (Linear Regression, Logistic Regression, Random Forest, SVM), and train a Scikit-learn model directly in the browser. Review evaluation metrics (MSE, RMSE, R², Accuracy, Precision, Recall, F1, ROC-AUC, Confusion Matrix), then use the live prediction form to get instant inferences.

---

## 🚀 Complete Feature Breakdown

### 🔐 Authentication & Access Control

| Capability | Description |
|:---|:---|
| **Multi-Provider Sign-In** | Email/Password registration and **Google OAuth** sign-in, both powered by **Firebase Authentication** |
| **JWT Token Architecture** | Stateless API authorization using JSON Web Tokens with automatic token injection via Axios interceptors |
| **Role-Based Access (RBAC)** | Two-tier role system (`user` / `admin`) controlling feature access and API permissions |
| **Password Recovery** | Dedicated forgot-password flow with Firebase-backed email reset links |
| **Account Management** | Full profile management including password change, role inspection, and GDPR-compliant account deletion |
| **Admin-Only Routes** | Protected route guards (`ProtectedRoute`, `AdminRoute`) enforcing authentication and role checks on every navigation |
| **Firebase + Local Sync** | Dual authentication pipelines — Firebase tokens are verified server-side via Firebase Admin SDK and synced with the local SQLAlchemy user database |

---

### 📁 Data Ingestion & Session Management

| Capability | Description |
|:---|:---|
| **Drag-and-Drop Upload** | Intuitive file upload interface with real-time progress indicators and file validation |
| **Multi-Format Support** | Accepts `.csv`, `.xlsx`, `.xls`, and `.json` files up to 100 MB |
| **In-Memory Caching** | Datasets are parsed by Pandas and cached in a UUID-keyed volatile memory store, enabling sub-millisecond column operations |
| **Preview-First Strategy** | Only a 100-row preview is sent to the frontend initially — the full dataset stays server-side, preventing browser memory overflow |
| **Session Isolation** | Each upload generates a unique session ID. Datasets are strictly isolated between sessions and users — zero cross-contamination |
| **Instant Reset** | One-click dataset restoration reverts all cleaning operations and edits, rolling back to the original uploaded state |

---

### 🔬 Data Quality & Anomaly Detection

| Capability | Description |
|:---|:---|
| **Dimensional Quality Score** | Composite quality index computed across four dimensions: **Completeness**, **Uniqueness**, **Validity**, and **Consistency** |
| **Completeness Analysis** | Maps and quantifies missing values across every column with percentage breakdowns |
| **Uniqueness Detection** | Identifies exact and fuzzy duplicates using **RapidFuzz** string matching and cardinality analysis |
| **Validity Checks** | Validates fields against regex patterns (email format, phone numbers, timestamps, URLs) to surface data entry errors |
| **Consistency Evaluation** | Measures data type uniformity and computes outlier ratios using IQR (Interquartile Range) |
| **Anomaly Detection Engine** | Powered by **Isolation Forest** (Scikit-learn) for numerical anomalies, plus temporal and categorical anomaly detectors |
| **Column Profiler** | Deep per-column statistical profiling including distribution shape, cardinality, and missing value visualization |
| **Recommendation Engine** | Actionable fix recommendations with priority levels (High / Medium / Low) and auto-fix capabilities |
| **ML Readiness Score** | Calculates a 0–100 readiness score indicating how prepared the dataset is for machine learning training |

---

### 🛠️ Data Surgery — Cleaning & Transformation Toolkit

| Capability | Description |
|:---|:---|
| **Missing Value Imputation** | Fill nulls with **mean**, **median**, **mode**, or a **custom value** — applied per-column with real-time preview |
| **Duplicate Removal** | Drop exact duplicate rows with a single click |
| **Column Deletion** | Remove irrelevant or noisy columns from the active dataframe |
| **Data Type Conversion** | Convert columns between `string`, `numeric`, `datetime`, and `boolean` types |
| **Outlier Removal** | Statistical outlier removal using IQR-based thresholds |
| **Text Transformations** | Bulk operations: uppercase, lowercase, trim whitespace, regex find-and-replace, substring extraction |
| **Currency & Percentage Cleaning** | Strip currency symbols (`$`, `€`, `£`) and percentage signs to convert financial and percentage columns to numeric |
| **Spreadsheet-Style Cell Editor** | Click any cell to edit it inline with optimistic UI updates, complete undo/redo stack, and live validation |
| **Column Sorting & Filtering** | Sort columns ascending/descending and apply filter conditions directly in the data grid |
| **Non-Destructive Operations** | Every transformation preserves the original dataset — full rollback available at any time via session reset |

---

### 📊 2D Visualization Suite

| Chart Type | Engine | Description |
|:---|:---|:---|
| **Bar Chart** | Recharts / Chart.js | Categorical comparison with customizable axes and group-by aggregation |
| **Line Chart** | Recharts / ApexCharts | Trend analysis over sequential data with smooth interpolation |
| **Pie Chart** | Recharts | Proportional distribution visualization with interactive legend |
| **Scatter Plot** | Plotly.js | Bi-variate relationship mapping with hover tooltips and zoom |
| **Area Chart** | Recharts | Cumulative value visualization with gradient fill |
| **Box Plot** | Plotly.js | Distribution summary showing quartiles, median, and outliers |
| **Histogram** | Plotly.js | Frequency distribution with configurable bin sizes |
| **Correlation Heatmap** | Plotly.js + Seaborn | Pearson correlation matrix with color-coded intensity mapping |

All charts feature:
- Dynamic column selection (X-axis, Y-axis, Group-by)
- Responsive rendering across desktop and mobile
- Built-in chart caching to prevent redundant API calls
- Dark/Light theme adaptation

---

### 🌐 3D Visualization Studio (Plotly)

| Chart Type | Description |
|:---|:---|
| **3D Scatter Plot** | Map three numeric dimensions to X, Y, Z axes with interactive rotation, zoom, and hover data |
| **3D Line Plot** | Trace paths through three-dimensional space to visualize sequential multi-variate data |
| **3D Surface Plot** | Render continuous surfaces from gridded data to reveal topological patterns and gradients |

The 3D Studio provides full orbital camera controls, axis labeling, color gradient mapping, and export capabilities — all rendered client-side using Plotly.js.

---

### 📈 Statistical Analysis Engine

| Metric | Description |
|:---|:---|
| **Mean / Median / Mode** | Central tendency measures computed per-column |
| **Standard Deviation / Variance** | Dispersion metrics for numeric distributions |
| **Min / Max / Range** | Boundary values and spread |
| **Skewness / Kurtosis** | Distribution shape analysis via SciPy |
| **Missing Value Count** | Per-column null frequency with percentage |
| **Unique Value Count** | Cardinality analysis for categorical detection |
| **Quantile Breakdowns** | Q1, Q2, Q3 percentile distributions |
| **Data Type Detection** | Smart classification: numeric, categorical, boolean, datetime, string |
| **Descriptive Stats Table** | Full Excel-style statistical summary panel with sortable columns and export |

Server-side pagination (default 50 rows, max 1,000) ensures the statistics engine scales gracefully even with datasets containing millions of rows.

---

### 🧠 Zero-Code Machine Learning Studio

#### Supported Algorithms

| Algorithm | Type | Use Case |
|:---|:---|:---|
| **Linear Regression** | Regression | Continuous target prediction (price, revenue, temperature) |
| **Random Forest Regressor** | Regression | Complex non-linear regression with ensemble decision trees |
| **Logistic Regression** | Classification | Binary/multi-class classification (spam detection, churn prediction) |
| **Random Forest Classifier** | Classification | High-accuracy classification with feature importance ranking |
| **Support Vector Machine (SVM)** | Classification | Margin-based classification for linearly and non-linearly separable data |

#### Training Pipeline

1. **Select Target Column** — Choose the column you want to predict
2. **Pick Features** — Select one or more input columns
3. **Configure Split** — Set the train/test ratio (default 80/20)
4. **Choose Algorithm** — Select from the supported model list
5. **Train** — The backend builds a Scikit-learn Pipeline with preprocessing (imputation, encoding, scaling), trains the model, and returns evaluation metrics

#### Evaluation Metrics

| Regression Metrics | Classification Metrics |
|:---|:---|
| Mean Squared Error (MSE) | Confusion Matrix |
| Root Mean Squared Error (RMSE) | Accuracy Score |
| R-Squared (R²) | Precision / Recall / F1-Score |
| | ROC-AUC Curve |

#### Live Prediction Interface
After training, a dynamic form appears with input fields for each feature column. Enter values, click predict, and receive instant inferences from the trained model — no API knowledge required.

---

### 🤖 AI Advisor & Chat Assistant

| Capability | Description |
|:---|:---|
| **AI Advisor Panel** | Automated dataset scan that generates prioritized issue cards with severity levels (High / Medium / Low) and confidence scores |
| **Smart Fix Buttons** | One-click auto-remediation for common issues: clean currency columns, normalize text, convert date strings, clamp outliers, scale features |
| **Auto-Clean Agent** | Batch-apply all recommended fixes simultaneously for rapid dataset preparation |
| **ML Readiness Score** | Visual gauge showing how prepared the current dataset is for ML training |
| **Floating AI Chat** | Global chat assistant available on every page — context-aware prompts that adapt based on the current page (Dashboard, Analytics, ML Studio, etc.) |
| **Smart Response Engine** | Intelligent local response system that analyzes your active dataset and provides targeted advice about cleaning, modeling, and visualization |
| **Gemini API Integration** | Backend hooks for Google's Gemini generative AI to provide deep-learning-powered dataset insights and automated chart recommendations |

---

### 🛡️ System Administration Console

Available exclusively to users with the `admin` role:

| Capability | Description |
|:---|:---|
| **System Health Monitor** | Real-time CPU, memory, and disk usage metrics via `psutil` |
| **User Directory** | Searchable list of all registered users with role management (promote/demote), account activation/deactivation |
| **Activity Logging** | Comprehensive audit trail of file uploads, data transformations, model training events, and session activity |
| **Database Diagnostics** | Connection pool status, query execution logs, and SQLAlchemy engine health checks |
| **API Latency Tracking** | Request logging middleware capturing method, path, status code, and response time for every API call |
| **Session Telemetry** | Live view of active in-memory dataset cache size and session distribution |

---

### 🎨 User Experience & Design

| Feature | Description |
|:---|:---|
| **Dark / Light Theme** | Full theme engine using CSS custom properties with smooth transitions — persisted across sessions |
| **Framer Motion Animations** | Micro-animations on page transitions, card hovers, modal entries, accordion expansions, and loading states |
| **Responsive Design** | Fully responsive across desktop, tablet, and mobile breakpoints |
| **Lazy Loading** | Every page is code-split and lazy-loaded via React `Suspense` with animated skeleton placeholders |
| **Premium Loading Spinners** | Multi-stage loading animations with contextual messages |
| **Glassmorphism UI** | Backdrop blur, frosted glass panels, and gradient accents throughout the interface |
| **Lucide Icon System** | Consistent iconography using the Lucide React icon library |
| **Animated Navbar** | Scroll-aware navigation bar with dynamic transparency, mobile hamburger menu, and profile dropdown |
| **Footer Navigation** | Comprehensive footer with links to all legal, informational, and product pages |

---

### 📄 SaaS Product Pages

Data Vizable ships as a complete SaaS product with the following public-facing pages:

| Page | Route | Purpose |
|:---|:---|:---|
| **Landing Page** | `/` | Hero section, feature showcase, testimonials, tech stack display, FAQ, and call-to-action |
| **Features** | `/features` | Complete 17-feature breakdown with technical descriptions and FAQ accordion |
| **Pricing** | `/pricing` | Three-tier pricing table (Starter — Free, Pro — $12/mo, Enterprise — $49/mo) with annual/monthly toggle |
| **About** | `/about` | Company story, team information, and mission statement |
| **FAQ** | `/faq` | Comprehensive question-and-answer section covering all platform capabilities |
| **Changelog** | `/changelog` | Version history from v1.0.0 (Dec 2025) through v3.0.0 (Apr 2026) with tagged releases |
| **Contact** | `/contact` | User feedback and support inquiry form |
| **Privacy Policy** | `/privacy` | Data handling, collection, and user rights documentation |
| **Terms of Service** | `/terms` | Platform usage terms and conditions |
| **Cookie Policy** | `/cookies` | Cookie usage disclosure and preferences |
| **Security** | `/security` | Platform security architecture and practices overview |

---

## 💰 Pricing Tiers

<div align="center">

| | **Starter** | **Pro** ⭐ | **Enterprise** |
|:---|:---:|:---:|:---:|
| **Price** | Free | $12/mo | $49/mo |
| Upload Limit | 5 datasets | Unlimited | Unlimited |
| File Formats | CSV, JSON | CSV, XLS, XLSX, JSON | All + Custom |
| Basic Charts | ✅ | ✅ | ✅ |
| Full Chart Suite + Plotly | ❌ | ✅ | ✅ |
| Statistical Analysis | Basic | Full | Full |
| Spreadsheet Editor | ❌ | ✅ | ✅ |
| Data Cleaning Tools | ❌ | ✅ | ✅ |
| Heatmap & Correlation | ❌ | ✅ | ✅ |
| ML Studio | ❌ | ✅ | ✅ |
| 3D Visualization Studio | ❌ | ✅ | ✅ |
| Export (CSV/Excel) | ❌ | ✅ | ✅ |
| AI / Gemini Integration | ❌ | ❌ | ✅ |
| Admin Panel | ❌ | ❌ | ✅ |
| Self-Hosted Deployment | ❌ | ❌ | ✅ |
| SSO & Advanced Auth | ❌ | ❌ | ✅ |
| Audit Logging | ❌ | ❌ | ✅ |
| SLA Guarantee | ❌ | ❌ | 99.99% |
| Support | Community | Email | Dedicated Manager |

</div>

---

## 🛠️ Technology Stack

### Frontend
| Technology | Purpose |
|:---|:---|
| **React 19** | Core UI framework with hooks, Suspense, and lazy loading |
| **Vite** | Lightning-fast build tool and dev server with HMR |
| **React Router DOM v7** | Client-side routing with protected and admin route guards |
| **Tailwind CSS 4.0** | Utility-first styling with custom design tokens |
| **Framer Motion** | Animation library for transitions, gestures, and layout animations |
| **Plotly.js** | Interactive 2D/3D scientific charting engine |
| **Recharts** | Composable React chart components |
| **Chart.js** | Lightweight canvas-based charting |
| **ApexCharts** | Modern interactive charts with zoom and pan |
| **Axios** | HTTP client with JWT interceptor for authenticated API calls |
| **Firebase Client SDK** | Google OAuth and email/password authentication |
| **Lucide React** | Consistent SVG icon system |

### Backend
| Technology | Purpose |
|:---|:---|
| **FastAPI** | High-performance async Python web framework |
| **Uvicorn** | ASGI server with SSL and worker configuration |
| **Pandas** | DataFrame-based data manipulation and analysis |
| **NumPy** | Numerical computing and array operations |
| **Polars** | High-performance DataFrame library (available for large datasets) |
| **SciPy** | Scientific computing — skewness, kurtosis, statistical tests |
| **Scikit-learn** | ML pipelines — estimators, preprocessors, metrics, model evaluation |
| **Plotly (Python)** | Server-side chart configuration and heatmap generation |
| **Seaborn / Matplotlib** | Statistical visualization and correlation matrix rendering |
| **SQLAlchemy 2.0** | ORM for user management, sessions, and activity logging |
| **SQLite / PostgreSQL** | Relational database (SQLite for dev, PostgreSQL/Supabase for production) |
| **Firebase Admin SDK** | Server-side token verification and user sync |
| **PyJWT / passlib** | JWT token generation and Bcrypt password hashing |
| **RapidFuzz** | Fuzzy string matching for duplicate detection |
| **psutil** | System resource monitoring (CPU, memory, disk) |
| **Redis / Cachetools** | Caching layer for API response optimization |
| **PyArrow** | High-performance columnar data processing |

---

## 🔒 Security & Privacy

| Layer | Implementation |
|:---|:---|
| **Authentication** | Firebase Auth (OAuth 2.0 + Email/Password) with server-side JWT verification |
| **Password Storage** | Bcrypt hashing via `passlib` — passwords are never stored in plaintext |
| **API Security** | Stateless JWT tokens with expiration, injected via Axios interceptors on every request |
| **Data Isolation** | Datasets are cached in volatile memory keyed by UUID — no cross-session access possible |
| **HTTPS Enforcement** | `HTTPSRedirectMiddleware` enabled in production; HSTS headers with 2-year max-age |
| **Security Headers** | `X-Content-Type-Options: nosniff`, `X-Frame-Options: DENY`, `X-XSS-Protection: 1; mode=block`, `Referrer-Policy: strict-origin-when-cross-origin` |
| **CORS Protection** | Configured allowlist of trusted origins — no wildcard access in production |
| **Error Handling** | Global exception handler prevents stack trace leakage — returns sanitized JSON error responses |
| **Data Volatility** | User uploads are never persisted to disk by default — processed entirely in-memory |
| **Compliance Pages** | Built-in Privacy Policy, Terms of Service, Cookie Policy, and Security pages accessible from the platform footer |

---

## 📋 API Endpoints

The backend exposes a fully documented RESTful API organized by domain:

| Prefix | Tag | Scope |
|:---|:---|:---|
| `/api/auth` | Auth | Registration, login, token refresh, password change |
| `/api/auth` | Firebase Auth | Google sign-in verification, Firebase user sync |
| `/api/admin` | Admin | User management, telemetry, system diagnostics |
| `/api/analyze` | Analysis | File upload, dataset parsing, session management |
| `/api/stats` | Statistics | Descriptive stats, ML training, predictions, data cleaning |
| `/api/charts` | Visualization | Chart configuration, heatmap generation |
| `/api/ai-advisor` | AI Advisor | Dataset scan, issue detection, auto-fix actions |
| `/api/profiling` | Profiling | Column profiling, missing value distributions |
| `/api/gemini` | Gemini | AI-powered chat and dataset insight generation |
| `/api/contact` | Contact | User feedback submission |
| `/api/health` | System | Health check, cache status, environment info |

*Interactive Swagger documentation available at `/api/docs` and ReDoc at `/api/redoc`.*

---

## 📌 Release History

| Version | Date | Highlights |
|:---|:---|:---|
| **v3.0.0** | April 2026 | PostgreSQL integration, async DB lifecycle, auto-admin creation, Bcrypt auth, connection pool pre-ping |
| **v2.5.0** | March 2026 | ML Studio with Scikit-learn, Regression + Classification, Gemini API hooks, prediction endpoints |
| **v2.0.0** | February 2026 | Data Cleaning engine, Spreadsheet cell editor, Undo/Redo, Bulk text transforms, Column type intelligence |
| **v1.5.0** | January 2026 | Server-side pagination, Lazy loading, Preview-first architecture, Chart caching, React ref optimization |
| **v1.0.0** | December 2025 | Initial release — JWT auth, File upload, Plotly visualizations, Descriptive statistics, Export system, Dark/Light theme |

---

<div align="center">

## 🌟 Start Analyzing Your Data Today

### **[→ Launch Data Vizable](https://data-vizable.vercel.app/)**

*No installation required. Free tier available. Start in seconds.*

<br/>

---

<sub>Built with ❤️ using React, FastAPI, Scikit-learn, and Plotly · © 2025–2026 Data Vizable™ · All Rights Reserved</sub>

</div>
