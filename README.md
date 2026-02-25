# 🛡️ Agentic SOC — AI-Powered Security Operations Center

> A portfolio of **7 AI agents** designed to transform SOC operations through a phased implementation approach — from advisory-only capabilities to collaborative autonomous orchestration — addressing Tier 1–3 threats while reducing MTTD, MTTR, and analyst burnout.

[![Platform](https://img.shields.io/badge/Platform-VS%20Code%20%2B%20Claude%20Opus%204.5-blue)]()
[![Integration](https://img.shields.io/badge/Integration-Microsoft%20Defender%20XDR%20%7C%20Sentinel%20%7C%20Data%20Lake-purple)]()
[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)]()
[![License](https://img.shields.io/badge/License-Private-lightgrey)]()

---

## Design Principles

| Principle                      | Description                                                             |
| ------------------------------ | ----------------------------------------------------------------------- |
| **Composable, not monolithic** | Each agent has a focused purpose; agents collaborate via shared context |
| **Governed by design**         | All agents operate within defined scope with audit trails               |
| **Human-in-command**           | Analysts maintain oversight; autonomy increases only with trust         |
| **Outcome-driven**             | Every agent targets measurable improvements in SOC metrics              |

---

## Agent Portfolio

| #   | Agent                 | Primary Function                   | Phase   | Autonomy                   |
| --- | --------------------- | ---------------------------------- | ------- | -------------------------- |
| 1   | **AnalystBot01**      | Alert Triage & Prioritization      | Phase 1 | Advisory → Semi-autonomous |
| 2   | **HUNTER**            | Threat Hunting Query Generation    | Phase 1 | Advisory                   |
| 3   | **INVESTIGATOR**      | Evidence Correlation & Analysis    | Phase 2 | Advisory → Semi-autonomous |
| 4   | **RISK ASSESSOR**     | CVE/Exploitability Analysis        | Phase 2 | Advisory                   |
| 5   | **SCRIBE**            | Incident Documentation & Reporting | Phase 2 | Semi-autonomous            |
| 6   | **IDENTITY GUARDIAN** | Identity Threat Specialist         | Phase 3 | Semi-autonomous            |
| 7   | **ORCHESTRATOR**      | Multi-Agent Coordination           | Phase 4 | Autonomous with guardrails |

---

## Threat Coverage

### Tier 1 — Critical Threats

| Threat                              | Primary Agent(s)                | Detection Products                            |
| ----------------------------------- | ------------------------------- | --------------------------------------------- |
| Ransomware & Human-Operated Attacks | AnalystBot01, INVESTIGATOR      | Defender for Endpoint, Defender XDR, Sentinel |
| Business Email Compromise           | AnalystBot01, IDENTITY GUARDIAN | Defender for Office 365, Purview              |
| Data Exfiltration                   | AnalystBot01, INVESTIGATOR      | Purview, Defender for Cloud Apps, Sentinel    |

### Tier 2 — High Priority Threats

| Threat                              | Primary Agent(s)     | Detection Products                         |
| ----------------------------------- | -------------------- | ------------------------------------------ |
| Infostealer Malware                 | AnalystBot01, HUNTER | Defender for Endpoint, Entra ID Protection |
| ClickFix Social Engineering         | AnalystBot01         | Defender for Office 365, SmartScreen       |
| Device Code Phishing                | IDENTITY GUARDIAN    | Entra ID Protection, Security Copilot      |
| Password Spray / Leaked Credentials | IDENTITY GUARDIAN    | Entra ID Protection, Defender for Identity |
| Phishing & Email Bombing            | AnalystBot01         | Defender for Office 365, Defender XDR      |
| Vulnerability Exploitation          | RISK ASSESSOR        | Defender Vulnerability Management          |

### Tier 3 — Emerging Threats

| Threat                                | Primary Agent(s)     | Detection Products                           |
| ------------------------------------- | -------------------- | -------------------------------------------- |
| AI-Enhanced Social Engineering        | AnalystBot01         | Defender for Office 365, Security Copilot    |
| Cloud Identity Abuse                  | IDENTITY GUARDIAN    | Entra ID Protection, Defender for Cloud Apps |
| Cloud Workload & Container Compromise | AnalystBot01, HUNTER | Defender for Cloud, Defender for Containers  |
| Access Broker Activity                | HUNTER, INVESTIGATOR | Defender for Identity, Sentinel              |

---

## Project Structure

```
├── agents/
│   ├── base_agent.py              # Shared base class for all agents
│   ├── analyst_bot_01/            # Phase 1 — Alert Triage & Prioritization
│   │   ├── agent.py
│   │   ├── enrichment.py
│   │   ├── triage.py
│   │   ├── prompts/
│   │   └── tests/
│   └── hunter/                    # Phase 1 — Threat Hunting Query Generation
│       ├── agent.py
│       ├── query_generator.py
│       ├── threat_mappings.py
│       ├── prompts/
│       └── tests/
├── shared/
│   ├── api_clients/               # Microsoft API integrations
│   │   ├── defender_client.py     #   Defender XDR
│   │   ├── graph_client.py        #   Microsoft Graph
│   │   └── sentinel_client.py     #   Microsoft Sentinel
│   ├── models/                    # Shared data models
│   │   ├── alert.py
│   │   ├── entity.py
│   │   └── hunt_result.py
│   └── utils/
│       ├── kql_validator.py
│       └── logging_config.py
├── queries/
│   ├── enrichment/                # Context enrichment KQL queries
│   └── hunting/                   # Threat hunting KQL queries
├── docs/                          # Architecture & design documentation
├── scripts/                       # Utility & test scripts
└── tests/                         # Integration & connectivity tests
```

---

## Implementation Roadmap

```
Phase 1 — Foundation (Weeks 1–4)
  ├── AnalystBot01: Alert triage, classification, priority scoring
  └── HUNTER: KQL query generation from natural language

Phase 2 — Investigation (Weeks 5–10)
  ├── INVESTIGATOR: Evidence correlation, timeline construction
  ├── RISK ASSESSOR: CVE contextualization, patch prioritization
  └── SCRIBE: Automated incident documentation

Phase 3 — Specialization (Weeks 11–16)
  └── IDENTITY GUARDIAN: Identity threat monitoring & response

Phase 4 — Orchestration (Weeks 17–24)
  └── ORCHESTRATOR: Multi-agent coordination with guardrails
```

---

## Target Metrics

| Metric                           | Baseline | Phase 1 | Phase 4    |
| -------------------------------- | -------- | ------- | ---------- |
| Mean Time to Detect (MTTD)       | 24 hrs   | 12 hrs  | **2 hrs**  |
| Mean Time to Respond (MTTR)      | 48 hrs   | 24 hrs  | **6 hrs**  |
| Mean Time to Triage              | 30 min   | 10 min  | **2 min**  |
| Alerts processed / analyst / day | 50       | 150     | **500**    |
| Investigation time / incident    | 4 hrs    | 2 hrs   | **30 min** |

---

## Getting Started

### Prerequisites

- **Python 3.11+**
- **VS Code** with Claude Opus 4.5 extension
- Access to **Microsoft Defender XDR**, **Microsoft Sentinel**, and **Microsoft Graph** APIs
- Azure AD app registration with appropriate permissions

### Installation

```bash
# Clone the repository
git clone https://github.com/<your-org>/agentic-soc.git
cd agentic-soc

# Create and activate virtual environment
python -m venv .venv
.venv\Scripts\activate   # Windows
# source .venv/bin/activate  # macOS/Linux

# Install dependencies
pip install -r requirements.txt

# Configure environment variables
cp .env.example .env
# Edit .env with your Azure credentials and API keys
```

### Configuration

Copy `.env.example` to `.env` and populate the required values:

```env
AZURE_TENANT_ID=your-tenant-id
AZURE_CLIENT_ID=your-client-id
AZURE_CLIENT_SECRET=your-client-secret
SENTINEL_WORKSPACE_ID=your-workspace-id
```

### Running Tests

```bash
pytest tests/ -v
```

---

## Tech Stack

| Category          | Technologies                                                |
| ----------------- | ----------------------------------------------------------- |
| **Language**      | Python 3.11+                                                |
| **AI Platform**   | Claude Opus 4.5 (via VS Code)                               |
| **Security APIs** | Microsoft Defender XDR, Microsoft Sentinel, Microsoft Graph |
| **Identity**      | Azure Identity SDK, Entra ID Protection                     |
| **Data**          | Pandas, Pydantic                                            |
| **Async**         | httpx, aiohttp                                              |
| **Observability** | structlog, Rich                                             |
| **Testing**       | pytest, pytest-asyncio, pytest-cov                          |

---

## Documentation

Full architecture and design documentation is available in the [`docs/`](docs/) directory:

- [Agent Architecture Design](docs/agentic-soc-agent-design.md) — Complete agent specifications, KQL examples, and collaboration patterns
- [AnalystBot01 Requirements](docs/analystbot01-requirements.md) — Detailed requirements for the Phase 1 triage agent
- [Architecture Diagram](docs/agentic-soc-diagram.mmd) — Mermaid diagram of system architecture
- [IDE Setup Guide](docs/IDE-setup.md) — Development environment configuration

---

## License

This project is private and proprietary. All rights reserved.
