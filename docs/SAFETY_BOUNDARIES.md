# Safety and Authority Boundaries

PersonaBridge assists a user; it does not become the user.

## Always approval-gated

- resumes and document sharing;
- job, opportunity, and referral requests;
- meetings and calendar commitments;
- personal or confidential information;
- financial, legal, medical, or other sensitive topics;
- promises, commitments, or representations on the user's behalf;
- ambiguous replies or uncertain contact identity.

## Never authorized

- impersonation or deceptive identity claims;
- fabricated personalization evidence;
- bypassing platform limits, verification, security controls, or access restrictions;
- collecting private information without a legitimate, disclosed purpose;
- treating silence as consent;
- converting a one-time approval into standing authority;
- publishing private personas, contacts, messages, credentials, or browser state.

## Kill switch

Every automated deployment must provide a user-accessible way to pause future runs. Pausing must not delete audit or recovery records. Resuming requires checking unresolved failures and confirming that the approved profile is still current.
