# Full-Stack CI/CD Pipeline Project

End-to-end **production-ready CI/CD pipeline** for a full-stack application using **GitHub Actions**, **Docker**, **custom reusable workflows**, and **multi-environment deployments**.

The project demonstrates real-world DevOps practices including security scanning, container image publishing, environment isolation, and production approval gates.

---

## Live Deployment (Production)

**Frontend (Production):**  
https://react-frontend-production-a98d.up.railway.app

---

## Architecture Overview

- **Frontend:** React + TypeScript (Vite), served via Nginx
- **Backend:** ASP.NET Core 8.0 REST API
- **Database:** MySQL 8.0
- **Containerization:** Docker
- **CI/CD:** GitHub Actions
- **Deployment:** Railway (Staging & Production), Docker Compose (Dev)
- **Configuration Management:** Ansible (Dev)

---

## Tech Stack

### Backend
- ASP.NET Core 8.0
- RESTful API
- Docker runtime image

### Frontend
- React + TypeScript (Vite)
- Nginx (Alpine) for static hosting

### DevOps & CI/CD
- GitHub Actions
- Reusable workflows
- Custom Docker S2I GitHub Action
- GitHub Container Registry (GHCR)
- Railway CLI
- Docker Compose
- Ansible

---

## Environments Details

| Environment | Deployment Method | Description |
|------------|------------------|-------------|
| **Dev** | Docker Compose + Ansible | Local deployment using self-hosted runner |
| **Staging** | Railway | Automatic deployment |
| **Production** | Railway | Requires manual approval |

---

## CI/CD Pipeline Flow

### CI – Backend (.NET) 
Use Automation workflow for dotnet from:
`salmataha88/Automation-Workflows/.github/workflows/dotnet.yml@main`

- Restore & build project
- Run unit tests
- GitLeaks secret scanning
- CodeQL static code analysis
- Build & push Docker image to GHCR
- Trivy vulnerability scanning
---
### CI – Frontend (React)

The frontend CI pipeline builds and packages the React application using a custom Docker-based S2I GitHub Action.

The pipeline leverages centralized automation components from:  
`salmataha88/Automation-Workflows/.github/actions/react-docker-s2i@main`

---
#### CI Workflow Includes:
- Dependency installation and optimized React build
- Security scanning using GitLeaks
- Static code analysis with CodeQL (JavaScript)
- Container image build via custom Docker S2I action
- Image publishing to GitHub Container Registry (GHCR)
- Vulnerability assessment using Trivy

---
### CD – Staging & Production
- Uses GitHub Environments
- Injects environment-specific secrets
- Deploys services via Railway CLI
- Production requires manual approval before deployment

---
### CD – Dev (Local)
- Runs on self-hosted GitHub Actions runner
- Uses Docker Compose
- Provisioned via Ansible playbook

---

## Repository Structure

### Main Project Repository

```
FullStack-DevOps-Pipeline
├── .github/workflows/
│ └── pipeline.yml
├── DotNet-Backend/
│ └── Dockerfile
├── React-Frontend/
│ └── nginx.conf
├── docker-compose.yml
├── playbook.yml
└── README.md

```

### Centralized Automation Repository

The centralized automation repository is located at:
`salmataha88/Automation-Workflows`


```
Automation-Workflows/
├── .github/workflows/
│ └── dotnet.yml
├── .github/actions/react-docker-s2i/
│ ├── action.yml
│ ├── Dockerfile.react
│ └── entrypoint.sh
└── README.md
```

---

## Security & Quality Controls

- GitLeaks for secret detection
- CodeQL for static code analysis (C# & JavaScript)
- Trivy for container vulnerability scanning
- Environment-level secrets (no hardcoded values)
- Production deployment approval gate enabled

---

## Key DevOps Concepts Demonstrated

- Reusable GitHub Actions workflows
- Custom Docker-based GitHub Actions
- Source-to-Image (S2I) build pattern
- Multi-environment CI/CD pipelines
- Security scanning integrated into CI
- Separation of application code and automation logic

---

## Project Status

- CI pipelines passing successfully
- Docker images published to GHCR
- Staging and Production deployed on Railway
- Production approval gate enforced
- Application accessible via public URL

---