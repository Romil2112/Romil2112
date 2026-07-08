## Hi, I'm Romil 👋

Software & Security Engineer with 3+ years building Python and C# backends, ETL pipelines, and security tooling on AWS and Azure. One of my projects integrates the Anthropic Claude API for security incident summaries, with concurrent batched calls and token-cost and latency instrumentation. MS Computer Science, Stevens Institute of Technology.

📍 Fremont, CA · 🎯 Open to Software / Backend / Security / Data Engineer roles · 🎓 MS Computer Science (Stevens)

### 🛠️ Tech Stack
![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=flat&logo=csharp&logoColor=white)
![Java](https://img.shields.io/badge/Java-007396?style=flat&logo=openjdk&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat&logo=postgresql&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=flat&logo=microsoftsqlserver&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat&logo=amazonwebservices&logoColor=white)
![Azure](https://img.shields.io/badge/Azure-0078D4?style=flat&logo=microsoftazure&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat&logo=docker&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?style=flat&logo=githubactions&logoColor=white)
![Splunk](https://img.shields.io/badge/Splunk-000000?style=flat&logo=splunk&logoColor=white)
![Claude](https://img.shields.io/badge/Claude%20API-D97757?style=flat&logo=anthropic&logoColor=white)

### Projects

[log-analyzer](https://github.com/Romil2112/log-analyzer) is a command-line tool that reads SSH `auth.log`, Windows Event Log CSVs, and Apache/Nginx access logs, then flags brute-force attempts, port scans, and web scans and tags each one with its MITRE ATT&CK technique. A rule engine catches the obvious patterns and an Isolation Forest model scores the rest for anomalies. The burst detector started as an O(n²) scan that compared every event against every other event; I rewrote it as a two-pointer sweep over a time-sorted window, and runtime on a 50k-line log dropped from 53 seconds to 0.8. It has 195 tests at 90% line coverage and can compile its detections to Splunk SPL, Elastic ES|QL, or Sentinel KQL.

[SOC-Dashboard](https://github.com/Romil2112/SOC-Dashboard) is the other end of that pipeline. log-analyzer POSTs each incident to its REST API, and the alerts land in a severity-ranked queue an analyst works through with one-click triage. It tracks MTTR, SLA-breach rate, and escalation rate, and draws them with Chart.js. The stats endpoint used to run a correlated subquery once per alert row; I replaced it with a single aggregate join and the query went from 24ms to 12ms at 20,000 alerts. It has 48 tests against a real PostgreSQL database at 95% line coverage.

[Face-Tracking-System](https://github.com/Romil2112/Face-Tracking-System) is a real-time face detector I built with Parshav. It runs a ResNet-SSD network and a Haar cascade together and merges the boxes with non-maximum suppression, since each catches faces the other misses. If a GPU backend fails it falls back from CUDA to OpenCL to CPU instead of crashing. Writing tests for the camera-failure path turned up a real bug: the recovery code called `ErrorHandler.handle_camera_error` without an instance bound to it, so every camera failure raised an `AttributeError` instead of resetting the camera. It has 204 tests at 96% line coverage.

log-analyzer and SOC-Dashboard are one loop. One detects and sends what it finds over HTTP; the other is where a person triages it. I checked that handoff end to end with 125 pushes, all returning HTTP 201.

### Work

I'm an IT Analyst at Unique Design Inc., building SSIS pipelines that move 8M+ rows a day into AWS RDS for 250+ Tableau users, plus Splunk triage. Before that I was at Dianco Inc. in NYC. [Full history on LinkedIn](https://linkedin.com/in/romil2112).

### Skills

Languages: Python, C#, Bash, SQL
Backend and data: Flask, FastAPI, PostgreSQL, SQL Server, SSIS ETL, psycopg2
Security: MITRE ATT&CK mapping, Sigma and pySigma, Splunk, Fernet encryption, threat-intel and GeoIP enrichment
Machine learning and vision: scikit-learn (Isolation Forest), OpenCV, ResNet-SSD, Haar cascades
Infrastructure: Docker, GitHub Actions, AWS RDS, Azure IaaS

### 📫 Connect
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/romil2112)
[![Resume](https://img.shields.io/badge/%F0%9F%93%84_Resume-PDF-555555?style=flat)](https://github.com/Romil2112/Romil2112/blob/main/Romil_Shah_Resume.pdf)
