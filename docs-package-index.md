# Resilient SOC — Case File #003
## Operation Autopilot: From Detection to Automated Response (SOAR Integration Lab)

**Team:** Resilient SOC
**Case ID:** RSOC-CF-003
**Series:** Case File #001 (SOC Foundation) → Case File #002 (Operation Nightfall) → **Case File #003 (Operation Autopilot)**
**Document status:** Living document — reflects lab state as of last update, not a final closure report
**Classification:** Educational lab documentation (public)

---

## What this package contains

This is the complete documentation package for Operation Autopilot, the SOAR integration lab that extends the
Resilient SOC training series from pure detection/investigation (Case Files #001–#002) into
**orchestration, enrichment, human-approved response**.

| File | Purpose |
|---|---|
| `README.md` | Repository landing page (see `docs-package-index.md` for this index) |
| `SOAR-Lab-Guide.md` / `.pdf` | Full technical build guide, implementation log, and validation record |
| `TEAM-NOTES.md` | Working notes, decisions made, open questions |
| `architecture/architecture.md` + `architecture.png` | Target architecture and current implementation diagram |
| `diagrams/operation-autopilot-flow.png` | Flow diagram of the end-to-end pipeline |
| `commands/lab-commands.txt` | Copy-pasteable command reference used to stand up and validate the stack |
| `screenshots/` | Evidence screenshots (see `evidence/EVIDENCE-INDEX.md` for the naming scheme and status) |
| `evidence/EVIDENCE-INDEX.md` | Master index mapping each screenshot to what it proves |
| `evidence/VALIDATION-CHECKLIST.md` | Stage-by-stage checklist: COMPLETED / VALIDATED / IN PROGRESS / PLANNED |

## Read this first — current status in one paragraph

The **core SOAR integration** (TheHive → Shuffle → Cortex → analyzer job → enrichment result) has been built and
directly validated component-by-component. The **dynamic observable hand-off** inside the Shuffle workflow
(TheHive 2 → Cortex 1) is **still being debugged** — Cortex is currently receiving an empty `data` field instead
of the expected `8.8.8.8`. The **Splunk webhook trigger, human-approval step, and controlled response** are
**designed but not yet built/executed** in this environment. See Section "Current Status" in
`SOAR-Lab-Guide.md` and `evidence/VALIDATION-CHECKLIST.md` for the authoritative, stage-by-stage breakdown.

No end-to-end (Splunk-to-containment) run has occurred. This documentation does not claim one did.

## Quick links

- Full guide: [`SOAR-Lab-Guide.md`](./SOAR-Lab-Guide.md)
- Architecture: [`architecture/architecture.md`](./architecture/architecture.md)
- Evidence index: [`evidence/EVIDENCE-INDEX.md`](./evidence/EVIDENCE-INDEX.md)
- Validation checklist: [`evidence/VALIDATION-CHECKLIST.md`](./evidence/VALIDATION-CHECKLIST.md)
- Command reference: [`commands/lab-commands.txt`](./commands/lab-commands.txt)
- Team handoff instructions: see final section of `SOAR-Lab-Guide.md`
