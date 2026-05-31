# Developer console UX review checklists

Use these as compact audit checklists.

## Global trust checklist

- Current workspace/project/environment is visible.
- Titles name user-facing objects.
- Implementation codenames are hidden.
- Technical details are useful and copyable.
- State is specific and timestamped where relevant.
- Errors are diagnostic.
- Dangerous actions are deliberate.
- Save behavior is predictable.
- URLs reflect important state.
- Accessibility and keyboard behavior are reliable.

## Copy checklist

- Does the copy say what happened?
- Does it say what object/scope is affected?
- Does it say what the user can do next?
- Does it reduce anxiety where risk exists?
- Does it avoid internal names?
- Does it avoid vague `Manage`, `Submit`, `Confirm`?
- Does it avoid raw backend errors?
- Does it avoid unnecessary `·` chains?

## Navigation checklist

- Sidebar is for places, not filters.
- Navbar is for context and global tools, not duplicate nav.
- Settings is not a landfill.
- User menu contains personal account items only.
- Workspace/project/environment switchers are discoverable.
- Breadcrumbs and page titles work together.
- Nested navigation reflects real product boundaries.
- Command palette accelerates rather than replaces IA.

## Header checklist

- Specific title.
- Clear scope.
- Short useful description.
- One dominant page-level action.
- Key status visible.
- Metadata clarifies, not decorates.
- Destructive action is not beside routine actions.
- Read-only/permission state is visible.

## Settings checklist

- Identity, security, billing/usage, preferences, notifications, privacy, danger zone are separated.
- Profile does not show provider IDs or internal user records.
- IDs are secondary and copyable.
- Tokens have proper empty/created states.
- Preferences are not mixed with cost/security risks.
- Save model is explicit.
- Danger zone starts a confirmation flow.
- Confirmation input is not prefilled.

## Security checklist

- Secrets hidden by default.
- Token actions are precise: generate, copy, rotate, revoke.
- Sign-in method is user-facing.
- Permission errors explain role/action.
- Re-auth copy is security-oriented, not error-like.
- Audit trail exists for sensitive changes.
- Destructive consequences are listed.

## Dialog checklist

- One purpose.
- Clear title.
- 1–3 inputs when possible.
- One primary action.
- No long form or advanced settings.
- Button text names the action/object.
- Errors are close to fields.
- Focus and keyboard behavior are correct.

## Sheet checklist

- Used for contextual inspection or light edit.
- Header names selected object and state.
- Main page context remains useful.
- Actions are few and object-specific.
- Raw JSON/logs are summarized first.
- Complex configuration has `Open full page`.
- Dangerous final confirmation uses Dialog or dedicated state.

## Table/list checklist

- Table is used only when comparison matters.
- Columns are task-focused.
- Row actions are minimal.
- Details live in Sheet/page.
- Filters are visible and clearable.
- Search placeholder names searchable fields.
- Empty state distinguishes no data from no results.
- Pagination/URL preserves state.

## Operational checklist

- Async work has clear states.
- Logs have structured fields and copyable request IDs.
- Webhook detail includes response, payload, retry history.
- Deployment detail includes build steps and rollback context.
- Audit log is precise and exportable if needed.
- Notifications are operational, not marketing.
- System status is discoverable.

## Billing/usage checklist

- Current plan visible.
- Usage period visible.
- Data freshness visible.
- Limits visible before failure.
- Exceeding-limit behavior explained.
- Cost-risk controls separated from preferences.
- Payment failure explains deadline and impact.
- Invoices are clear and downloadable.

## Red-flag phrase list

Call out these when seen in user-facing console UI:

```text
clerk_session
google_auth
Clerk user
tenant_id
auth_subject
principal_id
feature_flag
strategy_google_oauth2
rbac_policy_denied
sync_workspace_entitlements
created_at
updated_by_user_id
Something went wrong
Are you sure?
Submit
Confirm
Manage
Resources
Entities
General
Details
```

These are not always forbidden, but they need strong justification or relocation to technical details.
