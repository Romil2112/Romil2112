## Hi, I'm Romil 👋

Software engineer building production Python services - an AI-powered log analyzer, SOC dashboard, and computer-vision pipeline - with Claude API and Orkes Conductor orchestration. Open to backend, AI engineering, and security tooling roles.

📍 Fremont, CA · 🎓 MS Computer Science, Stevens Institute of Technology

### 🛠️ Tech Stack
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![Go](https://img.shields.io/badge/Go-00ADD8?style=flat&logo=go&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=flat&logo=csharp&logoColor=white)
![Java](https://img.shields.io/badge/Java-007396?style=flat&logo=openjdk&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white)
![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?style=flat&logo=elasticsearch&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat&logo=apachekafka&logoColor=white)
![gRPC](https://img.shields.io/badge/gRPC-4285F4?style=flat&logo=google&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=flat&logo=microsoftsqlserver&logoColor=white)
![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?style=flat&logo=kubernetes&logoColor=white)
![Terraform](https://img.shields.io/badge/Terraform-7B42BC?style=flat&logo=terraform&logoColor=white)
![GCP](https://img.shields.io/badge/GCP-4285F4?style=flat&logo=googlecloud&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazonwebservices&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoftazure&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-EE4C2C?style=flat&logo=pytorch&logoColor=white)
![OpenTelemetry](https://img.shields.io/badge/OpenTelemetry-000000?style=flat&logo=opentelemetry&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat&logo=githubactions&logoColor=white)
![Splunk](https://img.shields.io/badge/Splunk-000000?style=flat&logo=splunk&logoColor=white)
![Claude](https://img.shields.io/badge/Claude%20API-D97757?style=flat&logo=anthropic&logoColor=white)

### Projects

[log-analyzer](https://github.com/Romil2112/log-analyzer) is a command-line tool that reads SSH `auth.log`, Windows Event Log CSVs, and Apache/Nginx access logs, flags brute-force attempts, port scans, and web scans, and tags each one with its MITRE ATT&CK technique. A rule engine catches the obvious patterns; an Isolation Forest model and a PyTorch autoencoder score the rest for anomalies (swap backends with `--detector`). The burst detector started as an O(n²) scan; I rewrote it as a two-pointer sweep over a time-sorted window and runtime on a 50k-line log dropped from 53 seconds to 0.8. It compiles detections to Splunk SPL, Elastic ES|QL, or Sentinel KQL; can push over REST or gRPC to SOC-Dashboard with OTel traces propagated end to end; bulk-indexes into Elasticsearch; publishes to Kafka; and runs a multi-step AI agent with MITRE ATT&CK STIX-based RAG retrieval. It has 372 tests at 90% line coverage, with K8s/Helm manifests, GCP/Terraform deployment, and a `--gcs-bucket` flag for optional GCS report upload.

[SOC-Dashboard](https://github.com/Romil2112/SOC-Dashboard) is the other end of that pipeline. Alerts arrive over REST (Flask) or gRPC (a Go ingest microservice), or from a Kafka consumer — all three converge in a severity-ranked queue analysts triage with one click. It tracks MTTR, SLA-breach rate, and escalation rate with Chart.js. SSE live updates broadcast over Redis pub/sub so every Gunicorn worker pushes queue changes in real time. pgvector semantic similarity (`GET /api/alerts/<id>/similar`) groups related incidents by cosine distance. The stats endpoint originally ran a correlated subquery once per row; I replaced it with a single aggregate join and latency dropped from 24ms to 12ms at 20,000 alerts. The `/api/alerts` endpoints support server-side pagination (LIMIT/OFFSET, `idx_alerts_created_at` index, paginated envelope) so the queue stays fast at any scale. It has 229 tests (142 pytest + 87 Go), K8s HPA manifests, and GCP/Terraform deployment.

[Face-Tracking-System](https://github.com/Romil2112/Face-Tracking-System) is a real-time face detector I built with Parshav. YOLOv8-nano is the primary detector; a Haar cascade takes over as a last-resort fallback if YOLO is unavailable or fails at runtime. NMS de-duplicates boxes; a 5-frame temporal filter suppresses one-frame false positives. If a GPU backend fails it falls from CUDA to OpenCL to CPU instead of crashing. Writing tests for the camera-failure path turned up a real bug: the recovery code called `ErrorHandler.handle_camera_error` without an instance, so every failure raised `AttributeError` instead of resetting the camera. It exposes the detector as a FastAPI service with per-IP rate limiting, a Prometheus `/metrics` endpoint, bounded concurrency that returns 503 on overflow, and Claude Haiku triage notes on low-confidence detections. It has 224 tests at 96% line coverage, with K8s HPA manifests that scale on CPU and the custom `face_detection_backend_per_second` metric, and GCP/Terraform deployment.

log-analyzer and SOC-Dashboard are one loop. One detects and sends what it finds over HTTP; the other is where a person triages it. I checked that handoff end to end with 125 pushes, all returning HTTP 201.

### Work

I was a Software Developer at Unique Design Inc. (Apr 2025 - Jul 2026), building SSIS pipelines that move 8M+ rows a day into AWS RDS for 250+ Tableau users and writing Splunk triage workflows. Before that I was a Software Engineer at Dianco Inc. in NYC, writing Python automation to parse and correlate firewall logs and building ETL pipelines to sync PostgreSQL e-commerce data into SQL Server. [Full history on LinkedIn](https://linkedin.com/in/romil2112).

### Skills

Languages: Python, Go, C#, Java, Bash, SQL
Backend and data: Flask, FastAPI, gRPC, PostgreSQL, Redis, Elasticsearch, Kafka, SQL Server, SSIS ETL, psycopg2, pgvector
LLM & AI: Claude API, Orkes Conductor, agentic tool-use workflows, RAG (fastembed + pgvector), concurrent batched LLM calls, token-cost/p50/p95 instrumentation, prompt engineering
Security: MITRE ATT&CK mapping, Sigma and pySigma, Splunk/Elastic/Sentinel SIEM, Fernet encryption, HMAC, RBAC, threat-intel and GeoIP enrichment
Machine learning and vision: scikit-learn (Isolation Forest), PyTorch (autoencoder), YOLOv8, OpenCV, Haar cascades, mediapipe
Observability: OpenTelemetry (traces + OTLP export), Prometheus, structlog
Infrastructure: Kubernetes, Helm, Terraform, GCP (Cloud Run + Cloud Build + Cloud Storage), AWS (RDS, Lambda), Azure IaaS, Docker, GitHub Actions

### 📫 Connect
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/romil2112)
[![Resume](https://img.shields.io/badge/%F0%9F%93%84_Resume-PDF-555555?style=flat)](https://github.com/Romil2112/Romil2112/blob/main/Romil_Shah_Resume.pdf)
