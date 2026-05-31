# Billing, usage, limits, quotas, and cost controls

## Billing and usage are trust surfaces

Billing pages should answer:

- What plan am I on?
- What am I using?
- What period is this for?
- What limit am I approaching?
- What happens if I exceed it?
- What will cost more?
- Which projects or keys drive usage?
- When was the data updated?
- How can I export or inspect details?

Do not make Billing only an invoices table.

## Usage summary

Good usage summary:

```text
Usage this period
12,482 requests
Updated 2 minutes ago
Billing period ends Jan 31
```

Add breakdowns:

```text
Top projects
Top models
Error rate
Estimated overage
```

## Limits and quotas

Limits should be visible before users hit them.

### Anti-pattern

User learns only from failure:

```text
Rate limit exceeded.
```

### Better

```text
Requests this month
800,000 of 1,000,000 included
Resets Jan 31
```

```text
Rate limit
1,000 requests per minute
Request a higher limit
```

## Exceeding limits

Explain what happens:

- Requests rejected?
- Automatic overage billing?
- Throttling?
- Downgrade?
- Grace period?

### Example

```text
If you exceed the included requests, additional requests are billed at the current overage rate.
```

or:

```text
Requests above this limit return `429 Rate Limited` until the next minute.
```

## Low-balance warnings

### Anti-pattern

```text
Quota warnings
$0
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

## Cost-risk controls

Settings that may increase cost should be in Billing, Usage, Cost controls, or Model access, not generic Preferences.

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

If enabling is risky, use a Dialog:

```text
Allow unpriced models?
Some providers may change prices without notice. Requests will be billed at the provider’s current rate.

[Cancel] [Allow unpriced models]
```

## Pricing updates

Provider/model pricing changes can be operational notifications if they affect users.

Good:

```text
Provider update digest
Receive email updates when providers add models or change pricing.
```

Avoid warning-colored styling if it is just a subscription preference.

## Invoices

Invoices table can be simple:

```text
Date
Amount
Status
Plan
Invoice
```

Actions:

- View invoice
- Download PDF

Do not overload invoice rows with unrelated billing settings.

## Payment failure

Payment failure is operational and high priority.

Good copy:

```text
Payment failed
Update your payment method to keep production requests running. Existing requests will continue until Jan 18.
```

Include:

- Impact
- Deadline
- Action
- Which workspace/account is affected

## Plan limits

Avoid internal `entitlements` language.

### Anti-pattern

```text
Entitlements
Feature gates for plan tier.
```

### Better

```text
Plan limits
View the features and usage limits included in this workspace plan.
```

## Balance and lifetime spend placement

Balance, spend, and request counts usually do not belong in Profile unless the product is truly personal-wallet-first.

Better locations:

- Billing summary
- Usage summary
- Account overview

Do not mix identity fields with financial metrics.

## Billing/usage anti-pattern checklist

- Billing page is only invoices.
- Usage has no period or freshness.
- Limits are only visible after failure.
- Cost-risk settings are styled as simple preferences.
- Pricing-change digest is styled as warning/danger.
- Balance/spend mixed into Profile identity card.
- Internal terms like `entitlements` appear.
- Payment failure copy does not state deadline or impact.
