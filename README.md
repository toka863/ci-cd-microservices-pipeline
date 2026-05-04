# 🚀 Microservices CI/CD Pipeline with Jenkins Shared Library

A complete **CI/CD pipeline for microservices** using a **Jenkins Shared Library** — one reusable template that powers all services automatically from code push to container deployment.

---

## 📌 Architecture Overview

![CI/CD Architecture](./architecture/ci-cd-architecture.png)

### 🔗 Integrated Components

* GitHub → Source code hosting & webhook trigger
* Jenkins → CI/CD automation
* Jenkins Shared Library → Reusable pipeline template
* Docker → Image build & container runtime
* Amazon ECR → Private Docker registry
* Deployment Server (VM / EC2) → Runs containers

---

## ⚙️ How It Works

1. Developer pushes code to any service repository
2. GitHub webhook triggers Jenkins automatically
3. Jenkins loads the Shared Library (`jenkins-shared-library`)
4. The pipelineTemplate() function runs dynamically
5. All CI/CD stages execute
6. Docker image is built and pushed to ECR
7. Container is deployed and exposed on a unique port

---

## 🧾 Jenkinsfile (Per Service)

```groovy
@Library('jenkins-shared-library') _

pipelineTemplate(
    imageName: 'service-a',
    imageTag:  'v1.0',
    port:      '8081',
    region:    'us-east-1',
    accountId: '123456789012',
    ecrRepo:   'service-a'
)
```

---

## 🔧 Dynamic Parameters

| Parameter | Description           |
| --------- | --------------------- |
| imageName | Docker image name     |
| imageTag  | Image version         |
| port      | Host port for service |
| region    | AWS region            |
| accountId | AWS account ID        |
| ecrRepo   | ECR repository name   |

---

## 🏗️ Pipeline Stages

| # | Stage        | Tool    | Description         |
| - | ------------ | ------- | ------------------- |
| 1 | Checkout     | Git     | Clone repository    |
| 2 | Compile      | Maven   | `mvn clean compile` |
| 3 | Test         | Maven   | Run unit tests      |
| 4 | Package      | Maven   | Build JAR           |
| 5 | Docker Build | Docker  | Build image         |
| 6 | Login ECR    | AWS CLI | Authenticate        |
| 7 | Tag Image    | Docker  | Tag for ECR         |
| 8 | Push Image   | Docker  | Push to ECR         |
| 9 | Deploy       | Docker  | Run container       |

---

## 📦 Microservices & Ports

| Service   | Port | URL                   |
| --------- | ---- | --------------------- |
| service-a | 8081 | http://localhost:8081 |
| service-b | 8082 | http://localhost:8082 |
| service-c | 8083 | http://localhost:8083 |

---

## 🧩 Shared Library Structure

```text
jenkins-shared-library/
├── vars/
│   └── pipelineTemplate.groovy
└── README.md
```

---

## 🔧 Jenkins Setup

### 1. Register Shared Library

Manage Jenkins → System → Global Pipeline Libraries

| Field           | Value                                                 |
| --------------- | ----------------------------------------------------- |
| Name            | jenkins-shared-library                                |
| Default Version | main                                                  |
| Repository      | https://github.com/toka863/jenkins-shared-library.git |

---

### 2. Create Pipeline Jobs

* New Item → Pipeline
* Definition → Pipeline script from SCM
* Repository → service repo
* Branch → `main`
* Script Path → Jenkinsfile

---

### 3. Add AWS Credentials

Manage Jenkins → Credentials

| Field      | Value           |
| ---------- | --------------- |
| Kind       | AWS Credentials |
| ID         | aws-creds       |
| Access Key | your key        |
| Secret Key | your secret     |

---

## ☁️ AWS ECR Setup

1. Create repositories:

   * service-a
   * service-b
   * service-c

2. Repository URI format:

```
<account-id>.dkr.ecr.<region>.amazonaws.com/<repo-name>
```

---

## 🐳 Deployment Strategy

Each service runs as a container:

```bash
docker run -d -p HOST_PORT:8080 IMAGE
```

Example:

```bash
docker run -d -p 8081:8080 service-a
```

---

## 🛠️ Technologies Used

| Tool       | Purpose            |
| ---------- | ------------------ |
| Jenkins    | CI/CD              |
| Groovy     | Pipeline scripting |
| GitHub     | Source control     |
| Maven      | Build tool         |
| Docker     | Containerization   |
| Amazon ECR | Image registry     |
| AWS CLI    | Authentication     |
| Java 17    | Runtime            |

---

## 💡 Key Concepts

* ✅ Shared Library (Reusable pipelines)
* ✅ Dynamic configuration per service
* ✅ Multi-service architecture
* ✅ Docker lifecycle automation
* ✅ CI/CD automation with Jenkins
* ✅ AWS ECR integration

---

## 🚀 Future Improvements

* Kubernetes deployment (EKS)
* Auto rollback strategy
* Blue/Green deployment
* Monitoring (Prometheus + Grafana)

---

*Built as a real-world DevOps lab demonstrating CI/CD pipelines, containerization, and cloud deployment using Jenkins & AWS.*
