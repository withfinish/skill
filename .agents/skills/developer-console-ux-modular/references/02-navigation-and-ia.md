# Navigation and information architecture

## Navigation is the product’s spatial model

A trustworthy console makes these obvious:

- Which workspace am I in?
- Which project am I in?
- Which environment am I changing?
- What resource am I viewing?
- Which scope will this action affect?
- Where can I go next?

Navigation is not just menus. It is how the user understands the system.

## Sidebar principles

Sidebars are for places and major product areas.

Good sidebar items:

```text
Projects
Deployments
Logs
API Keys
Webhooks
Usage
Members
Billing
Audit log
Settings
```

Weak sidebar items:

```text
Resources
Entities
Management
Configure
Admin
General
Tools
Platform
Core
V2
```

Use user-facing nouns and tasks, not internal modules.

## Sidebar scope

If the product has multiple scopes, make scope visible near navigation:

- Workspace
- Project
- Environment
- Region
- Branch

### Anti-pattern

Workspace is only in the user avatar menu.

### Better

Sidebar top:

```text
Agent Velo              v
Acme API                v
Production              v
```

or navbar:

```text
Agent Velo / Acme API / Production
```

## Multi-sidebar patterns

Multiple sidebars can work if each layer has a distinct responsibility.

### Good two-layer model

Global sidebar:

```text
Workspace switcher
Projects
Usage
Members
Billing
Audit log
Workspace settings
```

Project sidebar:

```text
Project switcher
Overview
Deployments
Logs
API Keys
Webhooks
Environment Variables
Domains
Project settings
```

The first answers “which workspace/product area?” The second answers “which project section?”

### Anti-pattern

Left sidebar:

```text
Settings
```

Second sidebar:

```text
Settings
General
Advanced
Management
```

Top tabs:

```text
Settings
Security
Billing
```

This duplicates levels and creates a maze.

## Avoid file-tree navigation unless the product truly requires it

### Anti-pattern

```text
Workspace
  Projects
    Acme API
      Deployments
      Logs
      API Keys
      Webhooks
      Settings
    Mobile App
      Deployments
      Logs
      API Keys
      Webhooks
      Settings
Members
Billing
Settings
```

This feels like an internal resource tree.

### Better

Keep global and project navigation separate.

## Navbar principles

Navbars are for current context and global tools, not a second sidebar.

Good navbar contents:

- Breadcrumb
- Workspace/project/environment switcher
- Global search or command palette
- Docs/help
- Notifications
- User menu
- Status indicator
- Carefully chosen global create action

Poor navbar contents:

- Duplicated sidebar links
- Page-level actions that belong in page headers
- Marketing CTAs everywhere
- Billing upsells that overpower the console

## Page-level actions do not belong in global navbar

### Anti-pattern

Global navbar always shows:

```text
Create
Upgrade
Invite
Deploy
```

### Better

- `Create project` appears on Projects page.
- `Create key` appears on API Keys page.
- `Deploy` appears on Deployments page.
- `Invite member` appears on Members page.
- Global command palette can find all actions.

## Command palette

A command palette is excellent for developer consoles because developers understand IDEs, terminals, and launchers.

It can support:

- Navigation
- Project switching
- Environment switching
- Creating resources
- Opening docs
- Copying IDs
- Searching logs
- Recent actions

### Example groups

```text
Pages
Projects
Actions
Docs
Recent logs
```

### Anti-pattern

A command palette that executes dangerous actions directly.

### Better

The palette can find `Delete project`, but selecting it opens the proper confirmation flow.

## Breadcrumbs

Breadcrumbs are useful for details and nested scope.

Good:

```text
Acme API / Deployments
Deployment #428
```

Bad:

```text
Projects / Acme API / Deployments / Deployment #428 / Details
Details
```

Breadcrumbs show path. The page title names the current object.

## Environment switcher

Environment is high-risk scope. It must be obvious.

### Anti-pattern

A tiny `prod` dropdown in a corner.

### Better

```text
Production API keys
Create and rotate keys used by production services.
```

or:

```text
Environment: Production
```

and confirmation copy:

```text
Revoke production key?
Apps using this production key will fail immediately.
```

## Project switcher

Project switchers should be easy to reach and searchable.

Good switcher features:

- Current workspace visible
- Search projects
- Recent projects
- Create/import project
- Project IDs copyable in details, not primary labels

Avoid hiding project switching in the avatar menu.

## User menu

User menu is for personal account actions:

```text
Profile
Account settings
Theme
Keyboard shortcuts
Sign out
```

Do not hide workspace/project business functions in the user menu:

```text
Billing
Members
API keys
Usage
Project settings
Integrations
```

## Settings is not a landfill

Core developer workflows should not be buried in Settings.

Do not hide these under generic settings if they are central to the product:

- API Keys
- Webhooks
- Logs
- Usage
- Deployments
- Environment Variables
- Members

Settings should contain configuration, preferences, security, account, and danger-zone controls.

## Filters are not navigation

Navigation answers “where am I going?” Filters answer “which subset of this page am I viewing?”

Do not put filters in the global sidebar:

```text
All logs
Error logs
Warning logs
Successful webhooks
Failed webhooks
Active keys
Revoked keys
```

Use tabs or filter controls inside the relevant page.

## Tabs vs sidebar

Tabs are for sibling views inside the current object or page.

Good tabs for a webhook delivery detail:

```text
Overview
Payload
Headers
Retries
```

Poor tabs:

```text
All
Failed
Production
Settings
Billing
```

This mixes filters, environment, navigation, and settings.

## Navigation badges

Use badges sparingly. They should indicate action-worthy states.

Good:

```text
Invites 2
Failed 3
Payment failed
```

Bad:

```text
Projects 24
Logs 12k
API Keys 8
Webhooks 4
```

If the number does not require action, it usually does not belong in navigation.

## Collapsed sidebar

Collapsed sidebars are useful for power users, but risky as the default.

Guidelines:

- Do not default to icon-only for new users.
- Keep current scope visible.
- Provide hover/focus labels.
- Use stable, recognizable icons.
- Do not rely on icons alone for Logs, Events, Traces, Deployments, and Webhooks.

## URLs and shareability

Developer users copy links, open multiple tabs, and share debugging context.

Good URLs:

```text
/projects/acme-api/deployments/428
/projects/acme-api/logs?level=error&range=24h
/workspaces/agent-velo/members
```

Poor URLs:

```text
/dashboard?id=123&type=deployment&tab=logs
/app/view/resource
```

Filtered logs, selected events, open sheets, and current tabs should be recoverable when possible.

## Navigation anti-pattern checklist

- Multiple navigation systems show the same item.
- Settings contains every unresolved product area.
- Workspace/project/environment scope is hidden.
- Sidebar labels are internal or vague.
- Filters appear as global nav.
- Statuses appear as navigation.
- User menu contains workspace/project functions.
- Navbar duplicates sidebar.
- Command palette replaces IA instead of accelerating it.
- URL does not reflect the current object or scope.
