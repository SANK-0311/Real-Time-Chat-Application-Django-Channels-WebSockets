

# Real-Time Chat Application (Django Channels, WebSockets)

A real-time chat application built with **Django**, **Django Channels**, and **WebSockets** for instant, bidirectional messaging. Users can authenticate, join rooms, and exchange messages live without page reloads. The project is structured for easy local development and ready to deploy with an ASGI server.

---

## ✨ Features
- User registration & authentication (login/logout)
- Public or named **chat rooms**
- **Real-time** message broadcasting via WebSockets
- Persistent message history (database)
- Clean, responsive templates
- Production-ready ASGI entrypoint (Daphne/Uvicorn)

---

## 🧰 Tech Stack
- **Python / Django 5.x**
- **Django Channels** (ASGI)
- **WebSockets**
- **Redis** as the Channels layer backend

---

## ✅ Prerequisites
- Python 3.10+ (3.12 recommended)
- Redis server (local or cloud)

---

## 🚀 Quick Start

```bash
# 1) Clone
git clone https://github.com/< SANK-0311 >/<Real-Time-Chat-Application-Django-Channels-WebSockets- >.git
cd <Real-Time-Chat-Application-Django-Channels-WebSockets- >

# 2) Create & activate a virtual env
python -m venv env
source env/bin/activate    # macOS/Linux
# env\Scripts\activate    # Windows PowerShell

# 3) Install dependencies
pip install -r requirements.txt

# 4) Migrate & create a superuser (optional)
python manage.py migrate
python manage.py createsuperuser

# 5) Start Redis (ensure it's running)
# macOS (Homebrew):
#   brew install redis
#   redis-server
# Linux:
#   sudo service redis-server start

# 6) Run the dev server (supports ASGI with Channels)
python manage.py runserver

# Alternative: run with Daphne (production-style)
# daphne -b 0.0.0.0 -p 8000 djangochat.asgi:application
```

Open the app at **http://127.0.0.1:8000/**.

---

## 🔧 Configuration
Create a `.env` file (or set environment variables) and configure your settings to read these values:

```
DEBUG=True
SECRET_KEY=change-me
ALLOWED_HOSTS=127.0.0.1,localhost
REDIS_URL=redis://127.0.0.1:6379/1
```

**Channel Layer (example)** in `settings.py`:
```python
# settings.py (example)
import os
REDIS_URL = os.getenv("REDIS_URL", "redis://127.0.0.1:6379/1")

CHANNEL_LAYERS = {
    "default": {
        "BACKEND": "channels_redis.core.RedisChannelLayer",
        "CONFIG": {"hosts": [REDIS_URL]},
    }
}
```

---

## 🗺️ Project Structure (example)
```
djangochat/
├─ djangochat/           # Project (settings, asgi.py, urls.py)
├─ chat/                 # Chat app (consumers, routing, views, models)
├─ templates/            # HTML templates
├─ static/               # Static files (CSS/JS)
├─ manage.py
└─ README.md
```

> Your actual app names may differ; update this section to match your structure if needed.

---

## 🔌 Endpoints (typical)
- HTTP pages: `/`, `/login/`, `/logout/`, `/signup/`, `/rooms/<room_name>/`
- WebSocket: `ws://<host>/ws/chat/<room_name>/`

---

## 🧪 Running Tests (optional)
If you have tests configured:
```bash
python manage.py test
```

---

## 🚢 Deployment Notes
- Use an ASGI server such as **Daphne** or **Uvicorn** behind Nginx/Apache
- Set `DEBUG=False` and configure `ALLOWED_HOSTS`
- Ensure a reachable **Redis** instance for Channels
- Serve static files (e.g., with WhiteNoise or via Nginx)

Minimal Daphne example:
```bash
daphne -b 0.0.0.0 -p 8000 djangochat.asgi:application
```

---

## 🤝 Contributing
Contributions are welcome! Please open an issue to discuss proposed changes before submitting a PR.

---
