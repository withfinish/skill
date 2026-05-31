---
name: developer-console-ux
description: Review, design, and rewrite developer-first dashboard, console, settings, navigation, copy, forms, dialogs, sheets, tables, tokens, security, privacy, billing, logs, and danger-zone UX. Use for audits, redesigns, product copy, patterns, anti-patterns, and UI guidance for trustworthy developer tools.
metadata:
  version: "1.0"
  domain: "product-design, developer-experience, ux-writing"
---

# Developer Console UX Skill

Use this skill when the user asks for help designing, auditing, rewriting, or improving developer-first dashboards, admin consoles, control panels, settings pages, account/security pages, billing/usage pages, API key pages, logs, webhooks, deployment pages, navigation, dialogs, sheets, tables, forms, copy, or danger-zone flows.

Do not use this skill for purely decorative visual-style naming or moodboard work. This skill is about product structure, interaction design, developer experience, operational clarity, user-facing copy, and trustworthy console behavior.

## Core philosophy

A trustworthy developer console should feel like a reliable instrument panel, not a marketing website and not an internal admin database.

It should:

- Expose structure, state, scope, control, and diagnostic evidence.
- Hide internal implementation details, codenames, provider IDs, database fields, feature flags, and framework artifacts.
- Make routine work fast and risky work deliberate.
- Reduce ambiguity, not necessarily complexity.
- Let developers act, verify, debug, secure, and automate.
- Avoid visual and copy noise: excessive chips, dotted metadata strings, CRUD tables, row action forests, generic labels, and vague errors.

A useful summary:

> Developer-first does not mean implementation-first. Show technical details when they help users act, verify, debug, secure, or automate. Hide details that merely reveal how the product is built.

## How to approach a review

When reviewing a console screen, first identify the user scope and task:

1. What object is the user viewing or changing?
2. What scope does the action affect: account, workspace, project, environment, region, branch, token, provider, deployment, request, or billing period?
3. Is this page for setup, operation, debugging, security, billing, or preferences?
4. What is the one primary action, if any?
5. What information must be immediately visible for trust?
6. Which details should be folded into technical details, logs, audit entries, or support-only views?
7. Is the save model clear: instant save, section save, page save, or confirmation flow?
8. Are risky operations separated from routine operations?

Then provide:

- A short diagnosis.
- Specific issues.
- Recommended structure.
- Copy rewrites.
- Patterns and anti-patterns.
- Priority fixes.

## Overall product tone

### Pattern

The product should feel calm, precise, and useful.

Good console copy:

- Names the object.
- Explains the scope.
- States the status.
- Gives the next action.
- Reduces anxiety by saying whether anything changed, whether production is affected, and what remains safe.

Examples:

- `Production variables saved. New deployments will use these values.`
- `Webhook delivery failed because your endpoint returned 401 Unauthorized.`
- `We couldn’t rotate this key. No changes were made.`
- `This action is recorded in the audit log.`
- `Apps using this key will fail immediately. Other keys are not affected.`

### Anti-pattern

Do not make the product sound like an internal system, a database, or a marketing page.

Avoid:

- `Something went wrong.`
- `PrismaClientKnownRequestError`
- `Mutation completed.`
- `You are signed in with google_auth.`
- `Manage resource.`
- `Ship faster with our next-generation platform.`
- `Oopsie! The deployment goblin failed again.`

Better:

- `Signed in with Google.`
- `This email is already invited.`
- `Deployment failed. The build command exited with code 1.`
- `Create a key to authenticate requests from your backend.`

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

## Visual and information-density principles

### Pattern

A developer console should have enough density to be useful, but enough structure to be readable.

Use:

- Clear section boundaries.
- Stable spacing.
- Low-noise metadata.
- Limited status badges.
- Copyable identifiers where useful.
- Progressive disclosure for technical details.

### Anti-pattern

Avoid:

- Every field inside a card.
- Every metadata item as a chip.
- Every resource page as a table.
- Every action as a row button.
- Every status in bright colors.
- Every setting as `label + input + save`.
- Huge marketing-style hero headers in console pages.

## Chips, badges, and status labels

### Pattern

Use badges for states that are quick to recognize and operationally meaningful.

Good badges:

- `Live`
- `Failed`
- `Building`
- `Paused`
- `Preview`
- `Production`
- `Read-only`
- `Beta`
- `Verified`

### Anti-pattern

Do not chip ordinary metadata.

Bad chips:

- `created 2m ago`
- `kai@example.com`
- `main`
- `us-east-1`
- `12 requests`
- `project id`
- `default`
- `root`
- `clerk_session`

Better:

```
Role: Owner
Sign-in: Google
Branch: main
Region: US East
Updated 2 minutes ago
```

Limit cards and list rows to one primary status badge and, if necessary, one scope badge.

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

## Copy and copy buttons

### Pattern

Copy affordances are a developer-first signal. Provide them for values that users paste elsewhere.

Good copy targets:

- API key
- Project ID
- Request ID
- Webhook secret
- Endpoint URL
- Environment variable name
- CLI command
- curl example
- Error code
- Deployment URL
- Docker command
- Git remote
- Log line
- JSON payload

### Rules

- Tooltip should be specific: `Copy project ID`, not just `Copy`.
- Feedback should be specific: `Copied request ID`, not just `Copied` when multiple things can be copied.
- If UI truncates a value, copy the full value.
- Sensitive values should be masked by default.
- Copying a secret should be intentional and logged when appropriate.
- Provide copy for grouped config when it fits the workflow.

Good grouped copy:

```bash
PROJECT_ID=prj_...
API_URL=https://api.example.com
ENVIRONMENT=production
```

### Anti-pattern

Avoid:

- Copy buttons everywhere without clear targets.
- Copy feedback missing.
- Copying truncated text.
- Copying labels or extra whitespace.
- Copy icons that are too small or inaccessible.
- Copying hidden sensitive values without user awareness.

## Keyboard shortcuts and kbd hints

### Pattern

Keyboard shortcuts are a promise. Use them for high-frequency actions and make them actually work.

Good examples:

- `⌘K` / `Ctrl K`: command palette
- `/`: search
- `?`: shortcuts help
- `Esc`: close dialog or sheet
- `⌘S`: save changes
- `⌘↵`: deploy or submit when appropriate
- `G P`: go to projects
- `G L`: go to logs

### Rules

- Show OS-appropriate shortcuts: `⌘` on macOS, `Ctrl` on Windows/Linux.
- Do not trigger global shortcuts while the user is typing.
- Provide keyboard focus states.
- Shortcuts should be discoverable in a help panel.
- Dangerous operations should not execute directly from a shortcut; they must still confirm.

### Anti-pattern

Avoid:

- Displaying shortcuts that do not work.
- `Esc` not closing a modal.
- `Enter` behavior changing unpredictably between forms.
- Shortcuts conflicting with browser defaults.
- Kbd hints used as decoration.

## Command palette

### Pattern

Command palettes are excellent for developer consoles because they match IDE, terminal, launcher, and CLI workflows.

Use command palettes for:

- Page navigation.
- Project switching.
- Environment switching.
- Opening docs.
- Creating keys.
- Viewing logs.
- Inviting members.
- Copying IDs.
- Running common actions.

Group results:

- Pages
- Projects
- Actions
- Docs
- Recent logs

### Anti-pattern

Do not use command palette as a substitute for information architecture. New users still need visible navigation.

Do not allow destructive commands to execute immediately from search. Route them to confirmation flows.

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

## Code snippets

### Pattern

Code snippets should behave like executable workflow aids.

Good snippets:

- Include the right language.
- Are copyable in full.
- Use real account/project context when safe.
- Avoid fake placeholder values unless clearly marked.
- Explain where to run them and what happens next.

Example:

```bash
curl https://api.example.com/v1/events \
  -H "Authorization: Bearer $API_KEY"
```

Helper text:

`Run this from your backend or terminal. Logs will appear here after the first request.`

### Anti-pattern

Avoid decorative code blocks that do not help users complete the workflow.

## Navigation and information architecture

### Core principle

Navigation should expose the product model, not the internal implementation model.

A user should always know:

- Which workspace they are in.
- Which project they are in.
- Which environment is active.
- Which resource they are viewing.
- Which scope an action affects.

### Sidebar

Sidebars are for places, not filters and not temporary states.

Good sidebar labels:

- `Projects`
- `Deployments`
- `Logs`
- `API Keys`
- `Webhooks`
- `Usage`
- `Members`
- `Billing`
- `Settings`

Bad sidebar labels:

- `Resources`
- `Entities`
- `Management`
- `Core`
- `Platform`
- `V2`
- `Tenants`
- `Principals`
- `Entitlements`

### Settings is not a landfill

Do not hide core developer workflows in Settings.

API Keys, Webhooks, Logs, Usage, and Deployments often deserve first-class navigation.

### Multi-sidebar structure

Multiple sidebars are acceptable only when each has a clear scope.

Good:

- Global sidebar: workspace-level navigation.
- Project sidebar: project-level navigation.
- Main area: current page.

Bad:

- Two sidebars both containing Settings.
- Sidebar + sub-sidebar + tabs + sub-tabs + accordions for the same scope.
- A file-tree-like hierarchy for a product that is not a file tree.

### Navbar

Navbars should carry current context and global tools, not duplicate the sidebar.

Good navbar items:

- Workspace switcher.
- Project switcher.
- Environment switcher.
- Breadcrumb.
- Search / command palette.
- Docs / help.
- Notifications.
- User menu.

Bad navbar items:

- Duplicate `Projects`, `Logs`, `Settings` when the sidebar already has them.
- Constant marketing CTA.
- Business features hidden in the user avatar menu.

### Breadcrumbs

Use breadcrumbs for deep context:

`Acme API / Deployments / Deployment #428`

Do not use breadcrumbs as the only page title.

### Environment switchers

Environment scope must be obvious when mistakes are costly.

Bad:

- Small dropdown showing `prod` in the corner.

Better:

- Page title: `Production API keys`
- Button: `Create production key`
- Confirmation: `Revoke production key?`

### Filters are not navigation

Do not put `All`, `Failed`, `Successful`, `Production`, `Preview`, or `500` in global navigation unless they are real places. These are usually filters or page tabs.

### URL and shareability

Developer users copy URLs. URLs should preserve meaningful state.

Good:

- `/projects/acme-api/logs?level=error`
- `/projects/acme-api/deployments/428`

Bad:

- `/dashboard?id=123&type=deployment&tab=logs`

Support shareable links for logs, webhook deliveries, deployments, and filtered views when possible.

## Page headers

### Core principle

Headers orient before they command.

A good page header names the current object, clarifies scope and state, and exposes the next useful action without turning into a toolbar.

### Pattern

A strong header may include:

- Breadcrumb.
- Specific title.
- Short scope or purpose copy.
- Important status.
- 2-4 useful metadata fields.
- One primary action.
- At most one or two secondary actions.
- Overflow for low-frequency actions.

Example:

```
Acme API / Deployments

Deployment #428   Live
Production release from branch main.

Deployment ID: dep_8f42... [Copy]
Updated 42 seconds ago
Region: US East

[View logs] [Rollback]
```

### Anti-pattern

Avoid:

- Title: `Details`
- Subtitle: `Manage details.`
- Five header buttons.
- Destructive action beside routine action.
- Generic `Settings` title when the scope is `Production environment variables`.
- Marketing copy in console headers.

### Header title examples

Bad → better:

- `Overview` → `Acme API overview`
- `Settings` → `Project settings`
- `Details` → `Deployment #428`
- `Environment Variables` → `Production environment variables`
- `Manage` → `Webhook endpoints`

### Header copy examples

Bad:

`Manage API keys.`

Better:

`Create keys for server-side requests. Keep production keys separate from development.`

Bad:

`Ship faster with our next-generation deployment engine.`

Better:

`Track builds, releases, and rollbacks for this project.`

## Dialogs

### Core principle

Use dialogs for focused decisions and short actions, not for configuring complex systems.

Dialog = decision or short action.
Sheet = contextual inspection or light manipulation.
Page = system configuration or complex workflow.

### Good dialog uses

- Create API key.
- Invite member.
- Rename project.
- Confirm deletion.
- Rotate key confirmation.
- Choose a template.
- Enter confirmation text.
- Generate one-time token.
- Select an environment.

### Dialog form rule

One purpose, ideally 1-3 inputs, one primary action.

Good:

```
Invite member
Invite someone to this workspace. They’ll receive an email and join with the role you choose.

Email
Role

[Cancel] [Send invite]
```

Good:

```
Rotate production API key?
Apps using the current key will continue working until you revoke it. A new key will be shown once.

[Cancel] [Create new key]
```

### Anti-pattern

Do not put full system setup in a dialog:

- Complete billing setup.
- Complex webhook configuration.
- SSO/SAML setup.
- Multi-environment variable editing.
- Full deployment settings.
- Long project creation forms.
- Permission matrices.
- Nested tables.
- Multi-tab forms.

### Dialog copy

Bad:

- `Are you sure?`
- `Configure settings`
- `Create resource`
- `Submit`
- `Confirm`

Better:

- `Delete project?`
- `Create API key`
- `Invite member`
- `Rotate production key?`
- `Connect GitHub repository`
- `Delete project`

### Dialog errors

Errors should be close to the relevant field.

Bad:

`Something went wrong.`

Better:

`This member has already been invited.`

Global dialog error:

`We couldn’t send the invite. No changes were made. Request ID: req_...`

## Sheets / side panels / flyouts

### Core principle

A sheet is for contextual inspection and light manipulation of a selected object. It should preserve the user’s place in the main view, not replace a full page.

### Good sheet uses

- Log detail.
- Webhook delivery detail.
- Deployment summary.
- Request or trace detail.
- API key metadata.
- Member detail.
- Audit event detail.
- Invoice detail.
- Usage breakdown.
- Environment variable history.

### Good sheet structure

```
Webhook delivery failed
Endpoint returned 401 Unauthorized.

Event ID: evt_... [Copy]
Last attempt: Jan 12, 14:03 UTC
Endpoint: https://api.example.com/webhook

Sections:
Response
Headers
Payload
Retry history

[Retry delivery] [Open full event]
```

### Anti-pattern

Avoid:

- Sheet title: `Details`.
- Full Settings page inside a sheet.
- Long forms.
- Many actions.
- Multi-level nested sheets.
- Huge raw JSON as the first thing shown.
- Wide tables in sheets.
- Danger operations completed casually inside the sheet.

If a sheet needs more than 50-60% of the viewport or contains many sections, consider a full page.

### Sheet actions

Use 1-3 natural actions. Examples:

- `Copy request ID`
- `Retry delivery`
- `Open full logs`
- `Revoke key` with confirmation dialog

Danger actions may start from a sheet, but final confirmation should be a dialog or dedicated confirmation state.

## Forms and settings controls

### Core principle

Forms should explain consequences, not just collect values.

Good field copy:

```
Project name
Shown in the dashboard, logs, and audit events.
```

```
Region
Builds and runtime data are processed in this region. You can’t change this after creation.
```

Bad:

```
Name
Enter project name.
```

```
Region
Select a region.
```

### Save models

Choose one clear save model per section or page:

1. Instant save: low-risk preferences.
2. Section-level save: related settings.
3. Page-level save: larger forms with unsaved state.
4. Confirmation flow: risky, irreversible, production, billing, or security-sensitive changes.

Always show:

- `Saving...`
- `Saved`
- `Unsaved changes`
- `Changes apply to new deployments only`

### Anti-pattern

Avoid:

- Some controls autosave while others require save without clear indication.
- Toggles for high-risk actions.
- Disabled buttons without visible explanation.
- Inline input for high-risk confirmation.
- Generic `Save` always visible even when nothing changed.

## Toggles and checkboxes

### Pattern

Use toggles for low-risk settings that can be switched on/off and have immediate or clearly saved state.

Good:

- Email digest.
- Theme preference.
- Compact mode.
- Low-risk notification preference.

### Anti-pattern

Avoid toggles for high-risk changes:

- Public access.
- Disable SSO.
- Allow production writes.
- Reset database.
- Delete protection.
- Unpriced model usage if it can create cost risk.

For high-risk settings, use a button or setting flow with explanation and confirmation.

## Danger zone and destructive operations

### Core principle

Routine work should be fast. Risky work should be deliberate.

Do not make dangerous operations look efficient.

### Bad pattern

```
Danger zone
Delete account   [input: email] [Delete account]
```

Problems:

- Dangerous action appears like a normal form row.
- Not enough space to explain consequences.
- Input and button are too close.
- User may not understand scope.
- Confirmation input may be prefilled.
- No re-auth or identity verification.

### Better pattern

Default state:

```
Danger zone

Delete account
Permanently delete your account, application tokens, saved settings, and usage history. Active subscriptions will be cancelled.

[Start account deletion]
```

Confirmation dialog or page:

```
Delete your account?

This will permanently delete:
- Your account
- Application access tokens
- Usage and error logs
- Notification and privacy preferences

This will cancel:
- Active subscriptions for this account

This will not delete:
- Invoices or records we must keep for legal or tax reasons
- Your external sign-in provider account

Type tethysplex@gmail.com to confirm.

[Cancel] [Delete account]
```

### Rules

- Do not prefill confirmation inputs.
- Require users to type the object name, email, or project name for irreversible actions.
- Repeat the object and scope in the title and button.
- Separate destructive action from routine actions.
- Explain whether the action is recoverable.
- Explain what is and is not affected.
- Require re-auth for sensitive security/account actions.
- Use audit logs for destructive operations when possible.

### Button copy

Bad:

- `Delete`
- `Confirm`
- `Yes`

Better:

- `Delete project`
- `Delete account`
- `Revoke API key`
- `Reset database`
- `Disable SSO`
- `Transfer ownership`

### Confirm vs verify vs authorize

- Confirm: user understands consequences, e.g. typing project name.
- Verify: user proves identity, e.g. password, SSO, 2FA.
- Authorize: user has permission, e.g. owner role.

Use the right mechanism for the risk.

## Security and credentials

### Application access tokens / API keys

Pattern:

```
Application access token
Use this token to authenticate API requests from your scripts or services.

No token created yet.
[Generate token]
```

After creation:

```
tok_••••••••••••a93f
Created Jan 12 by Tethys Plex
Last used 2 hours ago

[Copy token] [Rotate token] [Revoke token]
```

Add:

`You’ll only be able to copy the full token once.`

### Anti-pattern

Avoid:

- Showing `not generated` as if it were a token value.
- Showing reveal/copy controls when no token exists.
- Using `Reset token` for a token that does not exist.
- Revealing secrets by default.
- Letting secrets remain visible forever after creation.

Prefer:

- `Generate token`
- `Rotate token`
- `Revoke token`

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

## Billing, usage, limits, and cost controls

### Pattern

Billing and usage pages must build trust.

Show:

- Current plan.
- Usage this billing period.
- Balance.
- Projected overage.
- Top projects or keys by usage.
- Plan limits.
- Reset date.
- Data freshness.
- Invoices.
- Payment method.

Limits should be visible before failure.

Good:

```
Requests this month: 80% of included usage
Resets on Jan 31
Current limit: 1,000 RPM
```

### Cost-risk settings

For settings like `Allow models with no posted price`, treat them as cost controls, not normal preferences.

Bad:

```
Preferences
[ ] Allow models with no posted price
Calls to models that don't have a configured price will succeed at the upstream's rate.
```

Better:

```
Cost controls

Allow unpriced models
Requests to models without a listed price will still run and will be billed at the provider’s current rate. This may increase costs unexpectedly.

[Change setting]
```

If enabling, show confirmation dialog.

## Notifications

### Pattern

Notifications in developer consoles should be operational.

Good notifications:

- Deployment failed.
- Usage nearing limit.
- Webhook delivery failing.
- Invoice payment failed.
- API key expires soon.
- SSO certificate expires soon.
- New security event.

Avoid polluting notifications with marketing updates, blog posts, or generic feature announcements.

### Notification settings

Bad:

`$0` input with unclear meaning.

Better:

```
Low-balance warning
Email me when my balance drops below:
$10.00

Set to $0 to turn off low-balance warnings.
```

Or:

```
Low-balance warning [On]
Threshold: $10.00
```

## Privacy settings

### Pattern

Privacy settings must explain what is collected, where it appears, and what remains true.

Bad:

`Record client IP in usage and error logs. Disable to keep IPs out of your own audit trail. Doesn't affect security blocks at the edge.`

Better:

```
Record client IP addresses in logs
When enabled, client IPs appear in usage and error logs. Security systems may still process IPs to prevent abuse.
```

Trust note:

```
Your data is not used to train models
Flint does not train models on your prompts or completions. Read the privacy policy.
```

### Anti-pattern

Avoid warning-colored backgrounds for ordinary privacy preferences unless there is a real warning.

## Settings pages

### Core principle

Settings pages should be organized by user concepts and risk level, not backend tables.

Recommended structure for user/account settings:

1. Account
2. Security
3. Billing and usage
4. Cost controls
5. Preferences
6. Notifications
7. Privacy
8. Danger zone

### Account / Profile

Good account section:

```
Profile
Tethys Plex
Email: tethysplex@gmail.com
Role: Account owner
Sign-in method: Google
Account ID: usr_UVVjnCGGbYmm [Copy]

[Manage profile]
```

Do not mix profile with billing metrics unless it is explicitly an account summary.

Anti-pattern:

- Username displays email while label says username.
- `Clerk user` appears in main profile.
- Empty `Organization` field is shown.
- Balance, lifetime spend, and requests are mixed into profile.
- Chips show `clerk_session`, `default`, `root`.

Better:

- Move balance/spend/requests to Billing or Usage.
- Hide or fold external identity IDs under `Technical details`.
- Convert `root` to `Owner` if it is a user-facing role.
- Remove `default` unless it has a clear user-facing meaning.

### Sign-in method

Bad:

```
clerk_session
Identity managed by Clerk · tethysplex@gmail.com
verified
[Manage account]
```

Better:

```
Sign-in method
Google
tethysplex@gmail.com
Verified

[Manage sign-in]
```

or:

```
Sign-in method
Email
tethysplex@gmail.com
Verified

[Manage sign-in settings]
```

### Language preferences

Pattern:

```
Language
Used for the console interface and account emails.

English  简体中文  繁體中文  Français  Русский  日本語  Tiếng Việt
```

Rules:

- Make selected state obvious.
- If saved instantly, show `Saved`.
- If not, show clear unsaved state and `Save changes`.
- If the list grows, use a searchable select.

### Save preferences

Do not place a global `Save preferences` button if users cannot tell which sections it applies to.

Better options:

- Instant save per row with feedback.
- Section-level `Save changes`.
- Sticky save bar when unsaved changes exist.

### Danger zone in settings

Do not inline input + delete. Use start flow + confirmation.

Bad:

```
Delete account [email input] [Delete account]
```

Better:

```
Delete account
Permanently delete your account, application tokens, saved settings, and usage history. Active subscriptions will be cancelled.

[Start account deletion]
```

Then dialog/page confirmation.

### Settings page anti-pattern checklist

Avoid:

- Internal provider names in user-facing sections.
- Unclear chips.
- Empty fields shown without action.
- Huge cards filled with mixed concepts.
- Security token controls that do not match state.
- Cost-risk settings inside ordinary preferences.
- Save model ambiguity.
- Danger actions inline.
- Warning colors for non-warning preferences.
- Generic button labels such as `Manage account`, `Reset token`, `Submit`.

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

## User menu

### Pattern

User menu should contain personal account actions.

Good:

- Profile
- Account settings
- Theme
- Keyboard shortcuts
- Sign out

### Anti-pattern

Do not hide workspace/project features in the user menu:

- Billing
- Members
- API keys
- Usage
- Project settings
- Integrations

## Notifications and system status

Expose platform status when relevant.

If an error may be platform-side, provide status link:

```
We’re investigating elevated errors in US East.
[View status]
```

Keep normal status page access low-noise in help menu.

Do not make users debug for an hour when the platform is degraded.

## Responsive and desktop split-screen behavior

Developer users often run the console beside an editor or terminal.

Design for narrow desktop widths:

- Tables convert to lists.
- Sidebar can collapse without losing scope.
- Header actions do not crush titles.
- Sheets remain usable.
- Code blocks scroll horizontally but copy full content.
- Filters collapse into a controlled panel.

Mobile support should prevent misoperation, especially for production and danger actions.

## Accessibility and focus

Reliable tools must be accessible.

Rules:

- Do not rely on color alone for status.
- Keep visible focus rings.
- Icon buttons need accessible names.
- Form errors must be associated with fields.
- Dialogs should focus the first useful element.
- Dangerous buttons should not receive default focus.
- Sheet closing returns focus to the trigger.
- Dynamic logs should not disrupt screen readers.
- Keyboard access must not be secondary.

## Color semantics

Use color consistently.

- Red: destructive or serious error.
- Yellow/amber: warning or attention.
- Green: healthy, live, successful.
- Blue: information or link/action.
- Gray: neutral, inactive, metadata.

Anti-pattern:

- Ordinary checkboxes on warning-tinted backgrounds.
- Feature announcement and warning both yellow.
- Every badge using brand color.
- Failed status visually indistinguishable from destructive button.

## Naming consistency

Use one name for one concept.

Avoid switching between:

- Project / App / Service / Resource.
- Rotate key / Regenerate key / Reset key / Refresh key.
- Live / Active / Ready / Running.
- Workspace / Organization / Team / Tenant.

Terminology drift makes the product feel unreliable.

## Changelog, API versioning, and deprecations

Developer products need traceable change.

Provide:

- Changelog.
- API version selector.
- Deprecation notices.
- Migration guides.
- Preview/Beta labels with behavior expectations.

Bad:

`feature_flag_agents_runtime_beta_v3`

Better:

`Agents runtime is in Preview. APIs and behavior may change.`

## Memory and user preference

A mature console can remember user workflow preferences:

- Recent projects.
- Recent environments.
- Last logs filter.
- Column preferences.
- Density setting.
- Command palette recent actions.

Be careful with environment memory. Do not silently reopen users in Production if that creates risk. Make scope visible.

## Final review checklist

Use this checklist when auditing a developer console screen.

### Scope and structure

- Is the current workspace/project/environment obvious?
- Is the page task clear: setup, operate, debug, secure, bill, or prefer?
- Does the page have one dominant action, if any?
- Are navigation, filters, tabs, and breadcrumbs serving distinct roles?
- Are URLs shareable and meaningful?

### Copy

- Are labels user-facing rather than internal?
- Are errors diagnostic and repairable?
- Are success messages scoped?
- Are high-risk actions clear about impact and recovery?
- Are vague labels like `Details`, `Manage`, `Submit`, and `Confirm` avoided?

### Developer workflow

- Are useful IDs copyable?
- Are code snippets executable and copyable?
- Are logs searchable and structured?
- Are request IDs, timestamps, regions, branches, commits, and versions shown where useful?
- Are shortcut hints functional?

### Risk and trust

- Are destructive actions isolated?
- Are secrets masked and only revealed intentionally?
- Are dangerous settings confirmed?
- Are permissions explained visibly?
- Are billing and quota impacts clear?
- Is data freshness visible?

### Visual and interaction noise

- Are chips limited to meaningful status?
- Are dotted metadata strings avoided when they flatten meaning?
- Are tables used only when appropriate?
- Are row actions minimized?
- Are card boundaries and section structure purposeful?
- Are dialogs short and sheets contextual?

### Settings-specific

- Are profile, security, billing, preferences, privacy, and danger separated?
- Are provider details like `Clerk` hidden unless user-relevant?
- Is the save model clear?
- Are high-cost or privacy-sensitive preferences treated with the right seriousness?
- Does Danger Zone start a flow instead of completing deletion inline?

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

