# Dialogs, sheets, forms, controls, and save models

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
