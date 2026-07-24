# skill-entity-readiness-execution-health

![Category: Entity Readiness](https://img.shields.io/badge/category-Entity%20Readiness-blue) ![Status: Active](https://img.shields.io/badge/status-active-brightgreen)

Validates the health of the **Atlas Entity Readiness Change Report** n8n workflow after each run. This is a read-only inspection skill — it analyzes execution results, surfaces errors and anomalies, and confirms whether a run is safe to rely on, without modifying anything in n8n.

---

## What It Does

- Fetches and parses a specific n8n execution by ID or URL for the `Entity Readiness Change Report - Weekly` workflow (`EirKWJBySSXugv3a`)
- Confirms execution status, checks for node-level errors, and validates that the Onspring Report 954 pull succeeded
- Verifies that normalization, diffing, delivery (email nodes), and baseline storage (Data Table upsert) all completed correctly
- Flags whether the workflow is currently active on a schedule, and warns clearly if it is not
- Classifies failures by type (authentication, data-shape, HTTP, delivery, storage, unknown) and recommends safe human actions

---

## How to Use

1. **Set your API key** — The skill requires `N8N_ENTITY_REPORT_API_KEY` (or `N8N_API_KEY` for backward compatibility) as an environment variable. Never paste the key directly into a prompt.

2. **Invoke the skill** with an execution URL or ID:

   ```bash
   export N8N_ENTITY_REPORT_API_KEY="..."
   python3 scripts/inspect_execution.py --execution "<execution URL or ID>"
   ```

3. **Read the report** — The skill returns a structured summary covering:
   - Overall status (success / failure)
   - Node-level errors with messages
   - Onspring pull health (record count, HTTP status)
   - Delivery node outcomes
   - Baseline write confirmation
   - Workflow activation state

> This skill is strictly read-only. It calls only `GET /api/v1/workflows/{id}` and `GET /api/v1/executions/{id}?includeData=true`. It will not retry, activate, deactivate, or modify any workflow or execution.

---

## Trigger Phrases

Use this skill when you hear:

- "Did the entity readiness workflow run successfully?"
- "Check the entity readiness execution"
- "Was the Onspring pull healthy?"
- "Did the baseline write complete?"
- "Is the entity readiness workflow active?"
- "Validate last night's entity readiness run"
- "Error triage for entity readiness"
- "Confirm entity readiness is safe to deploy"
- "Post-run check on the entity readiness report"

---

## Category

**Entity Readiness** — Atlas HXM internal automation skill for validating weekly country-readiness workflow execution health.

Related skill: [`entity-readiness-baseline-analyst`](https://github.com/diamitani) — analyzes the baseline data table output, not the execution itself.

---

## Author

**Patrick Diamitani**
GTM AI & Automation Manager, Atlas HXM
[linkedin.com/in/diamitani](https://linkedin.com/in/diamitani)

---

> Built with Claude Code · Part of the [Patrick's Skills Library](https://github.com/diamitani)
