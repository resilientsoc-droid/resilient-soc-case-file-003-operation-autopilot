# Evidence Index — Case File #003 (Operation Autopilot)

Master index of every screenshot referenced in `SOAR-Lab-Guide.md`. Update the **Status** and **Notes**
columns as real screenshots are captured and dropped into `screenshots/`, replacing the placeholder images
currently in that folder. Do not mark a row "Captured" until the real image is actually in place.

| ID | Evidence | Screenshot | Status | Notes |
|----|----------|------------|--------|-------|
| 01 | Docker stack running | `01-docker-stack.png` | Placeholder | Capture `docker ps` output for both compose stacks |
| 02 | Services healthy | `02-services-healthy.png` | Placeholder | |
| 03 | TheHive dashboard | `03-thehive-dashboard.png` | Placeholder | |
| 04 | Cortex dashboard | `04-cortex-dashboard.png` | Placeholder | |
| 05 | TheHive↔Cortex connection OK | `05-thehive-cortex-ok.png` | Placeholder | Config screen showing Status: OK |
| 06 | Cortex analyzers list | `06-cortex-analyzers.png` | Placeholder | Should show IPinfo_1_3 |
| 07 | TestAnalyzer success | `07-testanalyzer-success.png` | Placeholder | Job status = Success |
| 08 | TheHive case ~122884224 | `08-thehive-case.png` | Placeholder | |
| 09 | Observable 8.8.8.8 | `09-observable-8.8.8.8.png` | Placeholder | |
| 10 | IPinfo_1_3 analyzer config | `10-ipinfo-analyzer.png` | Placeholder | Show worker ID; hide API key |
| 11 | IPinfo analysis result | `11-ipinfo-result.png` | Placeholder | Direct analyzer run result |
| 12 | Shuffle dashboard | `12-shuffle-dashboard.png` | Placeholder | |
| 13 | SOC-Auto-Response workflow canvas | `13-shuffle-workflow.png` | Placeholder | |
| 14 | TheHive 2 node config | `14-thehive2-config.png` | Placeholder | |
| 15 | TheHive 2 output | `15-thehive2-output.png` | Placeholder | Proves Shuffle retrieved the case observable; needed to fix Section 10 blocker |
| 16 | Cortex 1 node config | `16-cortex1-config.png` | Placeholder | Custom Action config; hide Authorization header value |
| 17 | Cortex Custom Action HTTP 200 | `17-cortex-http200.png` | Placeholder | Static-payload proof |
| 18 | Cortex job success | `18-cortex-job-success.png` | Placeholder | |
| 19 | Analysis result (in workflow) | `19-analysis-result.png` | Placeholder | |
| 20 | Final E2E run | `20-final-e2e.png` | Not applicable yet | Blocked — dynamic mapping unresolved (Section 10) |
| 21 | Webhook config | `21-webhook-config.png` | Not applicable yet | Stage not built |
| 22 | Splunk alert action | `22-splunk-alert.png` | Not applicable yet | Stage not built |
| 23 | Human approval step | `23-human-approval.png` | Not applicable yet | Stage not built |
| 24 | TheHive final status | `24-thehive-final-status.png` | Not applicable yet | Depends on response stage |
| 25 | Report draft | `25-report-draft.png` | Not applicable yet | Depends on all prior stages |

**Legend:**
- **Captured** — real screenshot in place, secrets redacted, verified against the filename/purpose above.
- **Placeholder** — stage has occurred/been validated, but a real screenshot has not yet been added to this
  package.
- **Not applicable yet** — the underlying stage has not been executed at all; there is nothing to screenshot.

**Reminder:** hide API keys, tokens, cookies, and passwords in every screenshot before it goes into
`screenshots/`.
