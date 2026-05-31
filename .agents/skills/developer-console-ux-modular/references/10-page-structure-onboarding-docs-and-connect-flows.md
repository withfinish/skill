# Page structure, section design, onboarding, docs, and connect flows

## Page structure patterns

Choose page structure by task, not by default template.

### Resource list

Use list or table depending on comparison needs.

### Debugging

Use event stream, timeline, detail sheet.

### Configuration

Use sections and field rows.

### Object detail

Use summary, details, history, related resources.

### Usage

Use metrics, trend, breakdown, freshness, limits.

### Security

Use credentials, sessions, auditability, risk explanations.

### Anti-pattern

Do not make every page:

`Header → filters → table → pagination → modal form`

That makes the product feel like a CRUD admin panel.


## Section design

Sections should reflect the type of content.

Examples:

- Status section: current status, freshness, last check.
- Configuration section: field rows, impact copy, save model.
- Credential section: masked values, copy, rotate, last used.
- Danger section: impact, confirmation flow.
- History section: timeline and audit.
- Usage section: current period, limits, breakdown.

Anti-pattern:

Every section looks like the same card with title, description, fields, and button.


## Onboarding and quickstart

### Pattern

Onboarding should be embedded where the user needs it.

Examples:

- API keys page with no key → create key and run first request.
- Logs page with no traffic → show command to send first request.
- Webhooks page with no endpoint → add endpoint and send test event.
- Deployments page with no repo → import repository.

### Anti-pattern

Avoid a detached checklist widget that does not integrate with actual pages.


## Docs and help integration

### Pattern

Docs links should be contextual.

Examples:

- API keys page → authentication docs.
- Webhooks page → signature verification docs.
- Logs page → error codes docs.
- Environment variables page → runtime config docs.
- Error state → exact repair doc.

Docs should supplement UI copy, not replace it.

Bad:

`Something went wrong. Read the docs.`

Better:

```
Webhook delivery failed because your endpoint returned 401 Unauthorized.
Check that your endpoint accepts requests from our webhook signer.
[View delivery logs] [Read signature docs]
```


## Import and connect flows

### Pattern

When connecting third-party services, explain access and effects.

Good:

```
Connect GitHub
Import repositories and trigger deployments from selected repos. We won’t make changes without your confirmation.
```

Explain:

- What will be accessed.
- What will not be accessed.
- Who can see it.
- How to disconnect.
- What happens after disconnecting.

### Anti-pattern

Avoid a bare `Connect GitHub` button with no permission context.


## Notifications and system status

Expose platform status when relevant.

If an error may be platform-side, provide status link:

```
We’re investigating elevated errors in US East.
[View status]
```

Keep normal status page access low-noise in help menu.

Do not make users debug for an hour when the platform is degraded.
