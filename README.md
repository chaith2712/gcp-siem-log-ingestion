Architecture

This project demonstrates a unified log ingestion pipeline using Google Cloud Logging → Pub/Sub → Cloud Functions → SIEM (Splunk/Elasticsearch).

Implementation
-Created GCP project and enabled required APIs
-Configured Cloud Logging sink to route VPC, firewall, and audit logs to Pub/Sub
-Implemented Python Cloud Function to decode and format logs for SIEM ingestion
-Used environment variables for secure SIEM endpoint and token configuration

Validation
-Generated real audit logs (Pub/Sub, IAM, Logging actions)
-Verified logs in Logs Explorer
-Confirmed Pub/Sub topic and subscription flow
-Validated decoded payload format in Cloud Function

Ethics & Security
-Followed principle of least privilege
-No sensitive data exposed
-SIEM tokens handled via environment variables

Deliverables
-Cloud Function code
-gcloud setup commands
-Sample ingested logs
-Screenshots for each stage
-README documentation
