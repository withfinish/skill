# Copy Rewrite Cheatsheet

## Internal implementation to user-facing copy

- `google_auth` → `Signed in with Google`
- `clerk_session` → `Email sign-in` or the actual user-facing provider
- `root` → `Owner` or `Account owner`
- `created_at` → `Created`
- `updated_by_user_id` → `Last updated by`
- `sync_workspace_entitlements` → `Refresh plan limits`

## Error copy

Bad: `Something went wrong.`
Good: `We couldn’t create the API key. No changes were made.`

Bad: `Forbidden.`
Good: `You need owner access to delete this workspace.`

Bad: `PrismaClientKnownRequestError...`
Good: `This email is already invited.`

## Risk copy

- `No changes were made.`
- `This only affects new deployments.`
- `Existing requests are not affected.`
- `You won’t be able to see this secret again.`
- `Apps using this key will fail immediately. Other keys are not affected.`
- `This action is recorded in the audit log.`
