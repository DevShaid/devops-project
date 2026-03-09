# DevOps-DevSecOps: AuditFlow Platform

[![Security Scan](https://github.com/DevShaid/devops-project/actions/workflows/build-single-service.yml/badge.svg)](https://github.com/DevShaid/devops-project/actions)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

An end-to-end (E2E) production-grade **Audit Logging Platform** deployed on **Kubernetes (K3s)**. This project demonstrates advanced automation across DevOps, SRE, and DevSecOps disciplines, focusing on security-first deployment and event-driven microservices.

## 🚀 Overview
The **AuditFlow Platform** is a Python-based microservices architecture that generates, processes, and visualizes audit events using an event-driven design powered by **RabbitMQ**.

### Key Technical Achievements:
* **Infrastructure as Code (IaC):** Automated cluster provisioning using **Terraform** and **Ansible**.
* **GitOps & Orchestration:** Managed K8s resources via **Helm** and **Kustomize** for environment-specific overlays.
* **Hardened CI/CD:** Integrated **SAST (Bandit)** and **SCA (Trivy)** directly into GitHub Actions.
* **Observability:** Full-stack monitoring with **Prometheus** and **Grafana**.

---

## 🏗 Architecture
AuditFlow utilizes an event-driven pattern to ensure decoupled service communication:

1.  **Generator:** Produces synthetic audit events.
2.  **Analysis:** Consumes RabbitMQ events and stores results in **PostgreSQL**.
3.  **Dashboard:** React/Python UI for real-time visualization.
4.  **Notification:** Triggers alerts via **Redis** and external webhooks based on analysis thresholds.



---

## 🛠 Technology Stack
| Category | Tools |
| :--- | :--- |
| **Cloud/Infra** | Terraform, Ansible, K3s (Kubernetes) |
| **CI/CD** | GitHub Actions, Docker Hub |
| **Backend** | Python, RabbitMQ, Redis, PostgreSQL |
| **Security** | Trivy (SCA/Container), Bandit (SAST) |
| **Monitoring** | Prometheus, Grafana |

---

## 📂 Project Structure
```text
├── .github/workflows   # CI/CD Pipelines (Build, Scan, Deploy)
├── infra/              # IaC (Terraform & Ansible)
├── k8s/                # Kubernetes (Helm Charts & Kustomize)
├── monitoring/         # Prometheus/Grafana Dashboards
├── src/                # Microservices (Python)
└── scripts/            # Automation & Helper scripts
🛡️ DevSecOps Integration
Security is integrated at every stage of the pipeline:

SAST: Automatic Python code analysis using Bandit during the build phase.

SCA: Dependency vulnerability scanning via Trivy to secure the supply chain.

Image Scanning: Docker images are scanned for CVEs before being pushed to the registry.

GitHub Security: Scan results are uploaded to the Security tab via SARIF for centralized tracking.

⚡ Getting Started
Prerequisites
Docker & Docker Compose

Terraform & Ansible

kubectl & helm

Quick Start
Provision Infrastructure:

Bash
cd infra/terraform && terraform apply
cd ../ansible && ansible-playbook site.yml
Deploy Application:

Bash
helm install auditflow ./k8s/charts/auditflow


Email: joji@jojees.net

Project Board: View GitHub Issues
