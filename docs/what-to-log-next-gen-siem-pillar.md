---
title: "What to Log in Your Next-Gen SIEM — 37 Sources Mapped to MITRE ATT&CK"
author: "Mike Palitto"
date: 2026-04-21
status: draft
series: "Threat-Informed Defense: Tools, Logs, and Agents"
series_number: 2
version: "4.1"
created: 2026-04-14T00:00:00Z
updated: 2026-04-21T00:00:00Z
meta_description: "37 log sources mapped to MITRE ATT&CK tactics across a 3-tier ingestion model. Covers detection, forensics, hunting, compliance, and AI agent operations for the Agentic SOC."
---

# What to Log in Your Next-Gen SIEM — 37 Sources Mapped to MITRE ATT&CK

Last year we published [What should I log in my data lake?](https://socautomators.substack.com/p/what-should-i-log-in-my-data-lake) — a short guide that answered the question every SOC team was asking when Sentinel's data lake went live. That article gave you a clean split: real-time detection and correlation in the SIEM, high-volume historical data in the lake, and a downloadable chart to make the decision for each source. It worked. It's still one of our most-read posts.

But the landscape has shifted underneath that guidance.

When we wrote the data lake article, AI agents were a roadmap item. MCP tools didn't exist. Federation was a conference demo. Graph analytics was a feature buried in documentation that nobody was using in production. The question was simple: **SIEM or data lake?**

That question is no longer sufficient. You're now operating in what we're calling the **Agentic SOC era** — where AI agents don't just read your alerts, they triage them, correlate across sources, query your lake programmatically via MCP tools, and surface context that would take an analyst hours to assemble. Where federation means you can extend your KQL reach to data in Databricks, ADLS Gen 2, and Fabric without ingesting a single byte. Where graph analytics turns your lake data into traversable relationship maps that make blast radius analysis tractable instead of theoretical.

The original data lake guidance gave you two tiers. This article gives you three — plus four analytical surfaces that turn the lake from cheap storage into an active intelligence platform. The original covered the "where" question for a handful of sources. This one covers 37, maps every source to MITRE ATT&CK tactics, and gives you a prioritized implementation path that accounts for AI agent telemetry, cross-cloud federation, and graph-driven investigation — none of which existed when we wrote the first version.

The goal hasn't changed: help you make log source selection a deliberate architecture decision instead of an afterthought. What's changed is the architecture itself — and the five critical SOC capabilities your log architecture must support.

Whether you run a fully internal SOC, outsource detection to an MDR provider, retain a DFIR firm on retainer, or split responsibilities across an MSSP and an internal threat hunting team — these five capabilities still need to work. The difference is who operates them and where the data needs to be accessible. Your log architecture determines what's possible for every team touching your security operations.

**Detection** needs real-time signal with high fidelity and low latency. Alerts that fire within minutes. Enough context to triage quickly. Low enough false-positive rates that analysts actually pay attention. This is the analytics tier's responsibility — the same role your SIEM played in the original guidance. If you outsource detection to an MDR provider, they still need these logs flowing to the analytics tier. The ingestion decision doesn't change just because someone else is watching the console.

**Forensics and correlation** need historical depth and relationship-rich data. When you're reconstructing how an attacker moved from initial access to data exfiltration over 30 days, you need logs that show the connections between identity, endpoint, email, and cloud activity — retained long enough to trace the full chain. The data lake handles this, but now with graph analytics and notebooks instead of just KQL search. If your DFIR capability is outsourced, your retainer team needs query access to this data — and they need it retained long enough to matter when the call comes six months after initial compromise.

**Hunting** needs raw breadth and behavioral baselines. Hunters write open-ended queries looking for anomalies, patterns, and weak signals that don't fit predetermined rules. They need data wide enough to find the unexpected. The lake's four analytical surfaces — KQL, graph, notebooks, and agent access — give hunters capabilities that didn't exist when the data lake was just "cheap storage with a search box." Hunting is the capability most often left on the table by organizations that outsource detection but don't invest in proactive operations.

**Compliance** needs long-retention audit trails, immutable records, and query-ready evidence for regulators. When an auditor asks "show me 12 months of privileged access activity," you need that data retained and accessible — not archived in cold storage you can't query. The data lake and federated tier solve this at a fraction of analytics-tier cost. This is the one capability that stays internal regardless of your operating model — the auditor asks you, not your MSSP.

**AI Agent operations** — this is the new capability that didn't exist in our original guidance. AI agents need agent-accessible data for automated triage, conversational investigation, enrichment, and report generation. When an AI agent triages an alert, it queries the same lake data an analyst would — but programmatically via MCP tools. The Sentinel MCP Server exposes your lake as structured tools: semantic table discovery, KQL execution, entity risk analysis, and a full triage toolkit. SOC teams can wrap validated KQL queries as deterministic MCP tools — agents execute the exact query the human wrote, no hallucination risk. This is the capability that transforms "data lake" from a cost optimization play into the operational backbone of an Agentic SOC. And unlike human analysts, agents don't care whether it's 2 AM — they need the data available and queryable around the clock.

Not every log source serves all five capabilities equally. The ingestion pattern you choose — analytics tier, data lake, federated tier, or a combination — determines which capabilities that source can support. If you read our original data lake article and implemented that two-tier split, you're ahead of most. This article shows you where to go next.

---

## The Detection Engine and Intelligence Platform

Before we walk through 37 sources, you need to understand where the data goes and what you can do with it once it's there.

```
+-----------------------------------------------------------+
|                    ANALYTICS TIER                          |
|  Real-time alerting - SOAR - Entity enrichment            |
|  Latency: <5 min - Cost: $$$ per GB (~$5.59 PAYG)        |
|  <-> Data promotion (notebooks can write back)            |
+-----------------------------------------------------------+
|                     DATA LAKE                             |
|                                                           |
|  +----------+ +----------+ +----------+ +----------+     |
|  | KQL Query| |  Graph   | | Notebooks| |Agent/MCP |     |
|  |          | | Analytics| | (PySpark)| |  Access  |     |
|  +----------+ +----------+ +----------+ +----------+     |
|  | Ad-hoc   | | Blast    | | ML/Stats | | NL query |     |
|  | hunting  | | radius   | | Graph    | | Entity   |     |
|  | Forensic | | Attack   | | Frames   | | analysis |     |
|  | invest.  | | paths    | | Custom   | | Triage   |     |
|  |          | | GQL      | | tables   | | Hunting  |     |
|  +----------+ +----------+ +----------+ +----------+     |
|  Latency: Minutes  Near-RT    Batch     Conversational    |
|  Cost: $ per GB (~$0.05 — long retention, searchable)    |
+-----------------------------------------------------------+
|                   FEDERATED TIER                          |
|  Query in place - Databricks, ADLS Gen 2, Fabric         |
|  Zero ingestion cost - Zero egress cost                   |
|  All 4 surfaces query federated data alongside native     |
|  Cost: $0 ingestion (compute charges for queries only)    |
+-----------------------------------------------------------+
```

The **analytics tier** handles real-time detection. Sub-5-minute alert latency, SOAR playbook execution, entity enrichment. It's expensive per GB, but it's what drives your detection rules. If a log source doesn't feed the analytics tier, it doesn't contribute to real-time alerting.

The **data lake** used to be cheap storage with a search box. Not anymore. Microsoft added three capabilities that turn it into an active intelligence platform:

**KQL Query** — The hunting workbench. Ad-hoc queries against full-retention data. Same KQL language, spanning months or years instead of the analytics tier's 90-day window.

**Graph Analytics** — Sentinel Graph represents security data as nodes (accounts, devices, IPs, files) and edges (authentication events, network connections, file access). Blast radius analysis, attack path visualization, and relationship traversal become tractable when the data is structured as a graph.

**Notebooks (PySpark)** — Full Python and PySpark environment running directly on lake data. GraphFrames for graph algorithms (PageRank, shortest paths, connected components), ML for anomaly detection, and data promotion — notebooks can write computed results back to the analytics tier as custom tables.

**Agent/MCP Access** — The Sentinel MCP Server exposes lake data as structured tools for AI agents. Semantic table discovery, KQL execution against the lake, AI-powered entity risk analysis, and a full triage toolkit. SOC teams can wrap validated KQL queries as deterministic MCP tools — agents execute the exact query the human wrote, no hallucination risk.

**Federated Tier** — The third tier. Data that lives in Azure Databricks, ADLS Gen 2, or Microsoft Fabric can be queried directly from Sentinel without ingesting it. Zero ingestion cost, zero egress cost. Federated tables appear alongside native tables in KQL, notebooks, and MCP tools — the analyst doesn't need to know whether the table is native or federated. This solves three problems: historical data retention cost (federate years of archives instead of re-ingesting), cross-team data access (query data science outputs without moving them), and compliance-constrained data that cannot be copied due to data residency requirements. No other SIEM platform offers this capability.

> **Note:** Sentinel data federation is currently in public preview (April 2026). Preview features may change before GA. See [Data federation overview](https://learn.microsoft.com/en-us/azure/sentinel/datalake/data-federation-overview) for current status.

The key insight: **your ingestion pattern determines which surfaces work with your data.** Analytics-only means real-time alerting but no long-term hunting, no graph intelligence, no agent access to history. Lake-only means rich hunting and graph analysis but zero real-time detection. Dual-ingest gives you both — alert-grade events to analytics for immediate detection, full stream to the lake for everything else. Federated means you can query external data without any ingestion cost — extending your visibility to data you'd never pay to ingest. Sentinel Data Collection Rules handle the analytics/lake split at ingestion time through a single DCR transformation.

### Ingestion Patterns

Each log source below is labeled with one of three ingestion patterns. Here is what they mean and what data goes where.

| Pattern | Analytics Tier | Data Lake | How It Works |
|---------|---------------|-----------|--------------|
| **Analytics** | All events | Mirror (delayed) | Full stream to analytics for real-time detection. Data replicates to the lake via continuous data export rules on a delayed basis (minutes to hours). |
| **Data Lake** | — | All events | Full stream to the lake only. No real-time alerting. Used for high-volume sources where analytics-tier cost is not justified. |
| **Dual-Ingest** | Alert-grade subset | Full raw stream | Active DCR split at ingestion time. One collection point, two routing destinations. Alert-grade events go to analytics for real-time detection; the complete raw stream goes to the lake for hunting and forensics. |
| **Federated** | — | Query in place | No ingestion. Data stays in Databricks, ADLS Gen 2, or Fabric. Sentinel queries it via federation connectors. KQL, notebooks, and MCP tools all access federated tables. Cannot drive real-time analytics rules — use data promotion via notebooks to surface insights in the analytics tier. |

**The analytics mirror.** Even sources labeled "Analytics" are not trapped in the analytics tier. Sentinel continuous data export can replicate analytics-tier tables to the data lake (ADX-linked tables) on a delayed basis. This means your "Analytics only" sources — Entra Sign-in Logs, Defender for Identity, MDO Email Logs — can also feed long-term hunting and notebook analysis through the lake. The mirror adds latency (minutes to hours), but it means you do not have to choose between real-time detection and long-term retention. You get both.

**What goes where in dual-ingest.** For each dual-ingest source in the tables below, the prose description specifies exactly which events route to analytics and which route to the lake. The general pattern: analytics gets the alert-grade, high-signal subset that drives real-time rules; the lake gets the complete raw telemetry stream that powers forensics, hunting, and behavioral analysis. For the full decision framework that drives these assignments — including cost modeling, MITRE coverage tradeoffs, and KQL verification queries — see Article 05: The Design Decisions That Will Define Your Detection Capability.

**What goes where in federated.** Federated sources are data that already exists in external systems — you're extending your reach to it rather than ingesting it. AWS CloudTrail logs sitting in S3, CrowdStrike FDR telemetry in its output bucket, HR lifecycle data in a Fabric Lakehouse, risk signals computed in Databricks pipelines. The Sentinel Federation Ninja Show demonstrated the killer scenario: HR data in ADLS joined with risk signals in Databricks joined with sign-in logs in Sentinel — all queried from a single KQL interface. No data movement, no duplication, no ingestion cost.

---

## MITRE ATT&CK Tactic Coverage Heat Map

Here's how the 37 sources map across all 14 MITRE ATT&CK Enterprise tactics.

| Tactic | ID | Sources Covering | Coverage | Key Gap |
|--------|-----|-----------------|----------|---------|
| Reconnaissance | TA0043 | 1 | Low | Pre-compromise; limited by nature |
| Resource Development | TA0042 | 1 (CI/CD) | Low | External; requires threat intel feeds |
| **Initial Access** | **TA0001** | **21** | **Strong** | Well-covered across identity, email, network, federated cloud |
| Execution | TA0002 | 13 | Strong | Endpoint + AI agent coverage |
| Persistence | TA0003 | 17 | Strong | Identity + endpoint + cloud + federated cloud |
| Privilege Escalation | TA0004 | 11 | Moderate | Cloud-native escalation paths need attention |
| Defense Evasion | TA0005 | 13 | Moderate | Log tampering detection is the gap |
| Credential Access | TA0006 | 10 | Strong | Identity sources well-positioned |
| Discovery | TA0007 | 7 | Moderate | Asset inventory via federation adds context |
| **Lateral Movement** | **TA0008** | **7** | **Moderate** | East-west visibility is the differentiator |
| Collection | TA0009 | 9 | Strong | Federated HR and risk signals close the enrichment gap |
| **Command and Control** | **TA0011** | **6** | **Moderate** | Encrypted C2 requires network layer |
| Exfiltration | TA0010 | 15 | Strong | Multi-channel + cross-cloud federated coverage |
| Impact | TA0040 | 3 | Low | Detection via endpoint, not explicit rules |

Three gaps to focus on:

**Lateral Movement (TA0008)** — Only 7 sources cover this, and coverage depends heavily on east-west visibility. Without micro-segmentation logs, you can't confirm whether segmentation held during an incident. East-west firewall logs are the differentiator — elevate them from "nice-to-have" to priority for flat-network environments.

**Command and Control (TA0011)** — DNS, proxy, firewall session logs, and NDR provide the network layer coverage. The hard challenge is encrypted C2 — DNS-over-HTTPS and TLS-based C2 channels evade traditional proxy and firewall inspection. If your organization performs TLS inspection, those decrypted traffic logs significantly improve detection here.

**Discovery (TA0007)** — The data exists in current sources (MDE process events, Defender for Identity, DNS). The gap is detection rule quality, not log source coverage. Discovery techniques generate noisy telemetry — the action item is analytics rule tuning, not adding sources.

---

## What You're Blind to Without These

Let's be direct about the gaps. Each missing source creates a specific blind spot.

**Identity blindness** — Without Entra sign-in logs, you can't detect password spray or AiTM session theft. With 80% of password spray activity concentrated in just 20 ASNs, the patterns are there — but only if you're collecting the data. Without Defender for Identity, you can't see DCSync or Kerberoasting — the ransomware pre-encryption chain that gives you your last chance to stop the attack before encryption begins.

**Network blindness** — Without DNS logs, C2 beaconing through DGA domains is invisible. Without east-west firewall logs, lateral movement after initial access is a black box. You'll see the initial compromise and the final impact, but the middle of the attack chain — the part where you could contain the blast radius — is missing. Without proxy logs, phishing URL clicks and web-based C2 callbacks go untracked.

**Cloud blindness** — Without Defender for Cloud Apps, exfiltration to external cloud storage is invisible. Data collection occurred in 80% of incident response engagements, with 51% confirmed exfiltration. You need to see where it's going. Without Azure Activity Logs, cloud pivot after initial access goes undetected — the attacker modifies your infrastructure and you don't know.

**AI blindness** — Without Purview Information Protection, cross-prompt injection against M365 Copilot agents is undetected. Without Defender for AI Alerts, prompt injection against Azure AI endpoints is invisible. These are production attack vectors today, not theoretical risks. If you're deploying AI agents without these sources, you're flying blind on an entirely new attack surface.

**Graph blindness** — This is more subtle. Without edge-producing sources in the data lake (authentication events, network connections, file access logs), your graph analytics surfaces have nothing to traverse. The blast radius analysis that makes lateral movement detection tractable depends on having those relationship-producing logs in the lake. Analytics-only routing for identity and endpoint sources means you get real-time alerts but no graph intelligence, no agent access to historical context, and no notebook-driven behavioral baselines.

**Cross-cloud and enrichment blindness** — Without federation, your SOC can only investigate data that's been ingested into Sentinel. CloudTrail stays in S3, CrowdStrike FDR stays in its bucket, HR data stays in its database. Every cross-cloud incident requires manual console-switching. Every insider threat investigation requires emailing HR for employee status. Federation eliminates these gaps by extending your KQL reach to where the data already lives.

---

## Executive Summary for Security Leadership

*For the security leader who needs the strategic view:*

> **Four questions for the CISO:**
>
> 1. **Can we trace a credential theft chain end-to-end through our logs — and does that trace span all 14 MITRE ATT&CK tactics where we have exposure?** If your log architecture covers Initial Access but has blind spots in Lateral Movement and C2, you can detect the breach but not the full scope.
>
> 2. **Are we routing to the detection engine and intelligence platform intentionally?** The data lake is no longer passive storage. Graph analytics, notebooks, and MCP agent access turn lake-resident data into active intelligence. Organizations paying for lake storage but only using KQL queries are leaving three surfaces of capability on the table.
>
> 3. **Do we have detection coverage for AI agent exploitation across our deployed Copilot and Azure AI endpoints?** AI agent abuse (AI System Attacks-AI Supply Chain) is a production threat today. If your log architecture predates your AI deployment, the AI attack surface is unmonitored.
>
> 4. **Are we paying to ingest data that we could federate instead?** Organizations with existing data in Databricks, ADLS Gen 2, or Fabric can extend SIEM visibility at zero ingestion cost. Federation is the difference between "we can't afford to ingest that" and "we can query it for free."
>
> If the answer to any of these is "no" or "unknown," log architecture is the first investment to make. Every detection capability, forensic investigation, and hunting program depends on having the right data connected to the right tier at the right retention.

---

## Graph-Oriented Blast Radius Analysis

One of the most powerful capabilities unlocked by routing log data to the data lake is graph-oriented investigation. Here's an example that demonstrates 2-hop blast radius traversal from a compromised identity.

```kusto
// Find all resources reachable by a compromised identity within 2 hops
let CompromisedUser = "user@contoso.com";
let DirectAccess = SigninLogs
| where TimeGenerated > ago(30d)
| where UserPrincipalName == CompromisedUser
| where ResultType == 0
| summarize
    AccessCount = count(),
    LastAccess = max(TimeGenerated)
    by ResourceDisplayName, AppDisplayName, DeviceDetail_deviceId;
let DevicesUsed = DirectAccess | distinct DeviceDetail_deviceId;
let SecondHop = SigninLogs
| where TimeGenerated > ago(30d)
| where DeviceDetail_deviceId in (DevicesUsed)
| where UserPrincipalName != CompromisedUser
| where ResultType == 0
| summarize
    SharedUsers = dcount(UserPrincipalName),
    UserList = make_set(UserPrincipalName, 5)
    by DeviceDetail_deviceId, ResourceDisplayName;
DirectAccess
| extend HopLevel = "Direct"
| union (SecondHop | extend HopLevel = "Second-Hop via Shared Device")
| order by HopLevel asc, AccessCount desc
```

This simulates a 2-hop blast radius traversal in KQL — starting from a compromised identity, finding every resource they accessed, then finding every other identity that used the same devices. In a full graph analytics implementation, this traversal happens natively across nodes and edges. The KQL version shows you the pattern; the graph version makes it scalable.

---

## What Comes Next

This article covered the architecture — the 3-tier ingestion model, the four analytical surfaces, MITRE coverage mapping, blind spots, and the strategic framing for security leadership. The companion articles dive into the details:

**Article 2a: Maturity Tiers — Why the Phased Approach Matters.** Not every organization needs all 37 sources on day one. This article walks through the Must-Have, Should-Have, Advanced, and Federated tiers — why they're sequenced the way they are, and how to match your implementation pace to your threat model and team maturity.

**Article 2b: Must-Have and Should-Have Log Sources — The 20 Sources to Start With.** The first 20 sources across Microsoft-native, network, identity, and endpoint categories. Source-by-source guidance: what each gives you, which MITRE tactics it covers, connector configuration, and the detection/forensics/hunting value for each.

**Article 2c: Advanced and Federated Log Sources — Specialized Hunting and Zero-Cost Federation.** The remaining 17 sources — advanced hunting telemetry, AI agent logs, cloud infrastructure, and the federated tier. Includes the full federation architecture, cross-cloud investigation patterns, and insider threat enrichment via federated HR data.

---

## Download the Full Reference

The complete 37-source reference table is available on the [SOC Automators GitHub repo](https://github.com/mikepalitto/socautomators).

---

*This article is part of the "Threat-Informed Defense: Tools, Logs, and Agents" series.*
