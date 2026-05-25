# EKS CodeBuild GameZone

Containerized GameZone application deployed on Amazon EKS using Docker, Kubernetes, Amazon ECR, and AWS CodeBuild with automated container image build and registry integration.

---

# Project Overview

This project demonstrates how to:

* Containerize a static web application using Docker
* Push Docker images to Amazon ECR
* Deploy containers on Amazon EKS
* Expose the application using Kubernetes LoadBalancer Service
* Automate Docker image build and push using AWS CodePipeline and AWS CodeBuild

The project uses a simple gaming website called **GameZone** to demonstrate a real-world AWS DevOps deployment workflow.

---

# Architecture

```text
GitHub Repository
        ↓
AWS CodePipeline
        ↓
AWS CodeBuild
        ↓
Docker Image Build
        ↓
Amazon ECR
        ↓
Amazon EKS Cluster
        ↓
Kubernetes Deployment & Service
        ↓
AWS Load Balancer
        ↓
Browser Access
```

---

# Technologies Used

| Technology           | Purpose                      |
| -------------------- | ---------------------------- |
| Docker               | Containerization             |
| Amazon ECR           | Docker image registry        |
| Amazon EKS           | Managed Kubernetes cluster   |
| Kubernetes           | Container orchestration      |
| AWS CodeBuild        | Automated Docker image build |
| AWS CodePipeline     | CI workflow automation       |
| NGINX                | Web server                   |
| EC2                  | EKS worker nodes             |
| LoadBalancer Service | Public application access    |


---

# File Explanation

## Dockerfile

Used to create the Docker image for the GameZone application.

### Responsibilities

* Uses NGINX base image
* Removes default NGINX files
* Copies project files into web directory
* Exposes port 80
* Starts NGINX server

---

## buildspec.yml

Used by AWS CodeBuild.

### Responsibilities

* Login to Amazon ECR
* Build Docker image
* Tag Docker image
* Push image to ECR

---

## deployment.yml

Kubernetes Deployment manifest.

### Responsibilities

* Creates application Pods
* Maintains desired replica count
* Pulls Docker image from ECR
* Manages rolling deployments

---

## service.yml

Kubernetes Service manifest.

### Responsibilities

* Exposes application externally
* Creates AWS Load Balancer
* Routes traffic to application Pods

---

## aws-auth-backup.yaml

EKS authentication ConfigMap backup.

### Responsibilities

* Maps IAM roles to Kubernetes RBAC
* Allows worker nodes to join cluster
* Provides cluster access permissions

---

## index.html

Frontend GameZone application.

### Features

* Responsive gaming UI
* Navigation bar
* Hero section
* Game cards section
* Modern styling using HTML and CSS

---

# Deployment Workflow

## Step 1 — Push Source Code to GitHub

Developer pushes application code to GitHub repository.

---

## Step 2 — AWS CodePipeline Trigger

CodePipeline detects changes from GitHub and starts the CI workflow.

![AWS CodePipeline](screenshots/AWS%20CodePipeline.png)

---

## Step 3 — AWS CodeBuild Starts Build Process

CodeBuild reads the `buildspec.yml` file and starts Docker image build.

![AWS CodeBuild](screenshots/AWS%20CodeBuild%20History.png)

---

## Step 4 — Docker Image Stored in Amazon ECR

The Docker image is pushed to Amazon Elastic Container Registry.

![Amazon ECR](screenshots/Amazon%20ECR%20Repository.png)

---

## Step 5 — Amazon EKS Cluster

The application is deployed inside an Amazon EKS Kubernetes cluster.

![Amazon EKS Cluster](screenshots/EKS%20Cluster.png)

---

## Step 6 — EC2 Worker Nodes

EKS worker nodes run Kubernetes Pods.

![EKS Worker Nodes](screenshots/EC2%20Worker%20Nodes.png)

---

## Step 7 — Kubernetes Deployment and Pods

Kubernetes Deployment manages the application Pods.

### Kubernetes Resources

* Deployment
* Pods
* Service
* LoadBalancer

![Kubernetes Resources](screenshots/Kubernetes%20Resources.png)

---

## Step 8 — LoadBalancer Service

Kubernetes LoadBalancer Service exposes the application publicly.

![Load Balancer](screenshots/Load%20Balancer%20Details.png)

---

## Step 9 — Access Application from Browser

The application becomes accessible using the AWS Load Balancer DNS.

## GameZone Homepage

![GameZone Homepage](screenshots/GameZone%20Homepage.png)

---

## GameZone Games Section

![GameZone Games Section](screenshots/GameZone%20Games%20Section.png)

---

# Kubernetes Cluster Verification

## Deployment, Service and Pods

![Cluster Resources](screenshots/Kubernetes%20Cluster%20Resources.png)

---

# EKS aws-auth ConfigMap

The `aws-auth` ConfigMap is used to map IAM roles and users to Kubernetes RBAC.

![aws-auth ConfigMap](screenshots/EKS%20aws-auth%20ConfigMap.png)


---

# Important Kubernetes Concepts Used

| Concept         | Description                           |
| --------------- | ------------------------------------- |
| Deployment      | Manages Pods and replicas             |
| Pod             | Smallest deployable Kubernetes unit   |
| Service         | Exposes Pods internally or externally |
| LoadBalancer    | Creates AWS Load Balancer             |
| Replica         | Multiple Pod copies for availability  |
| imagePullPolicy | Controls image pulling behavior       |

---

# CI Workflow

## Automated

* GitHub integration
* Docker image build
* Docker image push to ECR
* Pipeline execution

## Deployment Management

Kubernetes deployment updates can be managed using rollout restart or deployment refresh after pushing updated images.

---




# Author

## Nasiroddin Khatib
