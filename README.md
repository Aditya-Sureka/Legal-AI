# Legal-AI

A full‑stack web application that combines a TypeScript/Next.js frontend with a Python/Flask backend to provide AI-assisted legal features (document analysis, Q&A, newsletter/contact pages, and project info). The repository organizes UI components in TypeScript, a Flask server for AI interactions, and static/public assets for the site.

Maintainer: Aditya-Sureka (they/them)

## Table of contents
- Project overview
- Key features
- Tech stack
- Repository structure
- Getting started (developer)
  - Prerequisites
  - Frontend (developer)
  - Backend (developer)
  - Docker
- Environment variables
- Development workflow & scripts
- Testing & linting
- Deployment notes
- Contributing
- License
- Contact

## Project overview
Legal-AI is designed to provide legal assistance via an interactive web UI and an API-backed AI service. The frontend uses TypeScript/React components to assemble pages and UX elements (navbar, footer, contact/newsletter components, project/skills sections). The Flask backend handles AI requests, integrations, and any server-side logic.

## Key features
- Interactive frontend built in TypeScript/React (components under components/)
- Flask-based backend (flask_server/) to handle AI requests and integrations
- Newsletter and contact form components
- Project/skills listing pages and reusable UI components
- Dockerfile present for containerized builds

## Tech stack
- Frontend: TypeScript, React, Next.js (TSX components, CSS modules)
- Backend: Python, Flask
- Styling: CSS / CSS modules
- Containerization: Docker (Dockerfile present)
- AI/third-party integrations: environment-driven (API keys and endpoints)

## Repository structure (top-level)
- components/ — React/TSX UI components (navbar, header, footer, contact, newsletter, projects, skills, etc.)
- pages/ — Next.js pages (site routes)
- public/ — static assets
- styles/ — global and component styles
- flask_server/ — Python Flask backend and server-side code
- README.md — this file

(Inspect the repository for additional files such as package.json, requirements.txt, Dockerfile, and any config files to confirm exact scripts and entrypoints.)

## Getting started (developer)

### Prerequisites
- Node.js (v16+ recommended; check package.json engines)
- npm or pnpm or yarn
- Python 3.8+ and virtualenv (for the Flask backend)
- Docker (optional, for containerized runs)

### Frontend — quick start
1. At repository root (the Next.js app likely lives at the repo root along with components/ and pages/):
   - Install dependencies:
     - npm install
     - or pnpm install
   - Start dev server:
     - npm run dev
   - Build for production:
     - npm run build
   - Start production server:
     - npm run start
2. Notes:
   - Confirm the exact script names in package.json (dev, build, start, lint, test).
   - If using environment variables for the frontend, they should be prefixed with NEXT_PUBLIC_ to be exposed to the browser.

### Backend (Flask) — quick start
1. Change into the backend directory:
   - cd flask_server
2. Create and activate virtual environment:
   - python -m venv .venv
   - source .venv/bin/activate (macOS/Linux) or .venv\Scripts\activate (Windows)
3. Install dependencies:
   - pip install -r requirements.txt
4. Run the app:
   - If there is an app entrypoint (e.g., app.py or run.py): python app.py
   - Or use Flask CLI:
     - export FLASK_APP=app.py
     - flask run --host=0.0.0.0 --port=5000
5. Notes:
   - Inspect flask_server/ to confirm the main module name and any available run scripts.
   - Backend will likely require API keys (see Environment variables).

### Docker
1. Build:
   - docker build -t legal-ai .
2. Run:
   - docker run -p 3000:3000 -p 5000:5000 --env-file .env -it legal-ai
3. If repository uses docker-compose, prefer docker-compose up --build to wire frontend and backend together.

## Environment variables
Create a .env (and .env.example) with the variables required by both frontend and backend. Example variables to include (adjust to actual keys used in code):
- OPENAI_API_KEY=your_openai_key_here
- NEXT_PUBLIC_API_BASE_URL=http://localhost:5000    # frontend → backend
- FLASK_ENV=development
- FLASK_APP=app.py
- PORT=3000
- MAILCHIMP_API_KEY=your_mailchimp_key_here (if newsletter uses Mailchimp)
- Any other keys referenced in config files or code (search for os.environ or process.env in the repo)

Always keep secret keys out of source control.

## Development workflow & scripts
- Use the frontend dev server for hot reload (npm run dev).
- Use the Flask dev server or a WSGI runner (gunicorn) for backend development.
- Use environment-specific .env files or local overrides for testing integrations.

Check package.json for scripts (lint, format, test) and run them before creating pull requests.

## Testing & linting
- Frontend: run npm test or the configured test script (Jest/React Testing Library likely).
- Backend: run pytest or python -m pytest if tests are present.
- Linting/formatting: run eslint / prettier if configured.

If test and lint scripts are not present, add them according to project standards.

## Deployment notes
- Frontend (Next.js) can be deployed to Vercel, Netlify, or any Node host.
- Backend (Flask) can be deployed to any Python host, containerized with Docker, or served behind gunicorn + nginx.
- Use CI/CD pipelines (GitHub Actions, etc.) to build and test on push/PRs.
- Store secrets in your cloud provider/hosting environment or GitHub Secrets.

## Contributing
- Fork the repo (or create branches directly if you have push access).
- Create a descriptive branch name: feat/<short-desc>, fix/<short-desc>, chore/<short-desc>
- Run linters and tests locally before submitting PRs.
- Provide a clear PR description and link to any related issues.
- Keep commits atomic and write clear commit messages.

## License
- Add a LICENSE file if none exists. A common default is the MIT license. Check the repository to confirm which license, or add one if you want the project licensed.

## Contact
- Maintainer: Aditya-Sureka (they/them)
- For support or questions, open an issue or contact via the project’s contact form.
