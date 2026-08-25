# 🚀 Production-Grade CI/CD Pipeline with Jenkins Multibranch & GitOps

![CI/CD](https://img.shields.io/badge/CI%2FCD-Jenkins-blue?logo=jenkins)
![Docker](https://img.shields.io/badge/Container-Docker-blue?logo=docker)
![Kubernetes](https://img.shields.io/badge/Kubernetes-AWS%20EKS-blue?logo=kubernetes)
![GitOps](https://img.shields.io/badge/GitOps-ArgoCD-orange?logo=argo)

---

## 📌 Project Overview

In this project 🎥, I built a **production-grade CI/CD pipeline** using:

* **Jenkins Multibranch Pipeline**
* **Docker & DockerHub**
* **GitHub (feature branches & PR workflow)**
* **Argo CD (GitOps)**
* **AWS EKS (Kubernetes)**

This repository demonstrates how **real-world DevOps teams** design, automate, and deploy applications from **code commit to live production** using modern DevOps best practices.

🔗 **Repository:** [Multi-Branch-Production](https://github.com/damodar-dev/Multi-Branch-Production.git)

---

## 🎯 What You Will Learn

✔ How feature branches (`featureA`, `featureB`) are handled in CI/CD
✔ Pull Request (PR) based merge strategy using GitHub UI
✔ Jenkins Multibranch Pipeline auto-detection & execution
✔ Docker image build, tagging, and push to DockerHub
✔ Updating Kubernetes manifests via Git (GitOps model)
✔ Argo CD automated sync & deployment to AWS EKS
✔ Accessing the live application using LoadBalancer service

---

## 🔁 End-to-End Deployment Flow

```text
Developer
   ↓
Feature Branch (featureA / featureB)
   ↓
Pull Request → Merge to main (GitHub UI)
   ↓
Jenkins Multibranch Pipeline (CI)
   ↓
Build Docker Image + Push to DockerHub
   ↓
Update Image Tag in Git (K8s Manifest Repo)
   ↓
Argo CD Sync (GitOps)
   ↓
AWS EKS Deployment
   ↓
LoadBalancer URL → Live Application
```

---

## 🛠️ Tools & Technologies Used

| Tool                                | Purpose                                         |
| ------------------------------------ | ----------------------------------------------- |
| 🐙 **GitHub**                       | Feature branches, Pull Requests, Source Control |
| 🧩 **Jenkins Multibranch Pipeline** | Continuous Integration (CI)                     |
| 🐳 **Docker**                       | Containerization                                |
| 📦 **DockerHub**                    | Image Registry                                  |
| ☸️ **Kubernetes (AWS EKS)**         | Container Orchestration                         |
| 🔄 **Argo CD**                      | GitOps-based Continuous Deployment              |
| 🌐 **LoadBalancer Service**         | External Application Access                     |

---

## 📸 Hands-On Walkthrough (Screenshots)

Below is a step-by-step visual walkthrough of the entire pipeline setup, from infrastructure provisioning to live production deployment.

### 1️⃣ Infrastructure Setup

**Attach IAM Role to the EC2 instance** — required so the instance can call AWS APIs (EKS, EC2, IAM) without hardcoded credentials.

![IAM Role Attach](./screenshots/01-iam-role-attach.png)

**Install & start Jenkins** on the Ubuntu server.

![Jenkins Installed](./screenshots/02-jenkins-installed.png)

**Install kubectl, AWS CLI, and eksctl** — the core CLI tools needed to manage the EKS cluster.

![CLI Tools Installed](./screenshots/03-cli-tools-installed.png)

**Install & start Docker**, then add the `jenkins` user to the `docker` group so Jenkins can build/push images.

![Docker Installed](./screenshots/04-docker-installed.png)

---

### 2️⃣ AWS EKS Cluster Creation

**Create the EKS cluster** using `eksctl` in the `ap-south-2` (Hyderabad) region across two availability zones.

![eksctl Create Cluster](./screenshots/05-eksctl-create-cluster.png)

**Verify the cluster nodes** — the Jenkins/k8s server plus the managed EKS worker nodes, all in a `Running` state.

![EC2 Instances Running](./screenshots/06-ec2-instances-running.png)

---

### 3️⃣ Application Code & Repository Setup

**Push the initial application code** (`app.py`, `Dockerfile`, `requirements.txt`) to the `main` branch on GitHub.

![Initial Git Push](./screenshots/07-initial-git-push.png)

**Repository structure on GitHub** after adding the Docker and Kubernetes manifest files (`k8s/`).

![GitHub Repo Structure](./screenshots/08-github-repo-structure.png)

**Configure Jenkins credentials** for GitHub and DockerHub, used by the pipeline to clone the repo and push images.

![Jenkins Credentials](./screenshots/09-jenkins-credentials.png)

---

### 4️⃣ GitOps Setup with Argo CD

**Create the Argo CD Application**, pointing it at the GitHub repository and the `k8s/` manifest path on the `main` branch.

![Argo CD App Source](./screenshots/10-argocd-app-source.png)

**Argo CD auto-syncs the application** — status shows `Synced` and `Sync OK`, deploying the app, service, and pods onto EKS.

![Argo CD Synced](./screenshots/11-argocd-synced.png)

---

### 5️⃣ Jenkins Multibranch CI Pipeline in Action

**Jenkins pipeline stage view** — Checkout → Build & Push Image → Update K8s manifest, completing in seconds on every commit.

![Jenkins Pipeline Stages](./screenshots/12-jenkins-pipeline-stages.png)

**Verify the deployment on the cluster** using `kubectl` — deployments, replica sets, pods, and the LoadBalancer service all healthy.

![kubectl Get Resources](./screenshots/13-kubectl-get-resources.png)

**The live application** ("ShopEasy") accessible via the LoadBalancer URL exposed by the Kubernetes service.

![ShopEasy Live App](./screenshots/14-shopeasy-live-app.png)

---

### 6️⃣ Feature Branch Workflow — `featureA`

**Pull Request from `featureA` → `main`**, merged via the GitHub UI to trigger the CI/CD pipeline automatically.

![GitHub PR featureA Merge](./screenshots/15-github-pr-featureA-merge.png)

**New feature reflected in production** — wishlist button and an "Out of Stock" badge, deployed automatically after the merge.

![ShopEasy featureA Live](./screenshots/16-shopeasy-featureA-live.png)

---

### 7️⃣ Feature Branch Workflow — `featureB`

**Push the `featureB` branch** to GitHub from VS Code, ready for a pull request.

![Git Push featureB](./screenshots/17-git-push-featureB.png)

**Pull Request merged** for `featureB` into `main`, again auto-triggering the Jenkins → Argo CD → EKS pipeline.

![GitHub PR featureB Merged](./screenshots/18-github-pr-featureB-merged.png)

---

### 8️⃣ Final Production Application

**Updated homepage** with a welcome banner and new order-tracking / user-account sections, live after the `featureB` merge.

![ShopEasy Homepage Final](./screenshots/19-shopeasy-homepage-final.png)

**Final cluster verification** — confirming updated pods and the LoadBalancer service are healthy after the rollout.

![kubectl Final Verification](./screenshots/20-kubectl-final-verification.png)

**Live Order Tracking demo** on the deployed application, showcasing the new feature end-to-end in production.

![ShopEasy Order Tracking Demo](./screenshots/21-shopeasy-order-tracking-demo.png)

---

## 👥 Who Is This Project For?

✅ DevOps Beginners & Intermediates
✅ Jenkins Multibranch Pipeline Learners
✅ Kubernetes & AWS EKS Users
✅ DevOps Interview Preparation
✅ CI/CD & GitOps Enthusiasts

---

## 🌐 Connect With Me

* 💼 **LinkedIn:** [https://www.linkedin.com/in/sdamodararao/](https://www.linkedin.com/in/sdamodararao/)
* 🐙 **GitHub:** [https://github.com/damodar-dev](https://github.com/damodar-dev)

---

## ⭐ Support & Feedback

If this project helped you:

* ⭐ Star this repository
* 🍴 Fork it and try your own improvements
* 📢 Share it with fellow DevOps learners

Happy Learning & Automating! 🚀

— **S Damodararao**
