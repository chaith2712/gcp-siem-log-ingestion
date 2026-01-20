📌Overview

This project implements a production-style security log ingestion pipeline on Google Cloud Platform (GCP), designed to forward security-relevant logs into a SIEM platform (Splunk / Elasticsearch compatible).

The solution demonstrates real-world SOC practices, including centralized logging, secure log routing, serverless processing, and SIEM-ready payload transformation — all built using native GCP services.

🏗️ Architecture
GCP Services
   ↓
Cloud Audit Logs (Admin Activity)
   ↓
Cloud Logging Sink
   ↓
Pub/Sub Topic
   ↓
Cloud Function (Python)
   ↓
SIEM (Splunk HEC / Elasticsearch-compatible)


Key Design Goals
-Real-time log ingestion
-Security-focused telemetry
-Scalable and serverless architecture
-Least-privilege and ethical testing

🔧 Technologies Used
-Google Cloud Logging
-Log Router (Sinks)
-Google Cloud Pub/Sub
-Cloud Functions (Python)
-Splunk HTTP Event Collector (HEC) format
-Git & GitHub (version control)

⚙️ Implementation Details
1️⃣ Log Generation
Security-relevant Admin Activity Audit Logs are generated automatically by GCP when administrative actions occur (e.g., Pub/Sub topic creation, IAM changes, logging configuration).
These logs are always enabled, making them ideal for SIEM ingestion and validation.

2️⃣ Log Routing
A Cloud Logging sink is configured to route selected logs to a Pub/Sub topic.
This decouples log producers from consumers and enables:
-Asynchronous processing
-High throughput
-Fault tolerance

3️⃣ Message Processing (Cloud Function)
A Python-based Cloud Function is implemented to:
-Consume Pub/Sub messages
-Decode Base64-encoded log payloads
-Parse structured JSON audit logs
-Transform them into SIEM-compatible format
The function prepares payloads following Splunk HTTP Event Collector (HEC) standards and supports Elasticsearch-style ingestion with minimal changes.

4️⃣ SIEM Integration (Design-Level)
Due to the use of paid SIEM platforms, the integration is implemented in a production-ready but simulated manner:
-Authentication headers handled via environment variables
-Payload format aligned with Splunk HEC requirements
-HTTP delivery logic included and deployment-ready
This mirrors real SOC development workflows, where pipelines are validated before live deployment.

📊 SIEM Index & Dashboard Design
SIEM Index
-Index Name: gcp_security
-Source: gcp-pubsub
-Sourcetype: gcp:audit

Key Fields Monitored
-protoPayload.serviceName
-protoPayload.methodName
-authenticationInfo.principalEmail
-resourceName
-timestamp
-severity

Example Dashboard Panels
-Administrative Actions Over Time
-Top GCP Services Generating Audit Logs
-IAM Policy Changes
-Resource Creation Events
-Privileged Operations Monitoring

🔍 Log Validation
Log ingestion was validated using real GCP Admin Activity Audit Logs, including:
-Pub/Sub topic creation
-Logging sink configuration
-Subscription creation
-IAM permission grants
These logs are security-critical and commonly prioritized in enterprise SIEM deployments.

Sample logs are included in the repository under:
sample-logs/

🧪 Infrastructure Reproducibility
Infrastructure setup is documented using gcloud CLI commands, covering:
-API enablement
-Pub/Sub topic creation
-Logging sink configuration
-IAM permission bindings
This provides Infrastructure-as-Code–style reproducibility without requiring Terraform.

🔐 Security & Ethical Considerations
-All testing was performed on a personal GCP project
-Only audit and administrative logs were used
-No unauthorized access, production systems, or sensitive data involved
-Secrets (SIEM tokens/endpoints) handled via environment variables

📁 Repository Structure

gcp-siem-log-ingestion/
├── cloud-function/
│ ├── main.py
│ └── requirements.txt
│
├── infra/
│ └── gcloud-commands.txt
│
├── sample-logs/
│ └── sample_audit_log.json
│
├── screenshots/
│ └── Fig1_...png
│
└── README.md


✅ Outcome
This project demonstrates:
-Strong understanding of cloud security logging
-Practical knowledge of SIEM ingestion pipelines
-Experience with Pub/Sub, serverless functions, and audit logs
-Ability to design scalable, ethical, and production-ready security solutions

🎯 Key Takeaway
This implementation reflects how modern SOC teams design and validate SIEM ingestion pipelines in cloud-native environments — prioritizing security relevance, scalability, and correctness over superficial deployments.
