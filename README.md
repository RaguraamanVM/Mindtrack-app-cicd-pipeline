# MindTrack - Application Deployment on AWS EKS

## Project Overview
This project focuses on deploying the "MindTrack" - React application in a production-ready environment using AWS cloud services and DevOps practices. The application was containerized using Docker, stored in Docker Hub Registry, and deployed on Amazon EKS using Kubernetes Deployment and Service manifests. A complete CI/CD pipeline was implemented using AWS CodeBuild and AWS CodePipeline to automate the build and deployment process from GitHub to EKS. AWS CloudWatch was used for monitoring and logging, ensuring visibility into build, deployment, and application activities. The solution provides an automated, scalable, and reliable deployment workflow for managing application releases in a Kubernetes environment.

---  

## Architecture

```text
GitHub Repository
        │
        ▼
AWS CodePipeline
        │
        ▼
AWS CodeBuild
        │
        ▼
Docker Image Build
        │
        ▼
Docker Hub Registry
        │
        ▼
AWS EKS Cluster
        │
        ▼
LoadBalancer Service
        │
        ▼
MindTrack Application
```
---

## Technologies Used

- ReactJS
- Docker
- Docker Hub Registry
- AWS EKS / Kubernetes
- AWS CodeBuild
- AWS CodePipeline
- AWS CloudWatch

---

## Prerequisites

- Docker Installed
- AWS CLI Installed
- kubectl Installed
- eksctl Installed
- Git Installed

---

## Step 1: Application build Artifacts

The application build artifacts were made available for deployment activities. Initial verification was performed to ensure the application was functioning correctly before proceeding with Dockerization and cloud deployment.

## Step 2: Run Application Locally

```bash
cd dist/
python3 -m http.server 3000

```

Application URL:

```text
http://localhost:3000
```

---
## Step 3: Dockerization

### Build Docker Image

```bash
docker build -t mindtrack-app .
```

### Run Docker Container

```bash
docker run -d -p 3000:3000 mindtrack-app
```

Verify:

```bash
http://localhost:3000
```

---

## Step 4: Push Image to Docker Hub Registry

### Login to Docker Hub in CLI

```bash

docker login -u <username>

```

### Tag Image

```bash
docker tag brain-tasks-app:latest \
<dockerhub-username>/mindtrack-app:latest
```

### Push Image

```bash
docker push \
<dockerhub-username>/mindtrack-app:latest
```

---

## Step 5: Create EKS Cluster

### Configure AWS CLI

```bash
aws configure
```

### Create Cluster

```bash
eksctl create cluster \
--name mindtrack-cluster \
--region <region> \
--nodes 2
```

### Verify Cluster

```bash
kubectl get nodes
```

---

## Step 6: Kubernetes Deployment

### Deployment YAML

File:

```text
deployment.yaml
```

### Service YAML

File:

```text
service.yaml
```

Apply Configuration:

```bash
kubectl apply -f deployment.yaml

kubectl apply -f service.yaml
```

Verify:

```bash
kubectl get deployments

kubectl get services

kubectl get pods
```

---

## Step 7: AWS CodeBuild

Created CodeBuild project with:

- Source: GitHub
- Environment: Managed Image (Amazon Linux)
- Build Specification: buildspec.yml

### Build Process

1. Pull source code
2. Build Docker image
3. Push image to Docker Hub
4. Generate deployment artifacts

---

## Step 8: AWS CodePipeline

Pipeline Stages:

### Source Stage

- GitHub Repository

### Build Stage

- AWS CodeBuild

### Deploy Stage

- AWS EKS

Pipeline automatically deploys the latest application version after successful build.

---

## Monitoring

AWS CloudWatch is used to monitor:

- Build logs
- Deployment logs
- Application logs

---

## Validation

Successfully verified:

- Local application execution
- Docker image build
- Docker image push to Docker Hub registry
- EKS cluster creation
- Kubernetes deployment
- Application access through LoadBalancer
- CI/CD pipeline execution

---

## Screenshots

Refer to the project documentation for detailed screenshots:

- Localhost Application
- Docker Build
- Docker Push
- Docker Hub Repository
- EKS Cluster
- Kubernetes Deployment
- Service LoadBalancer
- CodeBuild Success
- CodePipeline Success
- CloudWatch Logs

---

## Author

Raguraaman V M
