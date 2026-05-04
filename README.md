#CI/CD Microservices Pipeline Project
📌 Overview

This project demonstrates an end-to-end CI/CD pipeline using Jenkins, Docker, and GitHub. It follows a multi-service architecture with a centralized Jenkins Shared Library to reuse pipeline logic.

#Architecture

#Tech Stack
Jenkins (CI/CD automation)
Docker (containerization)
GitHub (source control)
Maven (build tool)
Linux environment

#Project Structure
service-a/  
service-b/  
service-c/  
shared-library/  
architecture/  
docs/
⚙️ Jenkins Shared Library

A centralized pipeline library is used to:

Build applications
Run tests
Build Docker images

This reduces duplication across services and improves maintainability.

#CI/CD Flow
Code pushed to GitHub
Jenkins triggers pipeline
Build stage (Maven)
Test stage (JUnit)
Docker image build
Deployment
