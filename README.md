## 🚀 End-to-End CI/CD Pipeline with Jenkins, SonarQube, Argo CD & AKS

![](https://user-images.githubusercontent.com/43399466/228301952-abc02ca2-9942-4a67-8293-f76647b6f9d8.png)

### 📌 Overview

This project demonstrates a **production-grade end-to-end CI/CD pipeline** implementing **GitOps principles** for deploying a Spring Boot application on **Azure Kubernetes Service (AKS)**.

The pipeline follows **industry best practices**:

* Jenkins handles **CI only**
* Git is the **single source of truth**
* Argo CD manages **continuous delivery**
* Kubernetes deployments are **fully automated**
* Rollbacks are performed via **Git revert**

---

### 🏗️ Architecture

```
Developer → GitHub (App Repo)
                |
                |  CI (Jenkins)
                |  - Maven Build
                |  - SonarQube Quality Gate
                |  - Unit Tests
                |  - Docker Image Build & Push
                |  - Update GitOps Manifests
                v
         GitHub (Manifests Repo)
                |
                |  CD (Argo CD – GitOps)
                v
        Azure Kubernetes Service (AKS)
```

---

### 🛠️ Tech Stack

* **Programming Language:** Java (Spring Boot)
* **CI:** Jenkins
* **Code Quality:** SonarQube (Quality Gates enforced)
* **Containerization:** Docker
* **Container Registry:** Docker Hub
* **CD / GitOps:** Argo CD
* **Orchestration:** Kubernetes
* **Cloud Platform:** Azure (AKS)
* **IaC / Config:** Kubernetes Manifests (GitOps)

---

### 🔁 CI Pipeline (Jenkins)

**Triggered on every GitHub push**

Stages:

1. Checkout source code
2. Maven build
3. SonarQube analysis
4. Quality Gate validation (fail pipeline if not passed)
5. Unit tests
6. Docker image build & push (tagged with Git commit SHA)
7. Update Kubernetes manifests repository (GitOps)

> Jenkins never runs `kubectl`.
> It only updates Git — following true GitOps principles.

---

### 🚢 CD Pipeline (Argo CD)

* Argo CD continuously watches the **manifests repository**
* Automatically syncs changes to AKS
* Performs rolling updates
* Self-heals drift
* Enables instant rollback via Git revert

---

### 🔄 Rollback Strategy

```bash
git revert <commit-id>
git push
```

Argo CD automatically rolls back the application in AKS —
**no Jenkins, no kubectl, no manual intervention**.

---

### 🔐 Security & Best Practices

* Fine-grained GitHub tokens
* Non-root Docker images
* SonarQube quality gate enforcement
* Immutable Docker image tags
* Git-based audit trail
* Separation of CI and CD responsibilities

---

### 📸 Proof of Deployment

* Application successfully running on AKS
* Pods pulling image tagged with Git commit SHA
* Argo CD showing **Synced & Healthy** state

---

### 📌 Key Learnings

* Real-world Jenkins pipeline design
* SonarQube webhook-based quality gates
* GitOps deployment model
* AKS production deployment patterns
* Debugging CI/CD issues in distributed systems

---

### 📂 Repositories

* **Application Repository:**
  `spring-boot-ci-cd`
* **GitOps Manifests Repository:**
  `spring-boot-manifests`

---

### 👨‍💻 Author

**Ayush Srivastava**
DevOps | Cloud | Kubernetes | CI/CD

---

