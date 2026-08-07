Jamais faça commits do tipo merge padrão ("standard merge", ex.: "git merge main"), já que o tal:

- Polui o histórico do Git ao criar commits de merge que agregam múltiplas alterações, dificultando entender onde cada modificação foi feita.
- Aumenta o risco de mudanças desnecessárias serem incorporadas ao main, já que podem passar despercebidas durante a revisão de pull requests por estarem diluídas em múltiplos commits.
- Dificulta reverter o projeto para o último estado funcional, pois não há garantias de que cada merge padrão aponte para um commit específico do main, algo difícil de identificar durante a revisão de pull requests.

Em seu lugar, use apenas commits merge fast-forward da seguinte forma:

01.0 - Deixe seu feature branch com um só commit, uma vez que você terá que resolver conflitos para cada commit divergente do main em seu feature branch, ou seja, terá que resolver conflitos para cada commit presente em seu feature branch:

01.1 - Confirme que a cópia local do seu feature branch está atualizada:

```bash
FEATURE_BRANCH=
BASE_BRANCH=main
```

```bash
git fetch --prune
git checkout $FEATURE_BRANCH
git pull
```

01.2 - Identifique o commit base do branch (de onde a branch divergiu):

```bash
BASE_COMMIT=$(git merge-base $FEATURE_BRANCH $BASE_BRANCH)
```

01.3 - Faça manualmente um backup em ZIP da pasta do repositório, uma vez que os comandos a seguir são irreversíveis.

01.4 - Faça um soft reset do feature branch (delete os commits, mas mantenha a alteração resultante deles na área "unstaged changes" do git):

```bash
git reset --soft $BASE_COMMIT
```

01.6 - Limpe seu STASH:

```bash
git stash clear
```

01.7 - Salve as alterações no STASH:

```bash
git add . && git stash
```

02.0 - Execute o merge do tipo fast-forward para atualizar seu feature branch ao main remoto:

```bash
git pull --rebase origin main
```

02.1 - Aplique as alterações salvas no STASH e resolva os eventuais conflitos (vide [06.1] para resolução através da interface do VSCode)

```bash
git stash apply
```

[06.1] https://www.youtube.com/watch?v=anykEUKy51U

03.0 - Crie um único commit cujo título seja o nome do feature branch:

```bash
git add . && git commit -m $FEATURE_BRANCH
```

04.0 - Deixe o feature branch remoto com um só commit para facilitar a análise de PRs e evitar futuras resoluções de conflitos redundantes:

```bash
if [[ -z "$FEATURE_BRANCH" ]]; then
  echo "Error: FEATURE_BRANCH está com o nome vazio."
elif [[ "$FEATURE_BRANCH" == "main" || "$FEATURE_BRANCH" == "master" || "$FEATURE_BRANCH" == "$BASE_BRANCH" ]]; then
  echo "Error: FEATURE_BRANCH não pode ser 'main', 'master' ou '$BASE_BRANCH'"
else
  git push origin "$FEATURE_BRANCH" --force
fi
```
