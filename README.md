# Threat Intelligence Hub

> **Serverless threat-intelligence hub with Python collectors, versioned JSON feeds, and a Next.js interface.**

[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Framework](https://img.shields.io/badge/Next.js-14-black)](https://nextjs.org)
[![Python](https://img.shields.io/badge/Python-3.11-3776AB)](https://python.org)

---

## Overview & Problem Statement

Cybersecurity researchers and SOC analysts frequently require lightweight access to aggregated open-source threat intelligence (OSINT) feeds—such as malicious IP lists, active phishing domains, and vulnerability indicators (CVEs). Operating complex SIEM servers or heavy database pipelines is often overkill for small security teams or independent research.

**Threat Intelligence Hub** provides a decoupled, serverless architecture that uses automated Python scripts to pull public OSINT feeds, normalize raw indicator formats into structured JSON schema, and serve them via a static API interface built with Next.js and React.

---

## My Role

I am the **Creator and Developer** of Threat Intelligence Hub. I designed the automated collection pipeline, data normalization schemas, JSON feed versioning structure, and Next.js frontend UI.

---

## Architecture & Data Flow

```
[ Public OSINT Sources ] (Malicious IP Feeds, Phishing Feeds, CVE Feeds)
           │
           ▼
[ Python Collector Pipeline ]
   ├── Feed Fetcher & Rate Limiter
   ├── Indicator Normalizer (IP / Domain / Hash / CVE Schema)
   └── Deduplication & JSON Versioner
           │
           ▼
[ Versioned JSON Feed Files ] (`/public/api/v1/feeds/`)
           │
           ▼
[ Next.js Interface & Static API ] ──► [ Security Analyst Dashboard ]
```

---

## Key Features

- **Automated Collection**: Modular Python collectors ingest publicly available threat indicator feeds.
- **Normalized Schema**: Unifies disparate raw formats into standardized JSON payload structure:
  ```json
  {
    "indicator": "192.0.2.1",
    "type": "ipv4",
    "threat_category": "malware_c2",
    "first_seen": "2026-08-01T12:00:00Z",
    "source": "public_osint_feed"
  }
  ```
- **Serverless & Cost-Effective**: Generates versioned static JSON endpoints deployed easily to Vercel or GitHub Pages without server management.
- **Fast Dashboard UI**: Next.js client interface with real-time client-side searching, filtering by indicator type, and JSON export.

---

## Getting Started & Local Development

### Prerequisites
- Node.js 18+ & npm
- Python 3.10+

### Setup Instructions

1. **Clone repository**:
   ```bash
   git clone https://github.com/MysticX662/Threat-Intelligence-Hub.git
   cd Threat-Intelligence-Hub
   ```

2. **Run Python Feed Collector**:
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   pip install -r requirements.txt  # or run collectors directly
   python3 collectors/main.py
   ```

3. **Launch Local Frontend**:
   ```bash
   npm install
   npm run dev
   ```
   Open [http://localhost:3000](http://localhost:3000) to view the threat feed interface.

---

## Ethical Use & Security Boundary

- **Ethical OSINT Notice**: This tool ingests only publicly available open-source threat intelligence feeds for defensive research and educational purposes.
- **Zero Confidential Data**: No private infrastructure, customer data, internal organizational feeds, or secret API credentials are exposed in this codebase.
