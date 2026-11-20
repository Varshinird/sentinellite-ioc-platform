# SentinelLite — IOC Threat Intelligence & Correlation Platform

A local blue-team portfolio project for validating Indicators of Compromise (IOCs), optionally enriching them with VirusTotal, assigning a transparent preliminary risk score, and saving investigations in SQLite.

## Features

- Accepts IPv4/IPv6 addresses, domains, and MD5/SHA1/SHA256 hashes.
- Local syntax validation and contextual security notes.
- Optional VirusTotal API v3 enrichment.
- Transparent preliminary risk scoring and verdict generation.
- FastAPI backend with a responsive dark navy and neon teal dashboard.
- SQLite-based investigation history.
- JSON REST API and interactive Swagger documentation.

## Technology Stack

- Python
- FastAPI
- SQLite
- HTML5
- CSS3
- JavaScript
- VirusTotal API v3 (optional)

## Project Structure

```text
sentinellite-ioc-platform/
├── app/
│   ├── main.py
│   └── static/
│       ├── app.js
│       ├── index.html
│       └── styles.css
├── data/
│   └── .gitkeep
├── .env.example
├── .gitignore
├── README.md
└── requirements.txt
```

## Requirements

- Python 3.10+
- Kali Linux, Ubuntu, macOS, or Windows
- Internet connection for package installation and optional VirusTotal enrichment

## Installation and Setup — Kali Linux

### 1. Clone the repository

```bash
git clone https://github.com/Varshinird/sentinellite-ioc-platform.git
cd sentinellite-ioc-platform
```

### 2. Install Python dependencies

```bash
sudo apt update
sudo apt install -y python3 python3-venv python3-pip
```

### 3. Create a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 4. Install project requirements

```bash
pip install -r requirements.txt
```

### 5. Start the application

```bash
uvicorn app.main:app --reload
```

### 6. Open the application

Dashboard: http://127.0.0.1:8000

API documentation: http://127.0.0.1:8000/docs

## Optional VirusTotal Integration

1. Obtain an API key from your VirusTotal account.
2. Copy the example environment file:

```bash
cp .env.example .env
nano .env
```

3. Add your key:

```env
VT_API_KEY=your_virustotal_api_key
```

4. Ensure the application loads `.env` using `python-dotenv` before reading the environment variable. Restart the application afterward.

Never commit your actual API key.

Without a configured key, local IOC analysis and investigation history can still work.

## Test Indicators

Use benign examples for basic parsing tests:

- `8.8.8.8`
- `example.com`
- A 64-character hexadecimal test hash

These examples test input validation, not threat reputation.

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/api/health` | Service health |
| POST | `/api/analyze` | Analyze an IOC |
| GET | `/api/investigations` | Retrieve investigation history |
| GET | `/api/investigations/{id}` | Retrieve a specific investigation |

Example request:

```json
{
  "indicator": "example.com"
}
```

## Security Considerations and Limitations

SentinelLite is an educational blue-team lab project, not an enterprise detection product.

- Risk scores are preliminary and based on basic local logic.
- A low score does not establish that an indicator is safe.
- VirusTotal usage is subject to its API limits and terms.
- Indicators submitted with an API key may be sent to VirusTotal.
- Do not submit confidential or internal indicators without authorization.
- Never publish API keys, database files, or private investigation data.

## Future Improvements

- Automated unit testing and sample fixtures.
- Analyst notes and case status tracking.
- MISP threat intelligence integration.
- Sigma-compatible alert export.
- Docker deployment.
- Continuous integration and automated security checks.

## Author

**R D Gunavarshini**

Cybersecurity | Blue Team | Threat Intelligence | Python

GitHub: https://github.com/Varshinird

