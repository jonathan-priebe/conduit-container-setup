# CI/CD Workflows – Conduit Container Setup

This document describes the GitHub Actions workflows in this repository and their responsibilities.

---

## Table of Contents
- [PR Test Workflow (`pr-test.yml`)](#-pr-test-workflow-pr-testyml)
- [GHCR Deployment Workflow (`ghcr-deployment.yml`)](#-ghcr-deployment-workflow-ghcr-deploymentyml)
- [VM Deployment Workflow (`vm-deploy.yml`)](#-vm-deployment-workflow-vm-deployyml)

---

## 🔹 PR Test Workflow (`pr-test.yml`)
- **Trigger:** Pull Requests targeting `main` or `dev-abgabe`
- **Purpose:** Validate code quality and container startup before merging
- **Flow:**
  - **Backend tests**
    - Build the backend Docker image  
    - Run the container in CI mode  
    - Verify Gunicorn configuration via CI status file  
  - **Frontend tests**
    - Generate a `.env` file from workflow environment variables  
    - Start backend + frontend with Docker Compose  
    - Perform health checks on backend (`/api`) and frontend (`:8282`)  

---

## 🔹 GHCR Deployment Workflow (`ghcr-deployment.yml`)
- **Trigger:** Push to `main` (or manual dispatch, depending on config)
- **Purpose:** Build and publish Docker images to GitHub Container Registry (GHCR)
- **Flow:**
  - **Backend**
    - Build image from `conduit-backend/Dockerfile`   
    - Push with tags: `latest`, commit SHA, branch/tag name  
  - **Frontend**
    - Build image from `conduit-frontend/Dockerfile`  
    - Pass build argument `API_URL`  
    - Push with the same tag scheme  

---

## 🔹 VM Deployment Workflow (`vm-deploy.yml`)
- **Trigger:** Manual (`workflow_dispatch`)  
- **Purpose:** Deploy the latest images to the target VM  
- **Flow:**
  - Connect to the VM via SSH (using secrets: `VM_HOST`, `VM_USER`, `VM_SSH_KEY`)  
  - Authenticate with GHCR  
  - Pull the latest backend and frontend images  
  - Restart containers using `docker compose` in the project directory  