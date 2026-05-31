# Settings Page Audit Template

## Information architecture

Check whether the page is grouped by user concepts:

- Account identity
- Security and credentials
- Billing, usage, and cost controls
- Preferences
- Notifications
- Privacy
- Danger zone

## Implementation leakage

List any internal terms visible to users:

- Auth provider IDs:
- Vendor implementation names:
- Database fields:
- Feature flags:
- Internal roles/codenames:

Rewrite them into user-facing terms.

## Save model

- Instant save:
- Section save:
- Page save:
- Confirmation flow:
- Unclear or mixed behavior:

## Risk review

- Cost-risk settings:
- Privacy-sensitive settings:
- Security-sensitive settings:
- Destructive actions:

## Copy rewrites

| Area | Current | Suggested |
|---|---|---|
| Profile |  |  |
| Security |  |  |
| Preferences |  |  |
| Privacy |  |  |
| Danger zone |  |  |
