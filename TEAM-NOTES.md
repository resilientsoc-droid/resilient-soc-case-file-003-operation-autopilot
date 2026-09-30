# Team Notes — Case File #003 (Operation Autopilot)

Working notes for the Resilient SOC team. Less formal than `SOAR-Lab-Guide.md` — use this for decisions,
open questions, and context that doesn't belong in the polished guide.

## Key decisions made

- **Reused existing TheHive Case `~122884224` / observable `8.8.8.8`** instead of creating new test data, to
  keep the evidence trail anchored to one case throughout the lab.
- **Built a local Cortex analyzer named `IPinfo_1_3`** (based on the catalog's `IPinfo_Details`) because the
  official catalog didn't ship an analyzer under the exact expected name. Analyzer ID `IPinfo_1_3_1_0`,
  Worker ID `c4538ef31090f3530d1f6e2b333ad580`.
- **Replaced Shuffle's built-in Cortex app action with a Custom Action** that calls the Cortex REST API
  directly, because the built-in app's `post_run_analyzer` function doesn't exist in the deployed Cortex app
  version. This gives more control and sidesteps the version mismatch entirely.
- Documented the original spec's `SOAR-HOST = 192.168.56.12` and older versions as **reference only** — the
  real environment runs on `192.168.1.11` with the versions in Section 2 of the guide.

## Open questions / blockers

- **[BLOCKING]** `TheHive 2 → Cortex 1` dynamic mapping: Cortex is receiving `{"data": ""}` instead of
  `8.8.8.8`. Need to inspect the raw `TheHive 2` output JSON structure for the real execution (not assume the
  shape) before trying another expression. See Section 10 of the lab guide for the full troubleshooting
  checklist.
- Webhook design (Splunk → Shuffle) is fully specified but **not implemented**. Need a real webhook ID from
  Shuffle once we get there — do not invent one in documentation.
- Human approval mechanism (Slack? email via Mailhog? Shuffle's own approval node?) — not yet decided. Pick
  this before building Step 4 of the target playbook.
- Response actions (AD account disable, firewall isolation) are reference PowerShell only — need a decision on
  whether these get built as Shuffle actions against a lab-only sandbox target, or stay manual/reference for
  this case file.

## Things that took longer than expected

- Cortex context path (`/cortex/api/...` vs `/api/...`) tripped up the first several API calls — anyone new to
  this Cortex deployment should read Section 17 of the guide first.
- The missing `requests` Python dependency in the analyzer runtime wasn't obvious from the Cortex UI error —
  had to check the analyzer's job logs directly.

## Reminder to self

- Don't claim the dynamic path works until Cortex actually logs `8.8.8.8` in a live workflow run, not just in
  a manual/static test.
- Rotate any credential that showed up on-screen during this session before screenshots go into the package.
