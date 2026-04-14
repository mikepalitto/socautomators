---
title: "2025 DBIR Threat Research Companion"
version: "1.0"
source: "Verizon 2025 Data Breach Investigations Report"
date: "2025-04-21"
document_type: "research-companion"
status: "curated"
source_file: "2025-dbir-data-breach-investigations-report.pdf"
tags: ["threat-research", "dbir", "breach-investigations", "verizon", "2025"]
related_docs: ["top-threats-2026.md", "2025-dbir-data-breach-investigations-report.md"]
---
# 2025 DBIR Threat Research Companion

This companion condenses the Verizon 2025 DBIR into threat-research notes that can be used alongside top-threats-2026.md. It prioritizes initial access, credential abuse, ransomware, social engineering, third-party exposure, and sector-level implications over general report narrative.

## Executive Summary

The strongest DBIR signal for 2025 is the continued convergence of three themes: vulnerability exploitation, credential-driven intrusion, and extortion-led monetization. Exploitation of vulnerabilities reached 20% of breaches and grew 34% year over year, while credential abuse remained the most common initial access vector at 22% in the non-Error, non-Misuse breach set. Ransomware continued to dominate complex intrusions, appearing in 44% of breaches overall and in 75% of System Intrusion breaches.

The second major signal is that third-party exposure is now a first-order breach driver rather than background risk. Third-party involvement doubled from 15% to 30% of breaches, and the report repeatedly ties operational disruption and downstream victimization to service providers, SaaS platforms, and credential reuse in third-party environments.

The third signal is that the modern credential ecosystem has become an industrialized access market. DBIR links infostealer logs, compromised databases, public code repositories, and ransomware victim disclosures into a coherent chain that supports access brokers, follow-on ransomware, and espionage-motivated access.

## Key Statistics Summary

| Category | Statistic | Value |
|----------|-----------|-------|
| Initial Access | Exploitation of vulnerabilities in breaches | 20% of breaches |
| Initial Access | Year-over-year growth in vulnerability exploitation | 34% increase |
| Initial Access | Edge devices and VPNs within exploitation cases | 22% |
| Initial Access | Fully remediated edge vulnerabilities | 54% |
| Initial Access | Median time to full remediation | 32 days |
| Credential Abuse | Use of stolen credentials in analyzed breaches | 22% |
| Credential Abuse | BWAA breaches involving stolen credentials | 88% |
| Credential Abuse | Systems in infostealer data estimated as enterprise devices | 30% |
| Credential Abuse | Corporate-login infostealer systems that were non-managed | 46% |
| Credential Abuse | Ransomware victims with domains found in infostealer or marketplace data | 54% |
| Credential Abuse | Ransomware victims with corporate emails in compromised logs | 40% |
| Ransomware | Ransomware presence in all reviewed breaches | 44% |
| Ransomware | Increase from prior year | 37% |
| Ransomware | Median ransom paid in 2024 | $115,000 |
| Ransomware | Victims that did not pay | 64% |
| Third Party | Third-party involvement in breaches | 30% |
| Third Party | Increase from prior year | doubled from 15% |
| Third Party | Median time to remediate leaked GitHub secrets | 94 days |
| Human Element | Breaches involving a human element | about 60% |
| Espionage | Breaches motivated by espionage | 17% |
| Espionage | Espionage breaches using vulnerability exploitation for initial access | 70% |
| AI | AI-assisted malicious emails over two years | doubled from roughly 5% to 10% |
| AI | Employees routinely accessing GenAI on corporate devices | 15% |
| AI | GenAI users with non-corporate account identifiers | 72% |
| AI | GenAI users with corporate email but no integrated auth | 17% |
| BEC | FBI IC3 reported BEC losses in 2024 | more than $6.3 billion |
| BEC | Median BEC loss | around $50,000 |

## Priority Threat Themes

### Vulnerability Exploitation Is Now a Core Access Path

The report frames exploitation of vulnerabilities as one of the clearest year-over-year escalations. The 20% share of breaches and 34% growth rate matter on their own, but the more actionable signal is where the exploitation is landing: edge devices, VPNs, firewall and management interfaces, file transfer systems, and externally reachable services that are difficult to patch quickly.

The remediation data is equally important for research and defensive planning. DBIR notes that only 54% of edge vulnerabilities were fully remediated during the year, and median remediation took 32 days. That lag explains why adversaries can repeatedly operationalize a small number of high-value flaws across large victim sets.

### Credential Ecosystems Are Feeding Both Ransomware and Espionage

DBIR’s strongest research contribution is the way it connects multiple credential sources. Infostealer logs, compromised databases, leaked secrets in repositories, and brute-force activity all reinforce the same operational reality: adversaries increasingly prefer valid access over noisy exploitation when they can get it.

The report’s numbers justify treating credential theft as a precursor ecosystem rather than a single technique. Thirty percent of sampled infostealer-compromised systems were estimated to be enterprise-licensed devices, 46% of corporate-login devices in that subset were non-managed, and 54% of ransomware victims had domains that appeared in infostealer or marketplace data. That is strong evidence for access-broker and follow-on monetization hypotheses.

### Ransomware Remains the Dominant Complex Intrusion Outcome

Ransomware remains the anchor threat for System Intrusion. It appeared in 44% of breaches overall, rose 37% from last year, and accounted for 75% of breaches within the System Intrusion pattern. The notable change is not reduced prevalence, but economic pressure on payouts: median paid ransom dropped to $115,000, and 64% of victims did not pay.

For research purposes, the most important reading is that attacker pressure did not decline even as payments softened. The intrusion model still depends on compromised credentials, exploited vulnerabilities, phishing, and partner exposure, with attackers adjusting demands and victim targeting rather than abandoning the model.

### Social Engineering Is Maturing Beyond Basic Phishing

DBIR reinforces that phishing is still central, but it also highlights broader social-engineering tradecraft. Prompt bombing, token theft, AiTM, SIM-swap-adjacent account compromise, and long-running relationship-building all appear as part of the same problem set.

The report also provides operationally useful BEC context: more than $6.3 billion in FBI IC3 losses, a median loss around $50,000, and wire transfer remaining the preferred payout rail at 88%. That suggests BEC remains one of the most scalable monetization tracks even as ransomware dominates headlines.

### Third-Party Risk Has Shifted From Governance Concern to Intrusion Multiplier

Third-party involvement doubling to 30% of breaches is the most important cross-cutting control signal in the report. Snowflake, Change Healthcare, CDK Global, and similar examples matter not just as isolated case studies, but as proof that attackers are exploiting concentration risk, shared infrastructure, and poor identity hygiene at provider boundaries.

This should influence threat research in two ways. First, third-party compromise needs to be treated as an initial-access and blast-radius problem. Second, partner dependency creates asymmetric downstream impact, especially when the victim does not control patching speed, MFA enforcement, token lifetime, or platform telemetry.

### AI Risk Is Present, but Access and Data Governance Still Matter More

DBIR does not support a fully AI-dominated threat narrative. Instead, it shows a measured but real increase in AI-enabled attacker effectiveness and enterprise exposure. AI-assisted malicious emails roughly doubled over two years, and 15% of employees were routinely accessing GenAI systems from corporate devices, often outside managed identity controls.

The more immediate research implication is not autonomous AI attacks, but leakage, policy bypass, and improved phishing quality. That places AI risk closer to existing identity, data protection, and social-engineering programs than to a completely separate threat category.

## Sector Notes

### Small- and Medium-Sized Businesses

SMBs remain disproportionately exposed to ransomware. DBIR reports ransomware in 88% of SMB breaches versus 39% in large organizations. The pattern suggests that smaller organizations are still attractive targets because they share the same attack surface categories as larger enterprises but generally operate with weaker recovery depth and lower control maturity.

### Healthcare

Healthcare remains a high-value target where system availability and patient-impacting operations amplify attacker leverage. System Intrusion overtook Miscellaneous Errors as the top breach pattern, and high-profile partner breaches remain central to sector risk. Medical data continues to be a major compromised data type.

### Manufacturing

Manufacturing showed one of the sharper espionage shifts in the report, with espionage-motivated breaches rising to 20% from 3% the prior year. Internal plans, reports, and email data were highly represented, which supports treating manufacturing as both a monetization target and an intelligence target.

### Public Sector

Public Sector breaches remained steady even as one contributor gap reduced incident totals. Ransomware appeared in 30% of public-sector breaches, and Misdelivery remained the leading error variety. The report also notes prompt bombing and credential misuse in government-targeted social-engineering activity.

## Top Threats 2026 Mapping Updates

| Existing threat in top-threats-2026.md | DBIR evidence to incorporate |
|----------------------------------------|------------------------------|
| Vulnerability Exploitation | Raise emphasis on edge devices, VPNs, and externally exposed management interfaces; include 20% breach share, 34% growth, 22% edge/VPN share, and 32-day median remediation |
| Leaked Credentials | Add repository-secret exposure and infostealer linkage; include 94-day median leaked secret remediation and 54% ransomware victim domain overlap with infostealer data |
| Ransomware and Human-Operated Attacks | Add DBIR’s 44% overall prevalence, 75% share within System Intrusion, $115K median paid ransom, and 64% non-payment rate |
| Business Email Compromise | Add 2024 FBI IC3 loss figure greater than $6.3B, median loss around $50K, and 88% wire-transfer preference |
| Phishing Attempts | Expand to include prompt bombing, token theft, AiTM, and the limited but real effect of training on reporting rather than click elimination |
| Access Broker Activity | Tie access brokers more directly to infostealer marketplaces, premium channels, live logs, and ransomware victim overlap |
| Nation-State Cyber Espionage | Add 17% espionage breach share overall and the 70% vulnerability-exploitation rate in espionage initial access |
| AI-Enhanced Social Engineering | Use the DBIR AI-assisted malicious-email increase as corroboration, but keep priority below credential theft, ransomware, and vulnerability exploitation |
| Cloud Workload and Container Compromise | Supplement with third-party/SaaS platform exposure and credential concentration risk where cloud control planes are identity-bound |

## Research Implications for the SOC Agent Work

1. Prioritize detection content and enrichment around valid-account abuse, leaked secrets, and infostealer-derived access because DBIR shows those are upstream enablers for multiple downstream threats.
2. Treat third-party compromise as part of initial access triage logic, not as a separate governance-only topic. The research evidence now supports operational correlation with provider incidents, partner accounts, and SaaS identity events.
3. Increase weight on ransomware precursor signals that combine vulnerability exploitation, credential reuse, and external remote access services. DBIR repeatedly ties those together.
4. Add sector-aware tuning for healthcare, manufacturing, public sector, and SMB environments where the dominant threat mix and business impact differ materially.
5. Keep AI threat coverage grounded in measurable exposure and phishing enhancement rather than speculative model-centric threats unless other sources provide stronger operational evidence.

## Limitations

This brief is a curated research summary, not a verbatim restatement of the DBIR. The underlying report remains the authoritative source for exact language, methodology, and context. Use the structured markdown companion for deeper citation and page-level review.
