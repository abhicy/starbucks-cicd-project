# Starbucks CI/CD Deployment Project

## Overview

This project demonstrates an end-to-end CI/CD pipeline for a containerized Starbucks web application using Jenkins, Docker, DockerHub, GitHub, and AWS EC2.

The pipeline automates application build, Docker image creation, image publishing to DockerHub, and deployment to an AWS EC2 instance.

## Project Objectives

- Automate application build and deployment
- Implement Continuous Integration and Continuous Delivery (CI/CD)
- Containerize the application using Docker
- Host application on AWS EC2
- Store and distribute images through DockerHub
- Reduce manual deployment efforts

---

## Technology Stack

### Cloud
- AWS EC2

### CI/CD
- Jenkins

### Source Code Management
- Git
- GitHub

### Containerization
- Docker
- DockerHub

### Runtime
- Node.js

### Operating System
- Ubuntu Linux

---

## Architecture

```text
Developer
    │
    ▼
GitHub Repository
    │
    ▼
Jenkins Pipeline
    │
    ├── Source Code Checkout
    │
    ├── npm Install
    │
    ├── Docker Build
    │
    ├── Docker Image Tagging
    │
    ├── DockerHub Push
    │
    └── Deployment Stage
            │
            ▼
      AWS EC2 Instance
            │
            ▼
     Docker Container
            │
            ▼
    Starbucks Web Application
```

---

## CI/CD Workflow

### Stage 1 - Source Code Checkout

Jenkins pulls the latest application code from GitHub.

### Stage 2 - Dependency Installation

Application dependencies are installed using npm.

### Stage 3 - Docker Build

A Docker image is created using the application's Dockerfile.

### Stage 4 - DockerHub Push

The image is tagged and pushed to DockerHub.

### Stage 5 - Deployment

The latest Docker image is pulled from DockerHub and deployed as a running container on AWS EC2.

---

## Jenkins Pipeline Stages

- Git Checkout
- Install Dependencies
- Build Docker Image
- Push Docker Image
- Deploy Application

---

## Docker Commands Used

Build Image

```bash
docker build -t starbucks-app .
```

Tag Image

```bash
docker tag starbucks-app <dockerhub-username>/starbucks-app:latest
```

Push Image

```bash
docker push <dockerhub-username>/starbucks-app:latest
```

Run Container

```bash
docker run -d \
--name starbucks-app-container \
-p 3000:3000 \
<dockerhub-username>/starbucks-app:latest
```

---

## Application Access

Application URL:

```text
http://<EC2-PUBLIC-IP>:3000
```

---

## Key Learnings

- Jenkins Pipeline Creation
- Docker Image Management
- DockerHub Integration
- AWS EC2 Deployment
- CI/CD Automation
- Linux Administration
- Git and GitHub Workflows
- Container-Based Deployments

---

## Future Enhancements

- GitHub Webhooks
- SonarQube Code Quality Analysis
- Trivy Security Scanning
- Terraform Infrastructure Provisioning
- Kubernetes Deployment
- Prometheus Monitoring
- Grafana Dashboards
- Nginx Reverse Proxy
- HTTPS using Let's Encrypt

---

## Author

Abhishek Yaragambalimath

DevOps | Cloud | Linux | Automation


                    +----------------+
                    |    Developer   |
                    +--------+-------+
                             |
                             |
                             v
                    +----------------+
                    |     GitHub     |
                    +--------+-------+
                             |
                             |
                             v
                    +----------------+
                    |    Jenkins     |
                    |    Pipeline    |
                    +--------+-------+
                             |
          +------------------+------------------+
          |                  |                  |
          v                  v                  v
     Git Checkout      npm Install      Docker Build
                                                |
                                                v
                                      +----------------+
                                      |   DockerHub    |
                                      +--------+-------+
                                               |
                                               |
                                               v
                                      +----------------+
                                      |    AWS EC2     |
                                      +--------+-------+
                                               |
                                               |
                                               v
                                      +----------------+
                                      | Docker Container|
                                      +--------+-------+
                                               |
                                               v
                                      Starbucks Application



