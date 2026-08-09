# PersonaBridge Agent Instructions

These instructions are authoritative for any AI agent explaining, configuring, or deploying this repository.

## Required reading order

1. `agent/PROJECT.yaml`
2. `docs/ARCHITECTURE.md`
3. `docs/PRIVACY.md`
4. `docs/SAFETY_BOUNDARIES.md`
5. `agent/RESPONSE_CONTRACT.md`
6. If the user wants deployment: `agent/DEPLOYMENT_INTERVIEW.md`
7. If the user wants automation: `agent/AUTOMATION_DEPLOYMENT.md` and `agent/QUESTIONNAIRE.yaml`

## Operating state machine

```text
EXPLAIN -> CONFIRM_INTENT -> INTERVIEW -> SPECIFY -> APPROVE
        -> DEPLOY -> DRY_RUN -> VALIDATE -> ENABLE
```

Never skip `APPROVE`, `DRY_RUN`, or `VALIDATE`. Do not treat a generated draft as a sent message or a planned deployment as an active deployment.

## First-response behavior

When a user provides this repository without a specific request:

1. Explain the problem PersonaBridge addresses.
2. Explain its goals, non-goals, principles, workflow, agent roles, durable state, and approval boundaries.
3. Ask whether the user wants to learn, create a deployment plan, build a local deployment, or add automation.
4. Do not request credentials, private conversations, or LinkedIn access during the explanation phase.

## Deployment rules

- Ask questions progressively. Prefer one coherent group at a time.
- Follow conditional questions in `agent/QUESTIONNAIRE.yaml`; do not ask irrelevant branches.
- Never infer approval, storage location, automation authority, target-person mix, or sensitive-message policy.
- Generate a private Deployment Profile matching `schemas/deployment-profile.schema.json`.
- Present a human-readable summary and approval matrix before implementation.
- Use fictional data for the first end-to-end dry run.
- Keep private personas, credentials, contact data, browser state, and real run manifests outside the public repository.
- Default to the least autonomous mode compatible with the user's objective.
- Referral, opportunity, resume, meeting, personal-information, commitment, and ambiguous-identity actions always require explicit human approval.

## Automation rules

Automation authority is capability-specific, not global. A user may authorize scheduled research without authorizing message sending. Record each capability separately.

Stop or pause when:

- identity evidence conflicts;
- stored state and visible platform state disagree;
- a required approval is absent;
- the target mix or batch limit fails;
- the storage write fails and no recovery event can be recorded;
- the platform presents a security, verification, rate-limit, or policy warning;
- the user-defined cost, volume, or error threshold is reached.

Never attempt to bypass platform limits, verification, security controls, or access restrictions.

## Completion contract

A deployment is complete only when its profile is approved, private storage is configured, a fictional dry run passes, a small real batch is reviewed, recovery behavior is tested, and enabled capabilities are explicitly recorded.
