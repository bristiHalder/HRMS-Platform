[![HRMS Thumbnail](https://github.com/user-attachments/assets/a141c947-aa8b-49b4-8fab-9e7ca04b8bc5)](https://www.youtube.com/watch?v=wycxYTBBwnc)

# AI-Powered HRMS - Recruitment Intelligence Module

An intelligent HR Management System with AI-powered resume parsing, candidate matching, and conversational screening capabilities.

## 📋 Overview

This project is a modern HRMS platform built for the future of recruitment. It uses cutting-edge AI technology to:

- **Parse resumes** and extract structured candidate data
- **Scrape digital footprints** from GitHub, LinkedIn, and portfolios
- **Match candidates** against job descriptions with intelligent scoring
- **Screen candidates** through conversational AI (text/voice)
- **Provide insights** to recruiters through an intuitive dashboard

## Architecture

The project follows a microservices architecture:

- **Frontend**: Next.js 14 (React) with TailwindCSS and Shadcn UI
- **Backend**: FastAPI (Python) for AI services
- **Database**: Supabase (PostgreSQL + Auth + Storage)
- **AI Engine**: Google Gemini — `gemini-2.5-flash` for text, Gemini Live for voice interviews

## Project Structure

```
HRMS-Platform/
├── frontend/           # Next.js application
│   ├── app/           # App router pages
│   ├── components/    # Reusable UI components
│   └── lib/          # Utilities and API clients
│
├── backend/           # FastAPI microservice
│   └── app/
│       ├── api/      # API endpoints
│       ├── services/ # Business logic and AI
│       ├── models/   # Data models
│       └── core/     # Configuration
│
├── supabase/         # Database migrations
└── .github/          # CI/CD workflows
```

## Getting Started

### Prerequisites

- Node.js 18+ and npm/yarn
- Python 3.11+
- Git
- Supabase account
- Google Gemini API key (from Google AI Studio) — used for both text and voice

### Environment Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/bristiHalder/HRMS-Platform.git
   cd HRMS-Platform
   ```

2. **Copy environment variables**
   ```bash
   cp frontend/env.example frontend/.env.local
   cp backend/env.example backend/.env
   ```

3. **Configure the env files**
   - Add your Supabase credentials
   - Add your `GEMINI_API_KEY` (powers resume parsing, matching, screening, and voice interviews)
   - Set a random `SECRET_KEY` in `backend/.env` (e.g. `openssl rand -hex 32`)
   - Update other configuration as needed

### Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

The frontend will be available at `http://localhost:3000`

### Backend Setup

```bash
cd backend
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```

The API will be available at `http://localhost:8000`

### Database Setup

1. Create a new Supabase project
2. Run migrations from `supabase/migrations/`
3. Configure Row Level Security policies

## Testing

### Frontend Tests
```bash
cd frontend
npm test
```

### Backend Tests
```bash
cd backend
pytest
```

## Deployment

Deploy the backend first so its URL can be given to the frontend.

### Backend (Render or Railway)
- Connect the GitHub repository and set **Root Directory** to `backend`
- **Render**: Build command `pip install -r requirements.txt`, Start command `uvicorn app.main:app --host 0.0.0.0 --port $PORT`
- **Railway**: picks up `backend/railway.toml` / `backend/nixpacks.toml` automatically
- Environment variables (see `backend/env.example`). Required: `SUPABASE_URL`, `SUPABASE_KEY` (service role key), `DATABASE_URL`, `GEMINI_API_KEY`, `SECRET_KEY`. Set `ENVIRONMENT=production`, `API_RELOAD=False`, and add your frontend URL to `CORS_ORIGINS` (any `*.vercel.app` domain is already allowed)

### Frontend (Vercel)
- Import the GitHub repository and set **Root Directory** to `frontend` (framework: Next.js)
- Environment variables (see `frontend/env.example`): `NEXT_PUBLIC_SUPABASE_URL`, `NEXT_PUBLIC_SUPABASE_ANON_KEY`, `NEXT_PUBLIC_API_URL` (the deployed backend URL)
- Deploys automatically on push to `main`

### Database (Supabase)
- Create a Supabase project and run these files from `supabase/migrations/` in the SQL Editor, in order: `001_init.sql`, `002_rls.sql`, `003_employee_portal.sql`, `003_voice_interviews.sql` (`combined_migration.sql` only covers 001 + 002)

## Key Features

### For Candidates
- Upload resume (PDF/DOC)
- Apply to job openings
- Participate in AI screening interviews

### For Recruiters
- Post job descriptions
- View ranked candidates with AI scores
- Review candidate digital footprints
- Conduct conversational AI screenings
- Access detailed evaluation reports

### For Admins
- View system-wide statistics
- Monitor recruitment metrics
- Manage users and roles

## Tech Stack

- **Frontend**: Next.js 14, React 18, TypeScript, TailwindCSS, Shadcn UI
- **Backend**: FastAPI, Python 3.11, Pydantic
- **Database**: Supabase (PostgreSQL)
- **Auth**: Supabase Auth with RBAC
- **Storage**: Supabase Storage
- **AI**: Google Gemini (`google-genai` SDK) — `gemini-2.5-flash` text + Gemini Live audio
- **Testing**: PyTest, Jest
- **CI/CD**: GitHub Actions
- **Hosting**: Vercel (Frontend), Render (Backend)

## 📊 API Documentation

Once the backend is running, visit:
- Swagger UI: `http://localhost:8000/docs`
- ReDoc: `http://localhost:8000/redoc`

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is part of a hackathon submission.

## Future Roadmap

- [ ] Add payroll management module
- [ ] Integrate attendance tracking
- [ ] Implement performance management
- [ ] Add multi-language support
- [ ] Enterprise integrations (ERP, ATS)
- [ ] Advanced analytics dashboard
- [ ] Calendar integration for interview scheduling
- [ ] Attrition prediction models

## Support

For support and queries, please open an issue in the repository.

---

Built with ❤️ for the Future of Work Challenge Hackathon

