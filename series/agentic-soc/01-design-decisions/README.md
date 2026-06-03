# Article 01 — The Design Decisions That Will Define Your Detection Capability

**Live:** https://open.substack.com/pub/socautomators/p/the-design-decisions-that-will-define

Article 01 is an architecture-and-design piece. It does not ship inline code; the decisions it covers (hot vs lake placement, dual-write, retention policy, ownership) drive the configurations that show up in later articles.

If you are looking for code touched by these decisions, see:

- `../03-threat-hunting/` — KQL hunts that depend on lake-retention design
- `../../../docs/log-sources-reference.html` — 37-source ingestion reference that the design decisions partition across tiers
