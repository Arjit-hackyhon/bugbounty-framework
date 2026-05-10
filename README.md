# BugBounty Automation Framework

> **LEGAL NOTICE**: This framework is for **authorized bug bounty programs only**.  
> Never test assets without explicit written permission. Follow all program rules.

---

## Overview

A modular, AI-assisted bug bounty automation framework for ethical security researchers.  
Automates recon → fingerprinting → safe vulnerability checks → report generation.

## Architecture

```
bugbounty-framework/
├── main.py                  # CLI entry point
├── config.py                # Global configuration
├── requirements.txt
├── docker-compose.yml
├── Dockerfile
├── install.sh               # Kali/Ubuntu auto-installer
│
├── database/
│   ├── __init__.py
│   ├── models.py            # SQLAlchemy ORM models
│   └── db.py                # DB connection manager
│
├── modules/
│   ├── __init__.py
│   ├── recon.py             # Full recon pipeline
│   ├── vuln_checks.py       # Safe vulnerability checks
│   ├── ai_analysis.py       # AI prioritization engine (Claude API)
│   ├── report_gen.py        # HackerOne/Bugcrowd report generator
│   ├── scope_manager.py     # In-scope / out-of-scope filtering
│   └── screenshot.py        # Web app screenshotting
│
├── api/
│   ├── __init__.py
│   ├── app.py               # FastAPI backend
│   ├── routes/
│   │   ├── targets.py
│   │   ├── recon.py
│   │   ├── findings.py
│   │   └── reports.py
│   └── schemas.py           # Pydantic models
│
├── workers/
│   ├── __init__.py
│   ├── queue_manager.py     # Async task queue
│   └── scheduler.py         # Scheduled scans
│
├── targets/                 # Auto-created per target
│   └── example.com/
│       ├── recon/
│       ├── screenshots/
│       ├── nuclei/
│       ├── js/
│       ├── endpoints/
│       ├── reports/
│       └── logs/
│
└── templates/
    ├── h1_report.md.j2      # HackerOne report template
    └── bc_report.md.j2      # Bugcrowd report template
```

## Quick Start

```bash
# Install (Kali/Ubuntu)
chmod +x install.sh && sudo ./install.sh

# Docker
docker-compose up -d

# Full recon
python3 main.py -d target.com --full-recon

# Safe vulnerability scan
python3 main.py -d target.com --safe-scan

# Generate report
python3 main.py -d target.com --generate-report

# Start API dashboard backend
python3 main.py --api

# Add scope from HackerOne
python3 main.py --import-scope h1 --program program-name
```

## CLI Reference

| Flag | Description |
|------|-------------|
| `-d DOMAIN` | Target domain |
| `--full-recon` | Run complete recon pipeline |
| `--safe-scan` | Run safe vuln checks only |
| `--generate-report` | Generate markdown report |
| `--api` | Start FastAPI backend |
| `--import-scope` | Import scope (h1/bc) |
| `--rate-limit INT` | Requests per second (default: 10) |
| `--threads INT` | Concurrent workers (default: 5) |
| `--output DIR` | Custom output directory |
| `--ai-analyze` | Run AI analysis on findings |
| `--resume` | Resume interrupted scan |

## Ethical Guidelines

- **Always** verify you have authorization before scanning
- **Never** test out-of-scope assets  
- **Never** perform destructive exploitation  
- **Never** exfiltrate real user data  
- **Always** verify findings manually before reporting  
- **Follow** each program's specific rules and rate limits  

## Tool Dependencies

```
subfinder, assetfinder, amass, httpx, nuclei, katana,
waybackurls, gau, naabu, dnsx, anew, gf, trufflehog,
interactsh-client, gowitness
```

Run `install.sh` to install all dependencies automatically.
