# Conditional Deployment Interview

Use `QUESTIONNAIRE.yaml` as the machine-readable source of question IDs and conditions. This document explains the intended conversation.

## Interview behavior

- Ask one coherent section at a time, normally 1–4 questions.
- Summarize recorded answers before advancing.
- If an answer activates a conditional branch, ask it next.
- If the user does not know, record `undecided`; do not invent a default for permissions or sensitive boundaries.
- Allow the user to revise any prior answer.
- Never ask for passwords, cookies, recovery codes, or secret values in chat.

## Phase 0 — Intent

Determine whether the user wants explanation, a deployment plan, local implementation, or automation. Stop the interview for explanation-only users.

## Phase 1 — User and career context

Collect career stage, school/program if relevant, location/timezone, target industry, target roles, experience, job-search stage, preferred languages, and LinkedIn experience.

## Phase 2 — Networking objectives

Ask for one primary objective and ranked secondary objectives. Define measurable but realistic success criteria. Do not equate raw connection count with relationship quality.

## Phase 3 — Target-person mix

Collect preferred schools, locations, companies, roles, seniority, background signals, exclusions, batch size, and weights. Validate that weights total 1.0.

## Phase 4 — Persona

Determine whether a private persona already exists, whether the user will use dot-skill, allowed source types, forbidden sources, language texture, editing tolerance, phrases to avoid, and decisions AI must never make.

## Phase 5 — Communication and conversation policy

Define formality, length, question count, praise policy, follow-up delay, maximum follow-ups, stage-advance evidence, natural-close behavior, and message types requiring approval.

## Phase 6 — Storage and privacy

Choose Excel, Google Sheets, or database storage; data location; retained fields; transcript policy; retention/deletion policy; recovery log; dashboard needs; and access restrictions.

## Phase 7 — Automation

Choose an automation level and follow only its conditional branches. Record separate permission for discovery, enrichment, drafting, auditing, reminders, CRM writes, browser preparation, and external sending. Follow `AUTOMATION_DEPLOYMENT.md`.

## Phase 8 — Scale, cost, and stops

Collect batch size, schedule, weekly limits, token/API budget, speed-versus-accuracy preference, audit coverage, retry limits, and stop conditions.

## Phase 9 — Acceptance criteria

Define a qualified contact, substantive reply, persona-consistent message, blocking error, escalation event, completed round, required sampling, dry-run pass, and rollback trigger.

## Interview output

Create a Deployment Profile matching `schemas/deployment-profile.schema.json`. Show the user a plain-language summary and explicit capability/approval matrix. Implementation begins only after the user approves that profile.
