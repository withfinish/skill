---
name: developer-console-ux
description: "Review, design, and rewrite developer-first dashboard, console, settings, navigation, copy, forms, dialogs, sheets, tables, security, privacy, billing, logs, and danger-zone UX. Use when asked to audit, redesign, or specify trustworthy developer tools."
---

# Developer Console UX

Use this skill to design, critique, rewrite, or specify developer-first dashboards, consoles, settings pages, account pages, API/token pages, logs, webhooks, billing, usage, privacy, security, navigation, page headers, dialogs, sheets, forms, tables, and danger-zone flows.

Do not use this skill for visual-only landing-page aesthetics. This skill is about product structure, interaction design, user copy, trust, operational clarity, and developer workflow.

## Core stance

A developer-first console should feel like a reliable instrument panel, not a marketing site and not an internal admin panel.

Expose structure, state, control, and diagnostics. Hide implementation leakage, internal codenames, framework/provider artifacts, database-field labels, feature-flag names, and organizational noise.

Use this rule repeatedly:

> Show implementation-relevant details only when they help the user act, verify, debug, secure, or automate. Hide everything that merely reveals how the product is built.

## Primary principles

1. **Product model over implementation model**  
   Use user-facing concepts such as Workspace, Project, API key, Webhook endpoint, Sign-in method, Billing, Usage, Logs. Avoid internal concepts such as `tenant_id`, `google_auth`, `clerk_session`, `feature_flag_console_v3`, `rbac_policy_denied`, or raw provider IDs.

2. **Routine work fast; risky work deliberate**  
   Copying IDs, creating keys, searching logs, and switching views should be fast. Deleting accounts, rotating production secrets, disabling SSO, resetting databases, changing billing owners, or enabling cost-risk settings should use clear confirmation flows.

3. **Scope, state, risk, and next action must be obvious**  
   Always clarify current workspace, project, environment, object, status, timestamp, and impact when mistakes could be costly.

4. **Friendly means “don’t make me guess”**  
   Developer-friendly copy is direct, specific, actionable, and calm. It does not need to be cute. It should reduce ambiguity and anxiety.

5. **Progressive disclosure beats dense control panels**  
   Keep primary paths simple. Provide technical details, raw JSON, request IDs, advanced options, and audit details where useful, but do not make every page a table or database record.

6. **Actions live at the right level**  
   Page-level actions in page headers, section-level actions in sections, object actions in details/sheets/pages, copy actions next to copyable values, dangerous actions isolated.

7. **Developer details should be useful, not noisy**  
   IDs, request IDs, commit hashes, regions, HTTP methods, timestamps, error codes, and CLI commands are useful. Internal providers, codenames, enum keys, feature flags, and backend job names are usually noise.

## When the user asks for an audit or redesign

Respond with a structured review. Prefer this order:

1. **What is working**: name the good patterns already present.
2. **Main problems**: group by product concept, copy, interaction, risk, and hierarchy.
3. **Recommended structure**: propose improved information architecture.
4. **Pattern-by-pattern fixes**: show current anti-patterns and better versions.
5. **User copy rewrites**: provide exact labels, helper text, button text, and confirmation copy.
6. **Prioritized changes**: identify the highest-impact fixes first.

Use concrete examples. Prefer “Before / Better” pairs.

## Quick pattern selector

- For general trust and developer-first principles, load `references/00-principles.md`.
- For wording, labels, terminology, codenames, error/success copy, dots, chips, IDs, and monospace, load `references/01-copy-and-terminology.md`.
- For sidebars, nested navigation, navbar, breadcrumbs, command palette, scope, tabs, URL, and settings IA, load `references/02-navigation-and-ia.md`.
- For page structure, section design, page headers, field rows, metadata, primary actions, and layout hierarchy, load `references/03-page-layout-and-headers.md`.
- For primary buttons, shortcuts, `kbd`, command palette, copy affordances, copy workflows, action placement, and keyboard/focus behavior, load `references/04-actions-shortcuts-and-copy.md`.
- For tables, lists, filters, search, row actions, timelines, pagination, and logs list patterns, load `references/05-tables-lists-filters-search.md`.
- For forms, settings pages, save models, toggles, inline inputs, preferences, notifications, privacy, and cost-risk controls, load `references/06-forms-settings-and-save-models.md`.
- For Dialog, Sheet, Drawer, Flyout, Modal, confirmation flows, and overlay selection, load `references/07-dialogs-sheets-and-overlays.md`.
- For security, tokens, secrets, sign-in methods, permissions, roles, sessions, privacy, danger zone, and destructive flows, load `references/08-security-privacy-and-danger-zone.md`.
- For operational state, errors, loading, empty states, success feedback, logs, webhooks, deployments, audit logs, status page, notifications, and diagnostics, load `references/09-operational-states-and-diagnostics.md`.
- For billing, usage, limits, quotas, low-balance warnings, plan limits, cost controls, pricing changes, invoices, and model/provider cost settings, load `references/10-billing-usage-and-limits.md`.
- For a complete settings page audit framework and a before/after example, load `references/11-settings-page-audit-framework.md`.
- For visual density, color semantics, accessibility, responsive desktop, cards, chips, separators, and consistency, load `references/12-visual-system-accessibility-responsive.md`.
- For a compact end-to-end audit checklist, load `references/13-review-checklists.md`.

## Red flags to call out immediately

- User-visible internal implementation names: `clerk_session`, `google_auth`, `Clerk user`, `tenant_id`, `feature_flag`, `strategy_google_oauth2`, `sync_workspace_entitlements`.
- Provider or framework leakage where the provider is not a user-managed integration.
- Generic headings: `Details`, `General`, `Manage`, `Resources`, `Entities`, `Settings` without clear scope.
- Metadata stuffed into chips or dot-separated strings: `Production · main · iad1 · 42s ago · Kai`.
- Tables used as the default layout for every resource.
- Row-level actions cluttering tables: `View`, `Edit`, `Duplicate`, `Delete`, `More` in every row.
- Dangerous inline forms: `Delete account [input: email] [Delete]`.
- Confirmation inputs that are prefilled.
- Dialogs or Sheets used as long-form pages.
- Ambiguous save model: some fields auto-save, some need a global `Save preferences`, some trigger destructive changes.
- Token pages showing `not generated` as if it were a token value, or showing reveal/copy controls when no token exists.
- Error copy ending at `Something went wrong` or raw backend exceptions.
- Disabled buttons with no visible explanation.
- Security, privacy, cost, or production-impact settings presented as casual checkboxes with no impact copy.

## Common output format for recommendations

Use concise sections:

```md
## Diagnosis
...

## Recommended structure
...

## Patterns and anti-patterns
| Area | Anti-pattern | Better pattern |
|---|---|---|

## Copy rewrites
Before: ...
Better: ...

## Priority fixes
1. ...
2. ...
3. ...
```

## Final quality bar

A good developer console should let the user say:

- I know where I am.
- I know what object and environment this affects.
- I know whether the system is healthy, stale, failing, or waiting.
- I know what I can copy, run, retry, rotate, revoke, or inspect.
- I know which actions are safe, risky, reversible, or permanent.
- I do not see the company’s internal codenames, provider IDs, database fields, or feature flags unless I explicitly need technical details.
