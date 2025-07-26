# mlops-irisapi-docker-k8s-cd
Sure, Satyam! Here's a clean, professional `README.md` file for your **Iris Classification API with CI/CD on GKE** setup:

---

## 🧠 Iris Classification API (CI/CD with GCP GKE & GitHub Actions)

This project serves a **Machine Learning API** that classifies Iris flower species using a trained `model.pkl`. It is containerized using Docker and deployed to **Google Kubernetes Engine (GKE)** with a complete **CI/CD pipeline using GitHub Actions**.

---

## 📦 Project Structure

```bash
.
├── Dockerfile                # Defines API container image
├── model/
│   └── model.pkl             # Trained scikit-learn model
├── app.py                   # Flask-based API
├── requirements.txt         # Python dependencies
├── kubernetes/
│   ├── deployment.yaml      # Kubernetes deployment config
│   └── service.yaml         # Kubernetes LoadBalancer service
└── .github/
    └── workflows/
        └── cd.yaml          # GitHub Actions CD workflow
```

---

## 🚀 How It Works

### 🛠 API Functionality

POST `/predict/`

```json
{
  "sepal_length": 5.1,
  "sepal_width": 3.5,
  "petal_length": 1.4,
  "petal_width": 0.2
}
```

Response:

```json
{
  "predicted_class": "setosa"
}
```

### 📦 Containerization

Docker is used to package the Flask app and model into a deployable container:

```bash
docker build -t gcr.io/<project-id>/iris-api:latest .
docker push gcr.io/<project-id>/iris-api:latest
```

---

## 🔁 Continuous Deployment

### ✅ Trigger:

Every push to the `main` branch triggers:

1. Docker build & push to Google Container Registry (GCR)
2. GKE deployment update using `kubectl set image`

### ✅ Secrets Needed (GitHub > Settings > Secrets and variables > Actions):

| Secret Key         | Purpose                              |
| ------------------ | ------------------------------------ |
| `GCP_SA_KEY`       | JSON credentials for service account |
| `GCP_PROJECT_ID`   | GCP Project ID                       |
| `GCP_CLUSTER_NAME` | Name of your GKE cluster             |
| `GCP_REGION`       | Region of your GKE cluster           |

---

## ☁️ Kubernetes Deployment

You must first apply the manifests:

```bash
kubectl apply -f kubernetes/deployment.yaml
kubectl apply -f kubernetes/service.yaml
```

> This creates a deployment and exposes the app through a GCP LoadBalancer.

---

## 🌐 Test the Endpoint

```bash
curl -X POST http://<EXTERNAL-IP>/predict/ \
  -H "Content-Type: application/json" \
  -d '{"sepal_length": 6.1, "sepal_width": 2.8, "petal_length": 4.7, "petal_width": 1.2}'
```

---

## ✅ Prerequisites

* Google Cloud Project with GKE and GCR enabled
* Docker installed locally (for manual testing)
* `kubectl` & `gcloud` installed and authenticated
* GitHub repository connected with proper secrets

---

## 🧪 TODO / Extensions

* ✅ Add CI step (unit test / pytest / CML)
* ⏳ Add monitoring (Prometheus/Grafana)
* ⏳ Use Helm charts for better config management
* ⏳ Add MLflow/Feast integration (if part of full pipeline)

---

## 👨‍💻 Author

**Satyam Srivastava**
Iris Deployment Project | GCP + GKE + CI/CD | MLOps Week 6

---

Let me know if you want the README in **PDF format** too.
