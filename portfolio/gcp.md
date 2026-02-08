---
layout: page
title: GCP Portfolio
permalink: /portfolio/gcp/
---

## GCP-Based Kubernetes (GKE Autopilot) CI/CD Deployment

React (Vite) + Spring Boot + MariaDB + Docker + GitHub Actions + Artifact Registry (GAR) + GKE Autopilot + External LoadBalancer + Cloud NAT

This project is a **hands-on DevOps implementation** built on **Google Cloud Platform (GCP)**.  
It operates a **Frontend (React/Vite)**, **Backend (Spring Boot)**, and **Database (MariaDB)** on **GKE Autopilot (Kubernetes)**,  
with a fully automated **CI/CD pipeline using GitHub Actions**.

- Source push → GitHub Actions trigger  
- Docker image build → Push to Artifact Registry (GAR)  
- Deployment to GKE Autopilot → **Runtime image pull by the cluster**  
- Frontend / Backend exposed externally via **Service type: LoadBalancer**  
- Cluster outbound traffic handled via **Cloud NAT (private egress only)**  


## 1. Overall Architecture Overview

The diagram below summarizes the complete **CI/CD and runtime flow** of the system  
(Dashed lines = CI/CD, Solid lines = Runtime traffic/operations)

**Final GKE Autopilot Architecture Diagram**

<img src="/assets/img/portfolio/architecture-gke-final.png" width="800">


## 2. End-to-End CI/CD and Runtime Flow

### ✔ Overall Flow (Step-by-step)

| Step | Description |
|------|-------------|
| 1 | Source code push to GitHub repository |
| 2 | GitHub Actions workflow triggered |
| 3 | Docker images built in GitHub Actions (Frontend / Backend) |
| 4 | Docker images pushed to Artifact Registry (GAR) |
| 5 | **Runtime image pull by GKE Autopilot** (during Pod creation/restart/rolling update) |
| 6 | Client → Frontend External LoadBalancer |
| 7 | Client/Admin → Backend External LoadBalancer (API access) |
| 8 | Frontend Pod → Backend Pod (internal API call) |
| 9 | Backend Pod → DB Pod (internal DB access) |
| 10 | Pod → Cloud NAT → Internet (Outbound only) |

> **Note:** Image pulling is a **runtime operation**, not part of CI/CD.  
> Therefore, it is represented as a **solid line**, not a dashed line.


## 3. GCP Resource Configuration (Project / Network / Registry / GKE)

### ✔ 3-1) Project Information

| Item | Value |
|------|--------------------|
| Project Name | matcha |
| Project ID | matcha-480312 |
| Region | asia-northeast3 |

Project information screenshot

<img src="/assets/img/portfolio/gcp-project-info.png" width="700">


### ✔ 3-2) VPC / Subnet Configuration

| Item | Value |
|------|--------------------|
| VPC | matcha-vpc (custom) |
| Region | asia-northeast3 |

#### ✔ Subnet Design

| Subnet | CIDR | Purpose |
|-------|------|---------|
| matcha-public-subnet | 10.0.1.0/24 | External entry point (LB External IP concept) |
| matcha-private-subnet | 10.0.2.0/24 | Reserved for future private resources (Cloud SQL / VM) |
| matcha-gke-subnet | 10.0.3.0/24 | GKE node and service network |

#### ✔ Secondary Range (Pod CIDR)

| Range | CIDR | Purpose |
|------|------|---------|
| GKE Pod Secondary Range | 10.219.0.0/17 | Dedicated Pod IP range |

Subnet and secondary range UI

<img src="/assets/img/portfolio/gcp-subnet-list.png" width="700">


### ✔ 3-3) Cloud NAT (Outbound Only)

| Item | Value |
|------|--------------------|
| Router | matcha-router |
| NAT | matcha-nat |
| Purpose | Handles outbound internet access for private cluster egress |

Cloud NAT configuration / static IP

<img src="/assets/img/portfolio/gcp-cloud-nat.png" width="700">


### ✔ 3-4) Artifact Registry (Docker Image Repository)

Artifact Registry is a **GCP-managed service**, not deployed inside a VPC or subnet.  
GitHub Actions pushes images to GAR, and GKE pulls them at runtime.

| Item | Value |
|------|--------------------|
| Service | Artifact Registry (GAR) |
| Repository | matcha-repo |
| Content | Frontend / Backend Docker images |
| Flow | GitHub Actions → GAR (push), GKE → GAR (pull) |

Artifact Registry image list

<img src="/assets/img/portfolio/gar-images.png" width="700">


## 4. GitHub Actions CI/CD Configuration

### ✔ 4-1) Successful Workflow Runs

GitHub Actions runs (success proof)

<img src="/assets/img/portfolio/gcp-github-actions-runs.png" width="700">


### ✔ 4-2) Repository Secrets

| Secret Name | Description |
|------------|-------------|
| GCP_PROJECT_ID | GCP Project ID |
| GCP_SA_KEY | Service Account JSON key |
| GKE_CLUSTER | GKE cluster name |
| GKE_LOCATION | GKE region |
| GAR_REPO | Artifact Registry repository |
| API_BASE_URL | Backend base URL for frontend |
| IMG_BASE_URL | Image upload base URL |

GitHub Secrets configuration

<img src="/assets/img/portfolio/github-secrets.png" width="700">


### ✔ 4-3) Workflow Summary

1) Checkout source  
2) Authenticate to GCP (Service Account)  
3) Docker build  
4) Push images to GAR  
5) Obtain GKE credentials  
6) Deploy via `kubectl apply`  
7) Verify rollout and status  

```yaml
name: Deploy to GKE Autopilot

on:
  push:
    branches: [ "main" ]

env:
  PROJECT_ID: ${{ secrets.GCP_PROJECT_ID }}
  GAR_LOCATION: asia-northeast3
  GAR_REPO: matcha-repo
  GKE_CLUSTER: ${{ secrets.GKE_CLUSTER }}
  GKE_LOCATION: ${{ secrets.GKE_LOCATION }}

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Authenticate to GCP
        uses: google-github-actions/auth@v2
        with:
          credentials_json: ${{ secrets.GCP_SA_KEY }}

      - name: Setup gcloud
        uses: google-github-actions/setup-gcloud@v2

      - name: Configure Docker
        run: gcloud auth configure-docker $GAR_LOCATION-docker.pkg.dev --quiet

      - name: Build & Push Images
        run: |
          docker build -t $GAR_LOCATION-docker.pkg.dev/$PROJECT_ID/$GAR_REPO/matcha-frontend:latest ./Matcha/frontend
          docker push $GAR_LOCATION-docker.pkg.dev/$PROJECT_ID/$GAR_REPO/matcha-frontend:latest

      - name: Get GKE Credentials
        run: gcloud container clusters get-credentials $GKE_CLUSTER --region $GKE_LOCATION --project $PROJECT_ID

      - name: Deploy Kubernetes
        run: kubectl apply -f Deploy/GCP/k8s/
```

## 5. Kubernetes Resource Design (GKE Autopilot)

In the GKE Autopilot environment, the **Frontend**, **Backend**, and **Database** are deployed as separate Kubernetes resources.  
Components that require external access (Frontend / Backend) are exposed using **Service type: LoadBalancer**,  
while the database is configured as **internal-only (ClusterIP)**.

### ✔ 5-1) Resource Summary

| Component | Deployment / Pod | Service Type | Public Access | Description |
|---------|------------------|--------------|---------------|-------------|
| Frontend | Deployment / Pod | LoadBalancer | ✅ | Provides user-facing UI via External IP |
| Backend | Deployment / Pod | LoadBalancer | ✅ | Provides REST API via External IP |
| DB (MariaDB) | Pod (or Stateful-style) | ClusterIP | ❌ | Internal database, cluster-only access |

`kubectl get pods` & `kubectl get svc`  
(Proof of running Pods, Service types, and assigned External IPs)

<img src="/assets/img/portfolio/kubectl-svc-pods.png" width="700">

**Key points**

- Services (LoadBalancers) are clearly separated from Pods to define **explicit entry points**
- The database is **not exposed externally** and is accessible only within the cluster
- Docker image pulling occurs at **runtime** (Pod creation / restart / rolling update), not during CI/CD execution

Kubernetes manifest directory structure

<img src="/assets/img/portfolio/k8s-yaml-tree.png" width="700">


## 6. Service Results (Live Validation)

- **Frontend (External LoadBalancer)**  
  `http://34.64.88.163/`

- **Backend (External LoadBalancer)**  
  `http://34.64.177.36/`

### ESG Introduction Page

<img src="/assets/img/portfolio/result-esg.png" width="700">

### Login and Core Feature Validation

<img src="/assets/img/portfolio/result-login.png" width="700">

### Admin Page (e.g., User Management)

<img src="/assets/img/portfolio/result-admin.png" width="700">


## 7. Project Structure

```text
PORTFOLIO
 ├── Deploy
 │   ├── AWS
 │   ├── GCP
 │   │   ├── k8s
 │   │   ├── docs
 │   │   └── README.md   ← This document
 │   └── NCP
 ├── Matcha              ← ESG Full-Stack Application
 └── README.md
