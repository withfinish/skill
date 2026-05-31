# Operational states, diagnostics, errors, logs, webhooks, deployments, and audit

## State clarity creates trust

Developer consoles must distinguish:

- Ready
- Live
- Queued
- Building
- Deploying
- Failed
- Paused
- Synced
- Retrying
- Rate limited
- Missing config
- Read-only
- Deprecated

Use states like system protocols, not emotional copy.

### Anti-pattern

```text
Oops! We hit a snag.
```

### Better

```text
Deployment failed.
The build command exited with code 1.
```

## State machines

For asynchronous work, show progression.

Deployment example:

```text
Queued
Building
Uploading assets
Deploying
Verifying
Live
```

Webhook retry example:

```text
Delivered
Failed
Retry scheduled
Retrying
Gave up after 5 attempts
```

Do not say `Done` before the state is truly final.

## Data freshness

Show freshness when data informs decisions.

Good:

```text
Updated 2 minutes ago
Last checked 30 seconds ago
Auto-refresh on
Usage updated hourly
```

Bad:

```text
Usage: 12,482 requests
```

without period or freshness.

## Error messages

Good error messages include:

- What failed
- Cause or likely cause
- What changed or did not change
- Next step
- Request ID when useful

### Example

```text
We couldn’t create the deployment.
The selected branch no longer exists. Choose another branch or push `main` again.
No production traffic was affected.
```

### Example with request ID

```text
We couldn’t load project settings.
Try again. If this continues, contact support with Request ID `req_...`.
```

## Raw technical details

Do not show raw stack traces by default. Provide a collapsible technical details section when appropriate.

Default:

```text
We couldn’t send the invite.
No changes were made.
```

Technical details:

```text
Error code: invite_already_exists
Request ID: `req_...`
```

## Empty states

Operational empty states should explain why data is absent.

```text
No logs yet.
Logs will appear here after this project receives requests.
```

```text
No webhook deliveries yet.
We’ll show delivery attempts after your endpoint receives its first event.
```

```text
No failed deployments in this time range.
Try a wider time range or clear the status filter.
```

## Loading states

Use specific loading copy:

```text
Loading deployments...
Checking build status...
Syncing GitHub repositories...
Fetching usage for the current billing period...
```

For long-running actions, show stages instead of a spinner.

## Logs

Logs should be structured enough for debugging.

Useful fields:

- Timestamp
- Level
- Method/path
- Status
- Request ID
- Environment
- Deployment
- Message

Details should include:

- Headers, if relevant and safe
- Body/payload, if relevant and safe
- Related deployment
- Copy request ID
- Open trace
- Retention note

## Webhook delivery detail

Good detail fields:

- Event name
- Status
- Endpoint URL
- Last attempt time
- Response code
- Response body
- Headers
- Payload
- Retry history
- Event ID
- Request ID
- Retry action
- Copy payload/event ID

Do not dump raw JSON first. Lead with summary.

## Deployment detail

A useful deployment detail page should show:

- Status
- Environment
- Branch
- Commit
- Region
- Started/finished time
- Duration
- Build steps
- Logs
- URL
- Rollback option
- Related audit events

Avoid a thin detail page with only name, ID, status, created, updated.

## Audit vs activity

Activity feed is for understanding. Audit log is for proof.

### Activity example

```text
Kai invited Alex.
Deployment #428 went live.
Webhook endpoint failed.
```

### Audit example

```text
Actor: Kai
Action: Rotated production API key
Target: Acme API
Time: Jan 12, 14:03 UTC
IP: 203.0.113.4
Request ID: `req_...`
Result: Success
```

Do not mix them without clear purpose.

## Notifications

Notifications should be operational, not social or marketing-heavy.

Good notifications:

- Deployment failed
- Usage nearing limit
- Webhook delivery failing
- Invoice payment failed
- API key expires soon
- SSO certificate expires soon
- New security event

Poor notifications:

- Blog post
- Marketing update
- Random tips
- Feature promo

Use changelog for product updates.

## System status

If the platform has incidents, make status discoverable.

When relevant errors occur:

```text
We’re investigating elevated errors in US East.
[View status]
```

Do not make users debug their own app when the platform is degraded.

## Diagnostics anti-pattern checklist

- Error copy ends at `Something went wrong`.
- Raw backend exception is shown as product copy.
- No request ID for support-worthy failures.
- Async tasks jump from loading to success with no stages.
- Data has no freshness indicator.
- Logs are raw and unstructured.
- Webhook details begin with huge raw JSON.
- Activity feed and audit log are conflated.
- Notifications include marketing clutter.
- System status is hidden when platform incidents exist.
