# Tables, lists, search, filters, and product states

## Tables and lists

### Core principle

Tables are for comparison and scanning structured data. They are not the default answer for every resource page.

Use tables when users need to compare many rows by the same fields.

Use lists, detail panels, timelines, or cards when users need context, state, or object lifecycle.

### Pattern

For API keys, a list may be better than a wide table:

```
Production key
Created Jan 12
Last used 2 hours ago
sk_live_••••a93f
[Copy]
```

For deployments:

```
Deployment #428
Status: Live
Environment: Production
Branch: main
Commit: 8f4a21c
Started 3 minutes ago
Duration: 48s
```

### Anti-pattern

Avoid wide CRUD tables like:

| Name | Status | Environment | Region | Branch | Created | Updated | Owner | Usage | Actions |
|---|---|---|---|---|---|---|---|---|---|

Avoid row action forests:

`View` `Edit` `Duplicate` `Delete` `More`

### Better action placement

- Row: at most one low-risk, high-frequency action such as `Open` or `Copy`.
- Detail sheet or page: object-specific actions.
- Header: page-level primary action.
- Toolbar: batch actions only after selection.
- Danger zone: destructive actions.


## Filtering and search within pages

### Pattern

Filters should refine the current view, not become navigation.

Good Logs filters:

- Search logs
- Level
- Time range
- Environment

Good search placeholder:

- `Search logs by request ID, path, or message`
- `Search projects by name or ID`
- `Search members by name or email`
- `Search deployments by branch, commit, or ID`

If advanced syntax exists, show examples without requiring it:

`level:error path:/api/users`

### Anti-pattern

Avoid chip walls:

`All` `Errors` `Warnings` `Info` `Production` `Preview` `GET` `POST` `500` `Last 24h` `Live tail`

Avoid putting filters in the global sidebar.

Avoid placeholder text like `Search...` when the searchable fields are not obvious.


## Empty states

### Pattern

Empty states must distinguish why there is no content.

Types:

- Never created.
- No matching results.
- Waiting for data.
- Permission denied.
- Feature not enabled.
- External service not connected.
- Data delayed.

Good examples:

```
No API keys yet.
Create a key to authenticate requests from your backend.
```

```
No logs yet.
Logs will appear here after this project receives requests.
```

```
No failed deployments in this time range.
Try a wider time range or clear the status filter.
```

### Anti-pattern

Avoid:

- `No data.`
- `No records found.`
- `This table is empty.`
- Empty illustrations with no next step.


## Loading states and asynchronous operations

### Pattern

Loading should explain what is happening.

Good:

- `Loading deployments...`
- `Checking build status...`
- `Syncing GitHub repositories...`
- `Fetching usage for the current billing period...`

For long operations, show stages:

`Queued` → `Building` → `Deploying` → `Verifying` → `Live`

### Anti-pattern

Avoid:

- Generic spinners for long operations.
- `Running mutation...`
- `Hydrating client...`
- `Polling job status...`
- Claiming `Deployed` when the build is only queued.


## Success states

### Pattern

Success feedback should say what changed and where it applies.

Good:

- `API key created. Copy it now; you won’t be able to see it again.`
- `Production variables saved. New deployments will use these values.`
- `Webhook endpoint added. We’ll send a test event next.`
- `Ownership transfer sent to Alex. You remain the owner until they accept.`

### Anti-pattern

Avoid:

- `Success.`
- `Done.`
- `Saved.` when scope matters.
- Toast-only feedback for high-risk actions.


## Error states

### Pattern

Error messages should be diagnostic and repairable.

Structure:

1. What happened?
2. Why did it happen, if known?
3. What can the user do?
4. What changed or did not change?
5. What can be copied for support?

Good:

```
We couldn’t create the deployment.
The selected branch no longer exists. Choose another branch or push main again.
No production traffic was affected.
```

```
Webhook delivery failed.
Your endpoint returned 401 Unauthorized on the last attempt.
Request ID: req_...
```

### Anti-pattern

Avoid:

- `Something went wrong.`
- `500 Internal Server Error` as the only message.
- Raw stack traces as primary UI copy.
- `Read the docs` as the only next step.
- Cute error copy in serious contexts.

Technical details may be available behind `Show technical details`.


## Permissions and access copy

### Pattern

Explain missing permission in terms of user role and action.

Good:

- `You need owner access to delete this workspace.`
- `Ask a workspace owner to change billing settings.`
- `You can view settings for this project. Owner access is required to make changes.`

### Anti-pattern

Avoid:

- `You are not allowed to do this.`
- `Permission denied: org.member.write`
- Disabled buttons with only hover tooltips.

If an action is disabled, explain why in visible text and offer a path when possible.


## Time, freshness, and auditability

### Pattern

Time is evidence in developer tools.

Use:

- Relative time for overview: `Updated 2 minutes ago`.
- Absolute time on hover or detail: `Jan 12, 2026, 14:03:22 UTC`.
- UTC or explicit timezone for logs and audits.
- Duration for builds and deployments.
- `Last checked`, `Last synced`, or `Auto-refresh on` for dynamic data.

### Anti-pattern

Avoid:

- `Updated 3:42` without date or timezone.
- Usage numbers without freshness: `12,482 requests`.
- Build status without start time.
- Hidden auto-refresh behavior.
