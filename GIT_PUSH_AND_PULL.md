# Git Push and Pull

Use these commands from the website repository:

```sh
cd /home/morgan/CyberTacticsForge/cybertacticsforge.github.io
```

## Publish local changes to `main`

First, check what changed:

```sh
git status
git diff
```

Save your changes in a local commit:

```sh
git add -A
git commit -m "Describe the website update"
```

Download changes from GitHub and replay your local commits on top of them:

```sh
git pull --rebase origin main
```

Then publish the updated `main` branch:

```sh
git push origin main
```

If `git commit` says there is nothing to commit, continue with `git pull --rebase origin main` and `git push origin main`.

## Pull down changes without publishing anything

If your working tree is clean and you only want the newest copy from GitHub:

```sh
git switch main
git pull --rebase origin main
```

Check whether the working tree is clean with `git status`. If you have unfinished changes that you do not want to commit yet, temporarily store them:

```sh
git stash push -u -m "work before pulling main"
git pull --rebase origin main
git stash pop
```

`git stash pop` can produce conflicts if the same lines changed locally and on GitHub. Resolve them using the conflict steps below.

## Resolve a conflict during `git pull --rebase`

Git stops and lists the conflicted files. Run:

```sh
git status
```

Open each conflicted file. Find sections like this:

```text
<<<<<<< HEAD
version from GitHub
=======
your local version
>>>>>>> your-commit
```

Edit the file so it contains the final version you want, and delete the `<<<<<<<`, `=======`, and `>>>>>>>` marker lines. Then stage the resolved file and continue:

```sh
git add path/to/resolved-file
git rebase --continue
```

Repeat `git status`, edit, `git add`, and `git rebase --continue` until Git reports that the rebase is complete. Then run:

```sh
git push origin main
```

If Git opens an editor during `git rebase --continue`, keep the commit message, save, and close the editor.

To cancel the rebase and return to the state from before the pull:

```sh
git rebase --abort
```

## If a push is rejected

A rejection usually means someone pushed to GitHub after your last pull. Do not force-push `main`. Run:

```sh
git pull --rebase origin main
git push origin main
```

Resolve any conflicts as described above.

## Quick everyday sequence

When your edits are ready, this is the normal sequence:

```sh
cd /home/morgan/CyberTacticsForge/cybertacticsforge.github.io
git status
git add -A
git commit -m "Describe the website update"
git pull --rebase origin main
git push origin main
```

