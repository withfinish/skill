# Dialogs, Sheets, Drawers, Flyouts, and overlay selection

## Overlay selection

Use this mental model:

```text
Dialog = focused decision or short action
Sheet = contextual inspection or light manipulation of a selected object
Page = complex configuration or full workflow
```

This is not absolute, but it prevents most mistakes.

## Dialogs

Dialog is useful. The problem is using a Dialog as a small page.

Dialog is good for:

- Create API key
- Invite member
- Confirm delete
- Rename project
- Rotate key confirmation
- Enter confirmation text
- Generate one-time token
- Choose template
- Confirm environment switch
- Short field edit

Dialog should have:

- One purpose
- Clear title
- 1–3 inputs when possible
- One primary action
- Direct copy
- Clear success/failure state

## Dialog examples

### Create key

```text
Create API key
Create a key for server-side requests. You’ll only be able to copy the full key once.

Name
Environment

[Cancel] [Create key]
```

### Rotate key

```text
Rotate production API key?
Apps using the current key will continue working until you revoke it. A new key will be shown once.

[Cancel] [Create new key]
```

### Invite member

```text
Invite member
Invite someone to this workspace. They’ll receive an email and join with the role you choose.

Email
Role

[Cancel] [Send invite]
```

## Dialog anti-patterns

- Long form with many sections.
- Advanced settings inside dialog.
- Nested tables.
- Multiple tabs.
- Long legal or security text with small scroll area.
- User must refer to page behind dialog.
- Dialog title says `Are you sure?` or `Configure settings`.
- Buttons say `OK`, `Submit`, or `Confirm` without object/action.

## Dialog title and button copy

### Anti-pattern

```text
Are you sure?
[Cancel] [Confirm]
```

### Better

```text
Revoke production key?
Apps using this key will fail immediately. Other keys are not affected.

[Cancel] [Revoke key]
```

## Dialog scrolling

Dialog scrolling is a warning sign. If unavoidable:

- Keep header stable.
- Keep footer actions stable.
- Do not enable primary action before critical content is visible if critical content must be read.
- Ensure errors are visible or focusable.
- Keep content length reasonable.

Often, a scrolling dialog should become a page or step flow.

## Sheet / side panel / flyout

A Sheet is for maintaining context while inspecting or lightly editing a selected object.

Good Sheet uses:

- Log detail
- Webhook delivery detail
- Deployment summary
- Request/trace detail
- API key metadata
- Member detail
- Audit log event
- Invoice detail
- Usage breakdown
- Environment variable history

The list remains behind the Sheet, preserving position.

## Sheet example: webhook delivery

Main list:

```text
Event | Status | Endpoint | Time
```

Sheet:

```text
Webhook delivery failed
Endpoint returned `401 Unauthorized`.
Last attempt: 14:03 UTC
Request ID: `req_...` [Copy]

Response
Headers
Payload
Retry history

[Retry delivery] [Open full event]
```

## Sheet is not a side-page

Sheet is poor for:

- Full SSO/SAML configuration
- Complete billing setup
- Complex permission matrix
- Full project settings
- Long environment variable editor
- Large code diff
- Wide comparison table
- Multi-step onboarding

Use a page or wizard.

## Sheet actions

Sheet actions should be few and contextual.

Good:

```text
Copy request ID
Copy payload
Retry delivery
Open full logs
View deployment
Edit details
Open full page
```

Bad:

```text
Edit
Duplicate
Delete
Archive
Move
Export
Share
Change owner
Change environment
Change region
Configure access
More
```

If a Sheet needs many actions, the object likely needs a full detail page.

## Sheet forms

Sheets can handle light edits:

- Display name
- Description
- Role
- Webhook URL
- Small metadata fields

Avoid:

- Multiple sections
- Advanced settings
- Long validation flows
- Complex dependent fields
- Nested tabs
- Wide tables

## Sheet headers

Sheet title should name the object and state.

### Anti-pattern

```text
Details
```

### Better

```text
Webhook delivery failed
Production API key
Deployment #428
Audit event: key rotated
```

## Sheet width

- Narrow Sheet: metadata, light edit.
- Medium Sheet: event/log/request detail.
- Wide Sheet: traces, payloads, code, but use cautiously.

If it needs more than about half the screen, consider a full page.

## Sheet and danger actions

A dangerous action may start from a Sheet, but final confirmation should use a Dialog or dedicated confirmation state.

### Anti-pattern

```text
API key detail Sheet
Revoke key [input] [Revoke]
```

### Better

Sheet:

```text
[Revoke key]
```

Dialog:

```text
Revoke production key?
Apps using this key will fail immediately. Other keys are not affected.

[Cancel] [Revoke key]
```

## Overlay stacking

Avoid complex stacks:

```text
Sheet → Sheet → Dialog → Nested popover
```

Better:

- Sheet for detail.
- Dialog for confirmation.
- Page for complex workflows.

## Overlay anti-pattern checklist

- Dialog contains a full page.
- Dialog contains long form or advanced settings.
- Sheet title says `Details`.
- Sheet has too many actions.
- Sheet contains multiple tabs that feel like full navigation.
- Sheet closes with unsaved changes and no warning.
- Dangerous operation completes inside a casual Sheet.
- Dialog button says `Confirm` instead of a specific action.
- User must scroll a lot inside overlay.
- Overlay hides context the user needs to complete the task.
