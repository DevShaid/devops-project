# AuditFlow Platform

End-to-end **audit logging platform** deployed on **Kubernetes (K3s)** demonstrating real-world **DevOps, SRE, and DevSecOps practices**.

The system generates, processes, analyzes, and visualizes audit events using an **event-driven microservices architecture**.

---

## Overview

AuditFlow is a distributed platform built to simulate how modern systems handle **audit logging, event processing, and alerting pipelines**.

The platform focuses on:

- Event-driven microservices
- Kubernetes-based infrastructure
- Automated CI/CD pipelines
- Integrated security scanning
- Observability and monitoring

All services run inside a **K3s Kubernetes cluster** and communicate asynchronously using **RabbitMQ**.

---

## Architecture

AuditFlow follows an **event-driven architecture** where services communicate through a message broker.

```
                         ┌──────────────────────────────┐
                         │        Kubernetes (K3s)      │
                         │   Container Orchestration    │
                         └───────────────┬──────────────┘
                                         │
                                         ▼
                         ┌──────────────────────────────┐
                         │      RabbitMQ Message Bus    │
                         │      (Event Broker Layer)    │
                         └───────────────┬──────────────┘
                                         │
          ┌──────────────────────────────┼──────────────────────────────┐
          │                              │                              │
          ▼                              ▼                              ▼
┌─────────────────────┐      ┌─────────────────────────┐      ┌─────────────────────┐
│ audit_event_generator│      │    audit-log-analysis   │      │ notification-service│
│                     │      │                         │      │                     │
│ Generates audit     │─────▶│ Consumes & analyzes     │─────▶│ Sends alerts       │
│ events              │      │ audit events            │      │ (webhooks/logs)    │
└─────────────────────┘      └─────────────┬───────────┘      └─────────────────────┘
                                           │
                                           ▼
                                ┌─────────────────────┐
                                │      Data Layer     │
                                └─────────┬───────────┘
                                          │
                    ┌─────────────────────┼─────────────────────┐
                    │                     │                     │
                    ▼                     ▼                     ▼
            ┌───────────────┐     ┌───────────────┐     ┌──────────────────┐
            │   PostgreSQL  │     │     Redis     │     │ event-audit      │
            │ Audit logs    │     │ Caching       │     │ dashboard        │
            │ Analysis data │     │ Temp data     │     │ (Web UI)         │
            └───────────────┘     └───────────────┘     └──────────────────┘
```

---

## Core Services

### `audit_event_generator`
Generates synthetic audit events and publishes them to RabbitMQ.

### `audit-log-analysis`
Consumes events, performs analysis, and stores results in PostgreSQL.

### `notification-service`
Subscribes to alert events and triggers notifications.

### `event-audit-dashboard`
Web interface used to visualize audit logs, alerts, and system metrics.

---

## Technology Stack

| Category | Tools |
|--------|--------|
| Infrastructure | Terraform, Ansible, K3s (Kubernetes) |
| CI/CD | GitHub Actions, Docker, Docker Hub |
| Backend | Python, RabbitMQ, PostgreSQL, Redis |
| Monitoring | Prometheus, Grafana |
| Security | Trivy, Bandit |

---

## DevSecOps Pipeline

Security scanning is integrated directly into the CI pipeline.

### Static Code Analysis (SAST)

Python code is scanned using **Bandit** to detect security issues.

### Dependency & Container Scanning (SCA)

**Trivy** scans:

- Python dependencies
- Container images
- Known CVEs

### Image Security

Docker images are scanned before being pushed to the container registry.

### GitHub Security Integration

Scan results are uploaded using **SARIF**, allowing vulnerabilities to appear in the repository **Security tab**.

---

## Observability

The platform includes full monitoring support:

- **Prometheus** for metrics collection
- **Grafana** dashboards for system visibility

Metrics include:

- Service CPU and memory usage
- RabbitMQ message throughput
- Database performance
- Kubernetes pod health

---

## Deployment

The platform is deployed using:

- **Terraform** for infrastructure provisioning
- **Ansible** for configuration management
- **Kubernetes (K3s)** for container orchestration

---

## License

MIT License
