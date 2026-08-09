# Privacy and Safety

Professional networking data can contain personal information about both the user and third parties. Treat it as private by default.

## Never commit

- real contact names, profile URLs, or conversation transcripts;
- private persona files or their source messages, emails, interviews, and notes;
- resumes, phone numbers, email addresses, credentials, or access tokens;
- browser profiles, cookies, screenshots, workbook backups, or runtime output;
- message drafts tied to identifiable real people;
- password files or `.codex-temp/` contents.

## Recommended separation

```text
public repository                 private local workspace
----------------                 -----------------------
schemas                           real persona
fictional examples               source conversations
empty templates                  contact CRM
architecture docs                run manifests
privacy guidance                 browser state and credentials
```

Use synthetic data in documentation. A name that looks fictional is not sufficient if its URL, employer, message content, or timeline can identify a real person.

## Human control

Never let the system autonomously make commitments, send sensitive information, request referrals, or act on uncertain identity. Users remain responsible for reviewing messages and complying with platform terms and applicable laws.
