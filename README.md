# Real-Time Ivy League Opportunity Intelligence & Student Competency

A full-stack web application that provides real-time aggregation and intelligent matching of opportunities (internships, fellowships, research positions, scholarships, conferences, etc.) from Ivy League universities with students based on their skills, interests, and domains of study.

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Architecture](#architecture)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Features](#features)
- [Setup & Installation](#setup--installation)
- [Running the Application](#running-the-application)
- [API Endpoints](#api-endpoints)
- [Database Models](#database-models)
- [Configuration](#configuration)
- [Deployment](#deployment)

## 🎯 Project Overview

The **Real-Time Ivy League Opportunity Intelligence & Student Competency (OI-SCI)** platform automates the discovery and intelligent matching of academic and professional opportunities from top-tier universities with qualified students. 

**Key Goals:**
- Aggregate opportunities from Ivy League RSS feeds in real-time
- Use AI (Google Gemini) to intelligently categorize, extract metadata, and match opportunities to students
- Provide students with personalized opportunity recommendations based on their academic domain and skills
- Enable efficient opportunity browsing with filtering and search capabilities

## 🏗️ Architecture

The application follows a **microservices architecture** with separated frontend and backend:

```
┌─────────────────────────────────────┐
│     Frontend (Django Web App)       │
│  - User Authentication & Dashboard  │
│  - Opportunity Browser & Filters    │
│  - Student Profile Management       │
└──────────────┬──────────────────────┘
               │ HTTP/REST API
               ↓
┌─────────────────────────────────────┐
│  Backend (FastAPI Service)          │
│  - RSS Feed Aggregation             │
│  - AI-Powered Opportunity Analysis  │
│  - Database Management              │
│  - RESTful API Endpoints            │
└──────────────┬──────────────────────┘
               │ 
               ↓
┌─────────────────────────────────────┐
│  Shared PostgreSQL Database         │
│  - Opportunities                    │
│  - Student Profiles                 │
└─────────────────────────────────────┘
```

## 💻 Technology Stack

### Backend
- **Framework**: FastAPI (Python)
- **ORM**: SQLAlchemy
- **Database**: PostgreSQL
- **AI**: Google Gemini API
- **Task Scheduling**: APScheduler
- **RSS Parsing**: feedparser, BeautifulSoup4
- **HTTP Client**: requests
- **Environment**: python-dotenv

### Frontend
- **Framework**: Django 5.2.11
- **Web Server**: Gunicorn
- **Database Client**: psycopg2-binary
- **HTTP Client**: requests
- **Environment**: python-dotenv
- **Templates**: HTML/CSS/JavaScript

### Database
- **PostgreSQL** (Production)
- **SQLite** (Development)

### External APIs
- **Google Gemini API** - For intelligent opportunity analysis and categorization
- **Ivy League RSS Feeds** - For real-time opportunity aggregation

## 📁 Project Structure

```
Ivy-League-Students-Website/
│
├── README.md                    # Project documentation
│
├── Backend/                     # FastAPI Backend Service
│   ├── main.py                  # FastAPI app, RSS feed aggregation
│   ├── models.py                # SQLAlchemy models (Opportunity)
│   ├── database.py              # Database configuration
│   ├── requirements.txt          # Python dependencies
│   ├── render.yaml              # Render deployment config
│   └── .env                      # Environment variables (not tracked)
│
└── Frontend/                    # Django Web Application
    ├── manage.py                # Django management script
    ├── db.sqlite3               # SQLite database (dev)
    ├── requirements.txt         # Python dependencies
    ├── Procfile                 # Procfile for deployment
    ├── render.yaml              # Render deployment config
    │
    ├── Project/                 # Django project settings
    │   ├── settings.py          # Django configuration
    │   ├── urls.py              # URL routing
    │   ├── asgi.py              # ASGI configuration
    │   └── wsgi.py              # WSGI configuration
    │
    ├── app/                     # Main Django app
    │   ├── models.py            # Django models (Student)
    │   ├── views.py             # View logic (Auth, Dashboard, Opportunities)
    │   ├── urls.py              # App URL patterns
    │   ├── admin.py             # Django admin config
    │   ├── tests.py             # Test cases
    │   ├── apps.py              # App configuration
    │   ├── migrations/          # Database migrations
    │   └── __pycache__/         # Python cache
    │
    ├── templates/               # HTML Templates
    │   ├── base.html            # Base template
    │   ├── home.html            # Home page
    │   ├── login.html           # Login page
    │   ├── register.html        # Registration page
    │   ├── dashboard.html       # Student dashboard
    │   ├── opportunities.html   # Opportunities listing
    │   └── all_opportunities.html # All opportunities page
    │
    ├── Arif/ & Ram/             # Virtual environments
    └── .env                      # Environment variables (not tracked)
```

## ✨ Features

### Backend Features
- ✅ **Real-Time RSS Feed Aggregation** - Continuously monitors Ivy League RSS feeds
- ✅ **AI-Powered Analysis** - Uses Google Gemini to:
  - Extract key information (deadline, eligibility, requirements)
  - Categorize opportunities (internship, fellowship, research, etc.)
  - Identify domain and sub-domain relevance
  - Generate summaries and skill requirements
- ✅ **Background Job Scheduling** - Automated feeds update using APScheduler
- ✅ **RESTful API** - Fast, modern API for frontend consumption
- ✅ **Database Persistence** - Stores opportunities with structured metadata

### Frontend Features
- ✅ **User Authentication** - Secure login and registration
- ✅ **Student Profile** - Students define academic domain and sub-domain
- ✅ **Dashboard** - Personalized opportunity recommendations
- ✅ **Opportunity Browser** - Browse, search, and filter opportunities
- ✅ **Real-Time Updates** - Fresh opportunities from backend
- ✅ **Responsive Design** - Mobile-friendly interface

## 🚀 Setup & Installation

### Prerequisites
- Python 3.9+ 
- PostgreSQL (production) or SQLite (development)
- Git
- Virtual environment tool (venv/virtualenv)
- API Keys:
  - Google Gemini API key

### Backend Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Ivy-League-Students-Website
   ```

2. **Create and activate virtual environment**
   ```bash
   python -m venv backend_env
   # Windows
   backend_env\Scripts\activate
   # MacOS/Linux
   source backend_env/bin/activate
   ```

3. **Install dependencies**
   ```bash
   cd Backend
   pip install -r requirements.txt
   ```

4. **Configure environment variables**
   ```bash
   # Create .env file in Backend/
   GEMINI_API_KEY=your_google_gemini_api_key
   DATABASE_URL=postgresql://user:password@localhost/ivyleague_db
   ```

5. **Initialize database**
   ```bash
   # Database will be created automatically via SQLAlchemy
   python main.py
   ```

### Frontend Setup

1. **Create and activate virtual environment**
   ```bash
   python -m venv frontend_env
   # Windows
   frontend_env\Scripts\activate
   # MacOS/Linux
   source frontend_env/bin/activate
   ```

2. **Install dependencies**
   ```bash
   cd Frontend
   pip install -r requirements.txt
   ```

3. **Configure environment variables**
   ```bash
   # Create .env file in Frontend/
   BACKEND_URL=http://localhost:8000
   SECRET_KEY=your-django-secret-key
   DEBUG=True
   ALLOWED_HOSTS=localhost,127.0.0.1
   ```

4. **Run migrations**
   ```bash
   python manage.py migrate
   ```

5. **Create superuser (optional)**
   ```bash
   python manage.py createsuperuser
   ```

## 🏃 Running the Application

### Run Backend (FastAPI)
```bash
cd Backend
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```
Backend will be available at: `http://localhost:8000`

### Run Frontend (Django)
```bash
cd Frontend
python manage.py runserver 8000
```
Frontend will be available at: `http://localhost:8000`

> **Note**: If running both on same machine, run backend on port 8000 and frontend on port 8001:
> ```bash
> python manage.py runserver 8001
> ```

## 🔌 API Endpoints

### Backend FastAPI Endpoints

**Opportunities Management**
- `GET /opportunities` - Fetch all opportunities
- `GET /opportunities/{id}` - Get specific opportunity
- `POST /opportunities` - Create new opportunity (internal)
- `PUT /opportunities/{id}` - Update opportunity (internal)
- `DELETE /opportunities/{id}` - Delete opportunity (internal)

**RSS Feed Operations**
- `POST /fetch-feeds` - Manually trigger RSS feed aggregation
- `GET /feed-status` - Get last feed update status

### Frontend Django Views

**Authentication**
- `POST /register` - Register new student
- `POST /login` - Login student
- `GET /logout` - Logout student

**Dashboard**
- `GET /dashboard` - Student dashboard with recommendations
- `GET /opportunities` - Browse all opportunities
- `GET /opportunities/search` - Search opportunities with filters

**Profiles**
- `GET /profile` - View student profile
- `POST /profile/update` - Update student profile

## 📊 Database Models

### Opportunity Model (Backend - SQLAlchemy)
```python
class Opportunity(Base):
    id: Integer (Primary Key)
    title: String - Opportunity title
    university: String - Source university
    category: String - Type (internship, fellowship, research, etc.)
    domain: String - Academic domain (CS, Business, Science, etc.)
    sub_domain: String - Specific field (ML, Web Dev, etc.)
    deadline: String - Application deadline
    eligibility: Text - Eligibility criteria
    skills_required: Text - Required/preferred skills
    application_link: String - URL to apply
```

### Student Model (Frontend - Django)
```python
class Student(Model):
    user: ForeignKey(User)
    domain: CharField - Academic domain
    sub_domain: CharField - Specific field of study
    created_at: DateTimeField
    updated_at: DateTimeField
```

## ⚙️ Configuration

### Backend Configuration (Backend/main.py)
- **RSS Feeds**: Currently configured for:
  - Harvard University News
  - Yale University News  
  - Cornell University News
- **Opportunity Keywords**: Filters for relevant opportunities
- **Application Keywords**: Detects if an opportunity has open applications

### Frontend Configuration (Frontend/Project/settings.py)
- **BACKEND_URL**: API endpoint for backend service
- **ALLOWED_HOSTS**: Allowed domain names
- **DEBUG**: Debug mode flag
- **DATABASES**: Database configuration

## 📦 Deployment

### Render Deployment (Recommended)

Both Backend and Frontend include `render.yaml` configuration files for easy deployment to Render.

**Backend Deployment** (`Backend/render.yaml`)
```yaml
services:
  - type: web
    name: ivy-league-backend
    env: python
    plan: starter
    buildCommand: pip install -r requirements.txt
    startCommand: uvicorn main:app --host 0.0.0.0 --port $PORT
```

**Frontend Deployment** (`Frontend/render.yaml`)
```yaml
services:
  - type: web
    name: ivy-league-frontend
    env: python
    plan: starter
    buildCommand: pip install -r requirements.txt && python manage.py migrate
    startCommand: gunicorn Project.wsgi:application --bind 0.0.0.0:$PORT
```

### Environment Variables for Production
Set these in your deployment platform:
- `GEMINI_API_KEY` - Google Gemini API key
- `DATABASE_URL` - Production PostgreSQL connection string
- `BACKEND_URL` - Backend API URL for frontend
- `SECRET_KEY` - Django secret key (strong, random string)
- `DEBUG` - Set to False in production
- `ALLOWED_HOSTS` - Production domain names

## 🔒 Security Notes

- Never commit `.env` files to version control
- Use strong `SECRET_KEY` in production
- Validate and sanitize all user inputs
- Use HTTPS in production
- Implement rate limiting on API endpoints
- Use environment-specific settings

## 📝 Environment Variables Template

### Backend (.env)
```
GEMINI_API_KEY=your_api_key_here
DATABASE_URL=postgresql://user:password@localhost/ivyleague
```

### Frontend (.env)
```
BACKEND_URL=http://localhost:8000
SECRET_KEY=your-secret-key-here
DEBUG=True
ALLOWED_HOSTS=localhost,127.0.0.1
```

## 🤝 Contributing

1. Create a feature branch (`git checkout -b feature/AmazingFeature`)
2. Commit changes (`git commit -m 'Add some AmazingFeature'`)
3. Push to branch (`git push origin feature/AmazingFeature`)
4. Open a Pull Request

## 📋 Future Enhancements

- [ ] Email notifications for matching opportunities
- [ ] ML-based improved opportunity-student matching
- [ ] More university RSS feed sources
- [ ] Advanced analytics dashboard
- [ ] Mobile application
- [ ] Opportunity save/bookmarking feature
- [ ] User activity tracking and insights
- [ ] API rate limiting and caching

## 📞 Support & Contact

For issues, questions, or suggestions, please open a GitHub issue or contact the development team.

## 📄 License

This project is licensed under the MIT License - see LICENSE file for details.

---

**Last Updated**: February 2026
