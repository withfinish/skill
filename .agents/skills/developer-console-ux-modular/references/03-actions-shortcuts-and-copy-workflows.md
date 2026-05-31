# Actions, shortcuts, command palette, and copy workflows

## Copy and copy buttons

### Pattern

Copy affordances are a developer-first signal. Provide them for values that users paste elsewhere.

Good copy targets:

- API key
- Project ID
- Request ID
- Webhook secret
- Endpoint URL
- Environment variable name
- CLI command
- curl example
- Error code
- Deployment URL
- Docker command
- Git remote
- Log line
- JSON payload

### Rules

- Tooltip should be specific: `Copy project ID`, not just `Copy`.
- Feedback should be specific: `Copied request ID`, not just `Copied` when multiple things can be copied.
- If UI truncates a value, copy the full value.
- Sensitive values should be masked by default.
- Copying a secret should be intentional and logged when appropriate.
- Provide copy for grouped config when it fits the workflow.

Good grouped copy:

```bash
PROJECT_ID=prj_...
API_URL=https://api.example.com
ENVIRONMENT=production
```

### Anti-pattern

Avoid:

- Copy buttons everywhere without clear targets.
- Copy feedback missing.
- Copying truncated text.
- Copying labels or extra whitespace.
- Copy icons that are too small or inaccessible.
- Copying hidden sensitive values without user awareness.


## Keyboard shortcuts and kbd hints

### Pattern

Keyboard shortcuts are a promise. Use them for high-frequency actions and make them actually work.

Good examples:

- `⌘K` / `Ctrl K`: command palette
- `/`: search
- `?`: shortcuts help
- `Esc`: close dialog or sheet
- `⌘S`: save changes
- `⌘↵`: deploy or submit when appropriate
- `G P`: go to projects
- `G L`: go to logs

### Rules

- Show OS-appropriate shortcuts: `⌘` on macOS, `Ctrl` on Windows/Linux.
- Do not trigger global shortcuts while the user is typing.
- Provide keyboard focus states.
- Shortcuts should be discoverable in a help panel.
- Dangerous operations should not execute directly from a shortcut; they must still confirm.

### Anti-pattern

Avoid:

- Displaying shortcuts that do not work.
- `Esc` not closing a modal.
- `Enter` behavior changing unpredictably between forms.
- Shortcuts conflicting with browser defaults.
- Kbd hints used as decoration.


## Command palette

### Pattern

Command palettes are excellent for developer consoles because they match IDE, terminal, launcher, and CLI workflows.

Use command palettes for:

- Page navigation.
- Project switching.
- Environment switching.
- Opening docs.
- Creating keys.
- Viewing logs.
- Inviting members.
- Copying IDs.
- Running common actions.

Group results:

- Pages
- Projects
- Actions
- Docs
- Recent logs

### Anti-pattern

Do not use command palette as a substitute for information architecture. New users still need visible navigation.

Do not allow destructive commands to execute immediately from search. Route them to confirmation flows.


## Code snippets

### Pattern

Code snippets should behave like executable workflow aids.

Good snippets:

- Include the right language.
- Are copyable in full.
- Use real account/project context when safe.
- Avoid fake placeholder values unless clearly marked.
- Explain where to run them and what happens next.

Example:

```bash
curl https://api.example.com/v1/events \
  -H "Authorization: Bearer $API_KEY"
```

Helper text:

`Run this from your backend or terminal. Logs will appear here after the first request.`

### Anti-pattern

Avoid decorative code blocks that do not help users complete the workflow.
