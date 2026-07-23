# GitHub Actions CI/CD Pipeline with Docker

A real-world DevOps practice project demonstrating how to build a **Continuous Integration (CI)** pipeline using **GitHub Actions**, **Docker**, and **Docker Hub**.

This project focuses on automatically building and publishing Docker images whenever a new version tag is pushed to GitHub.

> **Status:** CI Completed ✅ | Manual CD Concept Learned ✅ | Auto CD (SSH Deployment) Planned 🔜

---

# 📚 Project Objectives

* Learn GitHub Actions Workflow
* Build Docker Images automatically
* Push Docker Images to Docker Hub
* Use Git Tags for Version Management
* Understand CI vs CD
* Learn Docker Image Versioning
* Prepare for Automated Deployment (Continuous Deployment)

---

# 🏗 CI Pipeline Architecture

```text
Developer
    │
    │ git push
    ▼
GitHub Repository
    │
    ▼
GitHub Actions
    │
    ├── Checkout Source Code
    ├── Login Docker Hub
    ├── Build Docker Image
    ├── Tag Version Image
    ├── Tag Latest Image
    ├── Push Version Image
    └── Push Latest Image
    ▼
Docker Hub
```

---

# 📂 Project Structure

```text
docker-ci-lab/
│
├── .github/
│   └── workflows/
│       └── docker.yml
│
├── index.html
├── Dockerfile
├── .gitignore
└── README.md
```

---

# 🐳 Dockerfile

Example Dockerfile:

```dockerfile
FROM nginx:alpine

COPY . /usr/share/nginx/html
```

---

# ⚙ GitHub Actions Workflow

Workflow File:

```text
.github/workflows/docker.yml
```

Main Tasks:

* Trigger workflow when a Git Tag is pushed
* Checkout project source code
* Login to Docker Hub
* Build Docker image
* Create two image tags:

  * Version Tag (`v1.0.0`)
  * Latest Tag (`latest`)
* Push both images to Docker Hub

---

# 🔐 GitHub Secrets

The following repository secrets are required:

| Secret          | Description             |
| --------------- | ----------------------- |
| DOCKER_USERNAME | Docker Hub Username     |
| DOCKER_TOKEN    | Docker Hub Access Token |

---

# 🏷 Docker Image Versioning

Example:

```text
docker-ci-lab:v1.0.0
docker-ci-lab:v1.0.1
docker-ci-lab:latest
```

## Why Use Tags?

Version tags allow us to:

* Deploy a specific release
* Roll back to an older version
* Track application versions
* Maintain release history

Example:

```bash
docker pull username/docker-ci-lab:v1.0.0
```

Latest version:

```bash
docker pull username/docker-ci-lab:latest
```

---

# 🚀 Release Workflow

Create a new version tag:

```bash
git tag v1.0.0
```

Push the tag:

```bash
git push origin v1.0.0
```

GitHub Actions automatically starts.

---

# 🔄 CI Workflow

```text
git push origin v1.0.0
        │
        ▼
GitHub Actions
        │
Checkout
        │
Docker Login
        │
Docker Build
        │
Create Version Tag
        │
Create Latest Tag
        │
Push Images
        ▼
Docker Hub
```

---

# 🧪 Verify Pipeline

After the workflow completes:

* GitHub Actions shows **Success**
* Docker Hub contains:

  * `v1.0.0`
  * `latest`

Example:

```text
docker-ci-lab

Tags
├── v1.0.0
└── latest
```

---

# 📦 Manual Continuous Delivery (Concept)

After CI finishes, the Docker image is available in Docker Hub.

A production server can manually deploy the application:

```bash
docker pull username/docker-ci-lab:v1.0.0

docker run -d \
  --name production-web \
  -p 80:80 \
  username/docker-ci-lab:v1.0.0
```

This is **Continuous Delivery (Manual Deployment)** because deployment is still performed manually.

---

# 🔄 Updating to a New Version

Release a new version:

```bash
git tag v1.0.1

git push origin v1.0.1
```

GitHub Actions builds:

```text
docker-ci-lab:v1.0.1

docker-ci-lab:latest
```

Production update:

```bash
docker pull username/docker-ci-lab:v1.0.1

docker stop production-web

docker rm production-web

docker run -d \
  --name production-web \
  -p 80:80 \
  username/docker-ci-lab:v1.0.1
```

---

# 📖 CI vs CD

## Continuous Integration (CI)

CI automatically:

* Builds the application
* Packages the application
* Creates Docker images
* Pushes Docker images to Docker Hub

Pipeline:

```text
Developer
      │
git push
      ▼
GitHub Actions
      │
Docker Build
      │
Docker Push
      ▼
Docker Hub
```

---

## Continuous Delivery (CD)

CD deploys the application to the production server.

Pipeline:

```text
Docker Hub
      │
docker pull
      ▼
Production Server
      │
docker run
      ▼
Website Live
```

In this project, the CD process is **manual**.

---

# 📌 Key Concepts Learned

* GitHub Actions Workflow
* Docker Build Automation
* Docker Hub Authentication
* GitHub Secrets
* Docker Image Versioning
* Git Tags
* Docker Image Tagging
* CI Pipeline Design
* Manual Continuous Delivery
* CI vs CD
* Docker Hub as an Artifact Repository
* Docker Image Lifecycle

---

# 🚀 Future Improvements

* SSH Authentication
* GitHub Actions Auto Deployment
* Continuous Deployment (Auto CD)
* Docker Compose Deployment
* Nginx Reverse Proxy
* SSL with Let's Encrypt
* VPS Deployment (Ubuntu Server)
* Kubernetes Deployment
* Helm Charts
* Production Monitoring

---

# 🛠 Technologies Used

* Git
* GitHub
* GitHub Actions
* Docker
* Docker Hub
* Nginx
* YAML

---

# 🎯 Learning Outcome

After completing this lab, I can:

* Build a complete CI pipeline using GitHub Actions.
* Automate Docker image building and publishing.
* Manage Docker image versions with Git tags.
* Push versioned and latest images to Docker Hub.
* Explain the difference between Continuous Integration (CI) and Continuous Delivery (CD).
* Understand the workflow from source code to Docker Hub.
* Prepare for automated deployments using SSH and Kubernetes in future projects.

---

# 👨‍💻 Author

**Aung Phyo Hein**

DevOps Engineer Learner | Docker & Cloud Enthusiast

This project was created as part of my hands-on journey to learn and practice modern DevOps workflows, including Docker, GitHub Actions, CI/CD pipelines, and container deployment strategies.
