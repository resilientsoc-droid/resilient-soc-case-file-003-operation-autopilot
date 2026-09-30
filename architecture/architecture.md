# Architecture — Case File #003: Operation Autopilot

## Target architecture (design)

```text
Splunk
  ↓
Detection / Correlation Rule
  ↓
Webhook
  ↓
Shuffle
  ↓
TheHive
  ↓
Observable / IOC
  ↓
Cortex
  ↓
Enrichment
  ↓
Human-in-the-loop Approval
  ↓
Controlled Response
  ↓
TheHive Case Update
  ↓
Report
```

This is the full production-style pipeline the lab is building toward. See `architecture.png` for the
diagram version, color-coded by validation status.

## Actual environment topology

```text
┌─────────────────────────────┐        ┌──────────────────────────┐
│  ~/resilient-soar/docker/    │        │       ~/shuffle           │
│  testing  (compose stack)    │        │   (separate compose)      │
│                               │        │                            │
│  Cassandra                   │        │   Shuffle                 │
│  Elasticsearch               │        │   http://192.168.1.11:3001│
│  Cortex   :9001/cortex       │◄──────►│   Workflow: SOC-Auto-      │
│  TheHive  :9000               │◄──────►│   Response                │
│  nginx                        │        │                            │
│  Mailhog                      │        │                            │
└─────────────────────────────┘        └──────────────────────────┘
```

All services run on host `192.168.1.11`. The original spec referenced `192.168.56.12`; that value is
retained here only as a historical note — it is not the address of anything actually running.

## What's validated vs. not, mapped onto the target diagram

| Stage | Status | Notes |
|---|---|---|
| Splunk detection / correlation rule | REFERENCE ONLY | SPL documented, not deployed as a live alert |
| Webhook (Splunk → Shuffle) | PLANNED | No webhook created or fired |
| Shuffle workflow engine | COMPLETED | `SOC-Auto-Response` exists and runs |
| TheHive case/observable | COMPLETED | Existing case `~122884224`, observable `8.8.8.8` |
| Shuffle → TheHive (retrieve observable) | VALIDATED (node level) | `TheHive 2` node confirmed via terminal + Shuffle |
| Shuffle → Cortex (static payload) | VALIDATED | Custom Action, HTTP 200, job created |
| Shuffle → Cortex (dynamic payload) | IN PROGRESS | Empty `data` field — see Section 10 of the lab guide |
| Cortex enrichment (IPinfo_1_3) | VALIDATED | Direct analyzer run, Job = Success |
| Human-in-the-loop approval | PLANNED | Not built |
| Controlled response | PLANNED / REFERENCE ONLY | PowerShell examples are reference only |
| TheHive case update (post-response) | PLANNED | Depends on response stage |
| Report generation | PLANNED | Depends on all prior stages |

See `diagrams/operation-autopilot-flow.png` for the visual flow and `evidence/VALIDATION-CHECKLIST.md` for the
maintained checklist version of this table.
