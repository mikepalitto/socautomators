# Article 02 — Migrating to Unified SecOps Without Breaking Detection

**Live:** https://open.substack.com/pub/socautomators/p/migrating-to-unified-secops-without

Article 02 is a migration playbook, not a code drop. The patterns it documents — assess, dual-write, validate parity, cut over deliberately, re-evaluate every Sentinel automation rule and Logic Apps playbook against the unified incident model — are operational rather than scripted.

The follow-on code in this repo references these patterns:

- `../03-threat-hunting/04-lateral-movement-promoted-rule.kql` — production-ready analytics rule with an explicit reminder about re-validating automation rules under the unified incident model.

When promoting any hunt to a Scheduled Analytics Rule under the Defender portal, re-validate:

1. The Sentinel automation rules that fire on incident creation.
2. The Logic Apps playbooks attached to those automation rules.
3. The run-as identity and its roles under the unified model.
4. Severity, owner assignment, and ticket creation against the unified incident shape.
