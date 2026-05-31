# Security, privacy, tokens, permissions, and danger zone

## Security surfaces should feel deliberate

Security pages must be clear, calm, and specific. Avoid raw auth/provider terms unless the user is configuring that provider.

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

Do not expose `Clerk`, `clerk_session`, or provider IDs in normal account settings.

## Tokens and secrets

Use precise actions:

- Generate token
- Copy token
- Rotate token
- Revoke token

Avoid vague `Reset token` unless it is truly a reset.

## Token not created state

### Anti-pattern

```text
Application access token
not generated      [Reveal] [Copy] [Reset token]
```

### Better

```text
Application access token
Use this token to authenticate API requests from your scripts or services.

No token created yet.
[Generate token]
```

## Token created state

```text
Application access token
Use this token to authenticate API requests from your scripts or services.

`tok_••••••••••••a93f`
Last used 2 hours ago
Created Jan 12 by Tethys Plex

[Copy token] [Rotate token] [Revoke token]
```

If full token is only visible once:

```text
Copy this token now. You won’t be able to see it again.
```

## Secrets should default to hidden

Do not show full API keys, webhook secrets, private keys, or tokens by default.

Show:

```text
sk_live_••••••••••••a93f
```

Offer:

```text
Reveal
Copy
Rotate
Revoke
Last used
Created by
Expires
```

## Permissions and roles

Do not only show role names. Explain capabilities.

### Anti-pattern

```text
Role: Admin
```

### Better

```text
Admin
Can manage projects, invite members, and rotate API keys. Cannot change the billing owner.
```

## Permission errors

### Anti-pattern

```text
You do not have permission: org.member.write
```

### Better

```text
You need workspace admin access to invite members.
Ask a workspace owner to change your role.
```

## Re-authentication

Re-auth is not an error; it is a safety step.

Good copy:

```text
Confirm it’s you
For security, sign in again before changing security settings.
```

```text
For security, sign in again before deleting this account.
```

## Sessions

Session management should show:

- Device/location summary
- Last active time
- Current session
- Revoke session
- Revoke all sessions
- Security impact

### Example

```text
Active sessions
Review where your account is signed in.

Current session
Chrome on macOS
Last active now

[Revoke other sessions]
```

## Danger zone

Danger zone should contain truly destructive or high-risk actions only.

Examples:

- Delete account
- Delete workspace
- Delete project
- Reset database
- Revoke all sessions
- Disable SSO
- Transfer ownership
- Clear retained logs

Do not use Danger zone as a dumping ground for every red button.

## Dangerous inline form anti-pattern

```text
Danger zone
Delete account    [tethysplex@gmail.com] [Delete account]
```

Problems:

- High-risk flow is compressed into one row.
- Confirmation input may be prefilled.
- Impact is not explained.
- User has no time to understand consequences.
- Button is too close to routine form behavior.

## Better dangerous flow

Default page:

```text
Danger zone

Delete account
Permanently delete your account, application tokens, saved settings, and usage history. Active subscriptions will be cancelled.

[Start account deletion]
```

Dialog/page:

```text
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

Type `tethysplex@gmail.com` to confirm.

[Cancel] [Delete account]
```

## Confirmation input rules

- Do not prefill confirmation input.
- Use the object name or email as exact confirmation text.
- Explain the reason for typing.
- Do not rely only on a checkbox.
- Destructive button text must repeat the action and object.

### Anti-pattern

```text
Email
[prefilled email]
[Delete]
```

### Better

```text
Type `tethysplex@gmail.com` to confirm deletion.
[empty input]
[Delete account]
```

## Confirm, verify, authorize

Do not confuse these:

- **Confirm**: user understands consequences.
- **Verify**: user proves identity, such as re-auth or 2FA.
- **Authorize**: user has permission to perform action.

High-risk actions may need more than one.

Examples:

- Delete project: type project name.
- Delete account: type email and re-auth.
- Disable SSO: owner permission and re-auth.
- Transfer ownership: owner permission and acceptance flow.

## Checkboxes are weak confirmation

### Weak

```text
[ ] I understand this action cannot be undone.
```

### Better

List concrete consequences and require typed confirmation.

If a checkbox is used, make it specific:

```text
[ ] I understand that apps using this production key will fail after it is revoked.
```

## Destructive result feedback

Do not rely only on toast.

### Anti-pattern

Toast:

```text
Deleted.
```

### Better

After deleting a project:

```text
Project deleted.
Production traffic for this project has stopped.
```

After revoking a key:

```text
API key revoked.
Apps using this key will fail immediately.
```

## Privacy settings

Privacy settings should explain what is collected, where it appears, and what is unaffected.

### Example

```text
Record client IP addresses in logs
When enabled, client IPs appear in usage and error logs. Security systems may still process IPs to prevent abuse.
```

## Privacy assurance

Good assurance note:

```text
Your data is not used to train models
Flint does not train models on your prompts or completions. Read the privacy policy.
```

Make sure this statement is true and supported by policy.

## Security/privacy anti-pattern checklist

- User sees internal auth provider keys.
- Vendor/framework appears where it is not user-facing.
- Tokens are visible by default.
- Token not created state still shows reveal/copy controls.
- `Reset token` used when `Generate`, `Rotate`, or `Revoke` is meant.
- Permissions show raw scopes without user explanation.
- Re-auth appears as an error.
- Dangerous action is inline.
- Confirmation input is prefilled.
- Danger zone includes unrelated low-risk actions.
- Deletion copy does not say what is deleted and what is not.
