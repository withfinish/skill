# Quality: accessibility, responsive behavior, color semantics, naming, and versioning

## Responsive and desktop split-screen behavior

Developer users often run the console beside an editor or terminal.

Design for narrow desktop widths:

- Tables convert to lists.
- Sidebar can collapse without losing scope.
- Header actions do not crush titles.
- Sheets remain usable.
- Code blocks scroll horizontally but copy full content.
- Filters collapse into a controlled panel.

Mobile support should prevent misoperation, especially for production and danger actions.


## Accessibility and focus

Reliable tools must be accessible.

Rules:

- Do not rely on color alone for status.
- Keep visible focus rings.
- Icon buttons need accessible names.
- Form errors must be associated with fields.
- Dialogs should focus the first useful element.
- Dangerous buttons should not receive default focus.
- Sheet closing returns focus to the trigger.
- Dynamic logs should not disrupt screen readers.
- Keyboard access must not be secondary.


## Color semantics

Use color consistently.

- Red: destructive or serious error.
- Yellow/amber: warning or attention.
- Green: healthy, live, successful.
- Blue: information or link/action.
- Gray: neutral, inactive, metadata.

Anti-pattern:

- Ordinary checkboxes on warning-tinted backgrounds.
- Feature announcement and warning both yellow.
- Every badge using brand color.
- Failed status visually indistinguishable from destructive button.


## Naming consistency

Use one name for one concept.

Avoid switching between:

- Project / App / Service / Resource.
- Rotate key / Regenerate key / Reset key / Refresh key.
- Live / Active / Ready / Running.
- Workspace / Organization / Team / Tenant.

Terminology drift makes the product feel unreliable.


## Changelog, API versioning, and deprecations

Developer products need traceable change.

Provide:

- Changelog.
- API version selector.
- Deprecation notices.
- Migration guides.
- Preview/Beta labels with behavior expectations.

Bad:

`feature_flag_agents_runtime_beta_v3`

Better:

`Agents runtime is in Preview. APIs and behavior may change.`


## Memory and user preference

A mature console can remember user workflow preferences:

- Recent projects.
- Recent environments.
- Last logs filter.
- Column preferences.
- Density setting.
- Command palette recent actions.

Be careful with environment memory. Do not silently reopen users in Production if that creates risk. Make scope visible.
