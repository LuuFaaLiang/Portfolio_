# Lianghok — Personal Portfolio Website

A modern, animated personal portfolio for Lianghok, a first-year Information Technology
student at the National University of Management (NUM), Cambodia. Built as a Flask
backend serving a single-page, responsive, dark-mode-aware frontend.

## Features

- **Hero** with typing effect (Typed.js), floating gradient blobs, and glassmorphism nav
- **About** section with an animated timeline and stat counters
- **Skills** with animated progress bars and a tool grid
- **Projects** with live search, technology filtering, and tech badges
- **Education** timeline
- **Certificates** gallery with category filters
- **Experience** cards (volunteer work, personal projects, hackathon goals, open source)
- **Contact form** with client-side + server-side (regex) validation, stored in SQLite
- **Resume page** with embedded PDF preview, download and print buttons
- Dark/light mode toggle with saved preference (`localStorage`)
- Scroll progress bar, scroll-spy navigation, back-to-top button
- Fully responsive: desktop, tablet, and mobile
- Custom 404 / 405 error pages
- Basic SEO: meta tags, Open Graph tags, `robots.txt`, `sitemap.xml`
- Accessible: keyboard-navigable, ARIA labels on icon buttons, `prefers-reduced-motion` support

## Tech stack

**Frontend:** HTML5, Tailwind CSS (CDN), vanilla JavaScript, AOS scroll animations,
Typed.js, Font Awesome icons.

**Backend:** Python, Flask, Flask Blueprints, Flask-Mail (optional email notifications),
SQLite, regex-based form validation, Python `logging`.

## Folder structure

```
portfolio-website/
├── app.py                 # App factory, DB init, blueprint registration, error handlers
├── config.py               # Configuration (secret key, mail, paths)
├── requirements.txt
├── README.md
│
├── database/
│   └── portfolio.db        # Created automatically on first run
│
├── routes/
│   ├── home.py              # Home page, resume page, CV download
│   ├── contact.py           # Contact form endpoint + validation + SQLite insert
│   └── api.py               # /api/stats, /api/messages (admin JSON)
│
├── templates/
│   ├── base.html            # Layout, nav, footer, CDN includes
│   ├── index.html           # All portfolio sections
│   ├── resume.html
│   ├── 404.html
│   └── 405.html
│
├── static/
│   ├── css/style.css
│   ├── js/main.js
│   ├── robots.txt
│   └── sitemap.xml
│
├── uploads/
│   └── resume.pdf           # Replace with your real CV
│
└── utils/
    └── validation.py        # Name / email / subject / message / phone regex validators
```

## Requirements

- Python 3.10+
- pip

## Run locally

```bash
# 1. Clone or unzip the project, then move into it
cd portfolio-website

# 2. Create and activate a virtual environment
python3 -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. (Optional) enable email notifications for contact form messages
export MAIL_USERNAME="you@gmail.com"
export MAIL_PASSWORD="your-app-password"

# 5. Run the app
python app.py
```

Visit **http://127.0.0.1:5000** in your browser. The SQLite database and the `uploads`
folder are created automatically if they don't exist.

Replace `uploads/resume.pdf` with your real CV, and update the placeholder GitHub/demo
links and social links in `templates/index.html` and `templates/base.html`.

## Deploy to GitHub

```bash
git init
git add .
git commit -m "Initial commit: portfolio website"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

## Deploy to Render

1. Push the project to GitHub (see above).
2. On [Render](https://render.com), create a **New Web Service** and connect the repo.
3. Set:
   - **Build command:** `pip install -r requirements.txt`
   - **Start command:** `gunicorn app:app` (add `gunicorn` to `requirements.txt` first)
4. Add `MAIL_USERNAME` / `MAIL_PASSWORD` as environment variables if you want email
   notifications for contact form submissions.
5. Deploy — Render will give you a live URL.

## Admin: viewing contact messages

Stored messages can be inspected via the JSON API while the app is running:

- `GET /api/messages` — list all messages, newest first
- `DELETE /api/messages/<id>` — delete a message
- `GET /api/stats` — total message count

(These are intentionally left unauthenticated for local/demo use — add login
protection before exposing them publicly.)

## Notes & next steps

This build focuses on a clean, working core. Natural extensions if you want to keep
going: a live GitHub contributions graph via the GitHub API, a password-protected
admin dashboard for messages, Khmer-language toggle, and a proper image gallery once
real project screenshots are available.
