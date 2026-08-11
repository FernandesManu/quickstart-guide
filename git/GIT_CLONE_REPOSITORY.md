01 - Define the repository to be cloned:

```bash
REPO_SSH_URL=
```

02 - Clone the project and enter the cloned folder:

```bash
git clone $REPO_SSH_URL &&
REPO_NAME=$(basename -s .git "$REPO_SSH_URL") &&
cd $REPO_NAME
```
