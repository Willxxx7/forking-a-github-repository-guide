# Troubleshooting

## Authentication failures

### Public key denied

Configure SSH or use HTTPS:

```bash
git remote set-url origin https://github.com/YOUR-USERNAME/REPOSITORY.git
```

### Repository not found

Check:

- The URL is correct.
- Your GitHub account can access the repository.
- The repository was not deleted or transferred.
- HTTPS/SSH credentials belong to the correct account.

## Git command failures

### Not a Git repository

```bash
cd /path/to/cloned/repository
git status
```

### Remote branch rejected

Fetch and merge the remote branch:

```bash
git fetch origin
git merge origin/CURRENT-BRANCH
git push
```

When rebasing is preferred:

```bash
git pull --rebase origin CURRENT-BRANCH
git push
```

### Merge conflict

1. Open each file Git marks as conflicted.
2. Choose or combine the desired changes.
3. Remove `<<<<<<<`, `=======`, and `>>>>>>>` markers.
4. Save the files.
5. Stage and commit:

```bash
git add .
git commit -m "Resolve merge conflict"
git push
```

### Diverged branches

Create a safety branch:

```bash
git branch backup-before-sync
```

Then rebase:

```bash
git pull --rebase origin main
git push
```

### Wrong remote

View and repair remotes:

```bash
git remote -v
git remote set-url origin https://github.com/YOUR-USERNAME/REPOSITORY.git
git remote set-url upstream https://github.com/colleague/REPOSITORY.git
```

## Pull request problems

| Problem | Resolution |
|---|---|
| No changes to compare | Verify that the branches differ and that you selected the feature branch |
| Merge conflicts | Update locally, resolve conflicts, and push again |
| Wrong target repository | Close the PR and open it against the colleague's original repository |
| Checks fail | Open the failed check and fix the reported issue |
| No compare button | Push the branch to your fork or open a branch-specific PR |

## Visual Studio Code issues

- Run **Git: Clone** from **Ctrl+Shift+P**.
- Open the repository folder, not only an individual file.
- Select **Source Control** to review staged and unstaged changes.
- Use **Terminal > New Terminal** if Git commands do not appear in the integrated terminal.

## Recovery commands

View history:

```bash
git log --oneline --decorate --graph --all
git reflog
```

Discard changes in one file:

```bash
git restore path/to/file
```

Discard all tracked local changes:

```bash
git restore .
```

Unstage a file:

```bash
git restore --staged path/to/file
```

## Security incidents

If a secret was committed:

1. Revoke or rotate it immediately.
2. Remove it from current source and add a suitable `.gitignore` rule.
3. Ask a Git specialist or the repository owner to remove the secret from Git history.
4. Do not assume deleting it in a new commit protects older commits.
