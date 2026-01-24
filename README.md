# CureWise AI Medical Healthcare

CureWise AI Medical Healthcare is a full-stack healthcare platform that combines hospital management workflows with AI-assisted medical features. The project includes a React frontend, a FastAPI backend, PostgreSQL for application data, and multiple AI integrations for medical Q&A, report parsing, and image-based disease analysis.

## Table of Contents

- [Overview](#overview)
- [Core Features](#core-features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Environment Variables](#environment-variables)
- [Getting Started](#getting-started)
- [Running with Docker](#running-with-docker)
- [Available Scripts](#available-scripts)
- [Backend API Areas](#backend-api-areas)
- [Current Notes](#current-notes)
- [License](#license)

## Overview

This repository contains a healthcare application focused on:

- patient and provider authentication
- hospital, admin, doctor, and department management
- appointment booking and scheduling flows
- medical history and profile management
- AI-powered medical query handling
- disease detection from medical images
- emergency hospital lookup and healthcare analytics

The frontend lives in `frontend/` and the backend lives in `backend/`.

## Core Features

- Authentication for users and healthcare roles
- Hospital and department management for admins
- Doctor management, time slots, and appointment views
- Appointment booking for patients
- Medical history and user profile APIs
- AI medical query endpoints
- General-purpose chatbot support
- Emergency hospital lookup endpoint
- Image classification flows for:
  - kidney disease
  - breast cancer
  - lymphoma
  - pneumonia
  - eye disease
- Follow-up chat endpoints for disease-specific guidance
- Docker-based local development setup

## Tech Stack

### Frontend

Frontend dependencies are declared in [frontend/package.json](frontend/package.json).

- React 19
- React Router DOM 7
- Tailwind CSS
- Framer Motion
- Axios
- Recharts
- React Icons

### Backend

Backend dependencies are declared in [backend/requirements.txt](backend/requirements.txt).

- FastAPI
- Python 3.9+
- Pydantic
- psycopg2
- python-jose
- passlib

### AI and Data

- LangChain
- Google Generative AI
- Groq
- OpenAI SDK
- Pinecone
- Llama Cloud / LlamaParse
- TensorFlow

### Infrastructure

- PostgreSQL 16
- Docker
- Docker Compose

## Project Structure

```text
CureWise-AI-Medical-Healthcare/
├── backend/
│   ├── config/              # Environment-backed settings
│   ├── models/              # Pydantic schemas
│   ├── notebooks/           # Research and experimentation notebooks
│   ├── routes/              # FastAPI route modules
│   ├── utils/               # Database, AI, parser, email, and helper logic
│   ├── main.py              # FastAPI application entry point
│   ├── requirements.txt     # Backend dependencies
│   └── Dockerfile           # Backend container config
├── frontend/
│   ├── public/              # Static assets
│   ├── src/
│   │   ├── components/      # Shared UI and layout components
│   │   ├── context/         # React context providers
│   │   ├── data/            # Static UI data
│   │   ├── pages/           # Route-level screens
│   │   └── utils/           # API and auth helpers
│   ├── package.json         # Frontend dependencies and scripts
│   ├── tailwind.config.js   # Tailwind configuration
│   └── Dockerfile           # Frontend container config
├── docker-compose.yml       # Multi-service local environment
├── AGENTS.md                # Project guidance for coding agents
└── README.md                # Project documentation
```

## Environment Variables

The backend reads configuration from `backend/.env` through `python-dotenv`, and the application settings are loaded in [backend/config/settings.py](backend/config/settings.py).

```env
JWT_SECRET=
JWT_ALGORITHM=
ACCESS_TOKEN_EXPIRE_MINUTES=60

DB_NAME=
DB_USER=
DB_PASSWORD=
DB_HOST=
DB_PORT=

GOOGLE_API_KEY=
GROQ_API_KEY=
OPENAI_API_KEY=
PINECONE_API_KEY=

EMAIL_SENDER=
EMAIL_PASSWORD=
SMTP_SERVER=
SMTP_PORT=

LOCAL_LLM=false

KIDNEY_MODEL_PATH=
BREAST_CANCER_MODEL_PATH=
LYMPHOMA_MODEL_PATH=
PNEUMONIA_MODEL_PATH=
EYE_DISEASE_MODEL_PATH=
```

The frontend currently uses `http://localhost:8000` as the API base URL in [frontend/src/utils/api.js](frontend/src/utils/api.js).

## Getting Started

### Prerequisites

- Python 3.9 or newer
- Node.js and npm
- PostgreSQL
- API keys for the AI services you plan to use

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd CureWise-AI-Medical-Healthcare
```

### 2. Set up the backend

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Create or update `backend/.env` with your database credentials, JWT settings, model paths, and AI API keys.

Start the backend server:

```bash
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

The backend entry point is [backend/main.py](backend/main.py).

### 3. Set up the frontend

Open a new terminal:

```bash
cd frontend
npm install
npm start
```

The frontend scripts are defined in [frontend/package.json](frontend/package.json). The frontend runs on `http://localhost:3000` and the backend runs on `http://localhost:8000`.

## Running with Docker

You can run the full stack with Docker Compose:

```bash
docker-compose up --build
```

Container services are defined in [docker-compose.yml](docker-compose.yml):

- `frontend` on port `3000`
- `backend` on port `8000`
- `postgres` on port `5432`

To stop the containers:

```bash
docker-compose down
```

## Available Scripts

### Frontend

Run these from `frontend/` using the scripts in [frontend/package.json](frontend/package.json):

```bash
npm start
npm run build
npm test
```

### Backend

Run these from `backend/` based on the app entry point in [backend/main.py](backend/main.py):

```bash
python -m uvicorn main:app --reload --host 0.0.0.0 --port 8000
python -m pytest
```

## Backend API Areas

The FastAPI app is assembled from [backend/main.py](backend/main.py) and route modules under [backend/routes](backend/routes).

- `/api/auth/*` for signup and login
- hospital and admin management endpoints
- doctor management and scheduling endpoints
- appointment booking and appointment history
- user profile and medical history endpoints
- `/api/medical-query` and `/api/general-query`
- disease image classification endpoints
- disease-specific chat endpoints
- emergency hospital lookup
- health analytics endpoints

## License

This repository includes an MIT [LICENSE](LICENSE).
