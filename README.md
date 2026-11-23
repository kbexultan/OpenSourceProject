# SAVEAT
Save food. Save money.

SAVEAT is [one sentence: what the app does, e.g. "a platform that helps people buy surplus food at a discount"] for [who uses it: customers, shops, cafes].

## Sustainable Development Goal
SAVEAT supports SDG 12 (Responsible Consumption and Production), target 12.3: reducing food waste. [One or two sentences in your own words: how exactly the app reduces food waste.]

## Platform independence
SAVEAT is built with open technologies: Next.js (web), React Native with Expo (mobile), FastAPI (backend) and PostgreSQL (database). The project can run locally with Docker (see `docker-compose.test.yml`), so it does not depend on one proprietary platform or cloud provider.

## Documentation
- Setup guide: see "How to run the project" below
- User guide: see "How to use SAVEAT" below
- Contributing: [CONTRIBUTING.md](CONTRIBUTING.md)
- Code of Conduct: [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)
- Privacy: [PRIVACY.md](PRIVACY.md)
- License: MIT, see [LICENSE](LICENSE)
- Ownership: [OWNERSHIP.md](OWNERSHIP.md)

## How to use SAVEAT
1. [Step 1, e.g. open the website and create an account]
2. [Step 2, e.g. browse available food offers]
3. [Step 3, e.g. add items to the cart and place an order]
4. [Step 4, e.g. pick up the order]

---

## How to run the project

This section explains what to install, where to put the configuration files and which commands to run.

### 1. Requirements
- Git
- Node.js 20+
- Python 3.13+
- uv

Check the installation:

```bash
git --version
node --version
npm --version
python --version
uv --version
```

### 2. Clone the project

```bash
git clone https://github.com/kbexultan/OpenSourceProject.git
cd OpenSourceProject
```

Project structure:

```
OpenSourceProject/
├── backend/
├── frontend/
├── mobile/
└── README.md
```

### 3. Environment files
Files with private data (database access, JWT secret, backend URL) are not stored in GitHub. Create them from the examples and ask the project maintainer for the real values.

**File 1:** `backend/.env`

```
OpenSourceProject/
└── backend/
    ├── app/
    ├── alembic/
    ├── .env          <- put the file here
    ├── pyproject.toml
    └── uv.lock
```

**File 2:** `frontend/.env.local`

```
OpenSourceProject/
└── frontend/
    ├── app/
    ├── components/
    ├── .env.local    <- put the file here
    ├── package.json
    └── package-lock.json
```

These files may contain access to Supabase/PostgreSQL, the JWT secret, the backend URL and other private settings. Never commit or push them to GitHub. Check that they are ignored:

```bash
git check-ignore -v backend/.env
git check-ignore -v frontend/.env.local
```

### 4. Backend
Install dependencies and apply database migrations:

```bash
cd backend
uv sync
uv run alembic upgrade head
```

Run the backend (from the `backend` folder):

```bash
uv run uvicorn app.main:app --reload --port 8001
```

- Backend: http://127.0.0.1:8001
- API docs (Swagger): http://127.0.0.1:8001/docs
- Database check: http://127.0.0.1:8001/health/database

Keep this terminal open.

### 5. Frontend
Open a second terminal.

```bash
cd frontend
npm install
npm run dev -- -p 3001
```

Open: http://localhost:3001

Keep this terminal open too.

### 6. What should be running
You need two terminals (three with the mobile app).

Terminal 1, backend:

```bash
cd OpenSourceProject/backend
uv run uvicorn app.main:app --reload --port 8001
```

Terminal 2, frontend:

```bash
cd OpenSourceProject/frontend
npm run dev -- -p 3001
```

Terminal 3, mobile (optional):

```bash
cd OpenSourceProject/mobile
npx expo start
```

Addresses:
- Frontend: http://localhost:3001
- Backend: http://127.0.0.1:8001
- Swagger: http://127.0.0.1:8001/docs
- Mobile (Metro): http://localhost:8081

### 7. First run on Windows (PowerShell)

```powershell
git clone https://github.com/kbexultan/OpenSourceProject.git
cd OpenSourceProject
```

Put the environment files in place:

```
.env       -> OpenSourceProject/backend/.env
.env.local -> OpenSourceProject/frontend/.env.local
```

Backend:

```powershell
cd backend
uv sync
uv run alembic upgrade head
uv run uvicorn app.main:app --reload --port 8001
```

Open a second PowerShell window:

```powershell
cd path\to\OpenSourceProject\frontend
npm install
npm run dev -- -p 3001
```

Open: http://localhost:3001

### 8. First run on macOS (Terminal)

```bash
git clone https://github.com/kbexultan/OpenSourceProject.git
cd OpenSourceProject
```

Put the environment files in place:

```
.env       -> OpenSourceProject/backend/.env
.env.local -> OpenSourceProject/frontend/.env.local
```

Backend:

```bash
cd backend
uv sync
uv run alembic upgrade head
uv run uvicorn app.main:app --reload --port 8001
```

Open a second Terminal tab:

```bash
cd /path/to/OpenSourceProject/frontend
npm install
npm run dev -- -p 3001
```

Open: http://localhost:3001

### 9. Installing uv
- Windows: `winget install --id=astral-sh.uv -e` (then restart the terminal)
- macOS (with Homebrew): `brew install uv`

Check: `uv --version`

### 10. If npm does not work
Check `node --version` and `npm --version`. If the commands do not work, install Node.js, then restart VS Code or the terminal.

### 11. Troubleshooting
**Backend does not start.** Make sure you are in `OpenSourceProject/backend`, then run:

```bash
uv sync
uv run uvicorn app.main:app --reload --port 8001
```

**Database connection error.** Check that the environment file is at `OpenSourceProject/backend/.env`, not at `OpenSourceProject/.env`. If the file is in the right place and the database still does not connect, contact the project maintainer. Never send secrets in a public chat or push them to GitHub.

**Frontend cannot reach the backend.** Check that the backend is running at http://127.0.0.1:8001 and that `OpenSourceProject/frontend/.env.local` is inside the `frontend` folder. After changing `.env.local`, stop the frontend with `Ctrl + C` and start it again:

```bash
npm run dev -- -p 3001
```

**Next.js behaves strangely after an update.** Stop the frontend with `Ctrl + C`, delete the `.next` folder and start again.

Windows PowerShell:

```powershell
Remove-Item -Recurse -Force .next
npm run dev -- -p 3001
```

macOS:

```bash
rm -rf .next
npm run dev -- -p 3001
```

### 12. Getting the latest changes
Before you start working:

```bash
git pull origin main
```

If dependencies changed:

```bash
cd backend
uv sync
```

```bash
cd frontend
npm install
```

If there are new migrations:

```bash
cd backend
uv run alembic upgrade head
```

### 13. Sending your changes to GitHub
From the project root (see also [CONTRIBUTING.md](CONTRIBUTING.md)):

```bash
git status
git add .
git status
git commit -m "Describe your changes"
git push origin main
```

Before committing, make sure these are not included:
- `backend/.env`
- `frontend/.env.local`
- `backend/.venv`
- `frontend/node_modules`
- `frontend/.next`

### 14. Quick start
If the project is already cloned, the environment files are in place and dependencies are installed:

Backend:

```bash
cd backend
uv run uvicorn app.main:app --reload --port 8001
```

Frontend (in another terminal):

```bash
cd frontend
npm run dev -- -p 3001
```

Open: http://localhost:3001

### 15. Mobile app (iOS / Android)
The mobile app lives in the `mobile/` folder and is built with React Native + Expo. It is not a separate project: it uses the same backend, database, users and JWT as the website.

```
Next.js web ─┐
             ├─► FastAPI (backend) ─► PostgreSQL / Supabase
React Native ┘
```

Install:

```bash
cd OpenSourceProject/mobile
npm install
```

Run:

```bash
cd OpenSourceProject/mobile
npx expo start
```

Then:
- press `a` for the Android emulator
- press `i` for the iOS simulator (macOS only)
- scan the QR code with the Expo Go app on a real phone

**Backend address for the phone.** Copy the example environment file:

```bash
cd OpenSourceProject/mobile
cp .env.example .env
```

Set the API address in `EXPO_PUBLIC_API_URL`:

| Where you run the app | EXPO_PUBLIC_API_URL |
|---|---|
| iOS simulator on the same computer | `http://127.0.0.1:8001` |
| Android emulator | `http://10.0.2.2:8001` |
| Real phone on the same Wi-Fi | `http://<computer-IP>:8001` |

On a real phone `127.0.0.1` does not work, because it is the phone's own address. Use your computer's IP in the local network (`ipconfig` on Windows, `ifconfig` on macOS), for example `http://192.168.1.50:8001`.

For the phone to reach the backend, start it not only on localhost:

```bash
cd OpenSourceProject/backend
uv run uvicorn app.main:app --reload --host 0.0.0.0 --port 8001
```

More details: `mobile/README.md`.

### 16. Checklist
- [ ] Project cloned with Git
- [ ] `backend/.env` is in place
- [ ] `frontend/.env.local` is in place
- [ ] `uv sync` done
- [ ] `uv run alembic upgrade head` done
- [ ] `npm install` done
- [ ] Backend runs on port 8001
- [ ] Frontend runs on port 3001
- [ ] http://localhost:3001 opens

If you work with the mobile app:
- [ ] `npm install` done in `mobile/`
- [ ] `mobile/.env` created from `mobile/.env.example`
- [ ] `EXPO_PUBLIC_API_URL` points to the backend (for a phone, the computer's IP)
- [ ] Backend started with `--host 0.0.0.0`
- [ ] `npx expo start` works

### 17. Automated tests
Backend tests use an isolated PostgreSQL in Docker and refuse to connect to Supabase or any other non-local database.

```bash
docker compose -f docker-compose.test.yml up -d --wait
cd backend && uv run pytest
cd ../frontend && npm test
cd ../mobile && npm test
docker compose -f docker-compose.test.yml down -v
```

Details, safeguards and manual QA steps: `backend/tests/README.md`.

---

SAVEAT. Save food. Save money.

If you have a problem with database access or secrets, contact the project maintainer.
