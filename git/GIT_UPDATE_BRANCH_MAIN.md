01 - Update the branch "main" and delet the local branchs that have already been incorporated into it:

```bash
{
GIT_TRUNK="main"
printf "\n"
printf -- "---[ START OF SCRIPT ]---"
printf "\n"
printf "Checking out '%s'..." "$GIT_TRUNK"
printf "\n"
git checkout "$GIT_TRUNK"
if git ls-remote --heads origin > /dev/null 2>&1; then
  printf "\n"
  printf -- "Authenticated. Proceeding."
  printf "\n"

  git fetch --prune


  OLD_STASH=$(git rev-parse -q --verify refs/stash 2>/dev/null || printf -- "")

  git add .
  git stash push -m "auto-before-pull" >/dev/null 2>&1

  NEW_STASH=$(git rev-parse -q --verify refs/stash 2>/dev/null || printf -- "")

  git pull

  OLD_STASH_EQUALS_NEW_STASH=$([ "$OLD_STASH" = "$NEW_STASH" ]; echo $?)

  printf -- "OLD_STASH:%s\n" "$OLD_STASH"
  printf -- "NEW_STASH:%s\n" "$NEW_STASH"
  printf -- "OLD_STASH_EQUALS_NEW_STASH:%s\n" "$OLD_STASH_EQUALS_NEW_STASH"

  if [ "$OLD_STASH_EQUALS_NEW_STASH" -eq 1 ] && [ -n "$NEW_STASH" ]; then
    git stash apply stash@{0}
  fi


  git for-each-ref refs/heads/ "--format=%(refname:short)" | while read branch; do
    [ "$branch" = "$GIT_TRUNK" ] && continue
    mergeBase=$(git merge-base "$GIT_TRUNK" "$branch") || continue
    tree=$(git rev-parse "$branch^{tree}") || continue
    commit=$(git commit-tree "$tree" -p "$mergeBase" -m _) || continue

    if git cherry "$GIT_TRUNK" "$commit" | grep -q '^-'; then
      printf "\n"
      printf "Deleting branch '%s' (squash-merged)\n" "$branch" "$GIT_TRUNK"
      git branch -D "$branch"
    else
      printf "\n"
      printf "Branch '%s' has unique commits — please review and delete the local branch manually if appropriate:\n" "$branch"
      git --no-pager log --oneline "${GIT_TRUNK}..$branch"
    fi
  done
else
  printf "\n"
  printf -- "Not authenticated. Please authenticate first."
fi

printf "\n"
printf -- "---[ END OF SCRIPT ]---"
}
```
