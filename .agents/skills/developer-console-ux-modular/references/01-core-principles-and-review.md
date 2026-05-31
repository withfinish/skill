# Core principles and review workflow

## Core philosophy

A trustworthy developer console should feel like a reliable instrument panel, not a marketing website and not an internal admin database.

It should:

- Expose structure, state, scope, control, and diagnostic evidence.
- Hide internal implementation details, codenames, provider IDs, database fields, feature flags, and framework artifacts.
- Make routine work fast and risky work deliberate.
- Reduce ambiguity, not necessarily complexity.
- Let developers act, verify, debug, secure, and automate.
- Avoid visual and copy noise: excessive chips, dotted metadata strings, CRUD tables, row action forests, generic labels, and vague errors.

A useful summary:

> Developer-first does not mean implementation-first. Show technical details when they help users act, verify, debug, secure, or automate. Hide details that merely reveal how the product is built.


## How to approach a review

When reviewing a console screen, first identify the user scope and task:

1. What object is the user viewing or changing?
2. What scope does the action affect: account, workspace, project, environment, region, branch, token, provider, deployment, request, or billing period?
3. Is this page for setup, operation, debugging, security, billing, or preferences?
4. What is the one primary action, if any?
5. What information must be immediately visible for trust?
6. Which details should be folded into technical details, logs, audit entries, or support-only views?
7. Is the save model clear: instant save, section save, page save, or confirmation flow?
8. Are risky operations separated from routine operations?

Then provide:

- A short diagnosis.
- Specific issues.
- Recommended structure.
- Copy rewrites.
- Patterns and anti-patterns.
- Priority fixes.


## Overall product tone

### Pattern

The product should feel calm, precise, and useful.

Good console copy:

- Names the object.
- Explains the scope.
- States the status.
- Gives the next action.
- Reduces anxiety by saying whether anything changed, whether production is affected, and what remains safe.

Examples:

- `Production variables saved. New deployments will use these values.`
- `Webhook delivery failed because your endpoint returned 401 Unauthorized.`
- `We couldn’t rotate this key. No changes were made.`
- `This action is recorded in the audit log.`
- `Apps using this key will fail immediately. Other keys are not affected.`

### Anti-pattern

Do not make the product sound like an internal system, a database, or a marketing page.

Avoid:

- `Something went wrong.`
- `PrismaClientKnownRequestError`
- `Mutation completed.`
- `You are signed in with google_auth.`
- `Manage resource.`
- `Ship faster with our next-generation platform.`
- `Oopsie! The deployment goblin failed again.`

Better:

- `Signed in with Google.`
- `This email is already invited.`
- `Deployment failed. The build command exited with code 1.`
- `Create a key to authenticate requests from your backend.`


## Visual and information-density principles

### Pattern

A developer console should have enough density to be useful, but enough structure to be readable.

Use:

- Clear section boundaries.
- Stable spacing.
- Low-noise metadata.
- Limited status badges.
- Copyable identifiers where useful.
- Progressive disclosure for technical details.

### Anti-pattern

Avoid:

- Every field inside a card.
- Every metadata item as a chip.
- Every resource page as a table.
- Every action as a row button.
- Every status in bright colors.
- Every setting as `label + input + save`.
- Huge marketing-style hero headers in console pages.
