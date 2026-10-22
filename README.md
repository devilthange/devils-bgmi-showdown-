# DEVIL'S BGMI SHOWDOWN — Tournament Registration Website

A starter project for a public squad-registration page and a private admin dashboard.

## Stack
- Frontend: React + Vite
- API: FastAPI
- Database: MongoDB
- Admin authentication: JWT
- Registration: one captain + three teammates; required IDs and IGN fields
- Admin actions: edit tournament details, approve/reject registrations, close registrations, export CSV

## Important
This project is source code, not a published live website. To get a shareable public URL, deploy the frontend and API and configure MongoDB. Do not share the admin password or JWT secret.

## 1. Run the API
Requirements: Python 3.10+

```bash
cd backend
python -m venv .venv
# Windows: .venv\Scripts\activate
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

Edit `backend/.env`:
- `MONGODB_URL`: your MongoDB connection string
- `MONGODB_DB`: database name
- `ADMIN_USERNAME`: admin login username
- `ADMIN_PASSWORD`: use a strong unique password
- `JWT_SECRET`: replace with a long random secret
- `CORS_ORIGINS`: frontend URL(s), comma-separated

Then run:
```bash
uvicorn app.main:app --reload
```
API docs: http://127.0.0.1:8000/docs

## 2. Run the frontend
Requirements: Node.js 18+

```bash
cd frontend
npm install
cp .env.example .env
```
Set `VITE_API_URL` to the API base URL (local default: `http://127.0.0.1:8000`), then:
```bash
npm run dev
```

## 3. Default tournament
The API creates a default tournament record if none exists:
- DEVIL'S BGMI SHOWDOWN
- 25 October 2026
- 8:00 PM IST
- Prize pool ₹500
- Maps: Erangel, Miramar, Rondo
- 3 matches
- 16 squads maximum

Edit these details from the admin dashboard after signing in.

## 4. Publish it
A typical setup is:
- Frontend: a static frontend host (e.g. Vercel or Netlify)
- Backend: a Python ASGI host (e.g. Render or Railway)
- Database: MongoDB Atlas

Set the frontend's `VITE_API_URL` to the deployed API URL. Set backend `CORS_ORIGINS` to the deployed frontend URL. Configure the environment variables on the hosting services. Then share the frontend URL in WhatsApp.

## Security / practical notes
- Change all secrets before deployment.
- Use HTTPS in production.
- Admin passwords are compared against an environment variable in this starter; use a unique strong password and restrict access to the admin panel.
- Public registrations are pending until approved.
- Avoid collecting phone numbers or other personal details unless you need them.
- This starter does not provide automatic BGMI ID verification or guarantee that the player will participate; approval is manual.
