# PersonaBridge Bootstrap Prompt

Copy this prompt into an AI agent together with the repository URL:

```text
Read this repository's AGENTS.md and agent/PROJECT.yaml first.

Explain PersonaBridge's target users, purpose, non-goals, design principles,
workflow, multi-agent architecture, durable state, privacy model, automation
levels, and approval boundaries. Do not deploy anything yet.

Ask whether I want to learn, create a deployment plan, implement locally, or
enable automation. If I choose deployment or automation, follow
agent/DEPLOYMENT_INTERVIEW.md and the conditional rules in
agent/QUESTIONNAIRE.yaml. Ask progressively, generate a private Deployment
Profile, summarize all capabilities and approval boundaries, and wait for my
explicit approval before implementation. Run a fictional dry run before any
real-data workflow or external action.
```
