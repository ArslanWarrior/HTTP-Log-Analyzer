HTTP Log Analyzer

A lightweight, command-line tool written in Python that analyzes HTTP access logs and produces a summary report of traffic, errors, and endpoint performance.

Built as part of a cybersecurity & DevOps learning journey to understand how real-world log analysis works — without heavyweight tools like ELK or Splunk.

Project Overview

Web servers generate access logs on every request. These logs contain valuable information: who visited, what they requested, how long it took, and whether it succeeded.

This tool parses those logs, extracts the meaningful data, and presents a concise report:

- **Traffic volume** — total requests
- **Error rate** — how many requests failed (4xx / 5xx)
- **Top talkers** — which IPs sent the most requests
- **Slowest endpoints** — which routes have the highest average latency

It's useful for DevOps, SRE, and security engineers who need quick insights from log files.

Features

- **Zero dependencies** — only Python standard library
- **Memory-efficient** — streams the log file line by line using generators
- **Structured parsing** — uses a frozen dataclass (`LogRecord`) for clean records
- **Graceful error handling** — malformed lines are skipped, not crashed on
- **Concise report** — top IPs, error rate, and slowest endpoints at a glance

Requirements

- Python 3.8 or higher
- No external packages needed

Log Format

The tool expects each line to follow this format:
GET / 200 12 10.0.0.1
POST /login 401 15 10.0.0.3
GET /products 500 120 10.0.0.5



| Field | Description |
|-------|-------------|
| `METHOD` | HTTP method (GET, POST, etc.) |
| `PATH` | Requested endpoint (e.g., `/products`) |
| `STATUS` | HTTP status code (200, 404, 500, etc.) |
| `LATENCY_MS` | Response time in milliseconds |
| `IP` | Client IP address |


How to Run:

python log.py access.log
