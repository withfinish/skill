# Billing, usage, notifications, privacy, and settings pages

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
