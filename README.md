# AWS DevSecOps Jenkins Pipeline

A hands-on Cloud Engineering and DevSecOps project for building a secure CI/CD pipeline using Jenkins, Docker, Terraform, AWS, Amazon ECR, Amazon ECS Fargate, Trivy, Checkov, CloudWatch, and automated deployment verification.

This project is the Jenkins version of my AWS DevSecOps CI/CD learning project.

The goal is to learn how Jenkins can automate the complete software delivery process from source code testing to secure AWS deployment.

---

# Project Goal

The main goal of this project is to build a complete Jenkins CI/CD pipeline that can:

```text
Source Code
    |
    v
Jenkins
    |
    v
Python Tests
    |
    v
Docker Build
    |
    v
Security Scanning
    |
    v
Terraform Validation
    |
    v
AWS Authentication
    |
    v
Amazon ECR
    |
    v
Terraform Deployment
    |
    v
Amazon ECS Fargate
    |
    v
Application Load Balancer
    |
    v
Deployment Verification
```

The project will gradually move from a basic Jenkins pipeline to a more advanced AWS DevSecOps deployment pipeline.

---

# Technologies

This project uses:

- Jenkins
- Jenkins Pipeline
- Jenkinsfile
- Python
- Flask
- Docker
- Terraform
- AWS CLI
- Amazon ECR
- Amazon ECS Fargate
- Application Load Balancer
- AWS IAM
- Amazon CloudWatch
- VPC Flow Logs
- AWS KMS
- Trivy
- Checkov
- Git
- GitHub

---

# Final Architecture

```text
Developer
    |
    v
GitHub Repository
    |
    v
Jenkins Server
    |
    +-------------------------+
    |                         |
    v                         v
Python Tests             Security Scans
                         Trivy + Checkov
    |                         |
    +------------+------------+
                 |
                 v
            Docker Build
                 |
                 v
          Amazon ECR
        Git SHA Image Tag
                 |
                 v
          Terraform Plan
                 |
                 v
      Infrastructure Safety
                 |
                 v
          Terraform Apply
                 |
                 v
              AWS VPC
                 |
                 v
      Application Load Balancer
                 |
                 v
        Amazon ECS Fargate
                 |
                 v
          Flask Container
                 |
          +------+------+
          |             |
          v             v
     CloudWatch     VPC Flow Logs
          |
          v
 Deployment Verification
```

---

# Jenkins Pipeline Flow

The final Jenkins pipeline will follow this structure:

```text
Checkout Source Code
        |
        v
Python Tests
        |
        v
Repository Security Scan
        |
        v
Docker Build
        |
        v
Container Security Scan
        |
        v
Terraform Format Check
        |
        v
Terraform Validate
        |
        v
Checkov IaC Scan
        |
        v
AWS Authentication
        |
        v
Amazon ECR Login
        |
        v
Build Production Image
        |
        v
Push Image to ECR
        |
        v
Terraform Plan
        |
        v
Terraform Apply
        |
        v
ECS Deployment
        |
        v
ECS Stability Check
        |
        v
Application Health Check
```

---

# Learning Roadmap

The project will be divided into labs.

## Lab 1 — Jenkins Basics

Learn:

- Jenkins installation
- Jenkins dashboard
- Jenkins jobs
- Pipeline jobs
- Jenkinsfile
- stages
- steps
- GitHub repository checkout

Target:

```text
GitHub
   |
   v
Jenkins
   |
   v
Basic Pipeline
```

---

## Lab 2 — Python CI

Add:

- Python setup
- dependency installation
- pytest
- automatic CI testing

Pipeline:

```text
Checkout
   |
   v
Install Dependencies
   |
   v
Python Tests
```

---

## Lab 3 — Docker CI

Add:

- Docker installation
- Docker build
- container execution
- application health test
- container cleanup

Pipeline:

```text
Python Tests
   |
   v
Docker Build
   |
   v
Run Container
   |
   v
Health Test
```

---

## Lab 4 — Trivy Security

Add:

- repository vulnerability scanning
- secret scanning
- Docker image scanning
- HIGH and CRITICAL security gate

Pipeline:

```text
Source
   |
   v
Trivy Repository Scan
   |
   v
Docker Build
   |
   v
Trivy Image Scan
```

---

## Lab 5 — Terraform and Checkov

Add:

- Terraform installation
- Terraform format checking
- Terraform initialization
- Terraform validation
- Checkov IaC security scanning

Pipeline:

```text
Terraform
   |
   +--> fmt
   |
   +--> validate
   |
   v
Checkov
```

---

## Lab 6 — Jenkins AWS Authentication and ECR

Add:

- AWS CLI
- Jenkins credentials
- AWS authentication
- Amazon ECR login
- Git SHA image tagging
- ECR image push

Pipeline:

```text
Jenkins
   |
   v
AWS Authentication
   |
   v
Docker Build
   |
   v
Amazon ECR
```

---

## Lab 7 — ECS Fargate Deployment

Terraform will create:

- VPC
- subnets
- Internet Gateway
- route table
- security groups
- Application Load Balancer
- target group
- ECS cluster
- ECS task definition
- ECS service
- CloudWatch logs
- VPC Flow Logs
- IAM roles
- KMS encryption

Architecture:

```text
Internet
   |
   v
Application Load Balancer
   |
   v
ECS Fargate
   |
   v
Flask Application
```

---

## Lab 8 — Deployment Reliability

Add more advanced DevOps controls:

- Jenkins deployment verification
- ECS service stability check
- ECS circuit breaker
- automatic rollback
- Terraform destructive-change detection
- running image verification
- health checks
- failure diagnostics
- CloudWatch log collection

Final deployment flow:

```text
Build
  |
  v
Scan
  |
  v
Push
  |
  v
Plan
  |
  v
Deploy
  |
  v
Verify
  |
  v
Monitor
```

---

# Application

The project uses a small Flask application.

Home endpoint:

```text
GET /
```

Expected response:

```json
{
  "message": "My AWS DevSecOps Pipeline"
}
```

Health endpoint:

```text
GET /health
```

Expected response:

```json
{
  "status": "healthy"
}
```

The health endpoint will be used by:

- Docker testing
- Application Load Balancer
- Jenkins deployment verification

---

# Docker

The application will run inside a Docker container.

Example flow:

```text
Application Code
      |
      v
Dockerfile
      |
      v
Docker Image
      |
      v
Trivy Scan
      |
      v
Amazon ECR
```

Docker images will use Git commit SHA tags.

Example:

```text
aws-devsecops-pipeline-app:abc123
```

This provides better release traceability.

---

# Security Scanning

## Trivy

Trivy will scan:

- repository dependencies
- secrets
- Docker images
- container vulnerabilities

Security gate:

```text
HIGH
CRITICAL
```

Serious findings can stop the pipeline.

---

# Infrastructure Security

## Checkov

Checkov will scan Terraform infrastructure before deployment.

The scan can detect issues such as:

- public exposure
- missing encryption
- weak networking rules
- missing logging
- insecure AWS configuration

Intentional learning-lab exceptions will be documented directly in Terraform.

---

# Terraform

Terraform will manage AWS infrastructure.

Main Terraform files may include:

```text
terraform/
├── alb.tf
├── backend.tf
├── cloudwatch.tf
├── ecs.tf
├── iam.tf
├── main.tf
├── outputs.tf
├── providers.tf
├── security-groups.tf
├── variables.tf
├── versions.tf
└── vpc.tf
```

---

# Terraform Remote State

Terraform state will be stored remotely in Amazon S3.

```text
Jenkins
   |
   v
Terraform
   |
   v
Amazon S3
   |
   +--> Remote State
   +--> State Locking
```

This prevents Terraform state from existing only on the Jenkins machine.

---

# Amazon ECR

Amazon ECR will store application Docker images.

Images will use Git commit SHA tags.

Example:

```text
123456789012.dkr.ecr.us-east-1.amazonaws.com/aws-devsecops-pipeline-app:abc123
```

Benefits:

- immutable application versions
- release traceability
- easier rollback
- easier troubleshooting

---

# Amazon ECS Fargate

The application will run using Amazon ECS Fargate.

Benefits:

- no EC2 server management
- managed container execution
- integration with ALB
- integration with CloudWatch
- deployment health monitoring

---

# Application Load Balancer

The Application Load Balancer will receive HTTP traffic and forward requests to ECS tasks.

```text
Internet
   |
   v
ALB :80
   |
   v
Target Group :5000
   |
   v
ECS Task
```

The ALB will use:

```text
/health
```

for target health checks.

---

# CloudWatch

CloudWatch will collect ECS application logs.

Example log group:

```text
/ecs/aws-devsecops-pipeline
```

CloudWatch will help troubleshoot:

- application crashes
- container startup problems
- deployment failures
- runtime errors

---

# VPC Flow Logs

VPC Flow Logs will provide network visibility.

They can help investigate:

- allowed traffic
- rejected traffic
- security group problems
- networking issues

---

# Jenkinsfile

The main Jenkins pipeline will be stored as code.

```text
Jenkinsfile
```

The Jenkinsfile will define stages such as:

```text
Checkout
Test
Security Scan
Docker Build
Terraform Validate
AWS Authentication
ECR Push
Terraform Plan
Terraform Apply
Deployment Verification
```

Using Pipeline as Code keeps Jenkins configuration inside GitHub.

---

# Expected Repository Structure

```text
aws-devsecops-jenkins-pipeline/
│
├── Jenkinsfile
│
├── app/
│   ├── app.py
│   ├── requirements.txt
│   └── tests/
│
├── docker/
│   └── Dockerfile
│
├── terraform/
│   ├── alb.tf
│   ├── backend.tf
│   ├── cloudwatch.tf
│   ├── ecs.tf
│   ├── iam.tf
│   ├── main.tf
│   ├── outputs.tf
│   ├── providers.tf
│   ├── security-groups.tf
│   ├── variables.tf
│   ├── versions.tf
│   └── vpc.tf
│
├── scripts/
│   ├── security-scan.sh
│   ├── deployment-check.sh
│   └── collect-diagnostics.sh
│
├── labs/
│   ├── lab-01-jenkins-basics/
│   ├── lab-02-python-ci/
│   ├── lab-03-docker-ci/
│   ├── lab-04-trivy-security/
│   ├── lab-05-terraform-checkov/
│   ├── lab-06-aws-ecr/
│   ├── lab-07-ecs-fargate/
│   └── lab-08-deployment-reliability/
│
├── .gitignore
│
└── README.md
```

---

# Jenkins Security

The project will follow several Jenkins security practices:

- avoid hard-coded credentials
- use Jenkins Credentials Store
- restrict AWS IAM permissions
- avoid exposing secrets in console logs
- use immutable Docker image tags
- scan dependencies and containers
- validate Terraform before deployment
- use security gates before AWS changes

---

# DevSecOps Pipeline

The final pipeline will apply security throughout the deployment lifecycle.

```text
Code
 |
 v
Test
 |
 v
Repository Scan
 |
 v
Docker Build
 |
 v
Container Scan
 |
 v
Terraform Validate
 |
 v
Checkov
 |
 v
AWS Authentication
 |
 v
ECR
 |
 v
Terraform Deployment
 |
 v
ECS
 |
 v
Deployment Verification
```

---

# Skills Demonstrated

This project demonstrates hands-on knowledge of:

- Jenkins
- Jenkins Pipeline
- Jenkinsfile
- CI/CD
- Docker
- AWS
- Terraform
- Infrastructure as Code
- Amazon ECR
- ECS Fargate
- Application Load Balancer
- IAM
- CloudWatch
- VPC networking
- VPC Flow Logs
- KMS
- Trivy
- Checkov
- DevSecOps
- container security
- deployment automation
- deployment troubleshooting
- cloud infrastructure security

---

# Portfolio Purpose

This repository is designed as a practical Cloud Engineering and Cloud Security portfolio project.

It demonstrates the ability to combine:

```text
Software
+
CI/CD
+
Containers
+
Infrastructure as Code
+
AWS
+
Security
+
Monitoring
```

into one automated delivery pipeline.

---

# Status

```text
Lab 1  — Jenkins Basics                    ⏳
Lab 2  — Python CI                         ⏳
Lab 3  — Docker CI                         ⏳
Lab 4  — Trivy Security                    ⏳
Lab 5  — Terraform + Checkov               ⏳
Lab 6  — AWS Authentication + ECR          ⏳
Lab 7  — ECS Fargate Deployment            ⏳
Lab 8  — Deployment Reliability            ⏳
```

The project will be built one lab at a time.
