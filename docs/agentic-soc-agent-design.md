# Agentic SOC Agent Architecture

**Version:** 1.0  
**Date:** February 5, 2026  
**Platform:** VS Code + Claude Opus 4.5  
**Integration:** Microsoft Defender XDR, Microsoft Sentinel, Security Data Lake

---

## Executive Summary

This document defines a portfolio of **7 AI agents** designed to transform SOC operations through a phased implementation approach. The agents progress from advisory-only capabilities in Phase 1 to collaborative autonomous orchestration in Phase 4, addressing Tier 1-3 threats while reducing Mean Time to Detect (MTTD), Mean Time to Respond (MTTR), and analyst burnout.

### Design Principles

| Principle                      | Implementation                                                          |
| ------------------------------ | ----------------------------------------------------------------------- |
| **Composable, not monolithic** | Each agent has a focused purpose; agents collaborate via shared context |
| **Governed by design**         | All agents operate within defined scope with audit trails               |
| **Human-in-command**           | Analysts maintain oversight; autonomy increases only with trust         |
| **Outcome-driven**             | Every agent targets measurable improvements in SOC metrics              |

---

## Agent Portfolio Overview

| #   | Agent Name            | Primary Function                   | Phase Introduced | Autonomy Level             |
| --- | --------------------- | ---------------------------------- | ---------------- | -------------------------- |
| 1   | **AnalystBot01**      | Alert Triage & Prioritization      | Phase 1          | Advisory → Semi-autonomous |
| 2   | **HUNTER**            | Threat Hunting Query Generation    | Phase 1          | Advisory                   |
| 3   | **INVESTIGATOR**      | Evidence Correlation & Analysis    | Phase 2          | Advisory → Semi-autonomous |
| 4   | **RISK ASSESSOR**     | CVE/Exploitability Analysis        | Phase 2          | Advisory                   |
| 5   | **SCRIBE**            | Incident Documentation & Reporting | Phase 2          | Semi-autonomous            |
| 6   | **IDENTITY GUARDIAN** | Identity Threat Specialist         | Phase 3          | Semi-autonomous            |
| 7   | **ORCHESTRATOR**      | Multi-Agent Coordination           | Phase 4          | Autonomous with guardrails |

---

## Threat Coverage Matrix

### Tier 1 - Critical Threats

| Threat                                  | Primary Agent                   | Supporting Agents    | Detection Products                                                |
| --------------------------------------- | ------------------------------- | -------------------- | ----------------------------------------------------------------- |
| **Ransomware & Human-Operated Attacks** | AnalystBot01, INVESTIGATOR      | HUNTER, SCRIBE       | Defender for Endpoint, Defender XDR, Defender for Cloud, Sentinel |
| **Business Email Compromise**           | AnalystBot01, IDENTITY GUARDIAN | INVESTIGATOR, SCRIBE | Defender for Office 365, Purview, Defender for Cloud Apps         |
| **Data Exfiltration**                   | AnalystBot01, INVESTIGATOR      | HUNTER, SCRIBE       | Purview, Defender for Cloud Apps, Sentinel                        |

### Tier 2 - High Priority Threats

| Threat                          | Primary Agent        | Supporting Agents               | Detection Products                                             |
| ------------------------------- | -------------------- | ------------------------------- | -------------------------------------------------------------- |
| **Infostealer Malware**         | AnalystBot01, HUNTER | INVESTIGATOR, IDENTITY GUARDIAN | Defender for Endpoint, Defender XDR, Entra ID Protection       |
| **ClickFix Social Engineering** | AnalystBot01         | INVESTIGATOR, SCRIBE            | Defender for Office 365, Defender for Endpoint, SmartScreen    |
| **Device Code Phishing**        | IDENTITY GUARDIAN    | AnalystBot01, INVESTIGATOR      | Entra ID Protection, Defender for Cloud Apps, Security Copilot |
| **Password Spray Attacks**      | IDENTITY GUARDIAN    | AnalystBot01, HUNTER            | Entra ID Protection, Defender for Identity                     |
| **Leaked Credentials**          | IDENTITY GUARDIAN    | AnalystBot01, RISK ASSESSOR     | Entra ID Protection, Sentinel                                  |
| **Phishing Attempts**           | AnalystBot01         | INVESTIGATOR, SCRIBE            | Defender for Office 365, Entra ID Protection                   |
| **Email Bombing & Vishing**     | AnalystBot01         | INVESTIGATOR                    | Defender for Office 365, Defender XDR                          |
| **Malware Detection**           | AnalystBot01, HUNTER | INVESTIGATOR                    | Defender for Endpoint, Defender for Office 365                 |
| **Vulnerability Exploitation**  | RISK ASSESSOR        | AnalystBot01, HUNTER            | Defender Vulnerability Management, Defender for Cloud          |

### Tier 3 - Emerging Threats

| Threat                                    | Primary Agent        | Supporting Agents               | Detection Products                           |
| ----------------------------------------- | -------------------- | ------------------------------- | -------------------------------------------- |
| **AI-Enhanced Social Engineering**        | AnalystBot01         | INVESTIGATOR, IDENTITY GUARDIAN | Defender for Office 365, Security Copilot    |
| **Cloud Identity Abuse**                  | IDENTITY GUARDIAN    | INVESTIGATOR, HUNTER            | Entra ID Protection, Defender for Cloud Apps |
| **Cloud Workload & Container Compromise** | AnalystBot01, HUNTER | INVESTIGATOR, RISK ASSESSOR     | Defender for Cloud, Defender for Containers  |
| **Access Broker Activity**                | HUNTER, INVESTIGATOR | IDENTITY GUARDIAN               | Defender for Identity, Sentinel              |
| **Suspicious Mailbox Activities**         | AnalystBot01         | INVESTIGATOR, SCRIBE            | Defender for Office 365, Purview             |
| **AI System Attacks**                     | AnalystBot01         | INVESTIGATOR, RISK ASSESSOR     | Purview, Defender for Cloud Apps             |

---

## Phase 1: Foundation Agents

### Agent 1: AnalystBot01 (Alert Triage & Prioritization)

**Purpose:** First-line defense that ingests, analyzes, and prioritizes security alerts to reduce alert fatigue and accelerate analyst response.

#### Capabilities

| Capability                         | Description                                                                   | Autonomy Level |
| ---------------------------------- | ----------------------------------------------------------------------------- | -------------- |
| Alert Ingestion                    | Connects to Sentinel and XDR APIs to pull alerts in real-time                 | Automated      |
| Context Enrichment                 | Augments alerts with asset criticality, user risk scores, historical patterns | Automated      |
| True/False Positive Classification | Analyzes alert context to recommend classification                            | **Advisory**   |
| Priority Scoring                   | Assigns severity based on threat intelligence, asset value, and attack stage  | **Advisory**   |
| Analyst Briefing                   | Generates concise alert summaries with recommended actions                    | **Advisory**   |

#### Input Sources

```
- Microsoft Sentinel Incidents API
- Microsoft Defender XDR Alerts API
- Security Data Lake (historical context)
- Microsoft Graph API (user/device context)
- Threat Intelligence feeds (TI indicators)
```

#### Output Artifacts

```
- Prioritized alert queue with confidence scores
- Alert summary with key IOCs and affected entities
- Recommended classification (True Positive, False Positive, Benign True Positive)
- Suggested next actions for analyst
- Handoff package for INVESTIGATOR agent
```

#### Threat Coverage

| Tier   | Threats Addressed                                                    |
| ------ | -------------------------------------------------------------------- |
| Tier 1 | Ransomware detection, BEC indicators, Data exfiltration alerts       |
| Tier 2 | Infostealer execution, ClickFix behavior, Phishing, Malware          |
| Tier 3 | AI-enhanced phishing, Cloud workload anomalies, Mailbox manipulation |

#### KQL Integration Examples

```kql
// Alert enrichment query - user risk context
let alertUser = "user@contoso.com";
IdentityInfo
| where AccountUPN == alertUser
| project AccountUPN, RiskLevel, RiskState, LastRiskUpdate = RiskLastUpdatedDateTime
| join kind=leftouter (
    SigninLogs
    | where UserPrincipalName == alertUser
    | where TimeGenerated > ago(7d)
    | summarize
        SigninCount = count(),
        FailedSignins = countif(ResultType != "0"),
        UniqueLocations = dcount(Location),
        RiskySignins = countif(RiskState == "atRisk")
) on $left.AccountUPN == $right.UserPrincipalName
```

```kql
// Historical alert pattern analysis
SecurityAlert
| where TimeGenerated > ago(30d)
| where Entities contains "targetEntity"
| summarize
    AlertCount = count(),
    AlertTypes = make_set(AlertName),
    FirstSeen = min(TimeGenerated),
    LastSeen = max(TimeGenerated)
| extend AlertVelocity = AlertCount / 30.0
```

#### Collaboration Pattern

```
AnalystBot01 receives alert
    ├── Enriches with context
    ├── Classifies and prioritizes
    ├── [If hunting needed] → Triggers HUNTER
    ├── [If investigation needed] → Hands off to INVESTIGATOR
    └── [Always] → Updates analyst dashboard
```

---

### Agent 2: HUNTER (Threat Hunting Query Generation)

**Purpose:** Proactively generates and refines threat hunting queries based on threat intelligence, IOCs, and emerging attack patterns to identify threats before they trigger alerts.

#### Capabilities

| Capability             | Description                                                   | Autonomy Level |
| ---------------------- | ------------------------------------------------------------- | -------------- |
| Query Generation       | Creates KQL queries from natural language threat descriptions | **Advisory**   |
| IOC Expansion          | Takes initial IOCs and generates related hunting queries      | **Advisory**   |
| Pattern Recognition    | Analyzes TTPs and generates behavioral detection queries      | **Advisory**   |
| Query Optimization     | Refines queries for performance and accuracy                  | Automated      |
| Hunt Playbook Creation | Generates structured hunting procedures                       | **Advisory**   |

#### Input Sources

```
- Threat Intelligence reports (MDDR, CISA alerts)
- IOC feeds (file hashes, IPs, domains)
- MITRE ATT&CK technique IDs
- Natural language threat descriptions
- AnalystBot01 agent escalations
- Security Data Lake schemas
```

#### Output Artifacts

```
- Validated KQL hunting queries
- Hunt hypothesis with rationale
- Expected results interpretation guide
- Related MITRE ATT&CK mappings
- Recommended hunt frequency
```

#### Threat Coverage

| Tier   | Hunting Focus Areas                                                      |
| ------ | ------------------------------------------------------------------------ |
| Tier 1 | RMM tool abuse, Encryption staging, Large data transfers                 |
| Tier 2 | Infostealer C2 patterns, Clipboard-to-shell behavior, Credential access  |
| Tier 3 | Cloud identity anomalies, Container escape attempts, Access broker recon |

#### Query Generation Examples

**Input:** "Hunt for ClickFix social engineering - users copying commands to PowerShell"

**Generated Query:**

```kql
// Hunt: ClickFix clipboard-to-terminal behavior
DeviceProcessEvents
| where TimeGenerated > ago(24h)
| where ProcessCommandLine has_any ("powershell", "cmd", "mshta")
| where InitiatingProcessFileName in~ ("explorer.exe", "chrome.exe", "msedge.exe", "firefox.exe")
| extend CommandLength = strlen(ProcessCommandLine)
| where CommandLength > 100  // Suspiciously long commands
| where ProcessCommandLine has_any (
    "Invoke-WebRequest", "IWR", "curl", "wget",
    "DownloadString", "DownloadFile", "Start-BitsTransfer",
    "hidden", "-enc", "-encodedcommand", "bypass"
)
| project
    TimeGenerated,
    DeviceName,
    AccountName,
    InitiatingProcess = InitiatingProcessFileName,
    CommandPreview = substring(ProcessCommandLine, 0, 200),
    FullCommand = ProcessCommandLine
| summarize
    EventCount = count(),
    Devices = make_set(DeviceName),
    Commands = make_set(CommandPreview)
    by AccountName
| where EventCount >= 1
```

**Input:** "Hunt for device code phishing token theft"

**Generated Query:**

```kql
// Hunt: Device code authentication anomalies
SigninLogs
| where TimeGenerated > ago(7d)
| where AuthenticationProtocol == "deviceCode"
| extend
    ParsedLocation = parse_json(LocationDetails),
    DeviceDetail = parse_json(DeviceDetail)
| extend
    City = tostring(ParsedLocation.city),
    Country = tostring(ParsedLocation.countryOrRegion),
    Browser = tostring(DeviceDetail.browser),
    OS = tostring(DeviceDetail.operatingSystem)
| summarize
    DeviceCodeAttempts = count(),
    UniqueLocations = dcount(strcat(City, Country)),
    Locations = make_set(strcat(City, ", ", Country)),
    SuccessCount = countif(ResultType == "0"),
    FailureCount = countif(ResultType != "0")
    by UserPrincipalName, AppDisplayName
| where DeviceCodeAttempts > 3 or UniqueLocations > 2
| extend RiskIndicator = case(
    UniqueLocations > 3, "High - Multiple locations",
    DeviceCodeAttempts > 10, "High - Excessive attempts",
    SuccessCount > 0 and FailureCount > 5, "Medium - Bruteforce pattern",
    "Low"
)
| where RiskIndicator != "Low"
```

#### Collaboration Pattern

```
HUNTER operates in two modes:

Proactive Mode:
    Scheduled hunt execution
        ├── Runs query portfolio against Data Lake
        ├── [If findings] → Creates alert for AnalystBot01
        └── [If clean] → Logs hunt completion

Reactive Mode (triggered by AnalystBot01):
    AnalystBot01 escalates suspicious pattern
        ├── HUNTER generates targeted queries
        ├── Executes hunt
        ├── [If findings] → Returns enriched context to INVESTIGATOR
        └── [If clean] → Returns "No additional findings" to AnalystBot01
```

---

## Phase 2: Investigation & Analysis Agents

### Agent 3: INVESTIGATOR (Evidence Correlation & Analysis)

**Purpose:** Autonomously drives investigations by correlating evidence across telemetry sources, building attack timelines, and synthesizing findings into actionable intelligence.

#### Capabilities

| Capability                  | Description                                                  | Autonomy Level |
| --------------------------- | ------------------------------------------------------------ | -------------- |
| Evidence Collection         | Gathers related events across XDR, Sentinel, and Data Lake   | Automated      |
| Timeline Construction       | Builds chronological attack narrative from disparate events  | Automated      |
| Entity Mapping              | Links users, devices, IPs, and files across the attack chain | Automated      |
| Root Cause Analysis         | Identifies initial access vector and attack progression      | **Advisory**   |
| Impact Assessment           | Determines blast radius and affected assets                  | **Advisory**   |
| Containment Recommendations | Suggests isolation and remediation actions                   | **Advisory**   |

#### Input Sources

```
- AnalystBot01 agent handoffs (prioritized alerts)
- HUNTER agent findings (hunt results)
- Microsoft Defender XDR Advanced Hunting
- Microsoft Sentinel entity pages
- Security Data Lake (90+ day historical)
- Microsoft Graph (organizational context)
```

#### Output Artifacts

```
- Investigation summary with confidence scores
- Visual attack timeline
- Entity relationship graph
- MITRE ATT&CK technique mapping
- Containment recommendation matrix
- Evidence package for SCRIBE agent
```

#### Investigation Workflow

```
Phase A: Scope Definition
    ├── Identify seed entities (user, device, IP, file hash)
    ├── Define investigation time window
    └── Set investigation hypothesis

Phase B: Evidence Collection
    ├── Query all relevant telemetry sources
    ├── Expand entity relationships
    └── Collect supporting artifacts

Phase C: Correlation & Analysis
    ├── Build temporal timeline
    ├── Map to MITRE ATT&CK
    ├── Identify gaps in visibility
    └── Assess confidence levels

Phase D: Synthesis
    ├── Generate investigation narrative
    ├── Produce containment recommendations
    └── Package findings for analyst review
```

#### Investigation Query Portfolio

```kql
// Investigation: Full entity timeline
let investigationWindow = 72h;
let targetUser = "compromised.user@contoso.com";
let targetDevice = "WORKSTATION-001";

// Unified timeline across all telemetry
union
    (SigninLogs | where UserPrincipalName == targetUser | extend Source = "Identity"),
    (DeviceLogonEvents | where AccountName has targetUser or DeviceName == targetDevice | extend Source = "Endpoint"),
    (DeviceProcessEvents | where DeviceName == targetDevice | extend Source = "Process"),
    (DeviceNetworkEvents | where DeviceName == targetDevice | extend Source = "Network"),
    (DeviceFileEvents | where DeviceName == targetDevice | extend Source = "File"),
    (EmailEvents | where RecipientEmailAddress == targetUser or SenderFromAddress == targetUser | extend Source = "Email"),
    (CloudAppEvents | where AccountDisplayName has targetUser | extend Source = "CloudApp")
| where TimeGenerated > ago(investigationWindow)
| project TimeGenerated, Source, Activity = coalesce(ActionType, ResultType, Operation),
          Details = pack_all()
| order by TimeGenerated asc
```

```kql
// Investigation: Lateral movement detection
let compromisedAccount = "compromised.user@contoso.com";
let compromiseTime = datetime(2026-02-05T10:00:00Z);

DeviceLogonEvents
| where TimeGenerated between (compromiseTime .. (compromiseTime + 24h))
| where AccountName has compromisedAccount or LogonType in ("RemoteInteractive", "Network")
| summarize
    DevicesAccessed = make_set(DeviceName),
    LogonTypes = make_set(LogonType),
    FirstAccess = min(TimeGenerated),
    LastAccess = max(TimeGenerated),
    AccessCount = count()
    by AccountName
| extend LateralMovementScore = case(
    array_length(DevicesAccessed) > 10, "Critical",
    array_length(DevicesAccessed) > 5, "High",
    array_length(DevicesAccessed) > 2, "Medium",
    "Low"
)
```

#### Collaboration Pattern

```
INVESTIGATOR receives case from AnalystBot01
    ├── Collects evidence (may request HUNTER for specific queries)
    ├── Builds timeline and entity map
    ├── Generates findings
    ├── [If containment needed] → Recommends actions (analyst approves)
    ├── [If CVE-related] → Consults RISK ASSESSOR
    ├── [If identity-focused] → Consults IDENTITY GUARDIAN
    └── [Always] → Hands off to SCRIBE for documentation
```

---

### Agent 4: RISK ASSESSOR (CVE & Exploitability Analysis)

**Purpose:** Evaluates vulnerabilities and exploitation risk by correlating CVE data with organizational context, threat intelligence, and asset criticality.

#### Capabilities

| Capability             | Description                                                        | Autonomy Level |
| ---------------------- | ------------------------------------------------------------------ | -------------- |
| CVE Contextualization  | Maps CVEs to affected assets in the environment                    | Automated      |
| Exploitability Scoring | Assesses real-world exploit likelihood using EPSS and threat intel | Automated      |
| Attack Path Analysis   | Models potential exploitation paths through the environment        | **Advisory**   |
| Patch Prioritization   | Recommends remediation order based on risk and feasibility         | **Advisory**   |
| Compensating Controls  | Suggests mitigations when patching isn't immediately possible      | **Advisory**   |

#### Input Sources

```
- Microsoft Defender Vulnerability Management
- NVD/CVE databases
- EPSS (Exploit Prediction Scoring System)
- CISA KEV (Known Exploited Vulnerabilities)
- Threat intelligence on active exploitation
- Asset inventory with criticality ratings
- AnalystBot01 alerts for exploitation attempts
```

#### Output Artifacts

```
- Prioritized vulnerability remediation list
- Risk heat map by asset/business unit
- Exploitation likelihood assessment
- Attack path visualization
- Compensating control recommendations
- Patch deployment timeline suggestions
```

#### Risk Scoring Model

```
Risk Score = (CVSS × Exploitability × Asset Criticality × Exposure) / Mitigating Controls

Where:
- CVSS: Base vulnerability severity (0-10)
- Exploitability: EPSS score + active exploitation in wild (0-1)
- Asset Criticality: Business impact rating (1-5)
- Exposure: Internet-facing, internal, or isolated (1-3)
- Mitigating Controls: Compensating controls in place (1-3)
```

#### Query Examples

```kql
// Vulnerability risk assessment with asset context
DeviceTvmSoftwareVulnerabilities
| where TimeGenerated > ago(1d)
| where VulnerabilitySeverityLevel in ("Critical", "High")
| join kind=leftouter (
    DeviceInfo
    | summarize arg_max(TimeGenerated, *) by DeviceId
    | project DeviceId, DeviceName, IsInternetFacing = isnotempty(PublicIP)
) on DeviceId
| extend ExploitRisk = case(
    CveId in (dynamic(["CVE-2024-XXXX", "CVE-2024-YYYY"])), "Critical - Active exploitation",
    IsInternetFacing and VulnerabilitySeverityLevel == "Critical", "Critical - Internet exposed",
    VulnerabilitySeverityLevel == "Critical", "High",
    "Medium"
)
| summarize
    AffectedDevices = dcount(DeviceId),
    DeviceList = make_set(DeviceName, 10),
    InternetFacingCount = countif(IsInternetFacing)
    by CveId, VulnerabilitySeverityLevel, ExploitRisk
| order by ExploitRisk asc, AffectedDevices desc
```

#### Collaboration Pattern

```
RISK ASSESSOR operates in two modes:

Continuous Assessment:
    Daily vulnerability scan analysis
        ├── Identifies new critical exposures
        ├── [If critical] → Alerts AnalystBot01 for monitoring
        └── Updates risk dashboard

Investigation Support:
    INVESTIGATOR requests CVE context
        ├── RISK ASSESSOR provides exploitation likelihood
        ├── Maps affected assets
        └── Returns risk context to INVESTIGATOR
```

---

### Agent 5: SCRIBE (Incident Documentation & Reporting)

**Purpose:** Automates incident documentation by synthesizing investigation findings into structured reports, executive summaries, and compliance artifacts.

#### Capabilities

| Capability             | Description                                                 | Autonomy Level      |
| ---------------------- | ----------------------------------------------------------- | ------------------- |
| Report Generation      | Creates detailed incident reports from investigation data   | **Semi-autonomous** |
| Executive Summaries    | Distills technical findings into business-impact narratives | **Semi-autonomous** |
| Timeline Visualization | Generates visual attack timelines for reports               | Automated           |
| Compliance Mapping     | Tags incidents to relevant compliance frameworks            | Automated           |
| Lessons Learned        | Extracts actionable improvements from incidents             | **Advisory**        |
| Metrics Tracking       | Maintains MTTD/MTTR statistics                              | Automated           |

#### Input Sources

```
- INVESTIGATOR findings packages
- AnalystBot01 alert context
- IDENTITY GUARDIAN identity analysis
- RISK ASSESSOR vulnerability context
- Analyst annotations and decisions
- Containment and remediation actions taken
```

#### Output Artifacts

```
- Full incident report (technical audience)
- Executive summary (leadership audience)
- Compliance documentation (audit audience)
- Post-incident review template
- Metrics dashboard updates
- Knowledge base article drafts
```

#### Report Templates

**Technical Incident Report Structure:**

```markdown
# Incident Report: [INC-2026-XXXX]

## Executive Summary

[2-3 sentence overview for leadership]

## Incident Classification

- **Severity:** Critical/High/Medium/Low
- **Type:** [Ransomware/BEC/Data Exfiltration/etc.]
- **Status:** [Active/Contained/Remediated/Closed]
- **MITRE ATT&CK:** [Technique IDs]

## Timeline

[Visual timeline generated from INVESTIGATOR data]

## Affected Assets

| Asset Type   | Count | Critical Assets |
| ------------ | ----- | --------------- |
| Users        | X     | [list]          |
| Devices      | X     | [list]          |
| Applications | X     | [list]          |

## Attack Narrative

[Detailed technical description of attack chain]

## Root Cause Analysis

[Initial access vector and contributing factors]

## Containment Actions

[Actions taken with timestamps]

## Remediation Status

[Current state and remaining tasks]

## Recommendations

[Short-term and long-term improvements]

## Appendices

- IOC List
- Query Results
- Evidence Artifacts
```

#### Collaboration Pattern

```
SCRIBE receives input from multiple agents:

    INVESTIGATOR completes investigation
        └── SCRIBE generates technical report draft

    IDENTITY GUARDIAN provides identity context
        └── SCRIBE incorporates identity findings

    RISK ASSESSOR provides vulnerability context
        └── SCRIBE incorporates risk assessment

    Analyst reviews and approves
        └── SCRIBE finalizes and publishes report
```

---

## Phase 3: Specialized Agents

### Agent 6: IDENTITY GUARDIAN (Identity Threat Specialist)

**Purpose:** Dedicated identity security agent that monitors, analyzes, and responds to identity-based threats including credential compromise, token theft, and privilege escalation.

#### Capabilities

| Capability                      | Description                                    | Autonomy Level      |
| ------------------------------- | ---------------------------------------------- | ------------------- |
| Identity Risk Monitoring        | Continuous monitoring of identity risk signals | Automated           |
| Credential Compromise Detection | Identifies leaked or stolen credentials        | Automated           |
| Token Abuse Analysis            | Detects OAuth token theft and replay attacks   | **Semi-autonomous** |
| Privilege Escalation Detection  | Monitors for unauthorized permission changes   | **Semi-autonomous** |
| Session Anomaly Detection       | Identifies suspicious session behavior         | **Semi-autonomous** |
| Remediation Recommendations     | Suggests identity-specific containment actions | **Advisory**        |

#### Input Sources

```
- Microsoft Entra ID Protection risk events
- Microsoft Defender for Identity alerts
- Microsoft Defender for Cloud Apps OAuth monitoring
- Signin logs and audit logs
- Conditional access policy evaluation results
- Threat intelligence on leaked credentials
```

#### Output Artifacts

```
- Identity risk assessment with confidence scores
- Compromised credential reports
- OAuth application risk analysis
- Privilege escalation timelines
- Session anomaly reports
- Identity-specific remediation playbooks
```

#### Threat-Specific Detection

**Device Code Phishing Detection:**

```kql
// Detect device code phishing indicators
let deviceCodeSignins = SigninLogs
| where TimeGenerated > ago(24h)
| where AuthenticationProtocol == "deviceCode";

let suspiciousPatterns = deviceCodeSignins
| summarize
    AttemptCount = count(),
    SuccessCount = countif(ResultType == "0"),
    UniqueIPs = dcount(IPAddress),
    UniqueLocations = dcount(Location),
    Locations = make_set(Location)
    by UserPrincipalName, AppId, AppDisplayName
| where AttemptCount > 2 or UniqueLocations > 1;

let postAuthActivity = suspiciousPatterns
| join kind=inner (
    AuditLogs
    | where TimeGenerated > ago(24h)
    | where OperationName has_any ("Add member", "Add owner", "Consent to application")
) on $left.UserPrincipalName == $right.InitiatedBy.user.userPrincipalName
| extend RiskLevel = "Critical - Post-auth suspicious activity";

union suspiciousPatterns, postAuthActivity
| extend AlertRecommendation = case(
    RiskLevel == "Critical - Post-auth suspicious activity", "Immediate: Revoke sessions, review consents",
    UniqueLocations > 2, "High: Verify with user, consider session revocation",
    AttemptCount > 5, "Medium: Monitor for additional indicators",
    "Low: Log for baseline"
)
```

**Cloud Identity Abuse Detection:**

```kql
// Detect OAuth consent phishing and token abuse
CloudAppEvents
| where TimeGenerated > ago(7d)
| where ActionType in ("Consent to application", "Add app role assignment to service principal")
| extend
    ConsentedApp = tostring(RawEventData.Target[0].ID),
    Permissions = tostring(RawEventData.ModifiedProperties)
| where Permissions has_any ("Mail.Read", "Files.Read", "User.Read.All", "Directory.Read.All")
| join kind=leftouter (
    AADServicePrincipalSignInLogs
    | where TimeGenerated > ago(7d)
    | summarize
        ServicePrincipalSignins = count(),
        UniqueResources = dcount(ResourceDisplayName)
        by ServicePrincipalId
) on $left.ConsentedApp == $right.ServicePrincipalId
| where ServicePrincipalSignins > 10 or UniqueResources > 3
| extend RiskAssessment = "High - Excessive service principal activity post-consent"
```

#### Collaboration Pattern

```
IDENTITY GUARDIAN operates continuously:

Monitoring Mode:
    Continuous identity risk monitoring
        ├── [If risk detected] → Alerts AnalystBot01
        ├── [If credential leaked] → Flags for password reset
        └── [If token abuse] → Recommends session revocation

Investigation Support:
    INVESTIGATOR requests identity analysis
        ├── IDENTITY GUARDIAN provides user risk history
        ├── Analyzes authentication patterns
        ├── Maps identity attack chain
        └── Returns identity-specific findings

Response Mode (Phase 3+):
    [Analyst approved] Session revocation
    [Analyst approved] Conditional access policy enforcement
    [Analyst approved] Password reset trigger
```

---

## Phase 4: Orchestration Layer

### Agent 7: ORCHESTRATOR (Multi-Agent Coordination)

**Purpose:** Coordinates multi-agent workflows, manages agent-to-agent communication, and drives end-to-end incident response with appropriate human oversight.

#### Capabilities

| Capability                  | Description                                              | Autonomy Level                 |
| --------------------------- | -------------------------------------------------------- | ------------------------------ |
| Workflow Orchestration      | Coordinates agent activities across incident lifecycle   | **Autonomous with guardrails** |
| Context Propagation         | Maintains shared investigation context across agents     | Automated                      |
| Decision Routing            | Determines which agent(s) to engage based on threat type | Automated                      |
| Escalation Management       | Ensures human-in-the-loop for high-risk decisions        | Automated                      |
| Response Playbook Execution | Executes approved response actions                       | **Autonomous with guardrails** |
| Performance Optimization    | Monitors agent effectiveness and optimizes workflows     | Automated                      |

#### Orchestration Workflows

**Workflow 1: Ransomware Response**

```
Alert received (Defender XDR: Ransomware behavior detected)
    │
    ├── ORCHESTRATOR activates response workflow
    │
    ├── Stage 1: Triage (Parallel)
    │   ├── AnalystBot01: Classify and prioritize alert
    │   └── HUNTER: Search for related RMM tools, lateral movement
    │
    ├── Stage 2: Investigation
    │   ├── INVESTIGATOR: Build attack timeline
    │   ├── IDENTITY GUARDIAN: Assess compromised credentials
    │   └── RISK ASSESSOR: Identify exploited vulnerabilities
    │
    ├── Stage 3: Containment (Human approval required)
    │   ├── ORCHESTRATOR: Present containment options
    │   ├── Analyst: Approves device isolation
    │   └── ORCHESTRATOR: Executes via Defender API
    │
    ├── Stage 4: Documentation
    │   └── SCRIBE: Generate incident report
    │
    └── Stage 5: Learning
        └── ORCHESTRATOR: Update detection rules, close case
```

**Workflow 2: Business Email Compromise Response**

```
Alert received (Defender for Office 365: BEC indicators)
    │
    ├── ORCHESTRATOR activates BEC workflow
    │
    ├── Stage 1: Identity Verification (Parallel)
    │   ├── IDENTITY GUARDIAN: Analyze user risk and sign-in patterns
    │   └── AnalystBot01: Review related email alerts
    │
    ├── Stage 2: Mailbox Investigation
    │   ├── INVESTIGATOR: Analyze mailbox rules, forwarding
    │   └── HUNTER: Search for similar patterns across org
    │
    ├── Stage 3: Containment (Semi-autonomous)
    │   ├── [Auto] ORCHESTRATOR: Revoke suspicious inbox rules
    │   ├── [Approval] ORCHESTRATOR: Reset user password
    │   └── [Approval] ORCHESTRATOR: Revoke OAuth consents
    │
    ├── Stage 4: Impact Assessment
    │   └── INVESTIGATOR: Identify data accessed/exfiltrated
    │
    └── Stage 5: Documentation
        └── SCRIBE: Generate BEC incident report
```

#### Guardrails & Human Oversight

| Action Category                                    | Autonomy Level   | Approval Required |
| -------------------------------------------------- | ---------------- | ----------------- |
| Alert enrichment and classification                | Fully autonomous | No                |
| Evidence collection and correlation                | Fully autonomous | No                |
| Hunting query execution                            | Fully autonomous | No                |
| Low-risk containment (email quarantine)            | Semi-autonomous  | Notification only |
| Medium-risk containment (session revocation)       | Semi-autonomous  | Async approval    |
| High-risk containment (device isolation)           | Human-in-loop    | Explicit approval |
| Critical actions (password reset, account disable) | Human-in-loop    | Explicit approval |

#### Agent Communication Protocol

```yaml
Message Schema:
  message_id: UUID
  timestamp: ISO8601
  source_agent: ANALYST_BOT_01 | HUNTER | INVESTIGATOR | RISK_ASSESSOR | SCRIBE | IDENTITY_GUARDIAN | ORCHESTRATOR
  target_agent: [agent or "broadcast"]
  message_type: REQUEST | RESPONSE | ALERT | STATUS | HANDOFF
  priority: CRITICAL | HIGH | MEDIUM | LOW
  context:
    incident_id: string
    investigation_id: string
    entities: [users, devices, ips, hashes]
  payload:
    action: string
    data: object
    confidence: float (0-1)
```

---

## Implementation Roadmap

### Phase 1: Foundation (Weeks 1-4)

| Week | Deliverable                           | Agents               |
| ---- | ------------------------------------- | -------------------- |
| 1    | Infrastructure setup, API connections | —                    |
| 2    | AnalystBot01 core triage capabilities | AnalystBot01         |
| 3    | HUNTER query generation engine        | HUNTER               |
| 4    | Integration testing, analyst feedback | AnalystBot01, HUNTER |

**Success Criteria:**

- AnalystBot01 processes 100% of Tier 1 alerts within 5 minutes
- HUNTER generates valid KQL for 90% of natural language inputs
- Analyst satisfaction score ≥ 7/10

### Phase 2: Investigation (Weeks 5-10)

| Week | Deliverable                      | Agents        |
| ---- | -------------------------------- | ------------- |
| 5-6  | INVESTIGATOR evidence collection | INVESTIGATOR  |
| 7    | RISK ASSESSOR CVE integration    | RISK ASSESSOR |
| 8-9  | SCRIBE documentation automation  | SCRIBE        |
| 10   | Cross-agent handoff workflows    | All Phase 1-2 |

**Success Criteria:**

- INVESTIGATOR reduces investigation time by 50%
- SCRIBE generates compliant reports in < 30 minutes
- MTTD improved by 30%

### Phase 3: Specialization (Weeks 11-16)

| Week  | Deliverable                             | Agents            |
| ----- | --------------------------------------- | ----------------- |
| 11-12 | IDENTITY GUARDIAN identity monitoring   | IDENTITY GUARDIAN |
| 13-14 | Advanced detection for Tier 2-3 threats | All agents        |
| 15-16 | Semi-autonomous response capabilities   | All agents        |

**Success Criteria:**

- IDENTITY GUARDIAN detects 95% of identity threats
- Semi-autonomous actions approved by analysts > 80%
- MTTR improved by 40%

### Phase 4: Orchestration (Weeks 17-24)

| Week  | Deliverable                         | Agents       |
| ----- | ----------------------------------- | ------------ |
| 17-18 | ORCHESTRATOR core coordination      | ORCHESTRATOR |
| 19-20 | Multi-agent workflow automation     | All agents   |
| 21-22 | Autonomous response with guardrails | All agents   |
| 23-24 | Full production deployment          | All agents   |

**Success Criteria:**

- End-to-end incident response time < 4 hours for Tier 1
- Analyst capacity increased by 60%
- False positive rate < 5%

---

## Metrics & KPIs

### Operational Metrics

| Metric                           | Baseline   | Phase 1 Target | Phase 4 Target |
| -------------------------------- | ---------- | -------------- | -------------- |
| Mean Time to Detect (MTTD)       | 24 hours   | 12 hours       | 2 hours        |
| Mean Time to Respond (MTTR)      | 48 hours   | 24 hours       | 6 hours        |
| Mean Time to Triage              | 30 minutes | 10 minutes     | 2 minutes      |
| Alerts processed per analyst/day | 50         | 150            | 500            |
| Investigation time per incident  | 4 hours    | 2 hours        | 30 minutes     |

### Quality Metrics

| Metric                     | Baseline | Target |
| -------------------------- | -------- | ------ |
| True positive rate         | 40%      | 85%    |
| False positive reduction   | —        | 70%    |
| Investigation completeness | 60%      | 95%    |
| Report compliance score    | 70%      | 98%    |

### Agent Performance Metrics

| Agent             | Key Metric                     | Target   |
| ----------------- | ------------------------------ | -------- |
| AnalystBot01      | Triage accuracy                | 90%      |
| HUNTER            | Query validity rate            | 95%      |
| INVESTIGATOR      | Evidence correlation coverage  | 90%      |
| RISK ASSESSOR     | Prioritization accuracy        | 85%      |
| SCRIBE            | Report generation time         | < 30 min |
| IDENTITY GUARDIAN | Identity threat detection rate | 95%      |
| ORCHESTRATOR      | Workflow completion rate       | 99%      |

---

## Technical Architecture

### Integration Architecture

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           VS Code + Claude Opus 4.5                     │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │                        ORCHESTRATOR                              │   │
│  │         (Workflow coordination, human-in-the-loop)               │   │
│  └─────────────────────────────────────────────────────────────────┘   │
│           │           │           │           │           │             │
│           ▼           ▼           ▼           ▼           ▼             │
│  ┌──────────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐        │
│  │ AnalystBot01 │ │ HUNTER  │ │INVESTIG-│ │  RISK   │ │ SCRIBE  │        │
│  │              │ │         │ │  ATOR   │ │ASSESSOR │ │         │        │
│  └──────────────┘ └─────────┘ └─────────┘ └─────────┘ └─────────┘        │
│                    │                                                     │
│                    ▼                                                     │
│           ┌─────────────────┐                                           │
│           │IDENTITY GUARDIAN│                                           │
│           └─────────────────┘                                           │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                    ┌───────────────┼───────────────┐
                    ▼               ▼               ▼
        ┌───────────────┐ ┌───────────────┐ ┌───────────────┐
        │Microsoft      │ │Microsoft      │ │Security       │
        │Defender XDR   │ │Sentinel       │ │Data Lake      │
        │               │ │               │ │(90+ days)     │
        └───────────────┘ └───────────────┘ └───────────────┘
                │                   │               │
                ▼                   ▼               ▼
        ┌─────────────────────────────────────────────────┐
        │              Microsoft Graph API                │
        │   (Users, Devices, Applications, Audit Logs)    │
        └─────────────────────────────────────────────────┘
```

### Data Flow

```
Telemetry Sources                    Agent Processing                    Outputs
─────────────────────               ─────────────────                   ───────

Defender XDR ─────┐                 ┌─────────────────┐
                  │                 │                 │
Sentinel ─────────┼────────────────▶│  AnalystBot01   │─────▶ Prioritized Queue
                  │                 │   (Triage)      │
Entra ID ─────────┤                 │                 │
                  │                 └────────┬────────┘
Data Lake ────────┤                          │
                  │                          ▼
Graph API ────────┤                 ┌─────────────────┐
                  │                 │                 │
Threat Intel ─────┘                 │    HUNTER       │─────▶ Hunting Queries
                                    │   (Proactive)   │
                                    │                 │
                                    └────────┬────────┘
                                             │
                                             ▼
                                    ┌─────────────────┐
                                    │                 │
                                    │  INVESTIGATOR   │─────▶ Investigation Reports
                                    │  (Correlation)  │
                                    │                 │
                                    └────────┬────────┘
                                             │
                        ┌────────────────────┼────────────────────┐
                        ▼                    ▼                    ▼
               ┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
               │  RISK ASSESSOR  │ │IDENTITY GUARDIAN│ │     SCRIBE      │
               │   (CVE/Risk)    │ │   (Identity)    │ │ (Documentation) │
               └─────────────────┘ └─────────────────┘ └─────────────────┘
                        │                    │                    │
                        └────────────────────┼────────────────────┘
                                             │
                                             ▼
                                    ┌─────────────────┐
                                    │                 │
                                    │  ORCHESTRATOR   │─────▶ Coordinated Response
                                    │ (Phase 4 Only)  │
                                    │                 │
                                    └─────────────────┘
```

---

## Appendix A: Agent Prompt Templates

### AnalystBot01 System Prompt

```
You are AnalystBot01, an AI security analyst specializing in alert triage and prioritization.

Your role is to:
1. Analyze security alerts from Microsoft Defender XDR and Sentinel
2. Enrich alerts with contextual information from multiple data sources
3. Classify alerts as True Positive, False Positive, or Benign True Positive
4. Assign priority scores based on threat intelligence, asset criticality, and attack stage
5. Provide concise briefings to human analysts with recommended actions

Operating Principles:
- Always explain your reasoning with confidence scores
- Flag uncertainty explicitly when classification confidence is < 80%
- Escalate to INVESTIGATOR when deeper analysis is needed
- Escalate to HUNTER when proactive threat hunting is warranted
- Never take containment actions without human approval

Output Format:
- Start with a one-sentence alert summary
- Provide classification with confidence percentage
- List key indicators that informed your decision
- Recommend next actions for the analyst
```

### HUNTER System Prompt

```
You are HUNTER, an AI threat hunting specialist focused on proactive threat detection.

Your role is to:
1. Generate KQL hunting queries from natural language threat descriptions
2. Expand initial IOCs into comprehensive hunting hypotheses
3. Map threats to MITRE ATT&CK techniques
4. Optimize queries for performance and accuracy
5. Interpret query results and identify true threats

Operating Principles:
- Generate queries that are syntactically valid and performant
- Include comments explaining query logic
- Provide expected results interpretation guidance
- Flag when visibility gaps may affect hunt effectiveness
- Collaborate with AnalystBot01 for alert context and INVESTIGATOR for findings analysis

Query Generation Standards:
- Use appropriate time windows (default: 24h for real-time, 30d for historical)
- Include entity projection for analyst readability
- Add summarization for pattern detection
- Include risk scoring where applicable
```

### INVESTIGATOR System Prompt

```
You are INVESTIGATOR, an AI security analyst specializing in incident investigation and evidence correlation.

Your role is to:
1. Collect and correlate evidence across multiple telemetry sources
2. Build comprehensive attack timelines
3. Map entity relationships across the attack chain
4. Identify root cause and initial access vectors
5. Assess blast radius and impact
6. Recommend containment and remediation actions

Operating Principles:
- Build timelines with precise timestamps
- Map findings to MITRE ATT&CK techniques
- Calculate confidence scores for each conclusion
- Identify gaps in evidence and visibility
- Escalate to specialized agents when domain expertise is needed
- Package findings for SCRIBE documentation

Investigation Standards:
- Always start with entity scoping
- Expand investigation window based on evidence
- Cross-reference multiple data sources for validation
- Document assumptions and limitations
```

---

## Appendix B: API Integration Specifications

### Microsoft Defender XDR APIs

```python
# Alert ingestion
GET /api/incidents
GET /api/alerts
GET /api/advancedqueries/run

# Response actions
POST /api/machines/{id}/isolate
POST /api/machines/{id}/unisolate
POST /api/machines/{id}/runantivirus
```

### Microsoft Sentinel APIs

```python
# Incident management
GET /incidents
PATCH /incidents/{incidentId}
POST /incidents/{incidentId}/comments

# Query execution
POST /query
GET /savedSearches
```

### Microsoft Graph Security APIs

```python
# Security information
GET /security/alerts_v2
GET /security/incidents
GET /security/secureScores

# Identity information
GET /users/{id}/signInActivity
GET /identityProtection/riskyUsers
GET /identityProtection/riskDetections
```

---

_Document generated for Agentic SOC implementation. Version 1.0._
