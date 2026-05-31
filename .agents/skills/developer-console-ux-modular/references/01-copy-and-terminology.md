# User copy and terminology

## Copy goal

Developer console copy should answer:

- What is this?
- What scope does it affect?
- What changed?
- What can I do next?
- What happens if I continue?
- Was anything affected?
- Can I verify it?

It should not expose internal implementation names or make the user infer product behavior.

## Use user concepts, not implementation concepts

### Anti-patterns

```text
You are signed in with google_auth.
clerk_session
Clerk user
strategy_google_oauth2
user_role_admin_internal
feature_flag_new_billing_flow
workspace_beta_enabled_true
sync_workspace_entitlements failed
```

### Better

```text
Signed in with Google.
Email sign-in
External identity ID
Workspace owner
Preview feature
Billing setup incomplete
We couldn’t refresh your plan limits. We’ll retry automatically.
```

## Do not use provider names unless the provider is user-facing

If the user intentionally connected GitHub, Google, Slack, Stripe, or Vercel, naming the provider is fine.

If the product internally uses Clerk, Prisma, Supabase, Stripe Billing, Auth0, LaunchDarkly, or another vendor, do not expose it in ordinary UI unless the page is specifically about that integration.

### Anti-pattern

```text
Clerk identity is not affected.
```

### Better

```text
Your external sign-in account will not be deleted.
```

## Labels should be productized

### Anti-patterns and better labels

| Anti-pattern | Better |
|---|---|
| `created_at` | Created |
| `updated_by_user_id` | Last updated by |
| `is_active` | Status |
| `billing_status_enum` | Billing status |
| `auth_provider` | Sign-in method |
| `tenant_id` | Workspace ID, only if useful |
| `principal_id` | Member ID, only if useful |
| `organization_user_invites` | Invites |
| `entitlements` | Plan limits |
| `webhook_consumers` | Webhook endpoints |

## Make titles specific

### Anti-pattern

```text
Details
General
Manage
Resources
Settings
```

### Better

```text
Production API keys
Project settings
Webhook deliveries
Deployment #428
Billing for Agent Velo
Account security
```

## Avoid copy that repeats the label

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

### Anti-pattern

```text
Language
Affects language.
```

### Better

```text
Language
Used for the console interface and account emails.
```

## Success copy should explain scope and effect

### Weak

```text
Saved.
Done.
Success.
Connected.
```

### Better

```text
Production variables saved. New deployments will use these values.
API key created. Copy it now; you won’t be able to see it again.
GitHub connected. You can now import repositories from `kai/agent-velo`.
Webhook endpoint added. We’ll send a test event next.
Ownership transfer sent to Alex. You remain the owner until they accept.
```

## Error copy should be diagnostic

A good error message includes:

1. What failed.
2. Why, if known.
3. What the user can do.
4. Whether anything changed.
5. A copyable request ID when useful.

### Anti-pattern

```text
Something went wrong.
```

### Better

```text
We couldn’t create the API key.
No changes were made. Try again, or contact support with Request ID `req_9xK2...`.
```

### Anti-pattern

```text
PrismaClientKnownRequestError: Unique constraint failed on the fields: ('email')
```

### Better

```text
This member has already been invited.
Ask them to accept the existing invite, or revoke and resend it.
```

### Anti-pattern

```text
You do not have permission: org.member.write
```

### Better

```text
You need workspace admin access to invite members.
Ask an owner to change your role.
```

## Use anxiety-reducing copy

These small lines create trust:

```text
No changes were made.
This only affects new deployments.
Existing requests are not affected.
You can change this later.
You won’t be able to see this secret again.
We’ll retry automatically.
Last checked 2 minutes ago.
Used by 3 active projects.
Requires workspace admin access.
This action is recorded in the audit log.
Production traffic will continue to use the previous version.
This may take up to 60 seconds.
The original key will remain active until you revoke it.
```

Use them when they answer a likely hidden question.

## Be careful with `·` separators

Dot-separated metadata often creates fake neatness and poor scanability.

### Anti-pattern

```text
Production · Ready · 2m ago · US East · main
```

### Better

```text
Ready
Production environment
Branch: `main`
Region: US East
Updated 2 minutes ago
```

Use `·` only for very low-weight pairs such as:

```text
Updated 2 minutes ago · by Kai
```

If a line has more than one dot separator, re-evaluate the information architecture.

## Chips and badges

Chips are not a container for all metadata. Use them sparingly.

Good chip/badge uses:

```text
Live
Failed
Building
Paused
Preview
Production
Read-only
Beta
Verified
```

Poor chip uses:

```text
created 2m ago
kai@example.com
main
us-east-1
12 requests
project id
updated by
clerk_session
default
root
```

### Anti-pattern

A profile card with chips:

```text
clerk_session   default   root
```

### Better

```text
Role: Owner
Sign-in method: Email
Account ID: `usr_...` [Copy]
```

## Monospace and inline code

Use monospace for exact technical values:

- Commands
- Code
- IDs
- Tokens
- Paths
- Headers
- HTTP methods
- Environment variables
- File names
- Commit hashes

Do not use monospace for ordinary labels, buttons, navigation, or user names.

### Good

```text
Add `DATABASE_URL` to deploy this project.
Request ID: `req_abc123`
Branch: `main`
```

### Bad

```text
`Create Project`
`Billing`
`You are signed in`
```

## ID copy

Do not make IDs the primary name when a human name exists.

### Anti-pattern

```text
Project prj_9xK2aQ
Workspace org_82jKls
User usr_7281
```

### Better

```text
Acme API
Project ID: `prj_9xK2aQ` [Copy]

Agent Velo
Workspace ID: `org_82jKls` [Copy]
```

## Button copy

Prefer specific action labels.

### Weak

```text
Submit
OK
Confirm
Reset
Manage
Delete
```

### Better

```text
Create key
Send invite
Rotate key
Revoke API key
Manage sign-in
Delete project
Save production variables
Start account deletion
```

## Dangerous confirmation copy

Never use only `Are you sure?`.

### Anti-pattern

```text
Are you sure?
[Cancel] [Confirm]
```

### Better

```text
Delete `Acme API`?
This permanently deletes deployments, logs, environment variables, API keys, and webhook endpoints for this project.
Type `Acme API` to confirm.

[Cancel] [Delete project]
```

## Search placeholders

Search placeholder copy should tell users what can be searched.

### Anti-pattern

```text
Search...
```

### Better

```text
Search logs by request ID, path, or message
Search projects by name or ID
Search members by name or email
Search deployments by branch, commit, or ID
```

If advanced syntax exists, show it as optional help, not as a requirement.

```text
Try `level:error path:/api/users`
```

## Terminology consistency

Do not rotate names for the same concept.

Bad:

```text
Project / App / Service / Resource
Rotate key / Regenerate key / Refresh key / Reset key
Live / Active / Ready / Running
```

Choose one primary term and use it consistently.
