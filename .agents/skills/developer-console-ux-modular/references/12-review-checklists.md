# Review checklists

## Final review checklist

Use this checklist when auditing a developer console screen.

### Scope and structure

- Is the current workspace/project/environment obvious?
- Is the page task clear: setup, operate, debug, secure, bill, or prefer?
- Does the page have one dominant action, if any?
- Are navigation, filters, tabs, and breadcrumbs serving distinct roles?
- Are URLs shareable and meaningful?

### Copy

- Are labels user-facing rather than internal?
- Are errors diagnostic and repairable?
- Are success messages scoped?
- Are high-risk actions clear about impact and recovery?
- Are vague labels like `Details`, `Manage`, `Submit`, and `Confirm` avoided?

### Developer workflow

- Are useful IDs copyable?
- Are code snippets executable and copyable?
- Are logs searchable and structured?
- Are request IDs, timestamps, regions, branches, commits, and versions shown where useful?
- Are shortcut hints functional?

### Risk and trust

- Are destructive actions isolated?
- Are secrets masked and only revealed intentionally?
- Are dangerous settings confirmed?
- Are permissions explained visibly?
- Are billing and quota impacts clear?
- Is data freshness visible?

### Visual and interaction noise

- Are chips limited to meaningful status?
- Are dotted metadata strings avoided when they flatten meaning?
- Are tables used only when appropriate?
- Are row actions minimized?
- Are card boundaries and section structure purposeful?
- Are dialogs short and sheets contextual?

### Settings-specific

- Are profile, security, billing, preferences, privacy, and danger separated?
- Are provider details like `Clerk` hidden unless user-relevant?
- Is the save model clear?
- Are high-cost or privacy-sensitive preferences treated with the right seriousness?
- Does Danger Zone start a flow instead of completing deletion inline?
