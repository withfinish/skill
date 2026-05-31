# Operational pages: logs, webhooks, deployments, audit, and activity

## Logs and debugging pages

### Pattern

Logs should help users investigate, not just display raw text.

Include:

- Time range.
- Level filter.
- Environment filter.
- Request ID search.
- Structured fields.
- Expandable detail.
- Copy line / request ID.
- Link to trace, deployment, or webhook event.
- Retention period.
- Live tail that users can start/stop.

### Anti-pattern

Avoid:

- A raw log stream with no structure.
- Logs without timezone.
- Logs with no copyable request ID.
- Live updates that move content while the user is reading.


## Webhooks and events

### Pattern

Webhook pages should make delivery state, endpoint behavior, and retries clear.

List row:

```
payment.succeeded
Failed
Endpoint: https://api.example.com/webhook
Last attempt: 14:03 UTC
```

Detail sheet:

- Status.
- Endpoint.
- Response code.
- Response body.
- Headers.
- Payload.
- Retry history.
- Event ID [Copy].
- Request ID [Copy].
- `Retry delivery`.

### Anti-pattern

Avoid putting full raw payload first. Start with summary and diagnostic evidence.


## Deployment pages

### Pattern

Deployment pages should show lifecycle and evidence.

Include:

- Status.
- Environment.
- Branch.
- Commit.
- Build duration.
- Region.
- Logs.
- Release URL.
- Rollback action.
- Related incidents.
- Audit trail.

A timeline is often better than a table:

`Queued` → `Building` → `Uploading assets` → `Deploying` → `Live`

### Anti-pattern

Avoid a wide deployment table with many actions in each row.


## Audit and activity

### Pattern

Separate activity feed from audit log.

Activity feed helps users understand recent events:

- `Kai invited Alex.`
- `Deployment #428 went live.`

Audit log proves what happened:

- Actor.
- Action.
- Target.
- Time.
- IP.
- User agent.
- Request ID.
- Before/after state.
- Result.

### Anti-pattern

Avoid vague audit entries:

- `Kai did something to project.`
- `Updated settings.`

Better:

- `Kai rotated the production API key.`
- `Project: Acme API`
- `Time: Jan 12, 14:03 UTC`
- `Request ID: req_...`
