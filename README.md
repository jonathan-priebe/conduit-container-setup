# Conduit-Container-Setup
This repository provides a complete Docker-based setup for the RealWorld Conduit App, featuring an Angular frontend and a Django backend. It's designed to offer a ready-to-run development and testing environment—perfect for learning, collaboration, or building your own fullstack applications.

## Project Handover  

📄 [Project Documentation PDF](<./Conduit Container Checkliste.pdf>)

---

## Table of Contents  
- [Prerequisites](#prerequisites)  
- [Quickstart](#quickstart)  
- [Usage](#usage)  
- [Me](#me)

---

## Prerequisites  
Before running this project, make sure the following tools are installed on your system:

| Tool            | Version Recommendation | Purpose                              |
|-----------------|------------------------|--------------------------------------|
| [Git](https://git-scm.com/)            | ≥ 2.30                 | Clone the repository                 |
| [Docker](https://www.docker.com/)      | ≥ 24.0                 | Container runtime                    |
| [Docker Compose](https://docs.docker.com/compose/) | ≥ 2.20 | Orchestrate multi-container setup   |

> 💡 Tip: Run `docker -v`, `docker compose version`, and `git --version` to verify your environment.

---

## Quickstart  

1. **Clone the repository**

    ```bash
    git clone https://github.com/Jonathan-Priebe/Conduit-Container-Setup.git
    cd Conduit-Container-Setup
    ```
    Get the submodules also:
    ```bash
    git submodule add -b dev-abgabe https://github.com/Jonathan-Priebe/conduit-frontend.git conduit-frontend
    git submodule add -b dev-abgabe https://github.com/Jonathan-Priebe/conduit-backend.git conduit-backend
    ```

All key settings are controlled via environment variables and Docker volumes. You can adjust them in the [Docker-Compose](./docker-compose.yml) file.

> ℹ️ To get started, copy the [example environment file](./example.env):
> ```bash
> cp example.env .env
> ```
> Then adjust the values to match your desired setup.

2. **Run Container with Dcoker Compose**

  ```bash
  docker compose up --build -d
  ```
  - Environment variables are loaded from your .env file

  - You can customize and exposed ports

  - To stop the server:

  ```bash
  docker compose down
  ```

  ## Usage  
  
  1. **Environment Configuration**
  
  Edit .env to define your Conduit-Backend and Frontend settings and Admin Interface in [example.env](example.env)

  2. **Customize the following variables to match your desired setup**

---

### ⚙️ Django Settings

| Variable                   | Description                                      |
|----------------------------|--------------------------------------------------|
| `DJANGO_SUPERUSER_USERNAME` | Username for Django admin user                 |
| `DJANGO_SUPERUSER_EMAIL`    | Email address for Django admin user            |
| `DJANGO_SUPERUSER_PASSWORD` | Password for Django admin user                 |
| `SECRET_KEY_Django`         | Secret key for Django cryptographic signing    |
| `API_URL`                   | Base path for backend API                      |

---

### 🌐 Server & CORS Settings

| Variable               | Description                                      |
|------------------------|--------------------------------------------------|
| `IP_ADDR`              | Public IP address of your server                |
| `CORS_ALLOWED_ORIGINS`| Allowed origin for frontend requests             |

---

### 📦 Frontend Configuration (Angular)

| Variable               | Description                                      |
|------------------------|--------------------------------------------------|
| `FRONTEND_PORT`        | Port exposed for Angular frontend                |
| `FRONTEND_API_URL`     | Full URL to access backend API from frontend     |

3. **🚀 Access Conduit App/Interface**

- Once running, access the **Angular Frontend** at:
```bash
http://YOUR_IP_OR_DOMAIN:YOUR_FRONTEND_PORT
```

## Me  

- Created and maintained by Jonathan 
- 📫 Reach me via GitHub or [LinkedIn](https://www.linkedin.com/in/jonathan-p-34471b1a5/)
