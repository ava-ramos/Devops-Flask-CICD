# 🚀 DevOps CI/CD Demo — Flask + Docker + GitHub Actions

A beginner-friendly DevOps portfolio project demonstrating a complete **CI/CD pipeline** for a Python Flask application. Every push to `main` is automatically linted, tested across multiple Python versions, containerized, and verified — exactly how it's done in real engineering teams.

![CI/CD Pipeline](https://github.com/YOUR_USERNAME/devops-flask-cicd/actions/workflows/ci-cd.yml/badge.svg)
![Python](https://img.shields.io/badge/python-3.11-blue)
![Docker](https://img.shields.io/badge/docker-ready-blue)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📋 What This Project Demonstrates

This project ticks the boxes for the core skills a junior DevOps engineer is expected to show:

- ✅ **Version control** — clean Git workflow with `main` branch protection in mind
- ✅ **Containerization** — multi-stage Dockerfile with a non-root user
- ✅ **CI/CD** — automated pipeline with GitHub Actions (lint → test → build → deploy)
- ✅ **Testing** — unit tests, endpoint tests, and matrix testing across Python versions
- ✅ **Code quality** — linting with flake8 and coverage reporting
- ✅ **Health checks** — Docker `HEALTHCHECK` and a `/health` endpoint
- ✅ **Production-readiness** — Gunicorn (not Flask dev server), env-based configuration

---

## 🏗️ Architecture

```
┌─────────────┐      ┌──────────────────┐      ┌──────────────┐
│   git push  │ ───> │  GitHub Actions  │ ───> │    Deploy    │
└─────────────┘      │                  │      └──────────────┘
                     │   1. Lint        │
                     │   2. Test        │
                     │   3. Build image │
                     │   4. Smoke test  │
                     └──────────────────┘
```

---

## 🚀 Quick Start

### Run locally with Python

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/devops-flask-cicd.git
cd devops-flask-cicd

# Set up a virtual environment
python -m venv venv
source venv/bin/activate          # macOS/Linux
# venv\Scripts\activate           # Windows

# Install dependencies
pip install -r requirements.txt

# Run the app
python -m app.main
```

Open http://localhost:5000 in your browser.

### Run with Docker

```bash
# Build and run with Docker Compose
docker compose up --build

# Or use Docker directly
docker build -t devops-flask-cicd .
docker run -p 5000:5000 devops-flask-cicd
```

### Run the tests

```bash
pytest tests/ -v --cov=app
```

---

## 📡 Endpoints

| Method | Path        | Description                          |
|--------|-------------|--------------------------------------|
| GET    | `/`         | Home page with deployment info       |
| GET    | `/health`   | Health check (returns JSON status)   |
| GET    | `/api/info` | Application metadata as JSON         |

Example:

```bash
curl http://localhost:5000/health
# {"status":"healthy","service":"devops-flask-cicd"}
```

---

## 🔁 The CI/CD Pipeline

Every push and pull request to `main` triggers `.github/workflows/ci-cd.yml`, which runs four jobs:

### 1. **Lint** — code-quality checks with `flake8`
Catches syntax errors and undefined names; warns on style issues.

### 2. **Test** — `pytest` across Python 3.10, 3.11, and 3.12
Matrix testing ensures the app works on multiple Python versions. Coverage is reported and uploaded as an artifact.

### 3. **Build** — Docker image build with smoke test
Builds the multi-stage Docker image, runs it, and curls `/health` to verify it actually starts up.

### 4. **Deploy** — placeholder for real deploys
Runs only on `main`. In a real project, this is where you'd push to a registry and deploy to a server, Kubernetes cluster, or PaaS like Render/Fly.io.

---

## 📁 Project Structure

```
devops-flask-cicd/
├── .github/
│   └── workflows/
│       └── ci-cd.yml          # GitHub Actions pipeline
├── app/
│   ├── __init__.py
│   └── main.py                # Flask application
├── tests/
│   ├── __init__.py
│   └── test_app.py            # Unit + endpoint tests
├── .gitignore
├── Dockerfile                 # Multi-stage build
├── docker-compose.yml         # Local orchestration
├── LICENSE
├── README.md
└── requirements.txt
```

---

## 🧪 Try Breaking the Pipeline (Recommended Learning Exercise)

The best way to understand CI/CD is to *break* it. Try these:

1. **Break a test** — change `assert add(2, 3) == 5` to `== 6` and push. Watch the pipeline fail at the test stage.
2. **Break the lint** — add `import os` to `main.py` but never use it. Push and see the linter complain.
3. **Break the Dockerfile** — change the Gunicorn command. The smoke test will catch it.

Then fix each one and watch the green checkmarks come back. That feedback loop *is* DevOps.

---

## 🛠️ Next Steps to Extend This Project

Once you're comfortable with this, level up:

- [ ] Push the Docker image to **Docker Hub** or **GitHub Container Registry**
- [ ] Add **Terraform** to provision a real cloud VM (AWS EC2 / Azure VM / GCP Compute)
- [ ] Deploy to **Kubernetes** with a Deployment + Service manifest
- [ ] Add **Prometheus** metrics and a **Grafana** dashboard
- [ ] Set up **branch protection rules** that require the CI to pass before merging
- [ ] Add a **Slack** or **Discord** notification on pipeline failures

---

## 📜 License

MIT — see [LICENSE](LICENSE) for details.

---

## 🙋 About

Built as a portfolio project to demonstrate hands-on DevOps fundamentals. Feedback and PRs welcome!
