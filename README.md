# CogniSphere — Government Scheme Assistant (MVP)

CogniSphere is a hackathon MVP prototype for discovering a small catalogue of Indian government schemes, checking preliminary eligibility against demo rules, generating document checklists, and tracking next steps locally.

> **Important:** Scheme records and eligibility rules in this repository are illustrative demo data, not an authoritative or live government database. Always verify scheme details, eligibility, dates, documents, and application links on the relevant official portal. This prototype does not submit applications or connect to government application-status systems. Use fictional data when demonstrating it; do not enter Aadhaar numbers, OTPs, passwords, bank details, or private documents.

## MVP features

- Search and browse a small demo catalogue of schemes and scholarships.
- Enter a basic profile and see rule-based preliminary matches with explanations.
- View an illustrative document checklist for a selected scheme.
- Add a scheme to a local application tracker and update its demo status.
- Ask the assistant for general guidance. Gemini integration is optional; without an API key, a built-in local fallback responds.

## Technology

- **Frontend:** React 18, Vite, Lucide React
- **Backend:** Python, FastAPI, Pydantic
- **Local persistence:** SQLite
- **Optional AI:** Google Gemini via `GEMINI_API_KEY`

## Project structure

```text
cognisphere_mvp/
├── .gitignore
├── README.md
├── backend/
│   ├── .env.example
│   ├── requirements.txt
│   └── app/
│       ├── __init__.py
│       ├── data.py
│       └── main.py
└── frontend/
    ├── index.html
    ├── package.json
    ├── vite.config.js
    └── src/
        ├── App.jsx
        ├── main.jsx
        └── styles.css
```

## Run locally

You need **Python 3.10+** and **Node.js 18+** (with npm).

### 1. Start the backend

Open a terminal:

```bash
cd backend
python -m venv .venv
```

Activate the environment:

```bash
# Windows PowerShell
.venv\\Scripts\\Activate.ps1

# macOS / Linux
source .venv/bin/activate
```

Install dependencies and start FastAPI:

```bash
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```

Backend health check: http://localhost:8000/api/health  
Interactive API documentation: http://localhost:8000/docs

### 2. Start the frontend

Open a **second terminal** from the project root:

```bash
cd frontend
npm install
npm run dev
```

Open the local URL shown by Vite (usually http://localhost:5173).

The frontend uses `http://localhost:8000` as its default backend URL. If your backend runs elsewhere, create `frontend/.env` with:

```env
VITE_API_URL=http://localhost:8000
```

Restart the Vite development server after changing the environment file.

## Optional Gemini assistant setup

The application works without Gemini using its local fallback assistant.

To enable Gemini:
1. Copy `backend/.env.example` to `backend/.env`.
2. Add your own key:

```env
GEMINI_API_KEY=your_api_key_here
GEMINI_MODEL=gemini-2.0-flash
```

3. Restart the backend.

**Never commit `.env` or publish API keys.** The `.gitignore` excludes `.env` files.

## Suggested demo flow (2–3 minutes)

1. Open Discover and search for `scholarship`.
2. Open Eligibility and use fictional sample values (for example: age 19, Karnataka, annual family income ₹150,000, student).
3. Show the preliminary matches and their explanations.
4. Open a scheme and show its suggested document checklist.
5. Add the scheme to the tracker and update its local demo status.
6. Ask the assistant: “What should I prepare before applying?”

## GitHub submission

1. Extract this ZIP file.
2. On GitHub, create a new repository (for example, `cognisphere-government-assistant`).
3. Upload the **contents of the `cognisphere_mvp` folder** to the repository, or use Git:

```bash
cd cognisphere_mvp
git init
git add .
git commit -m "Add CogniSphere government scheme assistant MVP"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/cognisphere-government-assistant.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your GitHub username. Do not upload `.env`, virtual environments, `node_modules`, build output, or local database files.

## Current prototype limitations

- The scheme catalogue is small and illustrative; it is not synchronized with government portals.
- Eligibility is a simple rule-based demonstration, not an official eligibility decision.
- Checklists are suggestions and must be verified against official requirements.
- Tracker entries are stored locally in SQLite on the machine running the backend.
- The assistant does not submit applications or retrieve live application status.
- Production deployment, authentication, and multi-user data security are not included.

## Possible next steps

- Verify and maintain scheme records with official source links and last-checked dates.
- Expand supported schemes and clearly document each eligibility rule.
- Add tests for API endpoints and eligibility edge cases.
- Add authentication and secure, consent-based document handling if required.
- Deploy frontend and backend with appropriate production security and database hosting.

---
**Hackathon note:** This repository is intended as a basic MVP/prototype demonstrating the core idea. It is not represented as a complete or production-ready product.
