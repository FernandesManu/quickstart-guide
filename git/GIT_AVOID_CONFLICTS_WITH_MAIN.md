[Ir para "a conflict occurs during the rebase or want to cancel the rebase"](#rebase-conflict)

1 — On your branch, make sure everything is committed

```bash
git status"
```

1.1 — If you still have uncommitted changes:

```bash
git add .
git commit -m "My change"
```

2 — Update main

```bash
git checkout main
git pull
```

3 — Go back to your branch

4 — Bring the latest main changes into your branch

```bash
git rebase main
```

5 — And only then do the push:

```bash
git push
```

5.1 — If your branch has already been pushed to GitHub before, the rebase will probably change the history that exists on GitHub. In that case, a normal push may be rejected.

```bash
git push --force-with-lease
```

<a id="rebase-conflict"></a>

⚠️ a conflict occurs during the rebase or want to cancel the rebase:

```bash
git add file-with-conflict git rebase --continue
```

or

```bash
git rebase --abort
```
