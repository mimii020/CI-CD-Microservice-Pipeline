# CI/CD Microservice Pipeline

Flask microservice built with TDD, containerised with Docker, and automatically tested and deployed to Kubernetes via GitHub Actions on every push.

## Pipeline

```
git push → GitHub Actions
              ├── pytest          (stops here if tests fail)
              ├── docker build + push
              └── kubectl apply   (rolling update, zero downtime)
```

## Repository Structure

```
├── app/
│   └── routes.py              # Flask API endpoints
├── tests/
│   └── test_routes.py         # Test cases (written before implementation)
├── k8s/
│   ├── deployment.yaml        # Rolling update, maxUnavailable: 0
│   └── service.yaml
├── .github/workflows/
│   └── ci-cd.yml
└── Dockerfile                 # Multi-stage build
```

## Run Locally

```bash
pip install -r requirements.txt
pytest tests/ -v
flask run --port 5000
```

## Deploy to Kubernetes

```bash
kubectl apply -f k8s/
kubectl rollout status deployment/flask-microservice
kubectl rollout undo deployment/flask-microservice  # rollback
```

## Stack

Flask · pytest · Docker · GitHub Actions · Kubernetes

---
**Imen Abidi** · [GitHub](https://github.com/mimii020) · [LinkedIn](https://linkedin.com/in/imen-abidi)
