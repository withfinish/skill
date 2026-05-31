# Page layout, sections, and headers

## Page structure should match the task

Do not default every page to:

```text
Header
Filters
Table
Pagination
Modal form
```

Choose structure by task:

| Task | Better structure |
|---|---|
| Browse resources | List + details, sometimes table |
| Compare values | Table |
| Debug events | Timeline or event stream |
| Configure settings | Sections + field rows |
| View object lifecycle | Summary + timeline + details |
| Onboard first use | Empty state + quickstart |
| Inspect usage | Metrics + breakdown + limits |
| Manage security | Policy sections + audit trail |

## Header responsibilities

A page header should answer:

- Where am I?
- What object or page is this?
- What scope does it affect?
- What is the state?
- What is the primary next action?

It is not a toolbar and not a marketing hero.

## Header template

```text
Breadcrumb
Title + key status
Short description
Useful metadata
Primary action + at most one or two secondary actions
```

Example:

```text
Acme API / Deployments
Deployment #428    Live
Production release from branch `main`.

Deployment ID: `dep_8f42...` [Copy]
Updated 42 seconds ago
Region: US East

[View logs] [Rollback]
```

## Header titles should be specific

### Anti-pattern

```text
Overview
Details
Settings
General
Manage
```

### Better

```text
Acme API overview
Production API keys
Project settings
Deployment #428
Webhook deliveries
Billing for Agent Velo
```

## Header descriptions should not repeat labels

### Anti-pattern

```text
API keys
Manage API keys.
```

### Better

```text
API keys
Create keys for server-side requests. Keep production keys separate from development.
```

## Header should show scope when risk is high

### Anti-pattern

```text
Environment variables
```

### Better

```text
Production environment variables
Used by new deployments in `Acme API`.
```

## One dominant action per page

A header usually has one primary page-level action.

Good:

```text
Projects → Create project
API keys → Create key
Members → Invite member
Webhooks → Add endpoint
Deployments → Deploy
Billing → Add payment method
```

Poor:

```text
[Create] [Import] [Export] [Refresh] [Docs] [Settings] [More]
```

If the header has many buttons, the page lacks a clear main task.

## Destructive actions do not belong beside routine actions

### Anti-pattern

```text
Project settings        [Save changes] [Delete project]
```

### Better

- `Save changes` appears near settings or in a sticky save bar.
- `Delete project` appears in Danger zone or overflow, then opens a confirmation flow.

## Header metadata should clarify, not decorate

### Anti-pattern

```text
Deployment #428   Live   Production   main   iad1   42s ago   Kai
```

### Better

```text
Deployment #428   Live
Production environment
Branch: `main`
Region: US East
Updated 42 seconds ago
```

Avoid turning metadata into a chip parade.

## Header copy should not be marketing copy

### Anti-pattern

```text
Ship faster with our next-generation deployment engine.
```

### Better

```text
Track builds, releases, and rollbacks for this project.
```

Users inside a console need orientation, not persuasion.

## Section design

Sections should differ by purpose.

| Section type | Emphasis |
|---|---|
| Status | Current state, freshness, action needed |
| Configuration | Field, value, impact, save behavior |
| Credential | Masked value, copy, rotate, revoke, last used |
| Danger | Impact, irreversibility, confirmation |
| History | Timeline, actor, timestamp, before/after |
| Usage | Current period, trend, limit, cost impact |

### Anti-pattern

Every section is the same card: title, description, button.

### Better

Match the structure to the content and risk.

## Field rows

Settings field rows should not look like raw database rows.

Good field row anatomy:

```text
Project name
Shown in the dashboard, logs, and audit events.
Acme API
[Edit]
```

```text
Region
Builds and runtime data are processed in this region. This cannot be changed after creation.
US East
```

Field copy should explain impact, not repeat the label.

## Empty states

Empty states should distinguish:

- Never created
- No results for filters
- No data yet
- Not enough permission
- Data delayed
- Feature not enabled

### Anti-pattern

```text
No data.
```

### Better

```text
No logs yet.
Logs will appear here after this project receives requests.
```

```text
No failed deployments in this time range.
Try a wider time range or clear the status filter.
```

## Loading states

Skeletons are not enough for operational tasks.

### Anti-pattern

A spinner with no context.

### Better

```text
Loading deployments...
Checking build status...
Syncing GitHub repositories...
Fetching usage for the current billing period...
```

For long tasks, show a state machine:

```text
Queued → Building → Uploading assets → Deploying → Verifying → Live
```

## Error page headers

Error pages should be specific.

### Anti-pattern

```text
Page not found
```

### Better

```text
Deployment not found
It may have been deleted, or you may not have access to this project.

[Back to deployments] [Retry]
```

### Anti-pattern

```text
Forbidden
```

### Better

```text
You need owner access to view billing
Ask a workspace owner to grant access.
```

## Page cards

Cards are useful, but do not wrap every small fact in a card.

### Anti-pattern

One card each for:

- Status
- Region
- Owner
- Project ID
- Last updated
- Usage

### Better

Use a single summary section with field rows, then reserve cards for independent modules.

## Browser titles

Developer users open many tabs. Browser titles should match headers.

Good:

```text
Production API keys - Acme API
Deployment #428 - Acme API
Logs - Acme API
```

Poor:

```text
Dashboard
Settings
Overview
```

## Header anti-pattern checklist

- Title says `Details` or `General`.
- Description repeats the title.
- Scope is hidden.
- Many buttons compete for attention.
- Destructive action sits beside routine action.
- Header is a marketing hero.
- Metadata is chip-heavy or dot-heavy.
- Page action is unrelated to page context.
- Header does not reflect read-only or permission state.
- Header and empty state duplicate the same CTA awkwardly.
