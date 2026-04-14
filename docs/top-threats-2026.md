# Top Threats 2026

**Version 8.0** | **Source: Microsoft Digital Defense Report 2025**

---

## Key Statistics Summary

| Category | Statistic | Value |
|----------|-----------|-------|
| **Initial Access** | ClickFix social engineering prevalence | 47% of initial access attempts |
| **Initial Access** | Device code phishing increase (H2 2024) | 93% increase |
| **Initial Access** | Infostealer malware prevalence | 51% of initial access methods |
| **Initial Access** | Phishing/social engineering as breach initiator | 28% of breaches |
| **Identity** | Cloud identity abuse increase | 23% increase |
| **Identity** | Password spray concentration (20 ASNs) | 80% of spray activity |
| **Identity** | Leaked credentials in dark web databases | 85% of breached credentials |
| **Identity** | Average credential appearances per username | 3 separate logs |
| **BEC & Email** | BEC as attack outcome | 21% (vs 16% ransomware) |
| **BEC & Email** | Research/academia sector BEC incidents | 49% of BEC incidents |
| **Data Theft** | Data collection in IR engagements | 80% of engagements |
| **Data Theft** | Confirmed data exfiltration | 51% of engagements |
| **Data Theft** | Ransomware incidents with data exfiltration | 82% of incidents |
| **Ransomware** | Human-operated ransomware increase | 87% YoY increase |
| **Ransomware** | Use of RMM tools for persistence | 79% of cases |
| **Ransomware** | Hybrid attacks (on-prem + cloud) | 40% of attacks |
| **Ransomware** | Average dwell time | 12 days |
| **Ransomware** | Average attack length | 58 days |
| **Cloud** | Azure security incident increase | 26% increase |
| **Cloud** | Cloud attacks involving cryptomining | 58% of attacks |
| **Cloud** | Container infection median time | Under 48 hours |
| **Vulnerability** | Breaches via unpatched web assets | 18% of breaches |
| **Access Brokers** | Identified brokers | 368 brokers |
| **Access Brokers** | Industries affected | 68 industries |
| **Access Brokers** | Countries affected | 131 countries |
| **Access Brokers** | Credential-based access methods | 80% of access sold |
| **AI Threats** | Organizations with AI-linked security incidents | 57% of organizations |
| **AI Threats** | AI-enhanced phishing click-through rate | 54% (vs 12% traditional) |
| **Insider** | Average insider incident containment time | 81 days |
| **Nation-State** | China IT sector targeting | 23% of activities |
| **Nation-State** | Iran targeting Israel | 64% of activities |
| **Nation-State** | Russia government entity targeting | 25% of activities |

---

## Table of Contents

- [1. Executive Summary](#1-executive-summary)
- [2. Unified Product Mapping Table](#2-unified-product-mapping-table)
- [3. Top 20 Threat Catalogue](#3-top-20-threat-catalogue)
  - [3.1 Infostealer Malware](#31-infostealer-malware)
  - [3.2 ClickFix Social Engineering](#32-clickfix-social-engineering)
  - [3.3 Device Code Phishing](#33-device-code-phishing)
  - [3.4 AI-Enhanced Social Engineering](#34-ai-enhanced-social-engineering)
  - [3.5 Cloud Identity Abuse](#35-cloud-identity-abuse)
  - [3.6 Password Spray Attacks](#36-password-spray-attacks)
  - [3.7 Leaked Credentials](#37-leaked-credentials)
  - [3.8 Business Email Compromise](#38-business-email-compromise)
  - [3.9 Phishing Attempts](#39-phishing-attempts)
  - [3.10 Email Bombing and Vishing](#310-email-bombing-and-vishing)
  - [3.11 Malware Detection](#311-malware-detection)
  - [3.12 Ransomware and Human-Operated Attacks](#312-ransomware-and-human-operated-attacks)
  - [3.13 Data Exfiltration](#313-data-exfiltration)
  - [3.14 Cloud Workload and Container Compromise](#314-cloud-workload-and-container-compromise)
  - [3.15 Vulnerability Exploitation](#315-vulnerability-exploitation)
  - [3.16 Access Broker Activity](#316-access-broker-activity)
  - [3.17 Suspicious Mailbox Activities](#317-suspicious-mailbox-activities)
  - [3.18 Nation-State Cyber Espionage](#318-nation-state-cyber-espionage)
  - [3.19 AI System Attacks](#319-ai-system-attacks)
  - [3.20 Insider Threats](#320-insider-threats)
- [4. Glossary](#4-glossary)

---

## 1. Executive Summary

The threat landscape in 2025 has undergone fundamental shifts that require organizations to rethink how they protect identities, data, and cloud environments. This version of the Top Threats document reflects these changes, expanding from 7 to 20 threats and incorporating findings from the Microsoft Digital Defense Report 2025. The threats documented here represent the most significant risks organizations face today, spanning identity compromise, AI-enabled attacks, cloud-native threats, and sophisticated social engineering campaigns.

### Initial Access Evolution

Initial access methods have evolved dramatically. ClickFix social engineering now accounts for 47% of initial access attempts, representing a shift from traditional email-based phishing to command-line execution attacks that bypass security controls. Device code phishing has increased 93% in the second half of 2024, enabling attackers to steal tokens without requiring passwords. Infostealer malware has reached 51% prevalence, with Lumma Stealer dominating the landscape and providing foundational access for downstream attacks. These modern initial access techniques demonstrate how attackers have adapted to improved email security and multifactor authentication deployments.

### Identity as Primary Target

Identity remains the primary target across the threat landscape. Cloud identity abuse increased 23%, with attackers targeting OAuth tokens, service principals, and workload identities rather than traditional user credentials. Password spray attacks continue to affect organizations globally, with just 20 autonomous system numbers responsible for 80% of observed activity. Leaked credentials appear in an average of three separate credential logs per username, with 85% of breached credentials available in dark web databases. These identity-focused threats highlight why phishing-resistant multifactor authentication remains the gold standard for security, blocking over 99% of unauthorized access attempts.

### Business Email Compromise and Data Exfiltration

Business email compromise and data exfiltration have emerged as primary attack objectives. Business email compromise now represents 21% of attack outcomes compared to 16% for ransomware, with the research and academia sector experiencing 49% of BEC incidents. Data exfiltration occurred in 80% of Microsoft incident response engagements, with 51% representing confirmed data theft. Eighty-two percent of ransomware incidents involved data exfiltration before encryption, demonstrating the shift toward double and triple extortion models. Suspicious mailbox activities including inbox rule manipulation and email forwarding enable both data theft and preparation for financial fraud.

### Ransomware and Destructive Attacks

Ransomware and destructive attacks have intensified in both frequency and impact. Human-operated ransomware campaigns increased 87% year-over-year, with attackers deploying destructive malware in cloud environments to maximize damage. Seventy-nine percent of ransomware operators use remote monitoring and management tools for persistent access, while 40% employ hybrid ransomware variants targeting both on-premises and cloud resources. The median time from infection to ransom demand remains under 48 hours in cloud workload compromises, compressing response windows and demanding rapid detection capabilities.

### Cloud Environment Threats

Cloud environments face escalating threats across workloads, containers, and infrastructure. Azure security incidents increased 26%, with 58% of cloud attacks involving cryptomining operations. Container compromise has accelerated, with median infection times under 48 hours from initial access to cryptomining deployment. Vulnerability exploitation in cloud-exposed infrastructure accounts for 18% of breaches, targeting systems including SimpleHelp, BeyondTrust, Fortinet, Cleo, and Apache Tomcat. Organizations must implement continuous cloud workload monitoring, container runtime protection, and rapid vulnerability management to defend cloud environments effectively.

### Cybercrime Economy

The cybercrime economy has matured with specialized roles and services enabling sophisticated attacks. Access brokers have affected 68 industries across 131 countries, with 368 identified brokers selling persistent access to ransomware operators and data extortion groups. Eighty percent of access methods sold involve credential-based attacks, bundled with reconnaissance data to accelerate buyer operations. This specialization allows threat actors to focus on monetization rather than initial compromise, increasing both attack velocity and success rates.

### Nation-State and Insider Threats

Nation-state actors and insider threats represent strategic risks beyond traditional cybercrime. Nation-state cyber espionage targets IT, government, and research sectors with advanced tradecraft including living-off-the-land techniques and supply chain compromise. North Korean IT worker infiltration embeds operatives globally for revenue generation with potential for espionage and sabotage, requiring organizations to enhance insider threat detection and background verification. The average containment time for insider incidents remains 81 days, highlighting detection challenges when threats originate from trusted insiders with legitimate access.

### AI-Enabled Threats

Artificial intelligence introduces both new attack vectors and enhanced threat capabilities. Fifty-seven percent of organizations experienced increased security incidents linked to AI usage, spanning prompt injection, training data poisoning, and insecure plugin architectures. AI-enhanced social engineering achieves 54% click-through rates compared to 12% for traditional phishing, with potential for 50 times greater profitability. Attackers use generative AI to create deepfakes, synthetic identities, and polymorphic malware, while simultaneously targeting AI systems themselves to bypass safety controls or extract proprietary models.

### Recommendations

The unified product mapping table in this document demonstrates how Microsoft security solutions provide comprehensive detection and response across this expanded threat landscape. Organizations should prioritize phishing-resistant multifactor authentication, implement zero trust architecture, deploy cloud-native security controls, and establish continuous monitoring for identity, data, and workload protection. By understanding these 20 threats and mapping them to defensive capabilities, partners can guide customers toward resilient security architectures that address both current attacks and emerging risks in 2025 and beyond.

---

## 1.1 How to Use This Document

This document provides guidance on the top threats identified in Microsoft security engagements. Partners use this document to prepare for customer engagements and to map discovered threats to Microsoft security products and recommended mitigations.

Each threat entry includes a description, detection themes, and recommended mitigation strategies aligned with Microsoft 365 and Azure security products. Use the Unified Product Mapping Table to quickly identify which products detect and mitigate specific threats.

The threat catalogue reflects the current landscape based on the Microsoft Digital Defense Report 2025 and addresses emerging attack vectors including AI-enabled threats, cloud-native attacks, and modern initial access techniques.

---

## 2. Unified Product Mapping Table

The following table provides a consolidated view of which Microsoft security products detect and respond to each threat in the Top 20 Threat Catalogue. This mapping helps organizations understand product coverage across the threat landscape and identify opportunities to enhance detection and response capabilities.

| Threat | Microsoft Products | Detection Coverage | Response Coverage |
|--------|-------------------|-------------------|-------------------|
| Infostealer Malware | Microsoft Defender for Endpoint, Microsoft Defender XDR, Microsoft Entra ID Protection, Microsoft Defender for Cloud Apps | Behavioral analysis of credential access, monitoring for known infostealer signatures, anomalous authentication patterns | Automated containment, credential reset workflows, identity protection policies |
| ClickFix Social Engineering | Microsoft Defender for Office 365, Microsoft Defender for Endpoint, Microsoft Defender XDR, Microsoft Defender SmartScreen | Email content analysis, script execution monitoring, browser protection against malicious sites | Automatic remediation of malicious emails, endpoint isolation, user notification |
| Device Code Phishing | Microsoft Entra ID Protection, Microsoft Defender for Cloud Apps, Microsoft Defender XDR, Microsoft Security Copilot | Device code authentication monitoring, anomalous OAuth token usage, cloud app access patterns | Conditional access enforcement, token revocation, automated investigation |
| AI-Enhanced Social Engineering | Microsoft Defender for Office 365, Microsoft Entra ID Protection, Microsoft Security Copilot, Microsoft Defender for Cloud Apps | Advanced phishing detection, identity risk scoring, AI-powered threat analysis | Email quarantine, identity protection policies, automated response orchestration |
| Cloud Identity Abuse | Microsoft Entra ID Protection, Microsoft Defender for Cloud Apps, Microsoft Defender for Identity, Microsoft Defender XDR | OAuth token anomalies, workload identity abuse, service principal monitoring | Conditional access policies, token revocation, identity investigation |
| Password Spray Attacks | Microsoft Entra ID Protection, Microsoft Defender for Identity, Microsoft Defender XDR | Failed authentication pattern analysis, distributed attack correlation, identity risk detection | Account protection policies, smart lockout, automated investigation |
| Leaked Credentials | Microsoft Entra ID Protection, Microsoft Defender XDR, Microsoft Sentinel | Credential leak detection, anomalous sign-in monitoring, threat intelligence integration | Password reset enforcement, conditional access, risk-based authentication |
| Business Email Compromise | Microsoft Defender for Office 365, Microsoft Purview, Microsoft Defender for Cloud Apps, Microsoft Defender XDR | Mailbox intelligence, payment fraud detection, user impersonation analysis | Email remediation, mailbox recovery, communication compliance alerts |
| Phishing Attempts | Microsoft Defender for Office 365, Microsoft Defender for Endpoint, Microsoft Entra ID Protection, Microsoft Security Copilot | URL reputation analysis, attachment detonation, credential harvest detection | Automatic email quarantine, user training, post-breach investigation |
| Email Bombing and Vishing | Microsoft Defender for Office 365, Microsoft Defender XDR, Microsoft Entra ID Protection | Email volume anomaly detection, authentication pattern analysis, cross-channel attack correlation | Email filtering, conditional access enforcement, automated response |
| Malware Detection | Microsoft Defender for Endpoint, Microsoft Defender for Office 365, Microsoft Defender XDR | Signature-based detection, behavioral analysis, AI-generated malware identification | Automatic malware remediation, endpoint isolation, threat investigation |
| Ransomware and Human-Operated Attacks | Microsoft Defender for Endpoint, Microsoft Defender XDR, Microsoft Defender for Cloud, Microsoft Sentinel | Ransomware behavior monitoring, RMM tool abuse detection, encryption activity analysis | Automated attack disruption, endpoint isolation, backup restoration guidance |
| Data Exfiltration | Microsoft Purview, Microsoft Defender for Cloud Apps, Microsoft Defender XDR, Microsoft Sentinel | Data movement monitoring, sensitive data classification, exfiltration pattern detection | Data loss prevention enforcement, cloud app blocking, incident investigation |
| Cloud Workload and Container Compromise | Microsoft Defender for Cloud, Microsoft Defender for Containers, Microsoft Defender XDR, Microsoft Sentinel | Container runtime protection, cryptomining detection, cloud workload monitoring | Automated container isolation, vulnerability remediation, cloud security posture management |
| Vulnerability Exploitation | Microsoft Defender for Endpoint, Microsoft Defender Vulnerability Management, Microsoft Defender for Cloud, Microsoft Defender XDR | Vulnerability scanning, exploitation attempt detection, post-exploitation behavior analysis | Patch deployment guidance, attack surface reduction, endpoint protection |
| Access Broker Activity | Microsoft Defender for Identity, Microsoft Defender for Endpoint, Microsoft Defender XDR, Microsoft Sentinel | Reconnaissance detection, credential access monitoring, persistence mechanism identification | Access revocation, lateral movement prevention, threat hunting |
| Suspicious Mailbox Activities | Microsoft Defender for Office 365, Microsoft Defender XDR, Microsoft Purview, Microsoft Entra ID Protection | Inbox rule monitoring, mailbox permission change detection, email forwarding analysis | Mailbox rule removal, permission revocation, audit log investigation |
| Nation-State Cyber Espionage | Microsoft Defender XDR, Microsoft Defender for Endpoint, Microsoft Sentinel, Microsoft Entra ID Protection | Advanced threat hunting, living-off-the-land technique detection, nation-state threat intelligence | Coordinated response orchestration, asset isolation, long-term monitoring |
| AI System Attacks | Microsoft Purview, Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection, Microsoft Security Copilot | Anomalous AI usage patterns, data access monitoring, prompt injection detection | Data governance enforcement, AI access restriction, usage audit |
| Insider Threats | Microsoft Purview, Microsoft Defender for Cloud Apps, Microsoft Entra ID Protection, Microsoft Sentinel | User behavior analytics, data exfiltration monitoring, privilege escalation detection | Data loss prevention, access revocation, insider risk investigation |

---

## 3. Top 20 Threat Catalogue

### 3.1 Infostealer Malware

**Threat ID:** T001 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Infostealer malware includes families such as Lumma Stealer, RedLine, Vidar, Atomic Stealer, and Raccoon Stealer that extract credentials, browser session tokens, and system context data from infected devices. These tools are typically delivered through malvertising, search engine optimization poisoning, cracked software, and social engineering techniques like ClickFix. Infostealers have evolved from post-exploitation tools to foundational components of modern access campaigns, enabling a division of labor across the cybercriminal ecosystem where initial operators deploy the malware, access brokers monetize the stolen data, and downstream actors use credentials to gain enterprise footholds.

#### Why This Threat Matters

Infostealer infections represent more than isolated compromises—they pose strategic risk of broader enterprise-wide intrusions. Organizations experiencing an infostealer infection are at high risk of future breaches including ransomware, data exfiltration, and extortion. With infostealers accounting for 51% of initial access methods observed by Microsoft Defender Experts, this threat enables ransomware groups and nation-state actors to bypass traditional security controls by using legitimate stolen credentials. The threat is amplified by the low cost and high availability of infostealer malware-as-a-service platforms that continuously evolve with real-time updates and enhanced capabilities.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unusual downloads from content delivery networks or GitHub repositories mimicking popular software
- Loader activity such as HijackLoader or Legion that precedes payload delivery
- Clipboard-to-shell behavior, especially PowerShell scripts from suspicious download paths
- Abnormal browser or credential store access patterns indicating data harvesting
- Execution of commands copied from external sources into terminal or command-line interfaces

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Endpoint | Detects infostealer execution, monitors clipboard-to-shell behavior, and blocks malicious downloads through behavior-based detection and real-time protection |
| Microsoft Defender XDR | Correlates signals across endpoints, identity, and cloud to identify infostealer infections and downstream compromise attempts |
| Microsoft Entra ID Protection | Detects sign-ins using stolen credentials and tokens, triggering risk-based conditional access policies |
| Microsoft Defender for Cloud Apps | Identifies anomalous cloud access patterns from compromised credentials and monitors session token abuse |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Endpoint Protection:** Deploy endpoint detection and response solutions with behavior-based analytics to detect and block infostealer execution, including monitoring for loader activity and clipboard manipulation
- **Credential Hygiene:** Limit password storage and autofill features on unmanaged or shared endpoints, implement phishing-resistant multifactor authentication, and monitor for credential exposure in breach databases
- **User Education:** Train users to recognize deceptive downloads, fake update pages, cracked tools, and social engineering techniques that deliver infostealers
- **Application Control:** Use Windows Defender Application Control or AppLocker to restrict execution of unauthorized applications and scripts, particularly from untrusted download locations

---

### 3.2 ClickFix Social Engineering

**Threat ID:** T002 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

ClickFix is a social engineering technique that tricks users into copying malicious commands from fake pop-ups, job applications, or support messages and pasting them into the Windows Run dialog or terminal. This approach bypasses traditional phishing protections by convincing users to execute PowerShell or mshta.exe commands themselves, which then pull malicious payloads directly into memory in a fileless process. ClickFix emerged in November 2024 and rapidly became the most common initial access method, used by both cybercriminal and nation-state actors to deliver infostealers, remote access trojans, and worms.

#### Why This Threat Matters

ClickFix represented 47% of initial access methods observed by Microsoft Defender Experts, making it the primary attack vector in 2025. Traditional phishing protections cannot catch ClickFix because the malicious activity occurs when users manually execute commands rather than clicking suspicious links. Successful campaigns have led to credential theft, malware staging, and persistent access using just a few keystrokes from the user. The technique is particularly effective because it appears legitimate and often mimics common troubleshooting or software update instructions, exploiting user trust in technical support processes.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Clipboard usage followed by immediate shell launches such as cmd.exe or powershell.exe
- Execution of PowerShell scripts with unusual command-line arguments sourced from clipboard content
- Browser or application activity involving copy operations followed by terminal execution
- PowerShell script execution from untrusted zones or with suspicious download patterns
- Unusual mshta.exe execution triggered by user-initiated commands

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Endpoint | Monitors clipboard-to-terminal behavior patterns, detects PowerShell script execution from suspicious sources, and blocks fileless malware execution |
| Microsoft Defender XDR | Correlates user clipboard activity with downstream execution patterns to identify ClickFix attack chains across endpoints |
| Microsoft Defender for Office 365 | Detects phishing emails and malicious content that contain ClickFix instructions or social engineering lures |
| Windows Defender Application Control | Restricts execution of unauthorized scripts and enforces PowerShell Constrained Language Mode to limit abuse |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **User Awareness:** Train users to recognize that pasting commands from unknown sources is as risky as clicking suspicious links, and educate them on ClickFix social engineering tactics
- **Script Execution Controls:** Enable PowerShell script block logging and use Constrained Language Mode to limit unauthorized script execution capabilities
- **Browser Security:** Disable clipboard access and scripting in untrusted zones through browser security policies and group policy settings
- **Behavioral Monitoring:** Implement detection rules that correlate clipboard usage with shell launches and flag suspicious execution flows from user-initiated commands

---

### 3.3 Device Code Phishing

**Threat ID:** T003 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

Device code phishing exploits the device code authentication flow to capture access and refresh tokens without requiring a password. Attackers trick users into entering a device code on legitimate authentication portals through phishing emails or third-party messaging applications, often posing as trusted contacts such as administrators or program organizers. Once the user enters the code, the attacker gains access and captures the tokens, enabling persistent access to target accounts, data, and services. This technique bypasses multifactor authentication and can maintain access even after password resets.

#### Why This Threat Matters

Device code phishing poses a high risk of data theft and exfiltration because it grants attackers access to data where the compromised user has permissions without needing a password. Ninety-three percent of device code phishing events observed by Microsoft occurred in the second half of 2024, indicating rapid adoption by both nation-state actors from Russia, Iran, and China, as well as cybercriminal groups. The technique is particularly dangerous because it uses legitimate authentication flows, making it difficult for traditional phishing detection tools to identify. Attackers have evolved tactics to include prompting victims to enter device codes into Teams invitations, making fraudulent activity harder for users to recognize.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unusual device code authentication requests from unfamiliar locations or devices
- Multiple device code generation attempts in short time periods
- Device code authentication flows initiated from suspicious IP addresses or geographic locations
- Token generation patterns that do not match typical user behavior
- Authentication attempts using valid device codes but with anomalous session characteristics

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Entra ID Protection | Detects anomalous device code authentication patterns and flags suspicious sign-in attempts based on risk scoring |
| Microsoft Defender for Cloud Apps | Monitors session token usage and identifies abnormal access patterns following device code authentication |
| Microsoft Defender XDR | Correlates device code phishing attempts with downstream malicious activity across identity, email, and cloud workloads |
| Microsoft Sentinel | Aggregates authentication logs to detect patterns of device code abuse and enables hunting for coordinated phishing campaigns |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Conditional Access Policies:** Implement risk-based conditional access that challenges or blocks authentication from suspicious locations, devices, or authentication flows
- **User Education:** Train users to recognize device code phishing attempts, especially those delivered through out-of-band communications like messaging apps or phone calls
- **Authentication Controls:** Disable device code authentication flow for user populations where it is not required, reducing the attack surface
- **Continuous Monitoring:** Deploy real-time monitoring for device code generation and usage patterns, with automated response to revoke suspicious tokens and sessions

---

### 3.4 AI-Enhanced Social Engineering

**Threat ID:** T004 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

AI-enhanced social engineering leverages generative artificial intelligence to create highly convincing phishing campaigns, deepfake audio and video content, and fraudulent messages at scale. Attackers use AI to automate the creation of personalized phishing emails, generate realistic voices for vishing attacks, and craft deceptive scenarios that adapt to defensive measures in real time. AI-automated phishing achieved 54% click-through rates compared to 12% for standard attempts, representing a 4.5x increase in effectiveness. These attacks enable scalable, multi-vector intrusions with minimal operational overhead and can increase profitability by up to 50 times through targeted automation.

#### Why This Threat Matters

AI-enhanced social engineering fundamentally changes the threat landscape by enabling attackers to operate at machine speed and scale. Traditional security awareness training becomes less effective when AI generates personalized, contextually relevant phishing content that closely mimics legitimate communications. The technology enables attackers to conduct sophisticated social engineering campaigns against thousands of targets simultaneously while maintaining the appearance of individualized, trusted communications. Organizations face increased risk of credential theft, business email compromise, and initial access attacks that bypass conventional email security controls through highly convincing AI-generated content.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Highly personalized phishing emails that reference specific organizational details or recent events
- Voice or video communications that exhibit subtle artifacts or inconsistencies in deepfake content
- Unusually high volumes of targeted phishing attempts with individualized messaging
- Social engineering attempts that rapidly adapt tactics when initial approaches fail
- Communications that combine multiple attack vectors such as email, phone calls, and messaging applications

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Office 365 | Uses AI-powered detection to identify sophisticated phishing attempts, including those using AI-generated content and impersonation techniques |
| Microsoft Purview | Detects and classifies sensitive information sharing attempts and monitors for data exfiltration following successful social engineering |
| Microsoft Security Copilot | Analyzes attack patterns and assists security teams in identifying AI-enhanced social engineering campaigns through natural language queries |
| Microsoft Defender XDR | Correlates social engineering attempts across email, identity, and endpoints to detect coordinated AI-driven campaigns |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Enhanced User Awareness:** Train users to recognize AI-generated content characteristics and implement verification procedures for sensitive requests, regardless of how convincing they appear
- **Multi-Channel Verification:** Establish out-of-band verification processes for high-risk actions such as financial transactions or credential changes, using trusted communication channels
- **AI-Powered Defense:** Deploy AI-driven security tools that can detect subtle patterns and anomalies in AI-generated phishing content at machine speed
- **Zero Trust Architecture:** Implement conditional access policies and phishing-resistant multifactor authentication to limit the impact of successful social engineering attacks

---

### 3.5 Cloud Identity Abuse

**Threat ID:** T005 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

Cloud identity abuse encompasses attacks targeting authentication mechanisms in cloud environments, including OAuth token theft, app consent phishing, Key Vault pivoting, and workload identity compromise. As organizations implement phishing-resistant multifactor authentication for user accounts, attackers are pivoting to target workload identities—apps, services, and scripts that access cloud resources—which often hold elevated privileges but lack sufficient security controls. Attacks include malicious OAuth apps that trick users into granting permissions, compromising apps with access to secrets for lateral movement, and combining device code phishing with OAuth consent phishing to bypass multifactor authentication.

#### Why This Threat Matters

Cloud identity abuse attacks increased by 23% in Azure environments, representing a fundamental shift in attacker tactics as traditional user identity protections improve. These attacks persist beyond password resets because they target authentication tokens and application permissions rather than credentials. Compromised workload identities can access any resource or process that the identity is trusted to access, including email, cloud services, and on-premises environments. The threat is amplified because attackers can conduct entire end-to-end attacks as legitimate users or resources, making detection extremely difficult without specialized monitoring of OAuth permissions, token usage, and workload identity behavior.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unusual OAuth application consent requests or applications with excessive permissions
- Access token usage from unexpected locations or devices
- Applications accessing Key Vault or secret stores outside normal operational patterns
- Workload identities performing activities inconsistent with their defined purpose
- Impossible travel scenarios for service principals or application identities

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Entra ID Protection | Detects risky sign-ins and monitors for anomalous authentication patterns, including token theft and replay attempts |
| Microsoft Defender for Cloud Apps | Identifies OAuth app risks, monitors application permissions, and detects suspicious access to cloud resources using app governance capabilities |
| Microsoft Defender XDR | Correlates identity compromise signals across user and workload identities to detect coordinated attacks and lateral movement |
| Microsoft Purview | Monitors for unauthorized access to sensitive data following identity compromise and tracks data exfiltration attempts |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **App Governance:** Enforce policies that require approval for OAuth app installations, regularly audit application permissions, and implement continuous monitoring of app behavior
- **Conditional Access:** Deploy risk-based conditional access policies that challenge suspicious authentication attempts and enforce phishing-resistant multifactor authentication
- **Workload Identity Security:** Apply least privilege principles to service principals and workload identities, regularly rotate secrets and certificates, and monitor for privilege escalation
- **Token Protection:** Implement continuous token monitoring, enforce token binding where possible, and establish automated response procedures to revoke suspicious tokens and sessions

---

### 3.6 Password Spray Attacks

**Threat ID:** T006 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Password spray attacks involve trying common passwords across many different accounts to gain unauthorized access while avoiding account lockouts. Attackers use a low and slow strategy, distributing attacks across numerous IP addresses and cloud infrastructure to evade detection. Just 20 Autonomous System Numbers account for 80% of malicious password spray activity, with attackers leveraging cloud-based infrastructure for virtualization, orchestration, and access to diverse IP addresses. These attacks target organizations with weak password policies or inconsistent multifactor authentication enforcement, with research and academic environments accounting for 52% of observed spray attempts.

#### Why This Threat Matters

Password spray attacks remain a persistent and high-volume threat despite their low per-attempt success rate. The concentration of attacks through specific infrastructure patterns underscores the importance of targeted threat intelligence and infrastructure-aware defenses. Organizations with limited multifactor authentication adoption are particularly vulnerable—in analyzed attacks, only 1.5% of login attempts using correct credentials were blocked by multifactor authentication, illustrating limited adoption rather than ineffectiveness. The threat is amplified by credential reuse, with 85% of usernames targeted in spray attacks appearing in known credential leak databases, and compromised usernames appearing in an average of three separate logs.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Multiple failed login attempts distributed across many accounts from similar IP address ranges
- Authentication attempts using common passwords across different user accounts
- Sign-in patterns showing coordinated activity from specific Autonomous System Numbers
- Failed authentication attempts spread over extended time periods to avoid rate limits
- Geographic anomalies in authentication attempts, especially from unexpected countries or regions

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Entra ID Protection | Detects password spray patterns through AI-driven analysis of authentication data and automatically blocks suspicious IP addresses |
| Microsoft Defender for Cloud Apps | Identifies anomalous authentication patterns across cloud applications and correlates failed login attempts to detect coordinated attacks |
| Microsoft Defender XDR | Aggregates authentication signals across identity systems to identify distributed password spray campaigns targeting multiple users |
| Microsoft Sentinel | Enables advanced hunting for password spray indicators and provides automated response capabilities to block malicious infrastructure |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Phishing-Resistant MFA:** Enforce multifactor authentication for all users, prioritizing phishing-resistant methods that block over 99% of unauthorized access attempts using compromised credentials
- **Password Protection:** Implement Microsoft Entra Password Protection to prevent use of weak or commonly compromised passwords, and use smart lockout to block attackers while allowing legitimate users to access accounts
- **Conditional Access:** Deploy risk-based conditional access policies that block or challenge sign-ins from suspicious IP addresses, geographies, or authentication patterns
- **Monitoring and Response:** Continuously monitor authentication logs for error patterns indicating spray activity, and maintain updated threat intelligence on malicious IP addresses and Autonomous System Numbers

---

### 3.7 Leaked Credentials

**Threat ID:** T007 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Leaked credentials occur when valid usernames and passwords of legitimate users are compromised and shared publicly on the dark web, paste sites, or traded on the black market. The Microsoft leaked credentials service monitors public and dark web sites, working with researchers, law enforcement, security teams, and other trusted sources to acquire username and password pairs. When credentials are matched against current valid credentials, a leaked credentials risk detection is created. These compromised credentials enable attackers to access accounts directly without needing to conduct phishing or password attacks.

#### Why This Threat Matters

Eighty-five percent of usernames targeted in password spray attacks appeared in known credential leak databases, with compromised usernames appearing in an average of three separate logs, highlighting the magnitude of the global credential leak problem. Organizations face significant risk because leaked credentials enable attackers to bypass many security controls by logging in as legitimate users. The threat is amplified by password reuse across multiple services, where credentials leaked from one breach can be used to access unrelated systems. Despite the availability of multifactor authentication, limited adoption means that leaked credentials blocked only 1.5% of unauthorized access attempts in analyzed attacks.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Sign-in attempts using valid credentials from unusual locations or unfamiliar devices
- Successful authentication followed by anomalous behavior such as data exfiltration or privilege escalation
- Account access from IP addresses associated with credential stuffing or replay attacks
- Authentication patterns that match known credential leak datasets
- User accounts accessing resources outside their typical usage patterns

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Entra ID Protection | Automatically detects when user credentials appear in leaked credential databases and triggers risk-based policies requiring password reset |
| Microsoft Defender for Cloud Apps | Identifies anomalous activities following successful authentication with leaked credentials and enforces session policies |
| Microsoft Defender XDR | Correlates leaked credential alerts with downstream malicious activities across identity, endpoints, and cloud applications |
| Microsoft Entra Password Protection | Prevents users from setting passwords that match known compromised passwords from breach databases |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Phishing-Resistant MFA:** Enable multifactor authentication for all accounts, especially privileged accounts, to block over 99% of identity-based attacks even when credentials are compromised
- **Automated Remediation:** Configure Microsoft Entra Self-Service Password Reset to enable automatic user remediation when leaked credentials are detected
- **Password Policies:** Implement modern password policies following NIST 800-63B guidance, including password complexity requirements and regular monitoring against breach databases
- **Conditional Access:** Deploy conditional access policies that challenge or block sign-ins from suspicious locations, devices, or authentication patterns associated with credential replay attacks

---

### 3.8 Business Email Compromise

**Threat ID:** T008 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Business Email Compromise is a targeted attack where criminals gain access to business email accounts to defraud organizations, often by manipulating financial transactions or stealing sensitive data. BEC attacks are typically initiated through identity compromise, with attackers gaining initial access through phishing, password spraying, or leaked credentials. Once inside, attackers pivot to BEC-specific activities including inbox rule manipulation, unauthorized SharePoint access, internal phishing, email thread hijacking, new multifactor authentication method registration, and multifactor authentication tampering. These techniques enable attackers to gain trust, escalate privileges, and execute financial fraud or data exfiltration.

#### Why This Threat Matters

Business Email Compromise was a more frequent outcome in attacks at 21% compared to ransomware at 16%, underscoring the need for organizations to defend against both threat types. The research and academia sector accounted for 49% of BEC incidents, followed by telecommunications at 11% and financial services at 7%. BEC attacks cause disproportionately high impact through financial loss, data theft, and reputational damage. The threat persists because attackers conduct attacks as legitimate users after compromising identities, making detection extremely difficult without specialized monitoring of email behavior, inbox rules, and authentication changes. Identity compromise serves as the primary entry point, highlighting the critical relationship between identity security and BEC prevention.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Suspicious inbox forwarding rules or external email forwarding configurations
- Unusual inbox manipulation rules that hide or delete specific email categories
- New multifactor authentication methods registered for user accounts without proper authorization
- Email thread hijacking where attackers insert themselves into existing business conversations
- Unusual sending patterns, especially financial requests or wire transfer instructions

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Office 365 | Detects BEC attempts through anti-phishing policies, identifies impersonation attacks, and monitors for suspicious email activities |
| Microsoft Defender for Cloud Apps | Identifies anomalous mailbox activities including suspicious forwarding rules and unusual email access patterns through anomaly detection policies |
| Microsoft Entra ID Protection | Detects the identity compromise that enables BEC by monitoring for risky sign-ins and compromised credentials |
| Microsoft Defender XDR | Correlates identity compromise signals with suspicious mail flow rules, external forwarding, and multifactor authentication changes |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Identity Protection:** Implement phishing-resistant multifactor authentication and conditional access policies to prevent the identity compromise that enables BEC attacks
- **Email Security:** Deploy Microsoft Defender for Office 365 with anti-phishing policies to protect against impersonation attacks and configure email authentication standards including SPF, DKIM, and DMARC
- **User Education:** Train users to recognize BEC tactics including email thread hijacking, impersonation, and fraudulent financial requests, and establish verification procedures for sensitive transactions
- **Monitoring and Response:** Enable alert policies for suspicious mailbox activities, regularly audit mailbox access and multifactor authentication device registrations, and establish procedures for rapid response to suspected BEC incidents

---

### 3.9 Phishing Attempts

**Threat ID:** T009 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Phishing attacks are scams that use social engineering bait or lure content to trick users into divulging sensitive information or installing malware. Legitimate-looking communications, usually email, link to phishing sites that mimic sign-in pages requiring users to input login credentials and account information, which the phishing site then captures. Another common technique uses emails directing users to open malicious attachments such as PDF files that request login credentials to access the document. Modern phishing campaigns combine multiple attack vectors including email, messaging platforms, and voice calls, with attackers increasingly using platforms like Microsoft Teams for impersonation attacks.

#### Why This Threat Matters

Twenty-eight percent of breaches are initiated through phishing or social engineering, making it a primary attack vector despite defensive improvements. Phishing remains effective because it exploits human psychology rather than technical vulnerabilities, and attackers continuously evolve tactics to bypass security controls. The threat landscape has expanded beyond traditional email phishing to include sophisticated campaigns that combine email bombing with vishing calls and Teams impersonation to convincingly pose as IT support and gain remote access. Organizations face risk of credential theft, malware infection, and initial access that enables broader compromise including ransomware deployment and data exfiltration.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Emails with suspicious links or attachments requesting credential input or software installation
- Domain impersonation or typosquatting attempting to mimic legitimate organizations
- Unusual sender addresses or reply-to addresses that do not match displayed sender information
- Urgent language or pressure tactics requesting immediate action on financial transactions or credential verification
- Multi-channel attacks combining email with phone calls or messaging application contacts

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Office 365 | Implements anti-phishing policies to protect against impersonation attacks and provides Safe Links and Safe Attachments to mitigate unknown malware threats |
| Exchange Online Protection | Verifies and filters email to mitigate known malware threats and enforces email authentication through SPF, DKIM, and DMARC records |
| Microsoft Defender XDR | Correlates phishing attempts across email, identity, and endpoints to identify coordinated campaigns and enable rapid response |
| Microsoft Security Copilot | Assists security teams in analyzing phishing campaigns and provides guidance on response actions through natural language queries |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Email Security:** Implement Microsoft Defender for Office 365 with Safe Links and Safe Attachments policies, and configure SPF, DKIM, and DMARC records for all email domains
- **User Awareness:** Conduct regular security awareness training using Attack Simulator to help users recognize phishing tactics and establish clear reporting procedures
- **Identity Protection:** Deploy phishing-resistant multifactor authentication to limit the impact of successful credential theft through phishing attacks
- **Monitoring and Response:** Enable alert policies for suspicious email activities and establish procedures for rapid investigation and remediation of reported phishing attempts

---

### 3.10 Email Bombing and Vishing

**Threat ID:** T010 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

Email bombing involves enrolling a target's email account in thousands of newsletters and online services to flood the inbox with subscription emails, creating noise that hides critical alerts such as multifactor authentication prompts, password resets, fraud alerts, or transaction notifications. This technique evolved from a smokescreen tactic to a first-stage attack vector in broader malware delivery chains. Attackers now combine email bombing with vishing or Microsoft Teams-based impersonation, contacting targets while posing as IT support and offering to resolve the inbox flood issue. Once trust is established, attackers guide targets into installing remote access tools, enabling hands-on-keyboard control, malware deployment, and persistence.

#### Why This Threat Matters

Email bombing creates urgency and confusion that attackers exploit to bypass security awareness training and establish trust with victims. The combination of inbox flooding with immediate follow-up contact from fake IT support creates a convincing scenario that prompts users to take risky actions. Organizations face risk of remote access tool installation, credential theft, and initial access for broader compromise. The threat is particularly effective because it targets the human element rather than technical controls, and the rapid timing between email bombing and vishing contact prevents victims from recognizing the attack pattern. Successful campaigns have led to deployment of malware, data exfiltration, and persistent access through legitimate remote management tools.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Sudden influx of subscription or newsletter emails to user accounts
- Mass sign-up events from suspicious IP addresses targeting specific email accounts
- Unsolicited contact from individuals claiming to be IT support offering assistance with email issues
- Installation or execution of remote access tools such as Quick Assist following email flooding
- Unusual authentication activity or password reset attempts during or after email bombing events

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Office 365 | Detects mass sign-up emails and identifies patterns indicating email bombing campaigns through advanced filtering and threat intelligence |
| Microsoft Defender for Endpoint | Monitors for unauthorized remote access tool installation and execution, particularly Quick Assist or other remote management utilities |
| Microsoft Defender XDR | Correlates email bombing events with remote access tool execution and subsequent malicious activities across the attack chain |
| Microsoft Defender for Cloud Apps | Identifies anomalous email patterns and detects suspicious activities following successful social engineering attacks |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Email Filtering:** Implement rules and heuristics to detect mass sign-up emails and alert users or security teams when inbox flooding patterns are identified
- **Communication Controls:** Restrict external tenant communication in Microsoft Teams and monitor for impersonation attempts from external contacts claiming to be IT support
- **Application Control:** Approve and monitor all remote access tools, blocking or alerting on unauthorized remote management utilities through Windows Defender Application Control or AppLocker
- **User Education:** Train users to recognize fake IT support scams, establish verification procedures for IT support contacts, and create awareness that legitimate IT support will not ask users to install remote access tools via unsolicited contact

---

### 3.11 Malware Detection

**Threat ID:** T011 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Malware is any software intentionally designed to cause damage or interruptions to IT infrastructure including servers, clients, or networks. Malware is categorized as known malware that can be identified using traditional anti-malware methods including signature-based file matching and file reputation signals, or unknown malware that cannot be matched using traditional methods and requires advanced detection through detonation platforms, heuristics, and machine learning models. Modern malware threats include AI-generated malware, deepfakes, synthetic identities, and commodity tools delivered through various vectors including email attachments, malicious links, compromised websites, and social engineering techniques.

#### Why This Threat Matters

Malware remains prevalent across email and data vectors, requiring both signature-based and behavior-based detection capabilities to address the full spectrum of threats. Organizations face risk from known malware that exploits common vulnerabilities and unknown malware designed to evade traditional detection systems. The threat landscape has evolved to include AI-generated malware that adapts to defensive measures and synthetic content used in fraud and social engineering campaigns. Successful malware infections can lead to data theft, system disruption, credential harvesting, ransomware deployment, and persistent access for attackers. The integration of AI into malware development enables attackers to create more sophisticated and evasive threats at scale.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Suspicious file downloads or email attachments with uncommon extensions or anomalous characteristics
- Execution of unknown or unsigned binaries on endpoints
- Network communications to known malicious command and control infrastructure
- Behavioral patterns indicating ransomware activity such as mass file encryption or deletion
- Anomalous system modifications including registry changes, scheduled task creation, or persistence mechanisms

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Office 365 | Detects unknown malware through Safe Attachments detonation platform and protects against malicious links through Safe Links policies |
| Exchange Online Protection | Identifies known malware using signature-based detection and file reputation signals to block threats at the email gateway |
| Microsoft Defender for Endpoint | Provides real-time protection against malware execution, uses behavior-based detection for unknown threats, and enables automated investigation and remediation |
| Microsoft Defender for Cloud Apps | Detects malware presence in cloud storage including SharePoint Online, OneDrive, Teams, and supported third-party applications, and identifies ransomware activity patterns |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Email Protection:** Deploy Microsoft Defender for Office 365 with Safe Attachments and Safe Links policies to protect against both known and unknown malware delivered through email
- **Endpoint Security:** Implement Microsoft Defender for Endpoint with real-time protection, behavior monitoring, and cloud-delivered protection to detect and block malware execution
- **Cloud Security:** Deploy Microsoft Defender for Cloud Apps with malware detection policies for cloud file storage and session policies to restrict file uploads from untrusted sources
- **User Awareness:** Conduct regular security awareness training using Attack Simulator to help users recognize malware delivery techniques including phishing emails and malicious attachments

---

### 3.12 Ransomware and Human-Operated Attacks

**Threat ID:** T012 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Ransomware and human-operated attacks involve cybercriminals actively controlling intrusions, moving through networks, stealing data, and manually deploying ransomware for maximum impact. Modern ransomware operations increasingly leverage social engineering to obtain or reset credentials through vishing or tech support scams, exploit public-facing applications using zero-day and known vulnerabilities, and target hybrid environments by moving laterally from on-premises into cloud. Approximately 79% of ransomware cases involve at least one remote monitoring and management tool for persistence, and 40% of attacks now involve hybrid components targeting both on-premises and cloud infrastructure.

#### Why This Threat Matters

Ransomware operations showed an 87% increase in destructive cloud campaigns, representing significant escalation in volume and impact. Organizations face risk of operational disruption, data loss, financial extortion, and reputational damage. The threat has evolved beyond simple encryption to include data exfiltration before encryption, with 82% of observed ransomware incidents involving large-scale data theft. Attacks reaching encryption stage increased 7% compared to 102% in the previous year, indicating improved defenses, but attackers have shifted focus to data exfiltration as primary objective. Average dwell time is 12 days with average attack length of 58 days, emphasizing the importance of rapid detection and response.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Installation or use of remote monitoring and management tools outside normal IT operations
- Exploitation of antivirus exclusions or tampering with security solutions
- Lateral movement patterns indicating reconnaissance and privilege escalation
- Large-scale data collection and staging for exfiltration
- Execution of encryption tools or mass file deletion activities targeting cloud and on-premises systems

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Endpoint | Detects ransomware execution, monitors for tampering with security solutions, and identifies suspicious remote management tool usage through behavior-based detection |
| Microsoft Defender for Cloud | Identifies destructive activities in Azure environments including VM deletion, storage encryption, and backup system compromise |
| Microsoft Defender XDR | Correlates ransomware indicators across endpoints, identity, cloud, and email to detect human-operated attack chains and enable coordinated response |
| Microsoft Sentinel | Enables advanced hunting for ransomware tactics, provides automated response playbooks, and correlates activities across hybrid environments |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Identity Protection:** Deploy phishing-resistant multifactor authentication and privileged access management to prevent credential compromise that enables human-operated attacks
- **Vulnerability Management:** Maintain rapid patching cycles for internet-facing applications and systems, prioritizing exploitation of public-facing services
- **Backup and Recovery:** Implement immutable backups with offline copies, test restoration procedures regularly, and ensure recovery capability for both on-premises and cloud resources
- **Detection and Response:** Deploy endpoint detection and response with behavior-based analytics, monitor for remote management tool abuse, and establish incident response procedures with focus on rapid containment

---

### 3.13 Data Exfiltration

**Threat ID:** T013 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Data exfiltration is the unauthorized transfer or theft of data from an organization, often involving sensitive information such as intellectual property, personally identifiable information, financial records, or trade secrets. Data collection was observed in 80% of reactive incident response engagements, with 51% showing confirmed exfiltration, making it a primary goal for attackers regardless of their motivation. Modern data exfiltration occurs through various channels including cloud storage uploads, email forwarding, command and control communications, and abuse of legitimate file sharing services. Attackers increasingly focus on data theft rather than or in addition to ransomware encryption, with 82% of ransomware incidents involving large-scale exfiltration.

#### Why This Threat Matters

Data exfiltration has become the primary objective for most attacks, surpassing ransomware encryption in frequency and strategic importance to adversaries. Organizations face severe consequences including regulatory compliance violations, legal liability, competitive disadvantage from stolen intellectual property, and reputational damage. The shift from encryption-focused ransomware to data exfiltration reflects attacker adaptation to improved backup and recovery capabilities, with stolen data providing leverage for extortion even when encryption is prevented. Proving exfiltration can be challenging due to slow, stealthy transfer methods that evade detection, but organizations should assume data exposure when threat actors access sensitive systems or data stores.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unusual data access patterns including mass file downloads or database queries
- Large outbound network transfers to external destinations or cloud storage services
- Use of compression or archiving tools to stage data for exfiltration
- Access to sensitive data repositories outside normal business hours or user patterns
- Suspicious use of legitimate file sharing services or cloud storage for unauthorized data uploads

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Purview Data Loss Prevention | Monitors data movement across endpoints, cloud services, and on-premises systems, enforcing policies to prevent unauthorized exfiltration |
| Microsoft Defender for Cloud Apps | Detects anomalous data access and upload activities in cloud applications, identifies suspicious file sharing, and enforces session policies |
| Microsoft Defender XDR | Correlates data exfiltration indicators across endpoints, identity, email, and cloud to identify coordinated theft campaigns |
| Microsoft Sentinel | Enables advanced hunting for data staging and exfiltration patterns, providing analytics to detect unusual data access and transfer activities |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Data Classification:** Identify and label sensitive data based on classification levels, implementing enhanced protections for high-value information assets
- **Access Controls:** Enforce least privilege access principles, implement zero trust network architecture, and regularly audit permissions to sensitive data repositories
- **Data Loss Prevention:** Deploy comprehensive data loss prevention policies across endpoints, email, cloud applications, and network boundaries to detect and block unauthorized data transfers
- **Monitoring and Response:** Maintain continuous visibility into data access patterns, establish baselines for normal data usage, and implement automated alerts for anomalous data movement or access activities

---

### 3.14 Cloud Workload and Container Compromise

**Threat ID:** T014 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

Cloud workload and container compromise involves attacks targeting applications, services, and processes running in cloud environments, including virtual machines, containers, serverless functions, and Kubernetes deployments. Attacks against Azure environments increased 26% in incident volume, with an 87% increase in destructive campaigns targeting cloud resources. Container compromise often occurs within the first 48 hours of deployment, with cryptomining representing 58% of container threats and credential theft accounting for 21%. Attackers exploit misconfigurations, vulnerable internet-facing services, and weak identity controls to gain access to cloud workloads and establish persistent presence.

#### Why This Threat Matters

Cloud environments have become primary battlegrounds for attackers, with organizations facing rapid compromise of newly deployed resources. The speed of container compromise—median infection time under 48 hours—emphasizes the critical need for immediate runtime protection from deployment. Organizations experience destructive attacks including mass deletion of virtual machines, encryption of cloud storage, and compromise of backup systems. The hybrid nature of modern infrastructure means that cloud compromise often enables lateral movement to on-premises systems, amplifying impact. Cloud-native attack techniques using legitimate cloud services for command and control make detection challenging without specialized cloud security monitoring.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unexpected cryptomining activity or unusual CPU and network utilization in containers or virtual machines
- Anomalous access to cloud secrets, Key Vault, or credential stores
- Suspicious command execution in containers or serverless functions
- Unauthorized modifications to cloud resources including configuration changes or permission escalations
- Unusual outbound network connections from cloud workloads to external command and control infrastructure

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Cloud | Provides runtime protection for containers and virtual machines, detects cryptomining and credential theft, and monitors for destructive activities in Azure |
| Microsoft Defender for Containers | Offers specialized protection for Kubernetes environments with vulnerability scanning, runtime threat detection, and security posture management |
| Microsoft Defender XDR | Correlates cloud workload compromise with identity and data signals to detect coordinated attacks across hybrid environments |
| Microsoft Sentinel | Enables advanced hunting for cloud-native attack patterns and provides automated response capabilities for cloud threat scenarios |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Immediate Runtime Protection:** Deploy cloud workload protection from the moment of resource deployment, with continuous monitoring for containers, virtual machines, and serverless functions
- **Configuration Management:** Implement security baselines for cloud resources, regularly audit configurations for misconfigurations, and enforce policy-as-code for infrastructure deployments
- **Identity and Access:** Apply least privilege principles to cloud identities, implement conditional access for cloud resources, and continuously monitor for privilege escalation attempts
- **Vulnerability Management:** Maintain container image scanning, regularly update base images and dependencies, and enforce policies preventing deployment of vulnerable workloads

---

### 3.15 Vulnerability Exploitation

**Threat ID:** T015 | **First Appeared:** v7.0 | **Status:** Active

#### Summary

Vulnerability exploitation involves attackers taking advantage of security flaws in software, systems, or configurations to gain unauthorized access, escalate privileges, or execute arbitrary code. Eighteen percent of breaches occur via unpatched web assets, with attackers incorporating exploits for known vulnerabilities faster than ever against infrastructure-level systems. Exploitation targets internet-facing devices, remote access tools, and commonly used enterprise systems including SimpleHelp, BeyondTrust, Fortinet, Cleo, and Apache Tomcat. Zero-day vulnerabilities and rapid weaponization of newly disclosed Common Vulnerabilities and Exposures create compressed windows between disclosure, patch availability, and deployment.

#### Why This Threat Matters

Vulnerability exploitation remains one of the most reliable, scalable, and silent methods of initial access for threat actors. Unlike phishing, exploitation requires no user interaction and can achieve outcomes including initial access, privilege escalation from user to admin, and arbitrary code execution enabling lateral movement or persistence. The strategic pivot toward infrastructure-level compromise represents a baseline shift in attacker tactics, with organizations facing compressed response windows as attackers operationalize exploits within hours or days of disclosure. The threat is amplified by the growing complexity of digital supply chains introducing more components for exploitation, and by attackers targeting less-protected internet-facing devices that offer both entry points and obfuscation layers.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unusual network traffic patterns to or from internet-facing systems
- Exploitation attempts detected by intrusion detection or prevention systems
- Anomalous post-exploitation behavior including Local Security Authority Subsystem Service access, registry dumping, or outbound tunneling
- Unexpected processes or services running on internet-facing systems
- Suspicious authentication attempts or privilege escalation activities following exploitation

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Endpoint | Detects exploitation attempts through behavior-based analytics, identifies post-exploitation activities, and provides vulnerability assessment capabilities |
| Microsoft Defender Vulnerability Management | Identifies vulnerable systems, prioritizes patching based on threat intelligence and exploitability, and tracks remediation progress |
| Microsoft Defender for Cloud | Monitors cloud resources for vulnerabilities and misconfigurations, provides security recommendations, and detects exploitation attempts |
| Microsoft Defender XDR | Correlates exploitation indicators with downstream malicious activities to identify complete attack chains and enable coordinated response |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Rapid Patching:** Prioritize patching for high-impact vulnerabilities especially in internet-facing infrastructure and remote access tools, maintaining aggressive patch deployment cycles
- **Attack Surface Reduction:** Restrict remote management tools and administrative consoles to management networks or VPN-only access, minimizing exposure of vulnerable services
- **Vulnerability Management:** Maintain comprehensive asset inventory, continuously scan for vulnerabilities, and implement risk-based prioritization for remediation activities
- **Compensating Controls:** Deploy virtual patching, network segmentation, and behavior-based detection to protect systems during the window between vulnerability disclosure and patch deployment

---

### 3.16 Access Broker Activity

**Threat ID:** T016 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

Access broker activity involves cybercriminals who specialize in breaching enterprise environments and selling persistent access to other criminals including ransomware operators, data extortion groups, and cyber mercenaries. Three hundred sixty-eight identified access brokers affected 68 industries across 131 countries, with credential-based attacks representing 80% of access methods sold. These brokers often bundle access with reconnaissance data including network topology, privileged account information, and valuable asset locations, making it easier for buyers to deploy ransomware or exfiltrate data. Access brokers primarily targeted victims in the United States at 31%, United Kingdom at 6%, and Thailand at 5%, focusing on public sector, consumer and industrial products, and professional services sectors.

#### Why This Threat Matters

Access brokers play a pivotal role in the cybercrime economy, enabling threat actors to outsource initial access and focus on monetization instead. Their services are foundational to the cybercrime-as-a-service model, with organizations purchasing access facing immediate risk of ransomware deployment or data theft rather than gradual compromise. The specialized nature of access broker activity means that a single successful breach can be sold multiple times or used in coordinated campaigns, amplifying the impact of initial compromise. Organizations may experience delayed attacks where access purchased from brokers is used weeks or months after initial compromise, complicating detection and response efforts.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unusual reconnaissance activities including network scanning, Active Directory enumeration, or system profiling
- Credential access attempts targeting privileged accounts or service accounts
- Lateral movement patterns suggesting environment mapping for future exploitation
- Establishment of persistent access mechanisms including backdoors or additional accounts
- Suspicious authentication patterns indicating testing of compromised credentials for resale validation

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Identity | Detects reconnaissance activities, lateral movement, and Active Directory enumeration commonly performed by access brokers |
| Microsoft Defender for Endpoint | Identifies suspicious reconnaissance tools, credential dumping attempts, and establishment of persistence mechanisms |
| Microsoft Defender XDR | Correlates access broker activities across endpoints, identity, and network to identify coordinated reconnaissance and access validation |
| Microsoft Sentinel | Enables advanced hunting for patterns indicating access broker reconnaissance and provides threat intelligence integration for known broker infrastructure |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Identity Protection:** Implement phishing-resistant multifactor authentication and privileged access management to prevent credential theft that enables access broker operations
- **Network Segmentation:** Deploy zero trust network architecture to limit lateral movement and reconnaissance capabilities even when initial access is achieved
- **Privileged Access:** Reduce standing administrative privileges, implement just-in-time access for privileged operations, and continuously monitor for privilege escalation attempts
- **Threat Intelligence:** Subscribe to threat intelligence feeds tracking access broker activity, monitor dark web marketplaces for organizational credential sales, and establish procedures for rapid response when access sales are detected

---

### 3.17 Suspicious Mailbox Activities

**Threat ID:** T017 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

Suspicious mailbox activities include unauthorized inbox manipulation, forwarding rule creation, email deletion, and mailbox permission changes that indicate post-compromise activity. Mailbox manipulation remains a common technique for data exfiltration, internal phishing, and lateral movement after initial account compromise. Attackers use mailbox rules to forward sensitive emails to external addresses, delete security alerts to maintain persistence, or access other mailboxes to expand their foothold. Business email compromise actors frequently leverage mailbox access to study communication patterns, identify payment processes, and conduct financial fraud, while ransomware operators use mailbox access to identify backup administrators and disaster recovery procedures.

#### Why This Threat Matters

Mailbox compromise represents a critical post-exploitation phase where attackers transition from initial access to sustained data theft or preparation for ransomware deployment. Unauthorized mailbox rules can persist for months, continuously exfiltrating sensitive communications including intellectual property, customer data, and credentials shared via email. Internal phishing from compromised mailboxes has significantly higher success rates because recipients trust emails from known colleagues, enabling rapid lateral movement across the organization. Mailbox activities often provide early warning of business email compromise attempts, where attackers study organizational communication patterns before launching financial fraud schemes.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Creation of inbox rules that forward emails to external addresses or delete messages containing specific keywords
- Unusual mailbox permission changes granting access to other users' mailboxes
- Bulk email deletion patterns that remove security alerts or forensic evidence
- Abnormal email access patterns including off-hours access or access from unusual geographic locations
- Suspicious mailbox folder operations including exporting mailbox contents or creating hidden folders

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender for Office 365 | Detects suspicious inbox rules, abnormal email forwarding patterns, and mailbox permission changes |
| Microsoft Defender XDR | Correlates mailbox activities with identity compromise signals and endpoint behaviors to identify post-compromise actions |
| Microsoft Purview | Monitors data exfiltration via email forwarding and provides audit logging for mailbox permission changes |
| Microsoft Entra ID Protection | Detects anomalous sign-in patterns that precede mailbox manipulation activities |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Email Security Configuration:** Disable automatic forwarding to external domains, implement transport rules blocking suspicious forwarding patterns, and require administrative approval for mailbox delegation
- **Monitoring and Alerting:** Enable unified audit logging for all mailbox operations, configure alerts for inbox rule creation and permission changes, and regularly review mailbox forwarding rules across the organization
- **Conditional Access:** Implement location-based and device-based conditional access policies to prevent mailbox access from compromised accounts on untrusted devices
- **User Awareness:** Train users to recognize signs of mailbox compromise including missing emails, unexpected inbox rules, and unfamiliar sent items

---

### 3.18 Nation-State Cyber Espionage

**Threat ID:** T018 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

Nation-state cyber espionage involves state-sponsored threat actors conducting targeted intelligence collection, intellectual property theft, and strategic surveillance against governments, critical infrastructure, and private sector organizations. IT, government, and research/academia sectors are most impacted, with only 4% of nation-state attacks motivated solely by espionage but generating significant strategic impact through sustained access and data collection. China focuses 23% of activities on IT sector targeting, Iran directs 64% toward Israel, Russia targets 25% government entities, and North Korea increasingly focuses on revenue generation through cryptocurrency theft and IT worker infiltration. Nation-state actors demonstrate advanced tradecraft including living-off-the-land techniques, supply chain compromise, and zero-day exploitation.

#### Why This Threat Matters

Nation-state actors operate with significantly greater resources, sophistication, and patience than financially motivated cybercriminals, often maintaining persistent access for years before detection. Their targeting of critical infrastructure, defense industrial base, and strategic technology sectors creates national security implications beyond individual organizational impact. Nation-state campaigns increasingly blend espionage with destructive capabilities, enabling actors to transition from intelligence collection to sabotage during geopolitical conflicts. The theft of intellectual property and research data undermines competitive advantages and can accelerate adversary technological development, particularly in artificial intelligence, quantum computing, and advanced manufacturing sectors.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Advanced persistent threat behaviors including long-term access maintenance and careful operational security
- Targeting of high-value assets including intellectual property, research data, and strategic communications
- Living-off-the-land techniques using legitimate administrative tools to evade traditional security controls
- Supply chain compromise attempts targeting software vendors or managed service providers with access to strategic targets
- Strategic timing of operations correlating with geopolitical events or policy decisions

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Defender XDR | Provides advanced threat hunting capabilities and correlates nation-state tactics across endpoints, identity, email, and cloud applications |
| Microsoft Defender for Endpoint | Detects advanced attack techniques including living-off-the-land, credential theft, and lateral movement associated with nation-state actors |
| Microsoft Sentinel | Enables long-term threat hunting for persistent access indicators and integrates nation-state threat intelligence for proactive defense |
| Microsoft Entra ID Protection | Identifies sophisticated identity attacks including token theft and authentication bypass techniques used by nation-state actors |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Assume Breach Posture:** Implement zero trust architecture assuming nation-state actors may already have presence, focusing on limiting lateral movement and data access even after initial compromise
- **Critical Asset Protection:** Identify and segment high-value assets including intellectual property and research data, implementing additional monitoring and access controls for strategic information
- **Advanced Threat Hunting:** Conduct proactive threat hunting using behavioral analytics and threat intelligence specific to nation-state tactics, techniques, and procedures relevant to your sector
- **Supply Chain Security:** Assess third-party risk, validate software integrity, and implement security requirements for vendors with access to sensitive environments or data

---

### 3.19 AI System Attacks

**Threat ID:** T019 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

AI system attacks involve exploiting vulnerabilities in artificial intelligence systems themselves, including prompt injection, training data poisoning, insecure plugin architectures, and model extraction. Fifty-seven percent of organizations experienced increased security incidents linked to AI usage, with risks spanning both attacks against AI systems and attacks enabled by AI capabilities. Adversaries target AI systems through prompt injection to bypass safety controls, poison training data to corrupt model outputs, exploit insecure extensions to gain unauthorized access, and extract proprietary models through API abuse. The rapid adoption of AI assistants and copilots across enterprise environments creates expanding attack surface where AI systems process sensitive data and execute actions with elevated privileges.

#### Why This Threat Matters

AI systems operate with unique security challenges that traditional security controls may not address, including the difficulty of validating AI decision-making processes and the potential for subtle manipulation of model behavior. Prompt injection attacks can cause AI systems to ignore safety instructions, leak sensitive information, or execute unauthorized actions, with particular risk when AI assistants have access to enterprise data or systems. The integration of AI into critical business processes means that compromised AI systems can amplify attacker capabilities, enabling sophisticated social engineering, automated vulnerability discovery, or manipulation of automated decision systems. Organizations deploying AI without adequate security controls risk creating new attack vectors that bypass traditional security architectures.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unusual AI system behavior including unexpected outputs, bypassed safety controls, or execution of unauthorized actions
- Anomalous API usage patterns suggesting model extraction attempts or adversarial probing
- Suspicious plugin or extension installations in AI assistant environments
- Data exfiltration through AI system prompts or responses containing sensitive information
- Pattern of failed AI interactions suggesting adversarial testing or prompt injection attempts

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Purview | Monitors data access and exfiltration risks when AI systems process sensitive information and enforces data governance policies |
| Microsoft Defender for Cloud Apps | Detects anomalous usage patterns in AI services and identifies shadow AI deployments that bypass security controls |
| Microsoft Entra ID Protection | Secures access to AI systems through conditional access policies and monitors for compromised accounts accessing AI resources |
| Microsoft Security Copilot | Provides AI-powered threat detection while implementing security controls specific to AI system protection |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **AI-Specific Security Controls:** Implement input validation and output filtering for AI systems, deploy prompt injection detection, and enforce content safety policies to prevent malicious use
- **Data Governance:** Apply data classification and access controls to limit sensitive information available to AI systems, implement data loss prevention for AI outputs, and audit AI system data access
- **Secure AI Development:** Follow secure development practices for AI deployments including model validation, adversarial testing, and security review of AI plugins and extensions
- **AI Usage Monitoring:** Establish logging and monitoring for AI system interactions, detect anomalous usage patterns, and implement rate limiting to prevent abuse or model extraction attempts

---

### 3.20 Insider Threats

**Threat ID:** T020 | **First Appeared:** v8.0 | **Status:** Active

#### Summary

Insider threats involve current or former employees, contractors, or business partners who misuse authorized access to harm organizational interests through data theft, sabotage, fraud, or espionage. The North Korean IT worker program represents a sophisticated insider threat variant, embedding tens of thousands of workers globally for revenue generation with potential for espionage, extortion, and sabotage. Organizations take an average of 81 days to contain identified insider incidents, with insider threats spanning negligent employees causing accidental data exposure, malicious insiders stealing intellectual property for personal gain, and state-sponsored infiltrators conducting espionage. The trusted nature of insider access enables bypassing perimeter security controls and makes detection significantly more challenging than external attacks.

#### Why This Threat Matters

Insiders possess legitimate access to sensitive systems and data, making their activities difficult to distinguish from normal business operations and enabling them to operate undetected for extended periods. The damage from insider incidents often exceeds external breaches because insiders understand where valuable data resides, how to access it without triggering alerts, and how to cover their tracks using authorized tools. North Korean IT worker infiltration demonstrates how insider threats extend beyond traditional employee risk to include state-sponsored programs deliberately placing operatives in organizations worldwide. Insider threats create complex response challenges because organizations must balance security monitoring with employee privacy, trust relationships, and legal considerations.

#### Detection Themes

Organizations can identify this threat through the following indicators:

- Unusual data access patterns including accessing files outside normal job responsibilities or bulk downloads of sensitive information
- Anomalous work hours or access from unexpected locations inconsistent with known employee behavior
- Use of unauthorized data transfer methods including personal cloud storage, external drives, or personal email accounts
- Privilege escalation attempts or accessing systems beyond authorized scope
- Behavioral indicators including financial stress, policy violations, disgruntlement, or imminent departure from the organization

#### Microsoft Security Product Mapping

| Product | How it Helps |
|---------|--------------|
| Microsoft Purview | Detects insider risk through data loss prevention, insider risk management policies, and behavioral analytics identifying anomalous data access |
| Microsoft Defender for Cloud Apps | Monitors cloud application usage for unauthorized data exfiltration and detects anomalous file sharing or download patterns |
| Microsoft Entra ID Protection | Identifies unusual authentication patterns and enforces conditional access policies limiting access from unexpected locations or devices |
| Microsoft Sentinel | Enables user and entity behavior analytics (UEBA) to detect anomalous insider activities and correlates insider threat indicators across multiple data sources |

#### Mitigation Themes

Organizations should implement the following security principles to mitigate this threat:

- **Least Privilege Access:** Implement just-in-time and just-enough-access principles, regularly review and recertify access permissions, and remove unnecessary standing privileges
- **Data Loss Prevention:** Deploy DLP policies preventing unauthorized data exfiltration, monitor for sensitive data transfers to external locations, and enforce encryption for data at rest and in transit
- **Behavioral Monitoring:** Implement user and entity behavior analytics to establish baselines and detect anomalous activities, with particular focus on privileged users and contractors
- **Offboarding Controls:** Establish procedures for immediate access revocation upon employee departure, conduct exit interviews to identify potential risks, and monitor for post-employment unauthorized access attempts

---

## 4. Glossary

| Term | Definition |
|------|------------|
| **Access Broker** | Cybercriminals who specialize in breaching enterprise environments and selling persistent access to ransomware operators, data extortion groups, and other threat actors |
| **API** | Application Programming Interface - A set of protocols and tools that allows different software applications to communicate and exchange data with each other |
| **BEC** | Business Email Compromise - A sophisticated attack where threat actors compromise or impersonate legitimate business email accounts to conduct financial fraud or data theft |
| **ClickFix** | A social engineering technique that tricks users into copying and pasting malicious commands into the Windows Run dialog or terminal, bypassing traditional phishing protections |
| **Conditional Access** | Security policies that enforce specific requirements before granting access to resources, such as requiring multifactor authentication or restricting access from certain locations |
| **Container** | A lightweight, standalone executable package that includes application code and all dependencies required to run it, commonly used in cloud environments |
| **Credential Stuffing** | An attack where stolen username and password combinations are tested across multiple services to gain unauthorized access |
| **Cryptomining** | The unauthorized use of computing resources to mine cryptocurrency, often deployed by attackers after compromising systems |
| **CVE** | Common Vulnerabilities and Exposures - A standardized identifier for known security vulnerabilities in software and hardware |
| **Data Exfiltration** | The unauthorized transfer of data from an organization to an external location controlled by threat actors |
| **Device Code Phishing** | An attack technique that exploits the OAuth device authorization flow to steal authentication tokens without requiring passwords |
| **DLP** | Data Loss Prevention - Technologies and processes designed to detect and prevent unauthorized data transfer or exposure |
| **Infostealer** | Malware designed to harvest credentials, browser data, cryptocurrency wallets, and other sensitive information from infected systems |
| **Lateral Movement** | Techniques used by attackers to move through a network after initial compromise, accessing additional systems and resources |
| **Living-off-the-Land** | Attack techniques that use legitimate system tools and processes to conduct malicious activities, making detection more difficult |
| **MFA** | Multifactor Authentication - A security mechanism requiring multiple forms of verification before granting access, typically combining something the user knows, has, or is |
| **OAuth** | An open standard authorization protocol that enables applications to obtain limited access to user accounts without exposing passwords |
| **Password Spray** | An attack where threat actors attempt a small number of commonly used passwords against many user accounts to avoid account lockout policies |
| **Phishing** | Fraudulent communications designed to trick recipients into revealing sensitive information, clicking malicious links, or executing harmful actions |
| **Phishing-Resistant MFA** | Authentication methods that cannot be bypassed through phishing attacks, such as FIDO2 security keys or certificate-based authentication |
| **Prompt Injection** | An attack against AI systems where malicious input is crafted to manipulate the AI's behavior or bypass safety controls |
| **Ransomware** | Malware that encrypts or locks access to systems and data, demanding payment for restoration |
| **RMM Tools** | Remote Monitoring and Management Tools - Legitimate software used by IT professionals for system management, frequently abused by ransomware operators for persistent access |
| **Service Principal** | An identity created for applications, services, or automation tools to access Azure resources |
| **Token** | A digital credential that proves authentication, allowing access to resources without repeatedly entering credentials |
| **UEBA** | User and Entity Behavior Analytics - Security technology that uses machine learning to establish baseline behaviors and detect anomalous activities indicating potential threats |
| **Vishing** | Voice Phishing - Phishing attacks conducted through phone calls, often combined with other social engineering tactics |
| **Workload Identity** | Non-human identities assigned to applications, services, and scripts that access cloud resources and perform automated tasks |
| **Zero Trust** | A security model that assumes no user or system should be automatically trusted, requiring verification for every access request regardless of location |

---

*Document prepared for research and analysis. Source: Microsoft Digital Defense Report 2025.*
