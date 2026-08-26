# AI-Disease-Outbreak-Prediction-System
# DiseaseWatch Kenya
ML-powered disease surveillance system for predicting and visualizing malaria and cholera outbreaks across Kenya's 47 counties.

## 📌 Overview

DiseaseWatch is a full-stack machine learning–powered outbreak prediction and surveillance system for Kenya's public health sector. It transforms environmental data — temperature, rainfall, humidity, population density, and sanitation levels — into actionable malaria and cholera risk scores, combining a scikit-learn Random Forest prediction engine with an interactive, county-level geospatial dashboard.

## 🔑 Key Features

- 📊 **Predictive Engine** — malaria and cholera outbreak risk prediction using two independently trained `RandomForestRegressor` models, with confidence scores and Low/Medium/High severity classification.
- 🗺️ **Interactive Hotspot Map** — a Leaflet.js choropleth map visualizing real-time risk severity across all 47 Kenyan counties.
- 🔔 **Automated Alerting** — high-risk conditions (≥70% predicted risk) automatically generate alert records and notify subscribed users.
- 📈 **7-Day Risk Forecasting** — short-term outbreak trend projection with contextual, actionable recommendations for health officers.
- 👥 **Role-Based Access** — differentiated access for Health Officers, National Health Analysts, and System Administrators.
- 📄 **Reporting** — generate and download county- or period-level surveillance reports.
- ⚙️ **Personal Settings** — configurable notification preferences, risk thresholds, and display options per user.

## 🏗️ Tech Stack

### Backend
- **Flask** — lightweight Python web framework handling routing and application logic.
- **Flask-SQLAlchemy** — ORM-based data access layer over SQLite.
- **Flask-Login / Flask-Bcrypt** — session-based authentication and password hashing.
- **Flask-CORS** — cross-origin request handling for the REST API.

### Frontend
- **Jinja2** — server-side templating for dashboard, prediction, report, and settings pages.
- **Bootstrap** — responsive layout and UI components.
- **Leaflet.js** — interactive county-level geospatial risk mapping.
- **JavaScript (AJAX/fetch)** — asynchronous communication with the backend API.

### Machine Learning
- **scikit-learn** — `RandomForestRegressor` models for malaria and cholera risk prediction.
- **pandas / NumPy** — feature engineering and numerical preprocessing.
- **joblib** — trained model persistence, loaded once at application startup.

## 🧠 System Architecture

```
[ Browser / Jinja2 + Leaflet.js Frontend ]
                 ↓  HTTPS / JSON
[         Flask Application Server         ]
   ├─ Authentication Service (Flask-Login, Bcrypt)
   ├─ Data Processing Service
   ├─ Weather Integration Service
   ├─ Prediction Engine (RandomForestRegressor)
   └─ Alerting Service
                 ↓  SQLAlchemy ORM
[         SQLite Database (diseasewatch.db)         ]
```

See the full layered architecture, DFDs, and UML diagrams in the project design documentation.

## ⚙️ Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/diseasewatch-kenya.git
cd diseasewatch-kenya
```

### 2. Set Up the Environment

```bash
python3 -m venv venv
source venv/bin/activate       # Linux/macOS
# or venv\Scripts\activate     # Windows

pip install -r requirements.txt
```

### 3. Initialize the Database

```bash
python init_db.py
```

This seeds the database with all 47 Kenyan counties and creates two default accounts:

| Role | Username | Password |
|---|---|---|
| Administrator | `admin` | `admin123` |
| Health Officer (Demo) | `demo` | `demo123` |

> ⚠️ Change these credentials before any production deployment.

### 4. Run the Application

```bash
python app.py
```

The app will be available at `http://127.0.0.1:5000/`.

## 🚀 API Endpoints

| Endpoint | Method | Description |
|---|---|---|
| `/api/predict` | POST | Returns malaria/cholera risk scores, severity level, and recommendations |
| `/api/predictions/history` | GET | Returns historical prediction records for a county |
| `/api/alerts` | GET | Returns active/recent high-risk alerts |
| `/api/dashboard-stats` | GET | Returns national aggregate risk statistics |
| `/api/counties` | GET | Returns county reference data |
| `/api/weather/<county>` | GET | Returns auto-fetched weather data for a given county |
| `/api/settings` | GET/POST | Retrieves or updates user account settings |

## 📊 Model Performance

The prediction engine uses two `RandomForestRegressor` models trained on an epidemiologically-informed synthetic dataset (weighted combinations of temperature, rainfall, humidity, sanitation, and county risk factors). Formal evaluation against verified historical outbreak data (RMSE, R²) is planned as future work — see Recommendations — once real DHIS2/KHIS case data can be sourced.

| Model | Algorithm | Status |
|---|---|---|
| Malaria Risk | RandomForestRegressor | Trained, functionally validated |
| Cholera Risk | RandomForestRegressor | Trained, functionally validated |

## 🧪 Testing

The system includes an automated `pytest` suite (`test_diseasewatch.py`) covering unit tests for the prediction module and integration tests for the full authentication → prediction → alerting workflow.

```bash
pytest test_diseasewatch.py -v
```

## 🗺️ Project Roadmap

- [x] Data preprocessing & feature engineering
- [x] Random Forest model training (malaria & cholera)
- [x] Flask REST API with session-based authentication
- [x] Interactive Leaflet.js hotspot map
- [x] Automated alerting on high-risk thresholds
- [x] Automated test suite
- [ ] Integration with live DHIS2/KHIS historical case data
- [ ] Migration to a production-grade RDBMS (e.g. PostgreSQL)
- [ ] In-app help/onboarding system
- [ ] Field validation with real county health officers
- [ ] Containerization and cloud deployment

## 👨‍💻 Author

**Arwa**
Final-Year Computer Science / Information Systems Student

## 📜 License

This project is for academic/research purposes.
