# Git-related tips

This file contains various tips and tricks for using the `git` CLI (and GitHub too!)

## Glossary

Some helpful `git` and GitHub related terms.

| Name | Abbreviation | Description |
| :--- | :--- | :--- |
| `repository` | **repo** | A repository is like a folder that holds a project's files, but unlike other folders, a repository is tracked for changes by `git` |
| `commit` | - | A commit holds the specific changes to files that were made since the last `commit` |
| `pull request` | **PR** | Short for "Pull Request", this is a request to merge the changes made on one repository or branch into another repository or branch |
| `branch` | - | A branch is like a new workspace for the same project, allowing you to work on changes, commit them, and push them to a repository without affecting the original branch |
| `fork` | - | A forked repository is a "copy" of a repository that has references to the original. GitHub will track differences between a fork and a source for you, and show the number of different commits |
| `clone` | - | Cloning a repository is the process of bringing the files and configuration from the online/external location to your local machine |
| `remote` | - | A remote repository is a repository stored outside your local computer (so, on GitHub or GitLab for example) |
| `stash` | - | Save the uncommitted work locally |

## Rebasing a Fork

You'll likely run in to situations where your forked version of a project "falls behind" the state of the source version. GitHub will allow you to make a pull request to bring the changes from the source into your fork, which _does work_, but creates a merge commit that will show up every time you create a PR back to the source.

Instead, to keep the commit history clean, you can `rebase` your fork against the source. Here are the steps to do so:

- Step one: Make sure you are on your primary branch with `git checkout <branchname>`. Most commonly, this will be `git checkout main`.
- Step two: Get the current state of the source repository with `git fetch upstream`. If it throws an error that there is no upstream, you'll need to set it ↓
  - Step two.five: To set the upstream, you'll use `git remote add upstream <url>`, where the URL is the clone URL for the source repository.
- Step three: Reset the state of your local repository to match the source with `git reset --hard upstream/<branchname>`, where `branchname` is the name of the primary branch. So, most likely `git reset --hard upstream/main`.
- Step four: Force your fork repo to match this new state with `git push -f`.
- Step five: Celebrate your success!

## Rebasing a PR

Sometimes you end up with merge conflicts in your pull request, because the target repository has had changes that do not mesh with _your_ changes. GitHub offers a handy GUI for fixing merge conflicts, but this is only available for "non-complex" merge conflicts. If this GUI is _not_ available, you can follow these steps to rebase your PR against the base branch of the fork and resolve the merge conflicts.

- Step one: Make sure you are on the branch you used for that pull request with `git checkout <branchname>`.
- Step two: Get the current state of the _source_ repository with `git fetch upstream`.If it throws an error that there is no upstream, you'll need to set it ↓
  - Step two.five: To set the upstream, you'll use `git remote add upstream <url>`, where the URL is the clone URL for the source repository.
- Step three: Trigger the interactive rebase flow with `git rebase -i upstream/branchname` where "branchname" is the name of the *default/primary* branch (most likely `main`.)
- Step four: Using the file that your editor opens up, ensure that all commits are marked as `pick` (they should be, by default.) Save and close the file.
- Step five: Your editor and `git` will now walk you through each commit that generates a merge conflict. Adjust the files, choosing which version of changes you want to keep. Make sure you remove the `<<<<<`, `>>>>>`, and `=====` that `git` adds to show the conflicts!
- Step six: As you fix each file, you will need to `git add <filename>` and `git commit` to commit the resolved changes.
- Step seven: Once all conflicts are resolved, `git` will allow you to `git push` those changes. Your PR should automatically update and reflect the new state, with no merge conflicts!
- Step eight: Celebrate your success! Merge conflicts can definitely be tricky!

## Squashing Your Commits

A maintainer might have a contributing requirement that PRs have only one commit, or they might ask you to squash your PR's commits into one. These steps will help you do so!

- Step one: Make sure you are on the branch you used for that pull request with `git checkout <branchname>`.
- Step two: Using `git`'s interactive rebasing feature, we are going to rebase against your current default branch with `git rebase -i origin/<branchname>` (the branch name is most likely `main`).
- Step three: Using the file that opens in your editor, set the commit at the *top* of the list to `pick` and the rest of the commits to `squash`. Save and close the file.
- Step four: Force your remote branch to accept this new commit history with `git push -f`.
- Step five: Celebrate your success! 🎉

> **Note**: Force-pushing a branch can have unintended side effects, so be very careful when force-pushing.

### Squashing the latest commit

If you want to squash the latest commit _only_, you can run one single command which is much shorter.

1. Be sure to verify that you're on the correct branch.
2. Stage all your changes by using `git add .` or `git add <filename>` for certain file.
3. Run the following command. This command will squash the current staged changes with the other commit's changes.

```bash
git commit --amend -m "commit message" -m "commit description (optional)"
```

4. Force-push your changes to the desired branch.

```bash
git push -f
```

5. You're done now! 🎉 The latest commit has been successfully changed.
