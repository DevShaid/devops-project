## High-Level Architecture

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
│ Generates synthetic │      │ Consumes & analyzes     │      │ Sends alerts       │
│ audit events        │─────▶│ audit events            │─────▶│ (console/email)    │
│                     │      │ Detects anomalies       │      │                     │
└─────────────────────┘      └─────────────┬───────────┘      └─────────────────────┘
                                           │
                                           │
                                           ▼
                                ┌─────────────────────┐
                                │   Data Layer        │
                                └─────────┬───────────┘
                                          │
                    ┌─────────────────────┼─────────────────────┐
                    │                     │                     │
                    ▼                     ▼                     ▼
            ┌───────────────┐     ┌───────────────┐     ┌──────────────────┐
            │   PostgreSQL  │     │     Redis     │     │ event-audit      │
            │               │     │               │     │ dashboard        │
            │ Audit logs    │     │ Caching       │     │ (Web UI)         │
            │ Analysis data │     │ Temp data     │     │ Visualization    │
            └───────────────┘     └───────────────┘     └──────────────────┘
```
