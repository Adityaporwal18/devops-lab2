# DevOps Lab 2 â€” Containerization & Kubernetes Orchestration

This repository contains the implementation, documentation, commands, and execution evidence for **Lab 2: Containerization & Kubernetes Orchestration**.

The lab demonstrates Docker containerization and lifecycle management, Docker Hub image publishing, Docker Compose, persistent storage, Docker networking, Kubernetes deployment with Minikube, scaling, rolling updates, rollback, and Jenkins-based continuous deployment.

## Objective

Containerize a sample Flask application with Docker, manage Docker images and containers, demonstrate storage and networking behavior, deploy the application to Kubernetes using Minikube, perform scaling and deployment strategies, and automate Kubernetes manifest application through Jenkins.

## Technology Stack

- Ubuntu 26.04 LTS on WSL2
- Docker Desktop with WSL integration
- Docker Compose
- Docker Hub
- Python / Flask
- Kubernetes
- Minikube
- kubectl
- Jenkins
- Git and GitHub

## Repository Structure

```text
devops-lab2/
â”œâ”€â”€ Dockerfile
â”œâ”€â”€ Jenkinsfile
â”œâ”€â”€ README.md
â”œâ”€â”€ REPORT.md
â”œâ”€â”€ app.py
â”œâ”€â”€ commands.txt
â”œâ”€â”€ compose.yaml
â”œâ”€â”€ requirements.txt
â”œâ”€â”€ bind-data/                  # bind-mount experiment artifacts
â”œâ”€â”€ kubernetes/
â”‚   â”œâ”€â”€ deployment.yaml
â”‚   â””â”€â”€ service.yaml
â”œâ”€â”€ docs/
â”‚   â”œâ”€â”€ ARCHITECTURE.md
â”‚   â”œâ”€â”€ EVIDENCE.md
â”‚   â”œâ”€â”€ EXPERIMENTS.md
â”‚   â”œâ”€â”€ FINAL_CHECKLIST.md
â”‚   â”œâ”€â”€ evidence/               # screenshots from actual execution
â”‚   â””â”€â”€ source/
â”‚       â””â”€â”€ Lab2-Evidence.docx  # original compiled evidence document
â””â”€â”€ scripts/
    â””â”€â”€ capture-final-state.sh
```

## End-to-End Flow

```text
Application Source
      |
      v
    Docker
      |
      +--> Docker Hub: Adityaporwal18/devops-lab2:v1 / v2
      |
      v
GitHub Repository
      |
      v
    Jenkins
      |
      | kubectl apply
      v
Minikube / Kubernetes
      |
      v
  Deployment
   /      \
 Pod      Pod
   \      /
    Service
      |
      v
Flask Application
```

## Lab Requirement Coverage

| Q | Requirement | Implementation / Evidence | Status |
|---|---|---|---|
| 1 | Containerize sample application | `Dockerfile`, image build, `docker history`, running Flask app | âœ… |
| 2 | Manage containers and images | list/start/stop/remove, tags, Docker Hub push, Compose | âœ… |
| 3 | Docker storage | ephemeral data loss, named volume persistence, bind mount | âœ… |
| 4 | Docker network | custom bridge network, name ping, IP ping, network inspection | âœ… |
| 5 | Kubernetes deployment | Minikube, Deployment, Service, running pods, app access | âœ… |
| 6 | Deployment strategies | scaling to 4, rolling update to v2, rollback to v1 | âœ… |
| 7 | Continuous deployment | Jenkins checkout + `kubectl apply` + rollout verification | âœ… |
| 8 | Record tools/documents | Dockerfile, YAML, commands, screenshots, report | âœ… |
| 9 | Final report | `REPORT.md` with architecture, results and observations | âœ… |

## Key Results

- Docker and Docker Compose were verified inside Ubuntu/WSL2.
- The Flask application was built as a Docker image and accessed at `localhost:5000`.
- Docker image layers were inspected with `docker history`.
- `v1` and `latest` image tags were demonstrated.
- A Flask + Redis multi-container stack ran with Docker Compose.
- `Adityaporwal18/devops-lab2:v1` and `v2` were pushed to Docker Hub.
- Container-local data loss after deletion was demonstrated.
- A named Docker volume preserved data across container replacement.
- A bind mount demonstrated host-to-container and container-to-host file sharing.
- Two containers communicated through a custom Docker bridge network by name and IP.
- Minikube created a Kubernetes control-plane node in `Ready` state.
- The application ran as two Kubernetes pods behind a NodePort Service.
- The Deployment was scaled from 2 replicas to 4 replicas.
- A rolling update changed the application from v1 to v2.
- Kubernetes rollback restored the previous revision.
- Jenkins successfully checked out the repository, applied the Kubernetes manifests, waited for rollout completion, verified resources, and finished with `SUCCESS`.
- The final captured Kubernetes state shows two running pods using `Adityaporwal18/devops-lab2:v2`.

## Documentation

- [Complete Lab Report](REPORT.md)
- [Command Reference](commands.txt)
- [Architecture](docs/ARCHITECTURE.md)
- [Experiment-by-Experiment Procedure](docs/EXPERIMENTS.md)
- [Evidence Gallery](docs/EVIDENCE.md)
- [Final Submission Checklist](docs/FINAL_CHECKLIST.md)
- [Original Evidence Document](docs/source/Lab2-Evidence.docx)

## Evidence

All screenshots in `docs/evidence/` were captured from the actual Lab 2 execution and extracted from the submitted evidence document. They are indexed and explained in [docs/EVIDENCE.md](docs/EVIDENCE.md).

> Jenkins evidence proves that the pipeline automates Kubernetes manifest application and rollout verification. The captured build was executed from Jenkins; it is not presented as proof of a GitHub webhook unless a webhook/SCM trigger is separately configured.
