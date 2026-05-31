# Visual system, accessibility, responsive behavior, and consistency

## Visual style should support trust

Developer consoles usually benefit from:

- Clear hierarchy
- Stable spacing
- Low-noise borders
- Moderate density
- Consistent color semantics
- Predictable interactions
- Readable typography
- Accessible focus states

Avoid over-decorating operational surfaces.

## Density

Developer users can handle dense information, but density must be structured.

Good density:

- Compact log rows with structured fields.
- Field rows in settings.
- Timelines with timestamps.
- Tables for comparison.
- Details sections with copyable IDs.

Bad density:

- Every value as a chip.
- Every row with many actions.
- Dot-separated metadata chains.
- Multiple sidebars plus tabs plus filters.
- Long forms in overlays.

## Cards

Cards should group meaningful modules, not every field.

### Anti-pattern

Separate cards for:

```text
Project ID
Region
Owner
Last updated
Status
Usage
```

### Better

One summary section:

```text
Project details
Status: Live
Region: US East
Owner: Kai
Project ID: `prj_...` [Copy]
Updated 2 minutes ago
```

## Chips and badges

Use chips/badges for state, not all metadata.

Good:

```text
Live
Failed
Building
Production
Preview
Verified
Read-only
Beta
```

Bad:

```text
clerk_session
default
root
main
us-east-1
kai@example.com
created 2m ago
```

## Color semantics

Keep colors stable.

- Red: destructive, failed, critical error.
- Yellow/amber: warning, attention, degraded.
- Green: healthy, success, verified.
- Blue: informational or interactive, depending on system.
- Gray: neutral, inactive, secondary.

Avoid:

- Brand color used as every status.
- Warning backgrounds for ordinary preference checkboxes.
- Danger color for non-danger metadata.
- Too many badge colors.

## Typography and monospace

Use monospace for exact technical values:

- IDs
- Commands
- Tokens
- Paths
- Environment variables
- Commit hashes
- HTTP methods

Do not use monospace for ordinary UI labels, user names, or buttons.

## Icons

Icons should support labels, not replace them.

For icon-only buttons:

- Provide accessible labels.
- Use tooltips where helpful.
- Make targets large enough.
- Do not rely on ambiguous icons for critical actions.

Common anti-pattern:

A row has only eye, copy, reset icons with no clear meaning, especially when token does not exist.

## Accessibility

Accessibility is reliability.

Guidelines:

- Do not convey status by color alone.
- Error messages are associated with fields.
- Focus ring is visible.
- Icon buttons have accessible names.
- Checkboxes/toggles have clear labels.
- Dynamic updates do not steal focus.
- Dialog focus is trapped and restored on close.
- Sheet close returns focus to triggering element.
- Keyboard shortcuts are not the only way to act.
- Dangerous primary buttons are not focused by default.

## Focus examples

Good:

- Dialog opens on first input or cancel area, not destructive button.
- `Esc` closes non-dangerous overlays.
- After closing a log detail Sheet, focus returns to the selected log row.
- After form submission error, focus moves to first invalid field.

## Responsive desktop

Developer consoles are often used in split-screen desktop setups.

Support:

- 1200px and below without collapse failure.
- Sidebar collapse with labels available.
- Tables converting to lists when narrow.
- Sheet width not consuming the whole viewport unexpectedly.
- Header actions wrapping or moving to overflow.
- Code blocks with horizontal scrolling and copy unaffected.
- Filters collapsible without losing state.

Mobile support matters, but developer console responsive design often means “works well beside an editor or terminal.”

## Status not by color alone

### Anti-pattern

A red dot alone means failure.

### Better

```text
Failed
Endpoint returned `401 Unauthorized`.
```

## Consistency

Consistency creates trust. Maintain consistent:

- Names
- Action labels
- Status words
- Save models
- Button placement
- Badge colors
- Error structure
- Timestamp format
- ID display
- Copy feedback

### Anti-pattern

Same action named:

```text
Rotate key
Regenerate key
Refresh key
Reset key
```

Choose one.

## Visual anti-pattern checklist

- Cards around every small fact.
- Chips for every metadata item.
- Warning color used for ordinary preference.
- Red used for non-danger actions.
- Icon-only navigation as default.
- Invisible focus rings.
- Status conveyed by color only.
- Monospace used for normal UI.
- Too much whitespace without clearer structure.
- Dense UI without hierarchy.
