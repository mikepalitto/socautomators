# VS Code IDE Setup for Agentic SOC Development

**Purpose:** Configure VS Code + Claude Opus 4.6 for building AnalystBot01 and HUNTER agents  
**Target Phase:** Phase 1 Foundation  
**Last Updated:** February 5, 2026  
**Status:** ✅ Validated — setup executed and verified on Windows 11 / Python 3.13 / VS Code 1.97+

---

## ⚠️ Known Issues & Gotchas (Read Before Starting)

These issues were discovered during actual setup on February 5, 2026. Save yourself time — read these first.

| Issue                                                    | Impact                                                     | Fix                                                                                                                  |
| -------------------------------------------------------- | ---------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| `azure-mgmt-securityinsight` has no stable 2.0.0 release | `pip install` fails with "No matching distribution found"  | Use `>=2.0.0b2` and install with `pip install --pre`                                                                 |
| `msgraph-sdk` has deeply nested file paths               | Install fails on Windows with "No such file or directory"  | Enable Windows Long Paths: `HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem\LongPathsEnabled = 1` (requires admin) |
| Azure CLI is not bundled with Windows                    | All Azure API calls and `az login` fail                    | Install via `winget install --id Microsoft.AzureCLI`                                                                 |
| MCP config in original doc used fictional packages       | `@anthropic/mcp-server-sentinel` does not exist on npm     | Use `@azure/mcp` for Azure MCP Server; use `https://mcp.svc.cloud.microsoft/enterprise` for Graph/Entra              |
| Enterprise MCP Server requires Entra admin provisioning  | Graph/Entra MCP tools won't connect without one-time setup | Run `Grant-EntraBetaMCPServerPermission -ApplicationName VisualStudioCode` with admin role                           |
| `.venv` path uses forward slashes in settings            | Python interpreter not found on Windows                    | Use `${workspaceFolder}/.venv/Scripts/python.exe` (VS Code handles slash conversion)                                 |

---

## Prerequisites Checklist

Before installing extensions, ensure you have:

- [ ] VS Code 1.95+ installed
- [ ] Python 3.11+ installed and in PATH (tested with 3.13)
- [ ] Git installed and configured
- [ ] Windows Long Paths enabled (required for `msgraph-sdk` — see gotchas above)
- [ ] Azure subscription with:
  - [ ] Microsoft Sentinel workspace provisioned
  - [ ] Microsoft Defender XDR enabled
  - [ ] Appropriate RBAC permissions (Security Reader minimum)
- [ ] Azure CLI installed (`winget install --id Microsoft.AzureCLI`, then `az login`)

---

## Part 1 — Install Essential VS Code Extensions

Why this matters:
Without the right extensions, agents work blindly, MCP integrations break, and your scripts become harder to test, refine, and maintain.
Extensions add language intelligence, schema awareness, and tooling support for the real formats security engineers use every day.

### Core Development Extensions

🔧 1. Prettier — Code Formatter
Why it matters:
Vibe coding produces code fast — sometimes sloppy. Prettier formats everything automatically, keeping your scripts readable and consistent across your team.

What it does:

Auto-formats JavaScript, JSON, Markdown, YAML

Removes messy indentation

Keeps coding style uniform

🔧 2. PowerShell Extension
Why it matters:
PowerShell is essential for Windows forensics, Defender data gathering, registry analysis, log processing, and automation.

What it does:

Syntax highlighting

Debugging

Inline error detection

Copilot-aware context

🔧 3. Python + Pylance + Python Environments
Install all three — they work together.

Why it matters:
Python is the universal glue for security: enrichment, ML models, log parsing, API correlations, notebook analytics.

What they do:

Python: Lets you run Python scripts

Pylance: Deep IntelliSense + type checking

Python Environments: Manage per-project dependencies (critical later for MCP agents)

🔧 4. ESLint
Why it matters:
Even if you’re not writing JavaScript daily, many automations, agent actions, and API helpers use it.

What it does:

Lints JS/TS code

Prevents subtle runtime issues

Keeps your agent-side scripts clean

🔧 5. YAML Extension
Why it matters:
YAML is everywhere:

MCP configuration

Agent settings

Workflow definitions

CI/CD pipelines

IaC templates

What it does:

Syntax validation

Autocomplete

Error highlighting

🔧 6. KQL Assistant
The ultimate VS Code extension for Azure Log Analytics, Microsoft Sentinel, and Azure Data Explorer.
Why it matters:
Every security analyst lives in KQL.
This extension transforms VS Code into a first-class KQL IDE.

What it does:

Syntax validation

Schema-aware auto-complete (no more guessing table names)

Query formatting for readability

Quick fixes for broken or inefficient queries

Collapsible query blocks for long hunting notebooks

This is your bridge between VS Code and Sentinel’s query engine — essential for fast iteration, building detectors, and prototyping agents that pivot on KQL output.

### NEW: Agent Development Extensions

🔧 7. REST Client (humao.rest-client)
Why it matters:
AnalystBot01 and HUNTER agents need to call Microsoft Security APIs directly. REST Client lets you prototype and test API calls inline without leaving VS Code.

What it does:

- Send HTTP requests directly from `.http` files
- Test Sentinel, Defender XDR, and Graph API endpoints
- Store and reuse authentication tokens
- Validate API responses before coding

Example `.http` file for testing:

```http
### Get Sentinel Incidents
@baseUrl = https://management.azure.com
@subscriptionId = YOUR_SUBSCRIPTION_ID
@resourceGroup = YOUR_RG
@workspaceName = YOUR_WORKSPACE

GET {{baseUrl}}/subscriptions/{{subscriptionId}}/resourceGroups/{{resourceGroup}}/providers/Microsoft.OperationalInsights/workspaces/{{workspaceName}}/providers/Microsoft.SecurityInsights/incidents?api-version=2023-11-01
Authorization: Bearer {{$aadToken}}
```

🔧 8. DotENV (mikestead.dotenv)
Why it matters:
Agent configurations require API keys, workspace IDs, and tenant credentials. DotENV provides syntax highlighting and keeps secrets organized.

What it does:

- Syntax highlighting for `.env` files
- Prevents accidental secret commits (pair with .gitignore)
- Environment variable management across projects

Required `.env` structure for agents:

```env
# Azure/Sentinel Configuration
AZURE_TENANT_ID=your-tenant-id
AZURE_SUBSCRIPTION_ID=your-subscription-id
SENTINEL_WORKSPACE_ID=your-workspace-id
SENTINEL_RESOURCE_GROUP=your-rg

# API Authentication
AZURE_CLIENT_ID=your-app-registration-id
AZURE_CLIENT_SECRET=your-client-secret

# Agent Configuration
AGENT_LOG_LEVEL=INFO
AGENT_MODE=advisory
```

🔧 9. Azure MCP Server (ms-azuretools.vscode-azure-mcp-server)
Why it matters:
This is the bridge between Claude and your Azure resources. Without it, agents can't query Sentinel tables or interact with Azure services.

What it does:

- Provides MCP tooling for Azure resources
- Enables natural language queries against Azure
- Required for AnalystBot01 agent's data access

🔧 10. Microsoft Sentinel Extension (ms-security.ms-sentinel)
Why it matters:
Direct integration with Sentinel notebooks, analytics rules, and hunting queries from VS Code.

What it does:

- Jupyter notebook support for Sentinel
- Analytics rule management
- Hunting query development

---

Part 2 — Integrate VS Code With MCP Servers
Why this matters:
This is where your AI assistants gain access to your real environment — Sentinel tables, Entra identities, Graph data — through a safe, standardized protocol.

Without MCP servers:
Copilot can only chat.

With MCP servers:
Copilot can act.

We’ll integrate the two Microsoft MCP servers most relevant to security engineering.

1. Microsoft Sentinel Data Exploration MCP Server
   This MCP server allows AI to browse, describe, and query Sentinel table structures using natural language.

What it enables (real use cases):
🏴 Password-Spray Hunt
Agent can:

Select correct sign-in tables

Aggregate attempts by IP/user

Detect slow, distributed spray patterns

🛰 Impossible Travel Detection
Agent can:

Correlate logins

Compute geodistances

Flag unrealistic travel speeds

🔐 MFA Failure Spike Analysis
Agent can:

Parse MFA logs

Identify suspicious clusters

Compare against baseline trends

🕵️ Dormant Account Wake-Up
Agent can:

Identify long-inactive identities

Surface fresh activity

Build chronological timelines

How to install:
Open VS Code

Go to Extensions

Search: Microsoft Sentinel MCP Server

Install

Reload VS Code

2. Microsoft MCP Server for Enterprise (Entra + Microsoft Graph)
   This MCP server translates natural language into Microsoft Graph API calls so AI agents can interact with live identity data.

What it enables:
Pull user/activity details

Analyze risky sign-ins

Inventory devices/apps

Correlate Sentinel telemetry with identity context

Build end-to-end identity investigations

Why it matters:
Sentinel gives you the events.
Entra gives you the identity context.

Together, they enable agent-driven investigations.

How to install:
Open VS Code

Search: Microsoft MCP Server for Enterprise

Install

Reload

Part 3 — Verify MCP Tools Are Connected
Why this matters:
We must confirm Copilot can call tools before building your first agent in Step 3.

Test 1: Sentinel MCP Server
Open Copilot Chat:

“List the sign-in related tables available in my Sentinel data lake.”

You should see:

a tool call

returned schema metadata

Copilot summarizing the results

Test 2: Enterprise MCP Server (Graph)
Ask:

“What Graph query retrieves all Conditional Access policies?”

You should see:

a Graph API call

structured output

## If both tests pass, you’re ready.

## Part 4 — Project Structure for Phase 1 Agents

Create this folder structure in your workspace:

```
agentic-soc/
├── .env                          # Environment variables (git-ignored)
├── .env.example                  # Template for .env (safe to commit)
├── .gitignore                    # Exclude secrets and outputs
├── requirements.txt              # Python dependencies
├── pyproject.toml               # Project configuration
│
├── agents/
│   ├── __init__.py
│   ├── base_agent.py            # Shared agent foundation
│   │
│   ├── analyst_bot_01/           # AnalystBot01 Agent
│   │   ├── __init__.py
│   │   ├── agent.py             # Main agent logic
│   │   ├── triage.py            # Alert triage functions
│   │   ├── enrichment.py        # Context enrichment
│   │   ├── prompts/
│   │   │   ├── system.md        # System prompt
│   │   │   └── classification.md # Classification prompt
│   │   └── tests/
│   │       └── test_triage.py
│   │
│   └── hunter/                  # HUNTER Agent
│       ├── __init__.py
│       ├── agent.py             # Main agent logic
│       ├── query_generator.py   # KQL generation
│       ├── threat_mappings.py   # MITRE ATT&CK mappings
│       ├── prompts/
│       │   ├── system.md        # System prompt
│       │   └── kql_generation.md # Query generation prompt
│       └── tests/
│           └── test_queries.py
│
├── shared/
│   ├── __init__.py
│   ├── api_clients/
│   │   ├── sentinel_client.py   # Sentinel API wrapper
│   │   ├── defender_client.py   # Defender XDR API wrapper
│   │   └── graph_client.py      # Microsoft Graph wrapper
│   ├── models/
│   │   ├── alert.py             # Alert data models
│   │   ├── entity.py            # Entity models (User, Device, IP)
│   │   └── hunt_result.py       # Hunt result models
│   └── utils/
│       ├── kql_validator.py     # KQL syntax validation
│       └── logging_config.py    # Structured logging
│
├── queries/                     # KQL query library
│   ├── hunting/
│   │   ├── ransomware.kql
│   │   ├── credential_theft.kql
│   │   └── lateral_movement.kql
│   └── enrichment/
│       ├── user_context.kql
│       └── device_context.kql
│
├── tests/                       # Integration tests
│   ├── __init__.py
│   ├── test_api_connectivity.py
│   └── test_mcp_tools.py
│
└── docs/
    ├── SETUP.md
    └── API_REFERENCE.md
```

---

## Part 5 — Required Python Dependencies

Create `requirements.txt`:

```txt
# Azure SDK
azure-identity>=1.15.0
azure-mgmt-securityinsight>=2.0.0b2
azure-monitor-query>=1.2.0

# Microsoft Graph
msgraph-sdk>=1.0.0

# HTTP & API
httpx>=0.27.0
aiohttp>=3.9.0

# Data Processing
pandas>=2.2.0
pydantic>=2.6.0

# Logging & Monitoring
structlog>=24.1.0
rich>=13.7.0

# Testing
pytest>=8.0.0
pytest-asyncio>=0.23.0
pytest-cov>=4.1.0

# Development
python-dotenv>=1.0.0
ipykernel>=6.29.0
```

Install with:

```powershell
pip install -r requirements.txt
```

---

## Part 6 — VS Code Settings for Agent Development

Add to `.vscode/settings.json`:

```json
{
  "python.defaultInterpreterPath": "${workspaceFolder}/.venv/Scripts/python.exe",
  "python.analysis.typeCheckingMode": "basic",
  "python.analysis.autoImportCompletions": true,

  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "[python]": {
    "editor.defaultFormatter": "ms-python.python",
    "editor.formatOnSave": true
  },
  "[kql]": {
    "editor.defaultFormatter": "petstuk.kql-assistant"
  },

  "files.associations": {
    "*.kql": "kql",
    "*.kusto": "kql",
    "*.env*": "dotenv"
  },

  "rest-client.environmentVariables": {
    "local": {
      "baseUrl": "https://management.azure.com",
      "graphUrl": "https://graph.microsoft.com/v1.0"
    }
  },

  "yaml.schemas": {
    "https://json.schemastore.org/github-workflow.json": ".github/workflows/*.yml"
  }
}
```

---

## Part 7 — MCP Configuration for Claude

Create/update `.vscode/mcp.json` for Claude agent integration:

```json
{
  "servers": {
    "Azure MCP Server": {
      "command": "npx",
      "args": ["-y", "@azure/mcp@latest", "server", "start"]
    },
    "Microsoft MCP Server for Enterprise": {
      "type": "http",
      "url": "https://mcp.svc.cloud.microsoft/enterprise"
    }
  }
}
```

> **Note:** The Azure MCP Server uses `@azure/mcp` (official npm package). Auth is handled
> through `az login` — no API key env vars needed. The Enterprise MCP Server provides
> Microsoft Graph / Entra ID access and requires a one-time tenant provisioning via
> `Grant-EntraBetaMCPServerPermission`. See [Microsoft docs](https://learn.microsoft.com/en-us/graph/mcp-server/get-started).

---

## Part 8 — Verification Tests for AnalystBot01 & HUNTER

### Test 1: API Connectivity

Create `tests/test_api_connectivity.py`:

```python
"""Verify API connectivity for AnalystBot01 and HUNTER agents."""
import os
import pytest
from azure.identity import DefaultAzureCredential
from azure.monitor.query import LogsQueryClient

@pytest.fixture
def credential():
    return DefaultAzureCredential()

def test_sentinel_connection(credential):
    """Verify Sentinel workspace is accessible."""
    workspace_id = os.getenv("SENTINEL_WORKSPACE_ID")
    assert workspace_id, "SENTINEL_WORKSPACE_ID not set"

    client = LogsQueryClient(credential)
    # Simple query to verify connectivity
    response = client.query_workspace(
        workspace_id=workspace_id,
        query="SecurityAlert | take 1",
        timespan="PT1H"
    )
    assert response is not None
    print(f"✅ Sentinel connection successful")

def test_graph_connection(credential):
    """Verify Microsoft Graph is accessible."""
    from msgraph import GraphServiceClient

    client = GraphServiceClient(credential)
    # Verify we can access user info
    me = client.me.get()
    assert me is not None
    print(f"✅ Graph connection successful: {me.display_name}")
```

Run tests:

```powershell
pytest tests/test_api_connectivity.py -v
```

### Test 2: MCP Tool Verification

In Claude chat, verify these commands work:

**AnalystBot01 Agent Prerequisites:**

```
"List all tables in my Sentinel workspace that contain 'Alert' in the name"
```

Expected: Tool call to Sentinel MCP, returns table names like `SecurityAlert`, `AlertEvidence`

**HUNTER Agent Prerequisites:**

```
"Show me the schema for the DeviceProcessEvents table"
```

Expected: Tool call returns column names, types for process event hunting

**Identity Context (for enrichment):**

```
"Get the risky users from Entra ID Protection"
```

Expected: Graph API call returns risk detection data

---

## Part 9 — Quick Start: First AnalystBot01 Agent Test

Once setup is complete, test the foundation with this minimal agent:

Create `agents/analyst_bot_01/test_triage.py`:

```python
"""Minimal AnalystBot01 triage test."""
import os
from azure.identity import DefaultAzureCredential
from azure.monitor.query import LogsQueryClient
from dotenv import load_dotenv

load_dotenv()

def get_recent_alerts(hours: int = 24) -> list:
    """Fetch recent security alerts for triage."""
    credential = DefaultAzureCredential()
    client = LogsQueryClient(credential)

    query = f"""
    SecurityAlert
    | where TimeGenerated > ago({hours}h)
    | project
        TimeGenerated,
        AlertName,
        AlertSeverity,
        Description,
        Entities,
        Status
    | order by TimeGenerated desc
    | take 10
    """

    response = client.query_workspace(
        workspace_id=os.getenv("SENTINEL_WORKSPACE_ID"),
        query=query,
        timespan=f"PT{hours}H"
    )

    alerts = []
    for row in response.tables[0].rows:
        alerts.append({
            "time": row[0],
            "name": row[1],
            "severity": row[2],
            "description": row[3],
            "entities": row[4],
            "status": row[5]
        })

    return alerts

if __name__ == "__main__":
    alerts = get_recent_alerts()
    print(f"Found {len(alerts)} alerts for triage")
    for alert in alerts:
        print(f"  [{alert['severity']}] {alert['name']}")
```

Run:

```powershell
python agents/analyst_bot_01/test_triage.py
```

---

## Extension Installation Summary

Install all required extensions:

```vscode-extensions
esbenp.prettier-vscode,ms-vscode.powershell,ms-python.python,ms-python.vscode-pylance,dbaeumer.vscode-eslint,redhat.vscode-yaml,petstuk.kql-assistant,humao.rest-client,mikestead.dotenv,ms-azuretools.vscode-azure-mcp-server,ms-security.ms-sentinel
```

---

## Next Steps

After completing this setup:

1. **Run `az login`** — Authenticate to your Azure subscription
2. **Copy `.env.example` → `.env`** — Fill in real tenant/workspace/client IDs
3. **Provision Enterprise MCP** — One-time Entra admin task (see Part 7 note)
4. **Run verification tests** — `pytest tests/test_api_connectivity.py -v`
5. **Review [agentic-soc-agent-design.md](agentic-soc-agent-design.md)** — Understand AnalystBot01 and HUNTER specifications
6. **Build AnalystBot01 first** — Start with alert triage (advisory mode)
7. **Build HUNTER second** — Add query generation capabilities
8. **Test collaboration** — Verify AnalystBot01 can trigger HUNTER for hunting requests

---

## Appendix A — Implementation Log (February 5, 2026)

This section documents exactly what was done to bring a fresh VS Code workspace from zero to a fully configured Agentic SOC development environment. Use it as a runbook.

### Environment Baseline

| Component | Version Found         |
| --------- | --------------------- |
| Python    | 3.13.12               |
| Git       | 2.52.0                |
| VS Code   | 1.97+                 |
| Azure CLI | Not installed (fixed) |
| OS        | Windows 11            |

### Step-by-Step Execution

**1. Installed Azure CLI**

```powershell
winget install --id Microsoft.AzureCLI -e --accept-source-agreements --accept-package-agreements
# Installed v2.83.0
```

**2. Installed missing VS Code extensions**

Extensions already present: Prettier, PowerShell, Python, Pylance, Python Environments, ESLint, YAML, Azure MCP Server.

Extensions installed:

- `humao.rest-client` — REST Client
- `mikestead.dotenv` — DotENV
- `petstuk.kql-assistant` — KQL Assistant
- `ms-security.ms-sentinel` — Microsoft Sentinel

**3. Created `.gitignore`**

Covers `.env`, `.venv/`, `__pycache__/`, test coverage outputs, Jupyter checkpoints, OS artifacts.

**4. Created `.env.example`**

Template with all required variables: `AZURE_TENANT_ID`, `AZURE_SUBSCRIPTION_ID`, `SENTINEL_WORKSPACE_ID`, `SENTINEL_RESOURCE_GROUP`, `AZURE_CLIENT_ID`, `AZURE_CLIENT_SECRET`, `AGENT_LOG_LEVEL`, `AGENT_MODE`.

**5. Created `.vscode/settings.json`**

Python interpreter pointed to `.venv`, format-on-save enabled, KQL/dotenv file associations, REST Client environment variables configured.

**6. Created `requirements.txt`**

Fixed `azure-mgmt-securityinsight` to `>=2.0.0b2` (no stable 2.0 release exists).

**7. Created virtual environment & installed dependencies**

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
pip install --pre -r requirements.txt
```

⚠️ **Hit Windows Long Path error** on `msgraph-sdk` install. Fixed by enabling Long Paths:

```powershell
# Requires elevated (admin) PowerShell:
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" `
    -Name "LongPathsEnabled" -Value 1 -PropertyType DWORD -Force
```

After enabling, re-ran `pip install --pre -r requirements.txt` — all 98 packages installed successfully.

**8. Created `.vscode/mcp.json`**

Original doc referenced fictional npm packages (`@anthropic/mcp-server-sentinel`, `@anthropic/mcp-server-graph`). Replaced with:

- **Azure MCP Server**: `@azure/mcp` (official npm package, auth via `az login`)
- **Enterprise MCP Server**: `https://mcp.svc.cloud.microsoft/enterprise` (HTTP-based, requires Entra provisioning)

**9. Scaffolded project structure**

Created the full directory tree with starter files:

- `agents/` — `base_agent.py`, `analyst_bot_01/` (agent, triage, enrichment, prompts, tests), `hunter/` (agent, query_generator, threat_mappings, prompts, tests)
- `shared/` — `api_clients/` (sentinel, defender, graph), `models/` (alert, entity, hunt_result with Pydantic), `utils/` (kql_validator, logging_config with structlog)
- `queries/` — `hunting/` (ransomware, credential_theft, lateral_movement KQL), `enrichment/` (user_context, device_context KQL)
- `tests/` — `test_api_connectivity.py`, `test_mcp_tools.py`

### Final Workspace Structure

```
Other-jobs/
├── .env.example
├── .gitignore
├── .venv/                        # Python virtual environment
├── .vscode/
│   ├── settings.json             # Editor & language settings
│   └── mcp.json                  # MCP server configuration
├── agents/
│   ├── __init__.py
│   ├── base_agent.py
│   ├── analyst_bot_01/
│   │   ├── __init__.py
│   │   ├── agent.py
│   │   ├── triage.py
│   │   ├── enrichment.py
│   │   ├── prompts/
│   │   │   ├── system.md
│   │   │   └── classification.md
│   │   └── tests/
│   │       └── test_triage.py
│   └── hunter/
│       ├── __init__.py
│       ├── agent.py
│       ├── query_generator.py
│       ├── threat_mappings.py
│       ├── prompts/
│       │   ├── system.md
│       │   └── kql_generation.md
│       └── tests/
│           └── test_queries.py
├── shared/
│   ├── __init__.py
│   ├── api_clients/
│   │   ├── sentinel_client.py
│   │   ├── defender_client.py
│   │   └── graph_client.py
│   ├── models/
│   │   ├── alert.py
│   │   ├── entity.py
│   │   └── hunt_result.py
│   └── utils/
│       ├── kql_validator.py
│       └── logging_config.py
├── queries/
│   ├── hunting/
│   │   ├── ransomware.kql
│   │   ├── credential_theft.kql
│   │   └── lateral_movement.kql
│   └── enrichment/
│       ├── user_context.kql
│       └── device_context.kql
├── tests/
│   ├── __init__.py
│   ├── test_api_connectivity.py
│   └── test_mcp_tools.py
├── docs/
│   ├── IDE-setup.md
│   ├── agentic-soc-agent-design.md
│   └── top-threats-2026.md
├── scripts/
│   └── hello_security.py
├── requirements.txt
└── Other-jobs.code-workspace
```

### Remaining Manual Steps

1. Run `az login` to authenticate to Azure
2. Copy `.env.example` → `.env` and populate with real values
3. Provision Enterprise MCP Server (requires Entra admin — see Part 7)
4. Run `pytest tests/test_api_connectivity.py -v` to validate connectivity
