# Reference Architecture

## Design goals

The architecture prioritizes authentic communication, evidence-backed personalization, human control, recoverability, and bounded context usage. It separates persona, workflow rules, contact data, and execution state so private material does not have to be embedded in general prompts.

## Components

### Main orchestrator

- translates the user's objective into a round definition;
- assigns target-person weights and batch size;
- loads only the required persona policy;
- creates and owns the round manifest;
- routes work to the three agents;
- enforces approval and synchronization gates;
- reports results and unresolved decisions to the user.

### Executor agent

- searches within the specified school, location, role, industry, or company scope;
- checks basic relevance and duplicate state;
- extracts verifiable profile evidence;
- drafts a specific, low-pressure note using the private persona layer;
- records drafts separately from actual send state;
- executes only actions that have passed the required gates.

The Executor is evaluated on relevance and evidence quality, not maximum send volume.

### Auditor agent

- independently verifies canonical URL, visible name, title, and company;
- checks whether personalization claims are supported by evidence;
- rejects generic praise and unsupported assumptions;
- checks persona consistency without accessing raw private source conversations;
- validates duplicates, target mix, and approval requirements;
- returns `approved`, `needs_revision`, `rejected`, or `escalate_to_user`.

Separating execution and audit reduces self-confirmation by the drafting agent.

### Conversation maintenance agent

- reads the contact summary and only loads full context when required;
- tracks conversation stage and the last meaningful inbound/outbound message;
- distinguishes a polite acknowledgment from a substantive reply;
- chooses among reply, wait, natural close, or escalation;
- prevents repeated follow-ups and premature requests;
- drafts context-aware replies using the private persona layer;
- escalates resumes, opportunities, referrals, meetings, commitments, and sensitive topics.

Success is a respectful and useful relationship, not indefinite conversation length.

## Shared state

Agents communicate through a versioned round manifest instead of relying on chat memory. The manifest stores objectives, target weights, candidates, evidence, drafts, review verdicts, conversation state, gates, and CRM synchronization status.

The JSON schema in `schemas/round-manifest.schema.json` is intentionally tool-neutral. A workbook, Google Sheet, or database can act as the durable CRM.

## Quality gates

| Gate | Question |
|---|---|
| Identity | Do URL, visible name, title, and company refer to the intended person? |
| Evidence | Is each personalized detail supported by visible evidence? |
| Duplicate | Has this profile or message already been processed? |
| Persona | Does the draft preserve the user's communication policy? |
| Quantity | Is the round size within the planned range? |
| Mix | Does the actual target distribution match the intended weights? |
| Conversation | Is this action appropriate for the current relationship stage? |
| Approval | Has the user approved every sensitive action? |
| Sync | Was the final state committed to durable storage or recovery log? |

## Token and context controls

1. **Role-scoped prompts:** each agent receives only its task policy and required records.
2. **Small batches:** process roughly 8–10 records, audit them, then continue.
3. **Incremental summaries:** retain key facts, stage, last message, allowed next action, and unresolved risks.
4. **Change-based context loading:** do not reread full conversations during an active waiting period unless state changes.
5. **Structured outputs:** use schema-validated records instead of repeatedly interpreting prose.
6. **Persona separation:** expose a compact behavior policy to agents, not raw messages, emails, or interviews.
7. **Recovery events:** if the CRM write fails, append a pending synchronization event before reporting completion.

## Conversation stages

The exact stages are configurable. A conservative default is:

1. **Establish connection:** thank the contact, mention one verified detail, and ask one low-cost question.
2. **Build trust:** respond to what was actually said and explore one topic at a time.
3. **Request feedback:** only after substantive exchange; resume-review requests require approval.
4. **Discuss opportunity:** only after trust and a concrete fit exist; job and referral requests require approval.
5. **Wait or close:** avoid repeated follow-ups, respect non-response, and preserve the relationship.

Stage count is not a quota. A conversation advances only when the interaction supports it.

## Storage adapters

The public templates are spreadsheet-ready, but the workflow should keep storage behind a simple adapter:

```text
loadRound(id)
saveRound(manifest)
loadContact(canonicalUrl)
upsertContact(record)
appendRecoveryEvent(event)
```

This makes Excel, Google Sheets, and databases interchangeable without changing agent responsibilities.
