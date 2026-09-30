# Validation Checklist — Case File #003 (Operation Autopilot)

Stage-by-stage status. This is the authoritative, checkable version of the status claims made throughout
`SOAR-Lab-Guide.md`. Keep this in sync as work continues — don't let the narrative document and this checklist
drift apart.

Legend: `[x]` = COMPLETED/VALIDATED  `[~]` = IN PROGRESS  `[ ]` = PLANNED/NOT STARTED  `[ref]` = REFERENCE ONLY

## Infrastructure

- [x] Docker Engine / Compose stack builds and starts (`~/resilient-soar/docker/testing`)
- [x] Elasticsearch running and healthy (recovered from low-disk watermark warning without data loss)
- [x] Cassandra running and healthy
- [x] TheHive running and reachable at `http://192.168.1.11:9000`
- [x] Cortex running and reachable at `http://192.168.1.11:9001/cortex`
- [x] Shuffle running and reachable at `http://192.168.1.11:3001` (separate compose stack)

## TheHive / Cortex integration

- [x] TheHive ↔ Cortex connection configured
- [x] TheHive ↔ Cortex connection validated (Status: OK)
- [x] Cortex API authentication validated (Bearer token)
- [x] TestAnalyzer executed — Job status: Success

## Case & observable

- [x] TheHive Case `~122884224` exists and reused (not duplicated) for this lab
- [x] Observable `8.8.8.8` present on the case

## Analyzer (IPinfo)

- [x] Local analyzer `IPinfo_1_3` created (based on catalog's `IPinfo_Details`, since the exact
      requested analyzer name wasn't in the official catalog)
- [x] Missing `requests` Python dependency identified and resolved
- [x] Analyzer enabled in Cortex
- [x] Analyzer executed directly against `8.8.8.8` — successful result

## Shuffle orchestration

- [x] `SOC-Auto-Response` workflow exists
- [x] Built-in Cortex app action attempted — **failed** (`post_run_analyzer` doesn't exist in deployed app)
- [x] Custom Action built to call Cortex REST API directly
- [x] Custom Action URL/header/body issues found and fixed (missing `/cortex` path, missing Content-Type)
- [x] Custom Action validated with a **static** payload — HTTP 200, Cortex job created
- [x] `TheHive 2` node created to retrieve the case observable
- [x] `TheHive 2` node validated independently (terminal + Shuffle)
- [~] `TheHive 2 → Cortex 1` dynamic mapping — **Cortex currently receives an empty `data` field**;
      root-cause/fix not yet completed (see Section 10 of the lab guide)

## Level 1 — Core SOAR Integration (TheHive → Shuffle → Cortex → Job → Analysis)

- [x] Proven with a static/manual payload
- [~] Proven with a fully dynamic, case-driven payload inside one live workflow run

## Webhook / Splunk trigger

- [ref] Splunk correlation search (SPL) documented and reviewed for correctness
- [ ] Splunk alert action configured to fire a webhook
- [ ] Shuffle webhook receiver created (no webhook ID exists yet — do not invent one)
- [ ] Live Splunk → Shuffle webhook call executed

## Human approval & response

- [ ] Human-approval step built in the workflow
- [ ] Approval mechanism selected (Slack / email / Shuffle native — undecided, see `TEAM-NOTES.md`)
- [ref] Response actions documented (PowerShell examples) — reference/lab-only, not executed
- [ ] Controlled response action built and tested in a safe/lab-only context

## Case update & reporting

- [ ] TheHive case auto-updated with final disposition (Contained/Escalated)
- [ ] Report draft auto-generated from workflow data

## Level 2 — Full Production-style Pipeline

- [ ] Not yet validated — depends on all items above from "Webhook / Splunk trigger" onward

## Evidence

- [ ] Real screenshots captured for all 25 evidence points (currently placeholders — see
      `EVIDENCE-INDEX.md`)
- [ ] All screenshots reviewed for exposed secrets before inclusion
- [ ] Evidence Index fully updated to "Captured" status

---

**Last known blocker:** `Cortex 1` node in `SOC-Auto-Response` receives `{"data": ""}` instead of `8.8.8.8`
from the `TheHive 2` node's output. See Section 10 of `SOAR-Lab-Guide.md` for the exact troubleshooting steps.
