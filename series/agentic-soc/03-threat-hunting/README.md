# Article 03 — Hunting at Machine Speed: KQL on the Sentinel Data Lake

**Live:** https://socautomators.substack.com/p/hunting-at-machine-speed-kql-on-the

This folder is the KQL library that pairs with Article 03. The article publishes one worked hunt inline (lateral movement). These six files are the rest of the library — referenced in the article and intended for adaptation, not blind execution.

## Files

| # | File | Threat / MITRE | What it does |
|---|------|----------------|--------------|
| 1 | [`01-auth-geography-baseline.kql`](01-auth-geography-baseline.kql) | Infostealer (Token Theft); TA0006 | Builds 180-day per-user sign-in geography baseline, flags recent sign-ins from never-before-seen locations |
| 2 | [`02-recon-breadth-scoring.kql`](02-recon-breadth-scoring.kql) | Suspicious Mailbox Activities; TA0007 Discovery | Flags identities whose 7-day daily resource breadth exceeds their own 90-day baseline by 3+ standard deviations |
| 3 | [`03-dns-beaconing-detection.kql`](03-dns-beaconing-detection.kql) | Nation-State DNS Tunneling; TA0011 C2 | Surfaces domains with sustained, high-entropy DNS query patterns over 30+ days within a 180-day window |
| 4 | [`04-lateral-movement-promoted-rule.kql`](04-lateral-movement-promoted-rule.kql) | Cloud Identity Abuse (Ransomware); TA0008 | Production-ready Scheduled Analytics Rule for the lateral-movement hunt published inline in the article |
| 5 | [`05-search-job-historical-c2.kql`](05-search-job-historical-c2.kql) | Nation-State (long-lived C2); TA0011 | Submit as Sentinel Search Job — 365-day async hunt for low-and-slow outbound connections |
| 6 | [`06-cross-vendor-federated-hunt.kql`](06-cross-vendor-federated-hunt.kql) | Cloud Identity Abuse; TA0008 | **Template** — joins MDE `DeviceProcessEvents` with a federated CrowdStrike FDR table (Sentinel data federation — Preview) |

## Before you run these

- **Behavioral baselines need clean data.** Legacy authentication and service-account noise will bury real signal until exclusion logic is built. Article 03 includes a hunt that produced only noise for exactly this reason.
- **Tune for your environment.** The thresholds in these files (180-day baselines, 5+ devices per 48 hours, 3-sigma deviation) are starting points. Your environment may need different windows or thresholds.
- **Preview-status capabilities.** Sentinel data federation and Sentinel MCP Graph tools are currently in **Preview** per Microsoft docs. The cross-vendor federated hunt template depends on federation; verify feature status for your tenant before relying on it for production detection.

## Unified incident model — read before promoting any of these to production rules

When Sentinel is onboarded to the Defender portal, Defender XDR owns the incident. Sentinel automation rules and Logic Apps playbooks that fired on incident creation under the legacy model may not behave the same way under the unified model. Before enabling any of these as Scheduled Analytics Rules in production, re-validate the downstream automation against the unified incident shape.

That is the failure mode Article 02 covers:
https://open.substack.com/pub/socautomators/p/migrating-to-unified-secops-without

## MCP-assisted hunting — Validator pattern

The Sentinel MCP server can generate KQL from natural-language hypotheses via `search_tables` and `query_lake`. Agents hallucinate column names and table schemas — confident, plausible, wrong. Treat agent-generated KQL as a draft. For any pattern that proves out, wrap the final query as a custom MCP tool with parameters fixed so agents execute exact, reviewed KQL rather than regenerating it every time.

The six files in this folder are exactly the kind of validated patterns that belong wrapped as custom MCP tools.

## License

GPL-3.0 — see the repo-level [LICENSE](../../../LICENSE).
