# InternLink – Kigali
**A Decoupled Full-Stack Platform for Skill-Based Internship Matching**

InternLink is a professional web application designed to bridge the gap between ambitious university students in Rwanda and innovative Small and Medium Enterprises (SMEs). Moving away from traditional, biased resume screening, InternLink utilizes a proprietary skill-matching engine to connect the right technical talent with the right local opportunities.

---

##  Core Features
* **Role-Based Access Control (RBAC):** Distinct dashboard experiences and authorization flows for Students and Employers (SMEs).
* **Smart Matching Engine:** Algorithmic matching of student skills to job requirements using keyword intersection.
* **Hybrid Job Feed:** Aggregates exclusive local InternLink opportunities with global remote roles via the Arbeitnow API.
* **Live Analytics Dashboard:** Real-time time-series charting (via Chart.js) for SMEs to track application pipelines.
* **Decoupled Architecture:** Independent Frontend (Client) and Backend (API) for scalable deployment and parallel team development.

---

## The Skill-Matching Algorithm (Implementation Details)
At the core of InternLink is our **Keyword Intersection Matching Engine**. To optimize for performance and transparency in our MVP, we implemented a deterministic algorithm that calculates compatibility based on technical requirements.

### The Execution Flow:
1. **Data Normalization:** When a student requests a match, the algorithm fetches their comma-separated skill string from the database (e.g., `React, Python, Django`). It standardizes the data by stripping whitespace and converting the string into a lowercased array: `['react', 'python', 'django']`.
2. **Corpus Generation:** The engine retrieves all active internships. For each job, it concatenates the `title` and `description` into a single, lowercased searchable text corpus.
3. **Intersection Scoring:** The algorithm iterates through the student's normalized skill array. For every skill found as a substring within a job's corpus, the job is awarded `+1` to its `match_score`. 
4. **Filtering & Sorting:** Jobs with a `match_score` of `0` are filtered out. The remaining viable matches are sorted in descending order, ensuring the most technically aligned opportunities appear at the very top of the student's feed.

*Computational Complexity:* The algorithm operates at an efficient $O(N \times M)$ time complexity, where $N$ is the number of active jobs and $M$ is the number of skills in the user's profile.

---

## System Architecture & Tech Stack

### Backend (The REST API)
* **Language:** Python 3.14
* **Framework:** Flask (with Flask-CORS for cross-origin resource sharing)
* **Database Driver:** Psycopg 3 (Modern PostgreSQL adapter)
* **Database:** Aiven Cloud PostgreSQL
* **Security:** Werkzeug password hashing (PBKDF2-SHA256)

### Frontend (The Client)
* **Structure:** HTML5 (Standalone/Decoupled pages)
* **Styling:** CSS3 (Custom CSS Variables, CSS Grid/Flexbox layouts, Dark/Light Theme Tokens)
* **Interactivity:** Vanilla JavaScript (ES6+ `async/await` Fetch API)
* **Data Visualization:** Chart.js

---

##  Team Roles & Development Workflow
This project was built collaboratively. To prevent Git merge conflicts and ensure clear accountability, domains were strictly separated:

| Name | Role | Primary Domain |
| :--- | :--- | :--- |
| **Charles** | **Backend Architect** | API Logic, Database Schema, Matching Engine, Security |
| **Cedric** | **Integration Engineer** | Asynchronous Fetch Logic, State Management |
| **Jesse** | **UI/UX Designer** | Global Styling, Theme Tokens, Responsiveness |
| **Liata** | **UI/UX Designer** | Global Styling, Theme Tokens, Responsiveness |
| **Ayobamidele** | **Student Experience** | Student Dashboard, Job Board Layouts, Profiles |
| **Ayobamidele** | **SME & Auth Lead** | Employer Dashboard, Authentication Flow, Onboarding |

**Git Protocol:** * Always run `git pull origin main` before branching. 
* Commit changes to isolated feature branches (e.g., `feature/login-ui`) before opening pull requests to the main branch.

---

## Local Setup & Installation

To run this project locally, the backend and frontend must be run simultaneously. 

### 1. Database Configuration
Create a `.env` file inside the `/backend` directory. **(Note: Never commit this file to version control).**
```env
DATABASE_URL=your_postgresql_connection_string
