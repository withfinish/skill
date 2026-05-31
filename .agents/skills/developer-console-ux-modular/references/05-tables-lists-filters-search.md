# Tables, lists, filters, search, timelines, and logs

## Tables are not the default answer

Developer products naturally have resources, but not every resource needs a table.

Use tables when the user needs to compare many rows across consistent columns.

Use lists, cards, detail pages, sheets, timelines, or sections when the user needs to inspect, configure, debug, or act.

## Table anti-pattern

```text
Name | Status | Environment | Region | Branch | Created | Updated | Owner | Usage | Actions
```

This often becomes a database grid, not a product workflow.

## Better resource list

For deployments:

```text
Deployment #428
Live
Production environment
Branch `main`
Commit `8f4a21c`
Started 3 minutes ago
Duration 48s

Actions: View logs, Rollback
```

A list or Sheet can carry richer hierarchy than a wide table.

## Row actions

Avoid mixing many actions into table rows.

### Anti-pattern

Every row contains:

```text
View | Edit | Duplicate | Delete | More
```

### Better

- Row opens detail Sheet or page.
- Copy action appears only where useful.
- Object actions live in Sheet/detail page.
- Destructive actions require confirmation.
- Bulk actions appear only after selection.

## When tables are appropriate

Tables work well for:

- Invoices
- Members when comparing roles/status
- API keys if columns are minimal
- Usage breakdowns
- Audit logs, if designed carefully
- Rate-limit events
- Webhook deliveries with minimal columns

Keep columns task-focused.

## Minimal API keys list

Good columns:

```text
Name
Environment
Last used
Created
Status
```

Avoid columns such as:

```text
User ID
Provider ID
Raw token value
Updated by user ID
Internal auth provider
Row actions for everything
```

## Filters

Filters should support the most common investigation paths without becoming a second navigation system.

Good default filters for logs:

```text
Search
Level
Time range
Environment
```

Avoid turning every dimension into a chip row:

```text
All  Errors  Warnings  Info  Production  Preview  GET  POST  500  Last 24h  Live tail
```

## Filter state

Good filters:

- Are visible and understandable.
- Can be cleared easily.
- Persist in URL when useful.
- Do not hide no-result causes.
- Distinguish no data from no matching results.

### No-result copy

```text
No failed deployments in this time range.
Try a wider time range or clear the status filter.
```

## Search

Search placeholders should name searchable fields.

```text
Search logs by request ID, path, or message
Search deployments by branch, commit, or ID
Search members by name or email
Search projects by name or ID
```

If advanced query syntax exists, provide optional examples:

```text
Try `level:error path:/api/users`
```

## Pagination and scrolling

Choose by content type.

| Content | Better navigation |
|---|---|
| Logs/events | Time-based list, live tail, load newer/older |
| Resources | Pagination or cursor list |
| Search results | Pagination, result count, clear filters |
| Audit log | Time range, export, cursor pagination |

Avoid infinite scroll for everything. Developers need shareable, recoverable states.

## Timelines

Timelines are better than tables for sequences and lifecycles.

Good for:

- Deployments
- Webhook retries
- Build steps
- Billing changes
- Permission changes
- Incident updates

### Anti-pattern

Build steps as table:

```text
Step | Status | Started | Ended | Duration | Action
```

### Better

```text
Queued
Building
Uploading assets
Deploying
Live
```

Each step can expand to logs and timestamps.

## Logs

Good logs pages include:

- Time range
- Level filter
- Environment
- Request ID search
- Structured fields
- Expandable details
- Copy line / copy request ID
- Link to trace, deployment, or request
- Retention period
- Live tail, if useful

### Anti-pattern

Raw log stream plus a generic search box.

### Better

Structured log list:

```text
14:03:22.184   ERROR   POST /v1/events   500   req_abc123
Message: Missing DATABASE_URL
[Open details] [Copy request ID]
```

## Webhook deliveries list

Good list columns:

```text
Event
Status
Endpoint
Time
```

Open Sheet/detail for:

- Payload
- Headers
- Response body
- Retry history
- Request ID
- Copy event ID
- Retry delivery

Do not put all payload and actions in the row.

## Audit logs

Audit logs can use tables, but must be precise.

Include:

- Actor
- Action
- Target
- Time
- IP, if relevant
- Result
- Request ID
- Before/after details in expansion

Avoid vague activity copy:

```text
Kai did something to project.
```

Better:

```text
Kai rotated the production API key.
Target: Acme API
Time: Jan 12, 14:03 UTC
Request ID: `req_...`
```

## Table/list anti-pattern checklist

- Table used because data exists, not because comparison is needed.
- Table has too many columns.
- Actions are mixed into every row.
- Row actions include destructive operations.
- Internal IDs are primary columns.
- Empty state says only `No data`.
- Filters are chips everywhere.
- Search placeholder says only `Search`.
- Infinite scroll prevents sharing and recovering state.
- Logs are raw dumps without structure.
