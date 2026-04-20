# 🚀 SDA DevOps Project

![Python](https://img.shields.io/badge/Python-3.10-blue.svg)
![Flask](https://img.shields.io/badge/Flask-2.0-lightgrey.svg)
![Docker](https://img.shields.io/badge/Docker-Containerized-blue.svg)
![Kubernetes](https://img.shields.io/badge/Kubernetes-Deployed-326CE5.svg)
![Jenkins](https://img.shields.io/badge/Jenkins-CI%2FCD-D24939.svg)
[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A containerized **Flask web application** with a full DevOps pipeline — Docker, Docker Compose, Jenkins CI/CD, and Kubernetes deployment.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Run with Docker Compose](#run-with-docker-compose)
  - [Run Locally (without Docker)](#run-locally-without-docker)
- [CI/CD Pipeline (Jenkins)](#cicd-pipeline-jenkins)
- [Kubernetes Deployment](#kubernetes-deployment)
- [Configuration](#configuration)
- [Contributing](#contributing)

---

## Overview

This project demonstrates a complete DevOps workflow for a Python Flask application. It covers:

- **Containerization** with Docker
- **Multi-service orchestration** with Docker Compose (Flask app + MySQL database)
- **Automated pipeline** with Jenkins (Build → Push → Deploy stages)
- **Production deployment** with Kubernetes (Deployment + NodePort Service)

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Application | Python 3.10, Flask |
| Containerization | Docker |
| Orchestration (local) | Docker Compose |
| Database | MySQL 5.7 |
| CI/CD | Jenkins |
| Deployment | Kubernetes |

---

## 📁 Project Structure

```
SDA-Project/
├── app/
│   ├── app.py               # Flask application entry point
│   ├── requirements.txt     # Python dependencies
│   └── templates/
│       └── index.html       # HTML templates
├── kubernetes/
│   ├── deployment.yaml      # Kubernetes Deployment manifest
│   └── service.yaml         # Kubernetes NodePort Service manifest
├── Dockerfile               # Docker image definition
├── docker-compose.yml       # Multi-container local setup
├── Jenkinsfile              # Jenkins CI/CD pipeline definition
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

Make sure you have the following installed:

- [Docker](https://docs.docker.com/get-docker/) & [Docker Compose](https://docs.docker.com/compose/install/)
- [Python 3.10+](https://www.python.org/downloads/) (for local runs)
- [kubectl](https://kubernetes.io/docs/tasks/tools/) (for Kubernetes deployment)
- [Jenkins](https://www.jenkins.io/doc/book/installing/) (for CI/CD pipeline)

---

### Run with Docker Compose

This spins up both the Flask app and a MySQL database together:

```bash
# Clone the repository
git clone https://github.com/your-username/SDA-Project.git
cd SDA-Project

# Build and start all services
docker-compose up --build
```

The app will be available at **http://localhost:5000**

To stop and remove containers:

```bash
docker-compose down
```

---

### Run Locally (without Docker)

```bash
cd app

# Install dependencies
pip install flask

# Start the app
python app.py
```

The app will be available at **http://localhost:5000**

---

## 🔧 CI/CD Pipeline (Jenkins)

The `Jenkinsfile` defines a three-stage pipeline:

| Stage | Description |
|---|---|
| **Build** | Builds the Docker image from the `Dockerfile` |
| **Push** | Pushes the Docker image to Docker Hub |
| **Deploy** | Triggers deployment to Kubernetes |

### Setup Jenkins Pipeline

1. Open Jenkins and create a new **Pipeline** job.
2. Under *Pipeline Definition*, select **Pipeline script from SCM**.
3. Point it to this repository — Jenkins will automatically detect the `Jenkinsfile`.
4. Configure your Docker Hub credentials in Jenkins' credentials store.
5. Run the pipeline.

---

## ☸️ Kubernetes Deployment

Kubernetes manifests are located in the `kubernetes/` directory.

### Deploy to a Cluster

```bash
# Apply the deployment
kubectl apply -f kubernetes/deployment.yaml

# Apply the service
kubectl apply -f kubernetes/service.yaml
```

### Access the App

The service is exposed as a **NodePort** on port `30007`.

```bash
# Get your node's IP
kubectl get nodes -o wide

# Access the app
http://<NODE_IP>:30007
```

### Check Status

```bash
# View running pods
kubectl get pods

# View service details
kubectl get svc flask-service
```

---

## ⚙️ Configuration

### Docker Image

Before deploying to Kubernetes, update the image name in `kubernetes/deployment.yaml`:

```yaml
containers:
  - name: flask
    image: your-dockerhub-username/myapp:v1   # ← Replace this
```

### Environment Variables

The MySQL service in `docker-compose.yml` uses the following default:

| Variable | Default Value |
|---|---|
| `MYSQL_ROOT_PASSWORD` | `root` |

> ⚠️ **Important:** Change the default MySQL password before deploying to any non-local environment.

---

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add some feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
