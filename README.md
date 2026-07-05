I'm Romil Shah. I work as an IT analyst in Secaucus, NJ, writing C# and building SSIS pipelines that move about 8 million rows a day from Sybase and PostgreSQL into AWS RDS for more than 250 Tableau users. Outside of work I build security tooling. Three projects below fit together into a small detection-to-triage setup.

## Projects

[log-analyzer](https://github.com/Romil2112/log-analyzer) is a command-line tool that reads SSH `auth.log`, Windows Event Log CSVs, and Apache/Nginx access logs, then flags brute-force attempts, port scans, and web scans and tags each one with its MITRE ATT&CK technique. A rule engine catches the obvious patterns and an Isolation Forest model scores the rest for anomalies. The burst detector started as an O(n²) scan that compared every event against every other event; I rewrote it as a two-pointer sweep over a time-sorted window, and runtime on a 50k-line log dropped from 53 seconds to 0.8. It has 193 tests at 91% line coverage and can compile its detections to Splunk SPL, Elastic ES|QL, or Sentinel KQL.

[SOC-Dashboard](https://github.com/Romil2112/SOC-Dashboard) is the other end of that pipeline. log-analyzer POSTs each incident to its REST API, and the alerts land in a severity-ranked queue an analyst works through with one-click triage. It tracks MTTR, SLA-breach rate, and escalation rate, and draws them with Chart.js. The stats endpoint used to run a correlated subquery once per alert row; I replaced it with a single aggregate join and the query went from 24ms to 12ms at 20,000 alerts. It has 48 tests against a real PostgreSQL database at 95% line coverage.

[Face-Tracking-System](https://github.com/Romil2112/Face-Tracking-System) is a real-time face detector I built with Parshav. It runs a ResNet-SSD network and a Haar cascade together and merges the boxes with non-maximum suppression, since each catches faces the other misses. If a GPU backend fails it falls back from CUDA to OpenCL to CPU instead of crashing. Writing tests for the camera-failure path turned up a real bug: the recovery code called `ErrorHandler.handle_camera_error` without an instance bound to it, so every camera failure raised an `AttributeError` instead of resetting the camera. It has 204 tests at 96% line coverage.

log-analyzer and SOC-Dashboard are one loop. One detects and sends what it finds over HTTP; the other is where a person triages it. I checked that handoff end to end with 125 pushes, all returning HTTP 201.

## Work

I'm an IT analyst at Unique Design Inc. in Secaucus, NJ, working in C# and Bash across UNIX and Windows, with SQL Server, PostgreSQL, and Splunk. Before that I was at Dianco Inc. in NYC, where a Python firewall-log parser I wrote pushed detection time under 5 minutes and an SSIS sync I built cut sync errors by 95%. Full history is on [LinkedIn](https://linkedin.com/in/romil2112).

## Skills

Languages: Python, C#, Bash, SQL
Backend and data: Flask, FastAPI, PostgreSQL, SQL Server, SSIS ETL, psycopg2
Security: MITRE ATT&CK mapping, Sigma and pySigma, Splunk, Fernet encryption, threat-intel and GeoIP enrichment
Machine learning and vision: scikit-learn (Isolation Forest), OpenCV, ResNet-SSD, Haar cascades
Infrastructure: Docker, GitHub Actions, AWS RDS, Azure IaaS

## Contact

Email: shahromil71321@gmail.com · GitHub: [Romil2112](https://github.com/Romil2112) · LinkedIn: [romil2112](https://linkedin.com/in/romil2112)
