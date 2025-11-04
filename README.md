# IntelliQuiz - AI-Powered Quiz Generator

[![Live Demo](https://img.shields.io/badge/Live-Demo-brightgreen)](https://intelliquizwiki.netlify.app/)
[![API Docs](https://img.shields.io/badge/API-Docs-blue)](https://intelliquiz-api.onrender.com/docs)
[![License](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

> Transform Wikipedia articles into interactive multiple-choice quizzes instantly using AI-powered generation

## 🚀 Live Deployment

- **Frontend Application**: [https://intelliquizwiki.netlify.app/](https://intelliquizwiki.netlify.app/)
- **Backend API**: [https://intelliquiz-api.onrender.com/docs](https://intelliquiz-api.onrender.com/docs)
- **API Documentation**: Interactive Swagger UI at backend URL

## 📋 Overview

IntelliQuiz is a full-stack web application that automatically generates educational quizzes from Wikipedia articles. Simply paste a Wikipedia URL, and our AI-powered backend will analyze the content and create a multiple-choice quiz with questions and answers.

### Key Features

- ✨ **AI-Powered Generation**: Intelligent quiz creation from Wikipedia content
- 🎯 **Multiple Choice Format**: Automatically generated questions with 4 options each
- 📊 **Quiz History**: Track and revisit previously generated quizzes
- ⚡ **Real-time Validation**: URL validation before quiz generation
- 🎨 **Modern UI**: Clean, responsive interface built with React
- 🔒 **Persistent Storage**: PostgreSQL database for quiz storage

## 🏗️ Architecture

### Technology Stack

#### Frontend
- **Framework**: React 18.3.1
- **HTTP Client**: Axios
- **Styling**: Custom CSS
- **Hosting**: Netlify
- **Build Tool**: Create React App

#### Backend
- **Framework**: FastAPI (Python)
- **ORM**: SQLAlchemy
- **Database**: PostgreSQL (Hosted on Render)
- **API Documentation**: Swagger/OpenAPI 3.1
- **AI Integration**: OpenAI GPT for quiz generation
- **Hosting**: Render
- **CORS**: Enabled for cross-origin requests

### System Components

```
IntelliQuiz
├── frontend/                  # React frontend application
│   ├── public/               # Static assets
│   ├── src/
│   │   ├── components/       # React components
│   │   │   ├── QuizForm.js   # Quiz generation form
│   │   │   ├── QuizDisplay.js # Quiz display interface
│   │   │   └── QuizHistory.js # Quiz history viewer
│   │   ├── App.js            # Main application component
│   │   └── App.css           # Styling
│   └── package.json          # Frontend dependencies
│
└── backend/                   # FastAPI backend application
    ├── app/
    │   ├── main.py           # FastAPI application entry point
    │   ├── models.py         # SQLAlchemy database models
    │   ├── schemas.py        # Pydantic request/response schemas
    │   ├── database.py       # Database configuration
    │   ├── crud.py           # Database CRUD operations
    │   └── __init__.py
    └── requirements.txt       # Python dependencies
```

## 🔌 API Endpoints

The backend API exposes the following endpoints:

### POST `/generate-quiz/`
Generate a new quiz from a Wikipedia URL

**Request Body:**
```json
{
  "url": "https://en.wikipedia.org/wiki/Artificial_Intelligence"
}
```

**Response:**
```json
{
  "id": 1,
  "title": "Artificial Intelligence Quiz",
  "url": "https://en.wikipedia.org/wiki/Artificial_Intelligence",
  "questions": [
    {
      "question": "What is AI?",
      "options": ["A", "B", "C", "D"],
      "correct_answer": "A"
    }
  ],
  "created_at": "2025-11-04T19:03:00"
}
```

### GET `/quizzes/`
Retrieve all generated quizzes from the database

**Response:** Array of quiz objects

### GET `/validate-url/`
Validate a Wikipedia URL before quiz generation

**Query Parameter:** `url`

**Response:**
```json
{
  "valid": true,
  "message": "Valid Wikipedia URL"
}
```

## 📦 Database Schema

### Quiz Model
```python
class Quiz(Base):
    id: Integer (Primary Key)
    title: String
    url: String (Wikipedia URL)
    questions: JSON (Array of question objects)
    created_at: DateTime
```

## 🚀 Getting Started

### Prerequisites

- Node.js 14+ and npm
- Python 3.8+
- PostgreSQL database
- OpenAI API key

### Frontend Setup

1. **Navigate to frontend directory:**
   ```bash
   cd frontend
   ```

2. **Install dependencies:**
   ```bash
   npm install
   ```

3. **Configure API endpoint:**
   Update the API base URL in your components to point to your backend:
   ```javascript
   const API_URL = 'https://intelliquiz-api.onrender.com' // or your local backend
   ```

4. **Start development server:**
   ```bash
   npm start
   ```

5. **Build for production:**
   ```bash
   npm run build
   ```

### Backend Setup

1. **Navigate to backend directory:**
   ```bash
   cd backend
   ```

2. **Create virtual environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables:**
   Create a `.env` file in the backend directory:
   ```env
   DATABASE_URL=postgresql://user:password@localhost/intelliquiz
   OPENAI_API_KEY=your_openai_api_key
   FRONTEND_URL=https://intelliquizwiki.netlify.app
   ```

5. **Run database migrations:**
   ```bash
   # SQLAlchemy will auto-create tables on first run
   ```

6. **Start development server:**
   ```bash
   uvicorn app.main:app --reload
   ```

   The API will be available at `http://localhost:8000`

7. **Access API documentation:**
   Navigate to `http://localhost:8000/docs` for interactive Swagger UI

## 🌐 Deployment

### Frontend Deployment (Netlify)

1. Connect your GitHub repository to Netlify
2. Configure build settings:
   - **Build command:** `npm run build`
   - **Publish directory:** `build`
   - **Base directory:** `frontend`
3. Add environment variables if needed
4. Deploy!

**Current deployment:** [https://intelliquizwiki.netlify.app/](https://intelliquizwiki.netlify.app/)

### Backend Deployment (Render)

1. Connect your GitHub repository to Render
2. Create a new Web Service
3. Configure settings:
   - **Build command:** `pip install -r requirements.txt`
   - **Start command:** `uvicorn app.main:app --host 0.0.0.0 --port $PORT`
   - **Root directory:** `backend`
4. Add environment variables:
   - `DATABASE_URL` (Render PostgreSQL connection string)
   - `OPENAI_API_KEY`
   - `FRONTEND_URL`
5. Deploy!

**Current deployment:** [https://intelliquiz-api.onrender.com/docs](https://intelliquiz-api.onrender.com/docs)

### Database (PostgreSQL on Render)

1. Create a PostgreSQL database on Render
2. Copy the internal/external database URL
3. Add to backend environment variables as `DATABASE_URL`
4. SQLAlchemy will handle table creation automatically

## 🔧 Configuration

### CORS Configuration

The backend is configured to accept requests from the frontend origin:
```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["https://intelliquizwiki.netlify.app"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

### Database Connection

PostgreSQL connection is managed through SQLAlchemy:
```python
DATABASE_URL = os.getenv("DATABASE_URL")
engine = create_engine(DATABASE_URL)
SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
```

## 📝 Development

### Project Structure Details

#### Backend (`backend/app/`)

- **`main.py`**: FastAPI application, routes, and middleware configuration
- **`models.py`**: SQLAlchemy ORM models for database tables
- **`schemas.py`**: Pydantic models for request/response validation
- **`database.py`**: Database connection and session management
- **`crud.py`**: Database CRUD operations (Create, Read, Update, Delete)

#### Frontend (`frontend/src/`)

- **`App.js`**: Main React component with routing and state management
- **`components/QuizForm.js`**: Form for submitting Wikipedia URLs
- **`components/QuizDisplay.js`**: Display generated quiz questions
- **`components/QuizHistory.js`**: View previously generated quizzes
- **`App.css`**: Global styling and component styles

### API Integration

The frontend communicates with the backend using Axios:

```javascript
import axios from 'axios';

const API_BASE_URL = 'https://intelliquiz-api.onrender.com';

// Generate quiz
const response = await axios.post(`${API_BASE_URL}/generate-quiz/`, {
  url: wikipediaUrl
});

// Get quiz history
const quizzes = await axios.get(`${API_BASE_URL}/quizzes/`);
```

## 🧪 Testing

### Frontend Testing
```bash
cd frontend
npm test
```

### Backend Testing
```bash
cd backend
pytest
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Akhand Pratap Shukla**

- Portfolio: [https://akhandshukla.vercel.app/](https://akhandshukla.vercel.app/)
- LinkedIn: [https://www.linkedin.com/in/akhand-pratap-shukla](https://www.linkedin.com/in/akhand-pratap-shukla)
- GitHub: [https://github.com/A-P-Shukla](https://github.com/A-P-Shukla)

## 🙏 Acknowledgments

- Wikipedia for providing free educational content
- OpenAI for GPT API
- FastAPI for the excellent Python framework
- React team for the powerful frontend library
- Netlify and Render for reliable hosting services

## 📞 Support

For issues, questions, or suggestions:

1. Open an issue in the GitHub repository
2. Contact via LinkedIn
3. Visit the project website

---

**Made with ❤️ by Akhand Pratap Shukla**
