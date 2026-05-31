# User copy, terminology, and implementation leakage

## User-facing copy principles

### Use user concepts, not implementation concepts

| Internal / bad | User-facing / better |
|---|---|
| `google_auth` | `Google` |
| `clerk_session` | `Email sign-in` or `Google sign-in` |
| `tenant_id` | `Workspace ID` only if needed; otherwise hide |
| `auth_subject` | hide; show account or member name |
| `rbac_policy_denied` | `You need owner access to do this.` |
| `feature_flag_console_nav_v3` | hide; maybe `Preview` if user-facing |
| `created_at` | `Created` |
| `is_active` | `Status` |
| `strategy_google_oauth2` | `Google sign-in` |
| `sync_workspace_entitlements` | `Refreshing plan limits` |

### Do not expose provider implementation unless user connected that provider

Allowed:

- `Connected to GitHub`
- `Stripe account linked`
- `Google account connected`

Avoid when it is only your backend provider:

- `Identity managed by Clerk`
- `Clerk user`
- `Supabase auth hook`
- `Managed by Stripe customer portal`

Better:

- `Sign-in method: Google`
- `Manage sign-in settings`
- `Your external sign-in account will not be deleted.`

### Avoid generic labels

Bad:

- `Details`
- `General`
- `Manage`
- `Configure`
- `Resource`
- `Submit`
- `Confirm`
- `OK`

Better:

- `Production API keys`
- `Project settings`
- `Webhook deliveries`
- `Create key`
- `Send invite`
- `Delete project`
- `Rotate production key`

### Avoid overusing dot separators

Do not flatten different types of metadata into one dotted string.

Bad:

`Production · Ready · 2m ago · US East · main · Kai`

Better:

```
Status: Ready
Environment: Production
Branch: main
Region: US East
Updated 2 minutes ago
```

Dot separators are acceptable only for low-risk, low-density metadata, such as:

`Updated 2 minutes ago · by Kai`

If a line has more than two dots, reorganize the information.

### Use anxiety-reducing copy

These phrases are useful when accurate:

- `No changes were made.`
- `Production traffic is not affected.`
- `This only affects new deployments.`
- `Existing requests are not affected.`
- `You can change this later.`
- `You won’t be able to see this secret again.`
- `We’ll retry automatically.`
- `Last checked 2 minutes ago.`
- `Requires workspace owner access.`
- `This action is recorded in the audit log.`
- `The original key remains active until you revoke it.`
- `This may take up to 60 seconds.`


## Monospace and inline code

### Pattern

Use monospace for values that are exact, copyable, executable, or protocol-like.

Good:

- `npm install @acme/sdk`
- `OPENAI_API_KEY`
- `project_abc123`
- `POST /v1/events`
- `200 OK`
- `main`
- `sha256:...`

### Anti-pattern

Do not use monospace for ordinary interface language.

Bad:

- Navigation labels in monospace.
- Buttons like `Create Project` in monospace.
- User names in monospace.
- Marketing copy in monospace.

Developer-friendly is not terminal cosplay.


## IDs and technical details

### Pattern

IDs are useful for verification, debugging, support, and automation. They should be available but rarely be the primary name.

Good:

```
Acme API
Project ID: prj_7K9s2D [Copy]
```

```
Deployment #428
Deployment ID: dep_8f42... [Copy]
```

### Anti-pattern

Avoid:

- `Project prj_9xK2aQ` as the primary title.
- User-facing names that are only IDs.
- Showing external provider IDs in main UI.

Use an optional `Technical details` section for:

- External identity IDs.
- Raw response IDs.
- Provider metadata.
- Internal identifiers useful to support.


## Quick rewrite patterns

### Internal auth provider

Bad:

`You are signed in with google_auth.`

Better:

`Signed in with Google.`

### Raw exception

Bad:

`PrismaClientKnownRequestError: Unique constraint failed on fields: email`

Better:

`This email is already invited. Ask them to accept the existing invite, or revoke and resend it.`

### Permission

Bad:

`Permission denied: org.member.write`

Better:

`You need workspace admin access to invite members.`

### Token missing

Bad:

`not generated` with reveal/copy/reset controls.

Better:

`No token created yet.`

`Generate token`

### Delete account

Bad:

`Delete account [email input] [Delete account]`

Better:

`Start account deletion` → confirmation dialog with typed email, impact list, and re-auth if needed.

### Cost-risk preference

Bad:

`Allow models with no posted price`

Better:

`Allow unpriced models. Requests to models without a listed price will still run and will be billed at the provider’s current rate. This may increase costs unexpectedly.`

### Empty state

Bad:

`No data.`

Better:

`No logs yet. Logs will appear here after this project receives requests.`

### Header

Bad:

`Settings — Manage settings.`

Better:

`Production environment variables — Used by new deployments in Acme API.`
