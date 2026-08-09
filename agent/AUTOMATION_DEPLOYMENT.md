# Automation Deployment

Automation in PersonaBridge is deployed as individually authorized capabilities. “Automate” never means blanket permission.

## Automation levels

### Level 0 — Guidance only

The agent explains the framework and produces recommendations. It creates no operational state and performs no external actions.

### Level 1 — Draft only

The system may research, classify, summarize, draft, audit, and update a private CRM. The user manually performs every LinkedIn action.

### Level 2 — Supervised

The system prepares an external action, shows the exact target and content, and waits for approval immediately before execution. Approval for one action does not authorize later actions.

### Level 3 — Bounded low-risk

Only explicitly listed low-risk capabilities may run on a schedule and within strict volume, cost, time, target-mix, and retry limits. Sensitive actions remain approval-gated. Platform warnings or verification challenges stop the run.

## Deployment workflow

### 1. Discover environment

Read-only checks identify the operating system, agent host, available storage adapter, scheduling mechanism, browser integration, secret manager, and private data location. Report missing dependencies before changing the environment.

### 2. Run the conditional interview

Evaluate `QUESTIONNAIRE.yaml` from top to bottom. Ask a question only when its `when` expression is true. Store answers by question ID so prior answers can activate or deactivate later branches.

### 3. Generate the Deployment Profile

Create a private profile matching `schemas/deployment-profile.schema.json`. Do not commit it. Generate a human-readable review containing:

- objective and success criteria;
- target-person mix;
- persona source policy;
- storage and retention policy;
- enabled and disabled capabilities;
- approval matrix;
- schedule, batch, cost, and retry limits;
- stop, recovery, and rollback conditions.

### 4. Require approval

The user approves the profile, not merely the general idea of automation. Any later expansion of capabilities requires a profile change and new approval.

### 5. Provision private state

Create the selected Excel, Google Sheets, or database store; a private persona location; schema-validated run manifests; an append-only recovery log; and an execution log that distinguishes `planned`, `drafted`, `approved`, `attempted`, `sent`, and `verified`.

Credentials must use the host's secret manager or approved environment configuration. Never store credentials in the repository or ask the user to paste them into chat.

### 6. Install triggers

Supported trigger patterns include:

- manual command;
- scheduled local task;
- agent automation or recurring task;
- CI workflow for analysis-only jobs without private browser state;
- webhook or database event for CRM maintenance.

The trigger invokes the orchestrator with a profile path and run ID. It must not embed secrets or private data in command arguments or logs.

### 7. Fictional dry run

Use fictional candidates and messages to verify routing, schemas, persona rules, approval gates, CRM writes, recovery events, and stop conditions. No real external action is allowed.

### 8. Small real batch

Run the smallest useful real batch in supervised mode. The Auditor independently verifies every record. The user reviews all proposed external actions and the resulting CRM state.

### 9. Enable approved automation

Enable only capabilities that passed validation. Record the profile version, activation time, enabled capabilities, and user approval evidence. Keep all unapproved capabilities disabled.

### 10. Monitor and recover

Each run produces a manifest with gate results and synchronization state. If storage fails, append a recovery event before reporting completion. Repeated failures, conflicting identity, missing approval, platform warnings, or threshold breaches pause the automation and notify the user.

## Capability matrix

| Capability | Draft only | Supervised | Bounded low-risk |
|---|---:|---:|---:|
| Candidate discovery | Optional | Optional | Optional within limits |
| Public-profile summarization | Optional | Optional | Optional within limits |
| Draft generation | Yes | Yes | Yes |
| Independent audit | Yes | Required | Required |
| CRM update | Optional | Optional | Optional with recovery log |
| Reminder creation | Optional | Optional | Optional within schedule |
| Browser preparation | No | Optional | Optional |
| External message sending | No | Per-action approval | Only if explicitly enabled; sensitive actions still require approval |

## Mandatory stop conditions

- identity mismatch or insufficient evidence;
- duplicate or unexpected external state;
- missing or expired approval;
- platform verification, security, policy, or rate-limit warning;
- target-mix, batch, weekly, cost, or retry limit exceeded;
- private storage unavailable and recovery event cannot be written;
- schema validation failure;
- user pause or kill switch.

Automation must never attempt to bypass a stop condition.
