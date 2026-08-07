Never use standard merge commits (e.g., git merge main), because they:

- Pollute the Git history by creating merge commits that combine multiple changes, making it harder to identify where each modification was introduced.
- Increase the risk of unnecessary changes being merged into main, since they can go unnoticed during pull request reviews when spread across multiple commits.
- Make it more difficult to roll back the project to the last known working state, as there is no guarantee that each standard merge points to a specific commit from main, making it harder to identify during pull request reviews.

Instead, use fast-forward merges by following the steps below.

01.0 - Keep your feature branch to a single commit, since you would otherwise need to resolve conflicts for every commit in your feature branch that diverges from main.

01.1 - Make sure your local feature branch is up to date:

```bash
FEATURE_BRANCH=
BASE_BRANCH=main
```

```bash
git fetch --prune
git checkout $FEATURE_BRANCH
git pull
```

01.2 - Find the branch's base commit (the point where it diverged from main):

```bash
BASE_COMMIT=$(git merge-base $FEATURE_BRANCH $BASE_BRANCH)
```

01.3 - The following commands are irreversible, so create a ZIP backup of the repository folder before continuing.

01.4 - Perform a soft reset of the feature branch (delete the commits, but keep the changes resulting from them in Git's "unstaged changes" area).:

```bash
git reset --soft $BASE_COMMIT
```

01.6 - Clear your stash:

```bash
git stash clear
```

01.7 - Save your changes to the stash:

```bash
git add . && git stash
```

02.0 - Fast-forward your feature branch to the latest remote main:

```bash
git pull --rebase origin main
```

02.1 - Apply the stashed changes and resolve any merge conflicts (See [06.1] for resolving conflicts using the VS Code interface.)

```bash
git stash apply
```

[06.1] https://www.youtube.com/watch?v=anykEUKy51U

03.0 - Create a single commit.Use the feature branch name as the commit message:

```bash
git add . && git commit -m $FEATURE_BRANCH
```

04.0 - Keep the remote feature branch with only one commit. This simplifies pull request reviews and helps prevent redundant conflict resolution in the future:

```bash
if [[ -z "$FEATURE_BRANCH" ]]; then
  echo "Error: FEATURE_BRANCH está com o nome vazio."
elif [[ "$FEATURE_BRANCH" == "main" || "$FEATURE_BRANCH" == "master" || "$FEATURE_BRANCH" == "$BASE_BRANCH" ]]; then
  echo "Error: FEATURE_BRANCH não pode ser 'main', 'master' ou '$BASE_BRANCH'"
else
  git push origin "$FEATURE_BRANCH" --force
fi
```
