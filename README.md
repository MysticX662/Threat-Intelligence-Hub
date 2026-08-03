# Threat Intelligence Hub

A serverless threat-intelligence project that collects public security feeds, converts them into versioned JSON snapshots, and presents the data through a lightweight Next.js interface.

## Architecture

```text
External threat-intelligence sources
                │
                ▼
      Python collection scripts
                │
                ▼
       Normalized JSON snapshots
          (`api/v1/*.json`)
                │
                ▼
         Next.js web interface
```

The project separates data collection from presentation. Python scripts fetch and normalize external data, while the frontend reads static JSON files. No application server is required at runtime, which keeps deployment simple and makes each dataset snapshot reproducible through Git history.

## Repository Structure

```text
ThreatMonitoring/
├── src/               # Python collectors and processing scripts
├── api/
│   └── v1/            # Generated, versioned JSON feeds
├── web/               # Next.js and TypeScript frontend
├── requirements.txt   # Python dependencies
└── .env.example       # Required environment variables
```

## Local Setup

### 1. Clone the repository

```bash
git clone https://github.com/MysticX662/ThreatMonitoring.git
cd ThreatMonitoring
```

### 2. Configure and run the Python collectors

```bash
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate
pip install -r requirements.txt
cp .env.example .env
python src/<collector_name>.py
```

Each collector writes its processed output to `api/v1/<feed_name>.json`.

### 3. Run the web interface

```bash
cd web
npm install
npm run dev
```

Open the local URL printed by Next.js.

## Deployment Model

The generated `api/v1/` directory can be served from GitHub Pages, Vercel, or another static host. Because the feed outputs are stored as JSON files, each update creates a reviewable and reproducible snapshot rather than depending on a continuously running backend.

## What This Project Demonstrates

- Python-based data ingestion and normalization
- Static API design
- Reproducible, version-controlled datasets
- Next.js and TypeScript frontend development
- Separation of data pipelines from user-facing product layers

## Status

This is a technical project and reference implementation. Data quality, update frequency, and source availability depend on the external feeds configured by the operator.
