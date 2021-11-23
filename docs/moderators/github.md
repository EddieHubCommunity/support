# Maintaining Repositories

This page is intended to provide guidelines for maintaining EddieHub's various repositories.

## When To Merge PRs

Pull requests should be merged only after:

- At least 2 maintainers have provided an approving review.
- All requested changes have been resolved (no "unresolved conversations").
- All CI checks (GitHub Actions) are passing.

## How to Merge PRs

When merging a pull request, you should generally perform a "Squash and Merge". This will squash all of the commits into one.

When you do this, GitHub's UI will give you a chance to edit the commit message. Be sure to follow the [Conventional Commit](https://www.conventionalcommits.org/en/v1.0.0/) format:

```txt
<type>(<scope>): <message>
```

- `type` is the nature of the change:
  - `feat` for new features
  - `fix` for bug fixes
  - `docs` for documentation changes
  - `chore` for changes such as updating developer configs (`.eslintrc.json`) or similar changes that don't affect the end user.
- `scope` is **optional**, and explains the part of the codebase the change touches:
  - `api` for a backend change
  - `client` for a front end change
  - `tools` for things like actions
  - `tests` for adding tests
  - ...and so on.
- `message` is a brief description of the changes the pull request makes.

For example, the commit message which created this file was `docs: add drafts for moderation guide`.

Additionally, GitHub will automatically append the pull request number at the end of the default commit message. **DO NOT REMOVE THIS**, as it allows people to reference the pull request that created the commit to check the full commit history.

## Handling Inactive PRs

If a contributor has not responded to reviews or comments on a PR, follow this general timeline for how to respond:

- After 7 days (one week) of inactivity, a maintainer should comment on the PR.
  - This comment should ping the author, ask for a status update, and remind them that we have a Discord server if they need assistance with contributing.
- After 14 days (two weeks) of inactivity **since the contributor's last comment**, a maintainer should close the pull request.
  - Be sure to leave a friendly message thanking them for their efforts and inviting them to request we re-open the PR when they are available to complete the changes.

In general, only *one* maintainer should be reaching out to the contributor. If multiple maintainers reach out, we could inadvertently make our contributors feel pressured/rushed. We are all busy, and want to respect each others' time.

## Handling Inactive Issues

In general, inactive issues are handled by `Stalebot`, which will add a label after a period of inactivity and close the issue a few days later.

If an issue should not be closed, remove the `stale issue` label that the action has added, and then leave a comment on the issue explaining why it is still necessary. If an issue is repeatedly being labelled by the bot, it may indicate that it is not a priority and we should re-evaluate the need.
