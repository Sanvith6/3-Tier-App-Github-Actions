# 3-Tier App with GitHub Actions DevSecOps Pipeline

This repository is focused on the implemented **GitHub Actions DevSecOps pipeline** for a Node.js + React + MySQL application.

## Implemented Scope

- `client/`: React frontend
- `api/`: Node.js/Express backend
- `mysql-init/`: MySQL initialization scripts
- `.github/workflows/node.js.yml`: CI/CD + DevSecOps workflow

## Current Focus of This Project

The main deliverable in this project is the DevSecOps workflow in GitHub Actions:

1. Syntax checks for frontend and backend JavaScript files
2. Secret scanning with Gitleaks
3. Dependency/filesystem vulnerability scanning with Trivy
4. Code quality and static analysis with SonarQube (frontend and backend)
5. Docker image build and push to Docker Hub (frontend and backend)

## GitHub Actions Workflow

Workflow file: `.github/workflows/node.js.yml`  
Trigger: Push and pull request on `main`

### Job Order

1. `compile`
2. `gitleaks`
3. `trivy_scan`
4. `sonar_frontend`
5. `sonar_backend`
6. `build_frontend_docker_image_and_push`
7. `build_backend_docker_image_and_push`

## Required GitHub Configuration

### Repository Variables

- `DOCKERHUB_USERNAME`

### Repository Secrets

- `DOCKERHUB_TOKEN`
- `SONAR_TOKEN`
- `SONAR_HOST_URL`

## Runner Requirements

- Jobs `compile`, `gitleaks`, `trivy_scan`, `sonar_frontend`, and `sonar_backend` are configured for runner label: `Agent-2`
- Docker build/push jobs use `ubuntu-latest`

Ensure your self-hosted runner is available with the label `Agent-2` if you keep this configuration.

## Application Run (Local)

### Backend

```bash
cd api
npm install
npm start
```

### Frontend

```bash
cd client
npm install
npm start
```

Backend uses MySQL and expects database/environment configuration in `api/.env`.

## Notes

- This README intentionally focuses on the implemented DevSecOps GitHub Actions pipeline and active app components.
- Infrastructure folders/scripts not part of the current implemented focus (for example EKS-related setup) are not covered here.
