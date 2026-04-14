# How I Set Up VS Code for Building AI Security Agents — And Every Gotcha I Hit Along the Way

**By Mike Palitto | February 5, 2026**

---

I'm building AI-powered security agents that triage alerts from Microsoft Sentinel and hunt for threats using KQL. The agents are called AnalystBot01 (alert triage) and HUNTER (proactive threat hunting), and they're designed to work alongside human analysts — not replace them.

Before writing a single line of agent code, I needed an IDE that could actually support the workflow: Python for logic, KQL for queries, MCP servers for live Azure access, and Claude as the AI backbone.

This post walks through the exact steps I followed to configure VS Code for agentic SOC development, including every error I hit and how I fixed it. If you're building AI agents that touch Microsoft Security APIs, this will save you hours.

---

## What We're Building Toward

Two AI agents:

- **AnalystBot01** — Monitors incoming Sentinel alerts, classifies them (true positive, false positive, benign), enriches them with identity and device context, and recommends response actions.
- **HUNTER** — Generates KQL hunting queries based on threat hypotheses, maps activity to MITRE ATT&CK, and surfaces indicators of compromise.

Both agents run in **advisory mode** — they suggest, they don't act. The human analyst stays in the loop.

To make this work, VS Code needs to be more than a text editor. It needs to be a security engineering workbench: connected to Azure, aware of KQL syntax, integrated with MCP servers, and wired into a Python environment with all the right SDKs.

---

## Prerequisites

Before you start, make sure you have:

- **VS Code 1.95+**
- **Python 3.11+** (I'm on 3.13 — works fine)
- **Git** installed and configured
- **An Azure subscription** with Microsoft Sentinel provisioned and Defender XDR enabled
- **Security Reader RBAC** (minimum) on your Azure resources

One thing _not_ pre-installed on my machine: **Azure CLI**. That caused problems later. Install it upfront:

```powershell
winget install --id Microsoft.AzureCLI -e --accept-source-agreements --accept-package-agreements
```

---

## Step 1: Install the Extensions

VS Code extensions fall into two categories for this project: **core development tools** and **agent-specific integrations**.

### Core Development Extensions

These are the foundation. You probably have some already:

| Extension           | ID                             | Why It Matters                                                   |
| ------------------- | ------------------------------ | ---------------------------------------------------------------- |
| Prettier            | `esbenp.prettier-vscode`       | Auto-formats JSON, YAML, Markdown. Keeps agent configs readable. |
| PowerShell          | `ms-vscode.powershell`         | Windows forensics, log processing, Defender automation.          |
| Python              | `ms-python.python`             | Run Python scripts — the core language for agent logic.          |
| Pylance             | `ms-python.vscode-pylance`     | Deep IntelliSense, type checking. Catches bugs before runtime.   |
| Python Environments | `ms-python.vscode-python-envs` | Manage per-project virtual environments.                         |
| ESLint              | `dbaeumer.vscode-eslint`       | Lint JS/TS — useful for API helpers and automations.             |
| YAML                | `redhat.vscode-yaml`           | Validates MCP configs, CI/CD pipelines, IaC templates.           |

### Agent Development Extensions

These are specific to security engineering and agent work:

| Extension          | ID                                      | Why It Matters                                                                                        |
| ------------------ | --------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| KQL Assistant      | `petstuk.kql-assistant`                 | Syntax checking, schema-aware autocomplete, formatting for KQL queries. Turns VS Code into a KQL IDE. |
| REST Client        | `humao.rest-client`                     | Test Sentinel/Defender/Graph API calls from `.http` files without leaving the editor.                 |
| DotENV             | `mikestead.dotenv`                      | Syntax highlighting for `.env` files where you store API keys and workspace IDs.                      |
| Azure MCP Server   | `ms-azuretools.vscode-azure-mcp-server` | The bridge between Claude and Azure — lets agents query Sentinel tables.                              |
| Microsoft Sentinel | `ms-security.ms-sentinel`               | Jupyter notebook support, analytics rule management, hunting query development.                       |

Install all of them in one shot:

```
esbenp.prettier-vscode,ms-vscode.powershell,ms-python.python,ms-python.vscode-pylance,dbaeumer.vscode-eslint,redhat.vscode-yaml,petstuk.kql-assistant,humao.rest-client,mikestead.dotenv,ms-azuretools.vscode-azure-mcp-server,ms-security.ms-sentinel
```

---

## Step 2: Create the Project Skeleton

Security agents need structure. Here's the layout I settled on:

```
your-workspace/
├── .env.example          # Template for secrets (safe to commit)
├── .gitignore            # Keep .env and .venv out of Git
├── .venv/                # Python virtual environment
├── .vscode/
│   ├── settings.json     # Editor config
│   └── mcp.json          # MCP server connections
├── agents/
│   ├── base_agent.py     # Shared agent foundation
│   ├── analyst_bot_01/   # AnalystBot01 agent (triage, enrichment)
│   └── hunter/           # HUNTER agent (KQL generation, threat mapping)
├── shared/
│   ├── api_clients/      # Wrappers for Sentinel, Defender, Graph APIs
│   ├── models/           # Pydantic data models (Alert, Entity, HuntResult)
│   └── utils/            # KQL validation, structured logging
├── queries/
│   ├── hunting/          # KQL templates: ransomware, credential theft, lateral movement
│   └── enrichment/       # KQL templates: user context, device context
├── tests/                # API connectivity and MCP verification tests
└── requirements.txt      # Python dependencies
```

The key design decisions:

- **Separate agents from shared code** — AnalystBot01 and HUNTER share API clients and models, but their logic is independent.
- **Prompts live alongside agents** — Each agent has a `prompts/` folder with its system prompt and task-specific prompts. This keeps prompt engineering version-controlled.
- **KQL queries are first-class files** — `.kql` files get syntax highlighting and validation from the KQL Assistant extension.
- **Pydantic models for everything** — Alerts, entities, and hunt results are all typed. No more guessing what shape the data is.

---

## Step 3: Create .gitignore and Environment Template

**`.gitignore`** — Protect your secrets:

```gitignore
.env
.env.local
.venv/
__pycache__/
*.py[cod]
.pytest_cache/
htmlcov/
.coverage
.ipynb_checkpoints/
```

**`.env.example`** — Template that's safe to commit:

```env
# Azure / Sentinel Configuration
AZURE_TENANT_ID=your-tenant-id
AZURE_SUBSCRIPTION_ID=your-subscription-id
SENTINEL_WORKSPACE_ID=your-workspace-id
SENTINEL_RESOURCE_GROUP=your-rg

# API Authentication (App Registration)
AZURE_CLIENT_ID=your-app-registration-id
AZURE_CLIENT_SECRET=your-client-secret

# Agent Configuration
AGENT_LOG_LEVEL=INFO
AGENT_MODE=advisory
```

Copy it to `.env` and fill in your real values. Never commit `.env`.

---

## Step 4: Configure VS Code Settings

Create `.vscode/settings.json`:

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
  }
}
```

Key settings to note:

- **Python interpreter** points to the `.venv` we'll create next.
- **File associations** map `.kql` files to the KQL language mode so the KQL Assistant kicks in.
- **REST Client** environment variables pre-populate Azure Management and Graph API base URLs.

---

## Step 5: Create the Virtual Environment — And the First Gotcha

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

Now install dependencies. Here's the `requirements.txt`:

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

Install:

```powershell
pip install --pre -r requirements.txt
```

### 🚨 Gotcha #1: `azure-mgmt-securityinsight` Has No Stable 2.0

If you use `>=2.0.0` (without the `b2` pre-release tag), pip will fail with:

```
ERROR: No matching distribution found for azure-mgmt-securityinsight>=2.0.0
```

**Fix:** Use `>=2.0.0b2` and install with the `--pre` flag.

### 🚨 Gotcha #2: `msgraph-sdk` Hits Windows Path Limits

The Microsoft Graph SDK generates deeply nested folder structures that exceed the Windows 260-character path limit. You'll see:

```
ERROR: [Errno 2] No such file or directory: '...very_long_path...get_response.py'
HINT: This error might have occurred since this system does not have Windows Long Path support enabled.
```

**Fix:** Enable Long Paths (requires admin PowerShell):

```powershell
New-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem" `
    -Name "LongPathsEnabled" -Value 1 -PropertyType DWORD -Force
```

Then re-run `pip install --pre -r requirements.txt`. It'll pick up right where it left off.

---

## Step 6: Configure MCP Servers — And the Second Major Gotcha

MCP (Model Context Protocol) is what turns Claude from a chatbot into an agent that can _act_ on your Azure environment. Without MCP, Claude can only generate code. With MCP, it can query your Sentinel tables, read Entra identity data, and interact with live services.

Create `.vscode/mcp.json`:

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

### 🚨 Gotcha #3: Beware Fictional Package Names

Many guides and early documentation reference MCP package names like `@anthropic/mcp-server-sentinel` or `@anthropic/mcp-server-graph`. **These don't exist.** The actual packages are:

- **Azure MCP Server**: `@azure/mcp` (official Microsoft npm package)
- **Enterprise MCP Server**: A hosted HTTP service at `https://mcp.svc.cloud.microsoft/enterprise`

The Azure MCP Server authenticates through your `az login` session — no API keys in environment variables needed.

### Enterprise MCP Requires Admin Provisioning

The Enterprise MCP Server (for Graph / Entra ID access) requires a one-time tenant setup by someone with Application Administrator or Cloud Application Administrator role:

```powershell
Install-Module Microsoft.Entra.Beta -Force -AllowClobber
Connect-Entra -Scopes 'Application.ReadWrite.All','Directory.Read.All','DelegatedPermissionGrant.ReadWrite.All'
Grant-EntraBetaMCPServerPermission -ApplicationName VisualStudioCode
```

Until this is done, Graph-related MCP tools won't connect.

---

## Step 7: Verify Everything Works

### Test MCP Connectivity

In Claude chat, try these prompts:

**Sentinel access:**

> "List all tables in my Sentinel workspace that contain 'Alert' in the name"

You should see a tool call to the Azure MCP server, followed by table names like `SecurityAlert` and `AlertEvidence`.

**Graph access:**

> "Get the risky users from Entra ID Protection"

You should see a Graph API call returning risk detection data.

### Test API Connectivity with Python

Run the integration test:

```powershell
pytest tests/test_api_connectivity.py -v
```

This validates that your Azure credentials can reach both Sentinel and Microsoft Graph.

---

## Step 8: Scaffold the Agent Code

With the environment ready, I created starter files for both agents:

**`agents/base_agent.py`** — Shared foundation:

```python
class BaseAgent:
    def __init__(self, name: str, mode: str = "advisory"):
        self.name = name
        self.mode = mode

    def run(self):
        raise NotImplementedError("Subclasses must implement run()")
```

**`agents/analyst_bot_01/agent.py`** — AnalystBot01 skeleton:

```python
from agents.base_agent import BaseAgent

class AnalystBot01Agent(BaseAgent):
    def __init__(self, mode: str = "advisory"):
        super().__init__(name="AnalystBot01", mode=mode)

    def run(self):
        # TODO: Implement alert triage pipeline
        pass
```

**`shared/models/alert.py`** — Typed data model:

```python
from pydantic import BaseModel
from datetime import datetime
from typing import Optional

class Alert(BaseModel):
    time_generated: datetime
    alert_name: str
    alert_severity: str
    description: str
    entities: Optional[str] = None
    status: str
```

I also created KQL hunting query templates for ransomware detection, credential theft, and lateral movement — all mapped to MITRE ATT&CK technique IDs. These live in `queries/hunting/` as `.kql` files and get full syntax highlighting from the KQL Assistant extension.

---

## The Full Picture

Here's what the finished workspace looks like after all nine steps:

```
your-workspace/
├── .env.example
├── .gitignore
├── .venv/
├── .vscode/
│   ├── settings.json
│   └── mcp.json
├── agents/
│   ├── base_agent.py
│   ├── analyst_bot_01/   (agent, triage, enrichment, prompts, tests)
│   └── hunter/     (agent, query_generator, threat_mappings, prompts, tests)
├── shared/
│   ├── api_clients/ (sentinel, defender, graph)
│   ├── models/      (alert, entity, hunt_result)
│   └── utils/       (kql_validator, logging_config)
├── queries/
│   ├── hunting/     (ransomware.kql, credential_theft.kql, lateral_movement.kql)
│   └── enrichment/  (user_context.kql, device_context.kql)
├── tests/
│   ├── test_api_connectivity.py
│   └── test_mcp_tools.py
└── requirements.txt
```

---

## Gotchas Summary

| #   | Problem                                    | Symptom                            | Fix                                                        |
| --- | ------------------------------------------ | ---------------------------------- | ---------------------------------------------------------- |
| 1   | `azure-mgmt-securityinsight` no stable 2.0 | pip "No matching distribution"     | Use `>=2.0.0b2` + `--pre` flag                             |
| 2   | `msgraph-sdk` exceeds Windows path limits  | pip "No such file or directory"    | Enable `LongPathsEnabled` in registry                      |
| 3   | Fictional MCP package names in docs        | npm "not found" or silent failures | Use `@azure/mcp` and Microsoft hosted endpoint             |
| 4   | Azure CLI not installed                    | `az login` not recognized          | `winget install --id Microsoft.AzureCLI`                   |
| 5   | Enterprise MCP needs Entra provisioning    | Graph tools don't connect          | `Grant-EntraBetaMCPServerPermission` (one-time admin task) |

---

## What's Next

With the environment configured, the real work starts:

1. **Build AnalystBot01** — Start with the alert triage pipeline. Pull recent `SecurityAlert` rows from Sentinel, classify them, enrich with user/device context from Graph.
2. **Build HUNTER** — Add KQL query generation. Give it a threat hypothesis, get back a targeted hunting query mapped to ATT&CK.
3. **Connect them** — AnalystBot01 detects something suspicious → triggers HUNTER to investigate deeper.
4. **Stay in advisory mode** — Both agents recommend actions. The human decides.

The IDE is ready. The APIs are connected. The MCP servers bridge Claude to live security data. Time to build the agents.

---

_This post is part of a series on building an Agentic SOC. Next up: designing the AnalystBot01 alert triage pipeline._
