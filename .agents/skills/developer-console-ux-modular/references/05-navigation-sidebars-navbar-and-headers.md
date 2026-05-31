# Navigation, sidebars, navbar, and page headers

## Navigation and information architecture

### Core principle

Navigation should expose the product model, not the internal implementation model.

A user should always know:

- Which workspace they are in.
- Which project they are in.
- Which environment is active.
- Which resource they are viewing.
- Which scope an action affects.

### Sidebar

Sidebars are for places, not filters and not temporary states.

Good sidebar labels:

- `Projects`
- `Deployments`
- `Logs`
- `API Keys`
- `Webhooks`
- `Usage`
- `Members`
- `Billing`
- `Settings`

Bad sidebar labels:

- `Resources`
- `Entities`
- `Management`
- `Core`
- `Platform`
- `V2`
- `Tenants`
- `Principals`
- `Entitlements`

### Settings is not a landfill

Do not hide core developer workflows in Settings.

API Keys, Webhooks, Logs, Usage, and Deployments often deserve first-class navigation.

### Multi-sidebar structure

Multiple sidebars are acceptable only when each has a clear scope.

Good:

- Global sidebar: workspace-level navigation.
- Project sidebar: project-level navigation.
- Main area: current page.

Bad:

- Two sidebars both containing Settings.
- Sidebar + sub-sidebar + tabs + sub-tabs + accordions for the same scope.
- A file-tree-like hierarchy for a product that is not a file tree.

### Navbar

Navbars should carry current context and global tools, not duplicate the sidebar.

Good navbar items:

- Workspace switcher.
- Project switcher.
- Environment switcher.
- Breadcrumb.
- Search / command palette.
- Docs / help.
- Notifications.
- User menu.

Bad navbar items:

- Duplicate `Projects`, `Logs`, `Settings` when the sidebar already has them.
- Constant marketing CTA.
- Business features hidden in the user avatar menu.

### Breadcrumbs

Use breadcrumbs for deep context:

`Acme API / Deployments / Deployment #428`

Do not use breadcrumbs as the only page title.

### Environment switchers

Environment scope must be obvious when mistakes are costly.

Bad:

- Small dropdown showing `prod` in the corner.

Better:

- Page title: `Production API keys`
- Button: `Create production key`
- Confirmation: `Revoke production key?`

### Filters are not navigation

Do not put `All`, `Failed`, `Successful`, `Production`, `Preview`, or `500` in global navigation unless they are real places. These are usually filters or page tabs.

### URL and shareability

Developer users copy URLs. URLs should preserve meaningful state.

Good:

- `/projects/acme-api/logs?level=error`
- `/projects/acme-api/deployments/428`

Bad:

- `/dashboard?id=123&type=deployment&tab=logs`

Support shareable links for logs, webhook deliveries, deployments, and filtered views when possible.


## Page headers

### Core principle

Headers orient before they command.

A good page header names the current object, clarifies scope and state, and exposes the next useful action without turning into a toolbar.

### Pattern

A strong header may include:

- Breadcrumb.
- Specific title.
- Short scope or purpose copy.
- Important status.
- 2-4 useful metadata fields.
- One primary action.
- At most one or two secondary actions.
- Overflow for low-frequency actions.

Example:

```
Acme API / Deployments

Deployment #428   Live
Production release from branch main.

Deployment ID: dep_8f42... [Copy]
Updated 42 seconds ago
Region: US East

[View logs] [Rollback]
```

### Anti-pattern

Avoid:

- Title: `Details`
- Subtitle: `Manage details.`
- Five header buttons.
- Destructive action beside routine action.
- Generic `Settings` title when the scope is `Production environment variables`.
- Marketing copy in console headers.

### Header title examples

Bad → better:

- `Overview` → `Acme API overview`
- `Settings` → `Project settings`
- `Details` → `Deployment #428`
- `Environment Variables` → `Production environment variables`
- `Manage` → `Webhook endpoints`

### Header copy examples

Bad:

`Manage API keys.`

Better:

`Create keys for server-side requests. Keep production keys separate from development.`

Bad:

`Ship faster with our next-generation deployment engine.`

Better:

`Track builds, releases, and rollbacks for this project.`


## User menu

### Pattern

User menu should contain personal account actions.

Good:

- Profile
- Account settings
- Theme
- Keyboard shortcuts
- Sign out

### Anti-pattern

Do not hide workspace/project features in the user menu:

- Billing
- Members
- API keys
- Usage
- Project settings
- Integrations
