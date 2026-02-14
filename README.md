# CivicClear AI

Enterprise-grade AI platform for analyzing government circulars, community announcements, and social media communications to improve clarity, detect ambiguity, and generate citizen-friendly explanations.

## Features

- **AI-Powered Analysis**: Uses Mistral AI via Ollama to analyze communication clarity
- **Clarity Scoring**: 0-100 score with detailed breakdown
- **Risk Assessment**: Identifies interpretation risks (Low/Medium/High)
- **Citizen-Friendly Output**: Automatically generates simplified explanations
- **Professional Dashboard**: Enterprise SaaS interface with analytics
- **Export Reports**: JSON export for further processing
- **On-Premise Ready**: Self-hosted with open-source LLMs

## Tech Stack

### Frontend
- React + Vite
- Tailwind CSS
- React Router
- Lucide Icons

### Backend
- Python FastAPI
- Uvicorn server
- Ollama integration (Mistral model)
- Pydantic validation
- CORS enabled

## Project Structure

```
/
├── src/                          # Frontend React application
│   ├── components/               # Reusable components
│   │   ├── Sidebar.jsx
│   │   ├── Navbar.jsx
│   │   ├── ScoreCard.jsx
│   │   ├── RiskBadge.jsx
│   │   ├── CitizenCard.jsx
│   │   └── LoadingSpinner.jsx
│   ├── pages/                    # Page components
│   │   ├── Dashboard.jsx
│   │   ├── Analyze.jsx
│   │   ├── CitizenView.jsx
│   │   ├── Reports.jsx
│   │   ├── Settings.jsx
│   │   └── About.jsx
│   ├── services/                 # API services
│   │   └── api.js
│   ├── utils/                    # Utility functions
│   │   └── helpers.js
│   ├── App.jsx
│   ├── main.jsx
│   └── index.css
├── backend/                      # Python FastAPI backend
│   ├── main.py
│   ├── requirements.txt
│   ├── .env.example
│   ├── routes/
│   │   └── analyze.py
│   ├── services/
│   │   ├── ai_engine.py
│   │   └── scoring.py
│   └── models/
│       ├── request_model.py
│       └── response_model.py
└── dist/                         # Production build
```

## Quick Start

### Prerequisites

- Node.js 18+
- Python 3.9+
- Ollama installed locally

### 1. Install Ollama and Pull Mistral

```bash
# Install Ollama (macOS/Linux)
curl -fsSL https://ollama.com/install.sh | sh

# Pull Mistral model
ollama pull mistral
```

### 2. Start the Backend

```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Copy environment file
cp .env.example .env

# Start the server
python main.py
```

The backend will start on `http://localhost:8000`

### 3. Start the Frontend

```bash
# In a new terminal, from the project root

# Install dependencies
npm install

# Copy environment file
cp .env.example .env

# Start development server
npm run dev
```

The frontend will start on `http://localhost:5173`

## API Endpoints

### POST /api/analyze

Analyze communication text for clarity issues.

**Request:**
```json
{
  "text": "string (10-10000 chars)",
  "type": "circular | announcement | social"
}
```

**Response:**
```json
{
  "clarity_score": 42,
  "ambiguity_level": "High",
  "interpretation_risk": "High",
  "confidence_index": 38,
  "confusing_phrases": ["phrase1", "phrase2"],
  "missing_context": ["context1", "context2"],
  "citizen_version": {
    "who_is_affected": "...",
    "what_is_required": "...",
    "deadlines": "...",
    "important_notes": "...",
    "simple_explanation": "..."
  }
}
```

### GET /api/health

Health check endpoint.

### GET /api/stats

Get dashboard statistics.

### GET /api/reports

Get analysis history.

## Environment Variables

### Frontend (.env)

```
VITE_API_URL=http://localhost:8000/api
VITE_ENVIRONMENT=development
```

### Backend (.env)

```
PORT=8000
HOST=0.0.0.0
OLLAMA_MODEL=mistral
OLLAMA_TIMEOUT=120
ALLOWED_ORIGINS=http://localhost:5173,http://localhost:3000
ENVIRONMENT=development
```

## Deployment

### Frontend Build

```bash
npm run build
```

Output will be in `dist/` directory.

### Backend Deployment

```bash
cd backend
pip install -r requirements.txt
uvicorn main:app --host 0.0.0.0 --port 8000
```

## Docker Deployment (Optional)

Create a `docker-compose.yml`:

```yaml
version: '3.8'

services:
  backend:
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - OLLAMA_MODEL=mistral
    depends_on:
      - ollama

  frontend:
    build: .
    ports:
      - "80:80"
    depends_on:
      - backend

  ollama:
    image: ollama/ollama
    volumes:
      - ollama_data:/root/.ollama

volumes:
  ollama_data:
```

## License

Enterprise License - CivicClear AI

## Support

For support and inquiries, contact: support@civicclear.ai
