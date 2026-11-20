# SentinelLite — IOC Threat Intelligence & Correlation Platform

A local blue-team portfolio project for validating indicators of compromise (IOCs), optionally enriching them with VirusTotal, assigning a transparent preliminary score, and saving investigations in SQLite.

## Features
- Accepts IPv4/IPv6 addresses, domains, and MD5/SHA1/SHA256 hashes.
- Local syntax validation and basic contextual notes.
- Optional VirusTotal API v3 enrichment.
- Transparent preliminary score and verdict.
- FastAPI backend, responsive dark navy / neon teal dashboard, SQLite case history.
- JSON API and interactive API documentation.

## Important limitations
This is an educational lab project, not an enterprise detection product. A low score does **not** mean an IOC is safe. Local scoring is intentionally basic and must not be represented as a verified maliciousness determination. VirusTotal free API limits and terms apply. Submitted indicators are sent to VirusTotal when an API key is configured; do not submit confidential or internal indicators without authorization. Never commit API keys.

## Requirements
- Python 3.10+
- Kali Linux, Ubuntu, macOS, or Windows
- Internet connection only for installing packages and optional VirusTotal enrichment

## Run on Kali Linux
```bash
sudo apt update
sudo apt install -y python3 python3-venv python3-pip git
git clone https://github.com/YOUR-USERNAME/sentinellite-ioc-platform.git
cd sentinellite-ioc-platform
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload
```
Open http://127.0.0.1:8000

API documentation: http://127.0.0.1:8000/docs

## Optional VirusTotal setup
1. Obtain an API key from your VirusTotal account, subject to its current terms and quota.
2. Copy `.env.example` to `.env` and add the key:
```bash
cp .env.example .env
nano .env
```
3. Restart Uvicorn. The application automatically loads `.env`.

Without a key, local analysis and history still work.

## Test indicators
Use benign examples such as `8.8.8.8`, `example.com`, or a test hash consisting of 64 hexadecimal characters. These examples test parsing only; they are not claims about reputation.

## API
- `GET /api/health` — service health
- `POST /api/analyze` — JSON body: `{"indicator":"example.com"}`
- `GET /api/investigations` — recent saved investigations
- `GET /api/investigations/{id}` — one investigation

## GitHub publishing
Create an empty public GitHub repository named `sentinellite-ioc-platform`, then:
```bash
git init
git add .
git commit -m "Initial commit: SentinelLite IOC platform"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/sentinellite-ioc-platform.git
git push -u origin main
```
Do not add `.env`, API keys, database files, or private investigation data.

## Suggested next improvements
- Add unit tests and sample fixtures.
- Add analyst notes and case status.
- Add MISP integration.
- Add Sigma-compatible alert export.
- Add Docker deployment and CI checks.
