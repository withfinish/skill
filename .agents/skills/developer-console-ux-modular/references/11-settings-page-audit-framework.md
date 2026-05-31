# Settings page audit framework

Use this guide when auditing a user settings/account page, especially one showing profile, security, preferences, notifications, privacy, and danger zone.

## What a mature user settings page should contain

Recommended structure:

```text
Account
Security
Billing and usage
Preferences
Notifications
Privacy
Danger zone
```

Each section should have a clear concept and risk level.

## Account section

Should show:

- Name
- Email
- Avatar
- Sign-in method
- Role, if relevant
- Account ID, if useful and copyable
- Manage profile/sign-in action

Should not show by default:

- Internal auth provider ID
- `Clerk user`
- Raw external identity ID
- `clerk_session`
- `default`
- `root` as an unexplained chip
- Balance/spend/requests mixed with identity

### Anti-pattern

```text
Tethys Plex
tethysplex@gmail.com
[clerk_session] [default] [root]

Username: tethysplex@gmail.com
User ID: usr_UVVjnCGGbYmm
Clerk user: user_3E7JBM3gRaH...
Organization:
Balance: $0.0000
Lifetime spend: $0.0000
Requests: 0
```

### Better

```text
Account
Tethys Plex
tethysplex@gmail.com

Sign-in method: Email
Role: Account owner
Account ID: `usr_UVVjnCGGbYmm` [Copy]

[Manage profile]
```

Move balance/spend/requests to Billing and usage.
Move external identity ID to collapsed Technical details if needed.

## Security section

Should include:

- Sign-in method
- Application token or API tokens
- Sessions
- 2FA/SSO if applicable
- Security-sensitive actions

### Token anti-pattern

```text
Application access token
Used by the system to access this account programmatically.
not generated     [eye] [copy] [Reset token]
```

### Better when no token exists

```text
Application access token
Use this token to authenticate API requests from your scripts or services.

No token created yet.
[Generate token]
```

### Better when token exists

```text
Application access token
Use this token to authenticate API requests from your scripts or services.

`tok_••••••••••••a93f`
Last used 2 hours ago
Created Jan 12 by Tethys Plex

[Copy token] [Rotate token] [Revoke token]
```

## Sign-in method

### Anti-pattern

```text
clerk_session
Identity managed by Clerk · tethysplex@gmail.com
verified
[Manage account]
```

### Better

```text
Email sign-in
tethysplex@gmail.com
Verified
[Manage sign-in]
```

or:

```text
Google sign-in
tethysplex@gmail.com
Verified
[Manage connected account]
```

## Preferences section

Preferences are low-risk personalization.

Good:

```text
Language
Used for the console interface and account emails.
[English] [简体中文] [繁體中文] [Français] [日本語]
```

Make selected state clear. Explain whether the setting auto-saves or requires `Save changes`.

Do not place cost-risk settings here.

## Cost-risk setting example

### Anti-pattern

```text
Preferences
Allow models with no posted price
Calls to models that don't have a configured price will succeed at the upstream's rate.
```

### Better

```text
Billing and usage / Cost controls
Allow unpriced models
Requests to models without a listed price will still run and will be billed at the provider’s current rate.
This may increase costs unexpectedly.

[Change setting]
```

## Notifications section

Should specify channel and condition.

### Anti-pattern

```text
Quota warnings
Email and dashboard alert when wallet balance drops below this threshold.
$0
```

### Better

```text
Low-balance warning
Email me when my balance drops below:
$10.00
Set to $0 to turn off low-balance warnings.
```

### Digest copy

```text
Provider update digest
Receive email updates when providers add models or change pricing.
```

Do not style a normal digest subscription as warning/danger.

## Privacy section

Should explain what is recorded and what is unaffected.

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

### Assurance note

```text
Your data is not used to train models
Flint does not train models on your prompts or completions. Read the privacy policy.
```

Keep assurances visually distinct from editable settings.

## Save preferences

Audit questions:

- Which sections does `Save preferences` save?
- Which fields auto-save?
- Is dirty state visible?
- Is there a section-level or page-level save model?
- Are high-risk settings confirmed separately?
- Can the user leave with unsaved changes accidentally?

### Better approaches

1. Immediate save for lightweight preferences, with `Saved` feedback.
2. Section-level `Save changes` for grouped settings.
3. Confirmation flow for security, cost, privacy, or destructive changes.

Do not mix all three without visible rules.

## Danger zone section

### Anti-pattern

```text
Delete account
Permanently delete your Flint account, all keys, and usage history. This cannot be undone. Active subscriptions are cancelled. Clerk identity is not affected.
[tethysplex@gmail.com] [Delete account]
```

Problems:

- Inline deletion is too casual.
- Confirmation input may be prefilled.
- Internal provider leakage.
- Impact list is incomplete.
- No re-auth mention.
- No clear distinction between what is deleted and what is retained.

### Better

Default section:

```text
Delete account
Permanently delete your Flint account, application tokens, saved settings, and usage history. Active subscriptions will be cancelled.

[Start account deletion]
```

Confirmation:

```text
Delete your account?
This will permanently delete:
- Your Flint account
- Application access tokens
- Usage and error logs
- Notification and privacy preferences

This will cancel:
- Active subscriptions for this account

This will not delete:
- Invoices or records we must keep for legal or tax reasons
- Your external sign-in provider account

Type `tethysplex@gmail.com` to confirm.

[Cancel] [Delete account]
```

For high-risk deletion, require re-auth.

## Visual and hierarchy concerns in settings pages

Watch for:

- Giant cards holding unrelated fields.
- Empty rows such as Organization with no value or action.
- Chips used for role/provider/default state.
- Warning-tinted backgrounds on ordinary preferences.
- Buttons like `Manage account` that do not reveal destination.
- Mono text applied to non-code values.
- Too much vertical space but not enough conceptual clarity.

## Priority fixes for a settings page like the example

1. Remove internal provider/framework terms from user-visible UI.
2. Split identity, security, billing/usage, preferences, privacy, and danger zone.
3. Move balance/spend/requests out of Profile.
4. Replace `clerk_session`, `default`, `root` chips with clear labeled fields.
5. Replace token `not generated` row with proper empty state and `Generate token`.
6. Move unpriced-model setting to Cost controls.
7. Make save behavior explicit.
8. Replace inline account deletion with `Start account deletion` and a confirmation flow.
9. Use color only for true state/risk semantics.
10. Add copy buttons only to values that users actually need to paste elsewhere.

## Settings audit checklist

- Is each setting in the right conceptual section?
- Does each section have one clear purpose?
- Are implementation details hidden by default?
- Are IDs copyable but secondary?
- Are sensitive values hidden?
- Is save behavior predictable?
- Are risky settings confirmed?
- Are dangerous actions isolated?
- Are empty values omitted or explained?
- Is copy specific about impact and scope?
- Are colors semantically meaningful?
