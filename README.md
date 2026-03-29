# InternLink 

InternLink is a full-stack internship matching platform connecting students and employers (SMEs).  
It includes a Flask + PostgreSQL backend and a static HTML/CSS/JS frontend.

## Features

- User authentication for `student` and `sme` roles
- Internship posting and management for SMEs
- Internship browsing and application tracking for students
- Student profile and skills management
- Skill-based internship matching
- Dashboard analytics (including a live applications time series for SMEs)

## Tech Stack

- Backend: Python, Flask, psycopg, PostgreSQL
- Frontend: HTML, CSS, Vanilla JavaScript
- Charts: Chart.js

## Project Structure

```text
internlink_sample/
  backend/
    app.py
    requirements.txt
    .env                # create this locally
  frontend/
    index.html
    listing.html
    login.html
    register.html
    dashboard.html
    sme_dashboard.html
    css/
    js/
```

## Prerequisites

- Python 3.10+
- PostgreSQL database
- A terminal (PowerShell, CMD, or Bash)

## Backend Setup

1. Navigate to backend:

   ```bash
   cd backend
   ```

2. (Recommended) Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   .venv\Scripts\activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Create `backend/.env`:

   ```env
   DATABASE_URL=postgresql://<username>:<password>@<host>:<port>/<database_name>
   ```

5. Start the Flask server:

   ```bash
   python app.py
   ```

The backend runs on `http://127.0.0.1:5000` by default.

6. Initialize database schema (first run only):

   Open this URL in your browser:

   ```text
   http://127.0.0.1:5000/init-db
   ```

## Frontend Setup

The frontend is static and expects the backend to run at `http://127.0.0.1:5000`.

From the project root:

```bash
cd frontend
python -m http.server 5500
```

Then open:

- `http://127.0.0.1:5500/index.html`

## Main API Endpoints

- `POST /register` - Register student or SME account
- `POST /login` - Login and receive role/user ID
- `GET|POST|PUT|DELETE /api/internships` - Internship CRUD (soft delete on close)
- `GET|POST|PUT /api/applications` - Apply and manage application status
- `GET|PUT /api/profile` - Student profile updates
- `GET /api/match` - Skill-based internship matching
- `GET /api/sme_metrics/applications_timeseries` - SME live applications chart data

## Notes

- The frontend also fetches external internships from `https://www.arbeitnow.com/api/job-board-api`.
- If you deploy the backend, update `API_BASE_URL` in `frontend/js/script.js`.
- There are `.docx` files in `frontend/` that appear to be documentation artifacts and are not required to run the app.

