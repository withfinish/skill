# Actions, shortcuts, copy affordances, and keyboard behavior

## Primary actions

Primary actions should be contextual and sparse. A page should usually have one dominant primary action.

Good:

```text
Create project
Create key
Invite member
Add endpoint
Deploy
Save changes
```

Bad:

```text
Create
Submit
OK
Confirm
Manage
```

## Primary action with shortcut

Showing a shortcut can signal that the product is built for frequent operation.

Good examples:

```text
Deploy    ⌘↵
Save changes    ⌘S
Open command palette    ⌘K
Search logs    /
Close    Esc
```

But a shortcut display is a promise. It must work.

## `kbd` anti-patterns

- Showing Mac `⌘` to Windows/Linux users without adaptation.
- Shortcut appears but does not work.
- Shortcut triggers while user is typing in an input.
- Dangerous action can be completed only with a shortcut.
- No shortcut help or command palette list.
- Focus management is broken after shortcut-triggered dialogs.

## Command palette

A command palette should allow users to express intent directly.

Useful actions:

```text
Create project
Invite member
View logs
Rotate API key
Open billing
Search requests
Deploy latest commit
Switch environment
Go to production
Create webhook
Copy project ID
```

Do not execute destructive actions directly. Open their confirmation flows.

## Copy buttons

Developer consoles need copy affordances for values users paste elsewhere.

Good copy targets:

- API key
- Project ID
- Request ID
- Webhook secret
- Environment variable name
- Endpoint URL
- CLI command
- curl example
- Error code
- Deployment URL
- Log line
- JSON payload
- Docker command
- Git remote
- SDK install command

Do not put copy buttons on everything. Copy affordance should reflect a workflow.

## Copy workflow design

Ask:

- What will the user paste this into?
- Is the displayed value truncated?
- Should copy include formatting?
- Is the value sensitive?
- Should multiple values be copied together?
- Does the user need feedback?

### Anti-pattern

A truncated value displays:

```text
project_abc...xyz [Copy]
```

and copy returns the truncated text.

### Better

Display truncated value, copy full value, and show feedback:

```text
Project ID: `project_abc...xyz` [Copy project ID]
Copied project ID
```

## Copy full config instead of many copy icons

### Anti-pattern

A page has copy icons for project ID, API URL, environment, and region.

### Better

Provide one copyable block when the workflow needs multiple values:

```bash
PROJECT_ID=prj_abc123
API_URL=https://api.example.com
ENVIRONMENT=production
```

Button:

```text
Copy config
```

## Copy tooltip/button text

Be specific.

### Weak

```text
Copy
Copied
```

### Better

```text
Copy project ID
Copy endpoint URL
Copy install command
Copied API key
Copied request ID
```

## Copy and sensitive values

Secrets should be masked by default:

```text
sk_live_••••••••••••a93f
```

Actions:

```text
Reveal
Copy
Rotate
Revoke
```

If a secret is only shown once, say so clearly:

```text
Copy this token now. You won’t be able to see it again.
```

## Action placement

Place actions by scope:

| Action scope | Placement |
|---|---|
| Page-level primary | Page header |
| Section-level action | Section header or footer |
| Object action | Detail page or Sheet |
| Copy action | Next to value |
| Bulk action | List toolbar after selection |
| Dangerous action | Danger zone or confirmation flow |
| Cross-page action | Command palette |

## Avoid action forests

### Anti-pattern

Every table row has:

```text
View  Edit  Duplicate  Delete  More
```

### Better

- Row click opens details.
- Sheet/detail page contains object-specific actions.
- Row only keeps one low-risk action if needed, such as `Copy ID` or `Open`.
- Bulk actions appear after selection.

## Dangerous actions are not routine actions

Do not put destructive actions beside normal actions.

### Anti-pattern

```text
[Save changes] [Delete account]
```

### Better

`Save changes` in the settings section.

`Delete account` in Danger zone, starting a separate confirmation flow.

## Disabled actions

Disabled states must not be the only explanation.

### Anti-pattern

Disabled `Delete workspace` button with tooltip:

```text
You must remove all projects first.
```

### Better

```text
Delete this workspace after removing its 3 active projects.
[View projects]
```

## Focus and keyboard behavior

A developer-first console should be usable by keyboard.

Guidelines:

- Dialog opens with focus on the first reasonable control, not destructive action.
- Esc closes non-dangerous dialogs and sheets.
- Closing a Sheet returns focus to the triggering row/item.
- Tab order follows visual order.
- Copy buttons are keyboard focusable.
- Form errors move focus to the first invalid field.
- Command palette shortcuts do not trigger inside text inputs.
- Shortcut help is available, commonly via `?` or command palette.

## Toasts

Toasts are good for simple feedback:

```text
Copied project ID
Invite sent
Changes saved
```

Toasts are poor for:

- Complex errors
- Destructive result explanations
- Recovery paths
- Multi-step outcomes
- Important warnings

Those belong in the page or dialog content.

## Action anti-pattern checklist

- Multiple primary buttons on one surface.
- Generic button text like `Submit` or `Confirm`.
- Destructive action in ordinary toolbar.
- Shortcut shown but not implemented.
- Copy buttons with vague tooltips.
- Copy returns truncated text.
- Sensitive values are visible by default.
- Disabled actions have no visible explanation.
- Toast is the only place important information appears.
