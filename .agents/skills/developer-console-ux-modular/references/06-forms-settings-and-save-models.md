# Forms, settings pages, save models, toggles, and inline inputs

## Settings pages are control panels, not miscellaneous forms

A Settings page should organize how an account, workspace, or project is identified, protected, billed, personalized, and deleted.

It should not be a collection of database fields or unresolved product features.

## Settings IA

For user/account settings, use sections like:

```text
Account
Security
Billing and usage
Preferences
Notifications
Privacy
Danger zone
```

For project settings, use:

```text
Project identity
Build settings
Production environment
Access
Integrations
Danger zone
```

For workspace settings, use:

```text
Workspace profile
Members and roles
Billing
Security
Audit log
Danger zone
```

## Field rows over raw forms

Settings should often be field rows, not a form with inputs always visible.

### Anti-pattern

```text
Name [input]
Slug [input]
Region [select]
Save
```

### Better

```text
Project name
Shown in the dashboard, logs, and audit events.
Acme API
[Edit]
```

```text
Region
Builds and runtime data are processed in this region. This cannot be changed after creation.
US East
```

## Form copy explains impact

### Anti-pattern

```text
Region
Select a region.
```

### Better

```text
Region
Choose where builds and runtime data are processed. You can’t change this after creation.
```

### Anti-pattern

```text
Project name
Enter project name.
```

### Better

```text
Project name
Shown in the dashboard, logs, and audit events.
```

## Save models

Settings pages need a clear save model.

### Immediate save

Good for:

- Theme
- Language
- Notification subscription
- Minor preferences

Show:

```text
Saving...
Saved
```

### Section-level save

Good for related fields in one section.

Show:

```text
Unsaved changes
[Save changes]
[Discard]
```

### Page-level save

Use sparingly for complex forms. Make dirty state obvious.

### Confirmation flow

Use for:

- Cost-risk settings
- Production-impact changes
- Security-sensitive changes
- Destructive actions

## Save model anti-pattern

A page where:

- Language changes immediately.
- Privacy checkbox requires `Save preferences`.
- Token reset happens immediately.
- Danger zone uses inline input.

This makes users guess what is saved.

## Inline inputs

Inline inputs are good for low-risk, local, reversible edits:

- Display name
- Description
- Label
- Notes
- Search/filter
- Low-risk preference

Do not use inline inputs for actions requiring understanding, confirmation, or risk acceptance.

### Dangerous anti-pattern

```text
Delete account    [email input] [Delete account]
```

### Better

```text
Delete account
Permanently delete your account and associated data.
[Start account deletion]
```

Then open a proper confirmation flow.

## Toggles

Toggles imply immediate, reversible, lightweight change. Do not use them casually for high-risk settings.

Poor toggle candidates:

- Disable SSO
- Public access
- Allow production writes
- Reset database
- Delete protection
- Billing-impact settings

Better pattern:

```text
Public API access
Allow unauthenticated requests to this endpoint.
[Change access]
```

Then show a confirmation or settings flow.

## Checkboxes

Checkboxes are fine for preferences, but not enough for high-risk understanding.

### Weak

```text
[ ] I understand this action cannot be undone.
```

### Better

List concrete consequences, then require typed confirmation when appropriate.

## Preferences

Preferences should be low-risk personalization:

- Language
- Theme
- Email digest preference
- Display density
- Notification format

Do not mix cost-risk, security-risk, or production-risk settings into Preferences.

### Example: language

Good:

```text
Language
Used for the console interface and account emails.
[English] [简体中文] [繁體中文] [Français] ...
```

Make selected state obvious. If selection requires saving, show unsaved state. If immediate, show saved feedback.

## Cost-risk settings do not belong in generic preferences

### Anti-pattern

```text
Preferences
[ ] Allow models with no posted price
Calls to models that don't have a configured price will succeed at the upstream's rate.
```

### Better

```text
Cost controls
Allow unpriced models
Requests to models without a listed price will still run and will be billed at the provider’s current rate.
This may increase costs unexpectedly.
[Change setting]
```

If enabling the setting is risky, use Dialog confirmation.

## Notifications

Notification settings should specify channel, threshold, and scope.

### Anti-pattern

```text
Quota warnings
$ 0
```

### Better

```text
Low-balance warning
Email me when my balance drops below:
$10.00
Set to $0 to turn off low-balance warnings.
```

or:

```text
Low-balance warning    On
Threshold: $10.00
```

## Privacy settings

Privacy settings need impact copy.

### Anti-pattern

```text
Record client IP in usage and error logs
Disable to keep IPs out of your own audit trail. Doesn't affect security blocks at the edge.
```

### Better

```text
Record client IP addresses in logs
When enabled, client IPs appear in usage and error logs. Security systems may still process IPs to prevent abuse.
```

## Assurance notes

Privacy/security assurances are useful but should be visually distinct from editable settings.

Good:

```text
Your data is not used to train models
Flint does not train models on your prompts or completions. Read the privacy policy.
```

Do not style ordinary preferences as warnings unless they are warnings.

## Forms should not be too long inside overlays

If a form has many fields, multiple sections, advanced settings, dependent fields, or requires reference to context, use a page or step flow, not a Dialog or small Sheet.

## Form anti-pattern checklist

- Internal database fields as labels.
- Always-visible inputs for values that rarely change.
- High-risk actions as inline controls.
- Mixed save behavior.
- Disabled buttons without visible explanation.
- Generic `Save` button with unclear scope.
- Toggles for irreversible or high-risk settings.
- Long forms in Dialogs or Sheets.
- Confirmation input prefilled.
- Helper text repeats label instead of explaining impact.
