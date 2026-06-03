# SOCAutomators — Substack Blog Companion

> Companion data, research, and resources for the [SOCAutomators](https://socautomators.substack.com/) Substack blog — exploring AI-powered security operations, threat research, and SOC automation.

---

## What's Here

| Folder     | Content                                                              |
| ---------- | -------------------------------------------------------------------- |
| `series/`  | Per-article companion code, organized by series and article number   |
| `docs/`    | Reference data, companion articles, and downloadable assets          |
| `images/`  | Diagrams, reference charts, and visual assets used in blog posts     |

---

## Series Code

### The Agentic SOC on Microsoft Sentinel

The successor series to *Threat-Informed Defense: Tools, Logs, and Agents*. Three arcs: Foundation, Operating Model, Implementation.

- [`series/agentic-soc/`](series/agentic-soc/) — series index, article folders, and KQL libraries

Currently shipped:
- [Article 03 — Hunting at Machine Speed: KQL on the Sentinel Data Lake](series/agentic-soc/03-threat-hunting/) — six adaptable KQL hunts (geography baseline, recon breadth, DNS beaconing, lateral movement promoted rule, Search Job, federated cross-vendor)

---

## Log Sources Reference (v4.0)

The **37 Log Sources Reference** is a companion to the *What to Log in Your Next-Gen SIEM* sub-series in the [Threat-Informed Defense](https://socautomators.substack.com/) series. Every source is mapped to MITRE ATT&CK v18.1 tactics, ingestion tier, and five SOC use cases: detection, forensics, hunting, compliance, and AI agent operations.

**Downloads:**

| Format | File | Use Case |
| ------ | ---- | -------- |
| Interactive HTML | [`log-sources-reference.html`](docs/log-sources-reference.html) | Open in any browser — sortable, searchable |
| Excel (.xlsx) | [`log-sources-reference.xlsx`](docs/log-sources-reference.xlsx) | Filter, sort, and customize in Excel or Sheets |
| JSON | [`log-sources-reference.json`](docs/log-sources-reference.json) | Programmatic access — feed to scripts, agents, dashboards |
| SVG | [`log-sources-reference.svg`](images/log-sources-reference.svg) | Scalable vector for presentations and embedding |
| PNG | [`log-sources-reference.png`](images/log-sources-reference.png) | Full reference chart image (1600px wide) |
| JPG | [`log-sources-reference.jpg`](images/log-sources-reference.jpg) | Compressed image for blog and social sharing |

**Companion article:** [What to Log in Your Next-Gen SIEM — Pillar](docs/what-to-log-next-gen-siem-pillar.md)

---

## Related Projects

- **[Agentic SOC](https://github.com/mikepalitto/agentic-soc)** *(private)* — The AI agent framework for SOC automation discussed in the blog

---

## Disclaimer

This is designed for educational purposes only and is not backed by Microsoft. Content represents the opinions of the authors and collaborators.

## License

This project is licensed under the GPL-3.0 License — see [LICENSE](LICENSE) for details.
