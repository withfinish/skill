# Risk, danger zones, security, credentials, and secrets

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
