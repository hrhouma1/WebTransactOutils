### Exercice Git : Combinaison de `git stash`, `git merge`, `git rebase`, et `git worktree`

#### Contexte de l’exercice
Dans cet exercice, vous allez manipuler des fonctionnalités comme `git stash`, `git merge`, `git rebase`, et `git worktree`. Ces commandes sont utilisées pour gérer le travail en cours, fusionner des branches de manière fluide et manipuler plusieurs branches ou versions du code de manière simultanée.

---

### Étape 1 : Utiliser `git stash` pour sauvegarder des modifications en cours
1. **Modifier un fichier sans le committer** :
   - Modifiez un fichier existant ou créez un nouveau fichier `file4.txt` :
     ```bash
     echo "Contenu temporaire de file4" > file4.txt
     ```
   - Ajoutez ce fichier à l’index, mais ne le commitez pas :
     ```bash
     git add file4.txt
     ```
2. **Utiliser `git stash` pour sauvegarder le travail en cours** :
   - Vous réalisez que vous devez basculer sur une autre branche pour travailler sur une autre fonctionnalité. Au lieu de committer ces changements, vous pouvez les sauvegarder temporairement :
     ```bash
     git stash
     ```
   - Cela sauvegarde vos modifications non commitées et vous permet de changer de branche ou de faire d'autres modifications sans compromettre votre travail en cours.

3. **Basculer vers une autre branche et récupérer le travail stashed** :
   - Changez de branche (par exemple, vers `feature`) et appliquez le stash pour retrouver vos changements :
     ```bash
     git checkout feature
     git stash pop
     ```

---

### Étape 2 : Utiliser `git merge` pour combiner deux branches
1. **Fusionner une branche dans une autre** :
   - Vous avez terminé de travailler dans la branche `feature` et souhaitez la fusionner avec la branche principale (`main`). Pour cela, vous devez revenir à la branche principale :
     ```bash
     git checkout main
     ```
   - Ensuite, utilisez la commande `git merge` pour fusionner la branche `feature` dans `main` :
     ```bash
     git merge feature
     ```
   - Si aucun conflit n’existe, Git combinera simplement les modifications. Sinon, vous devrez résoudre les conflits manuellement avant de terminer la fusion.

---

### Étape 3 : Utiliser `git rebase` pour réorganiser les commits
1. **Réorganiser les commits d’une branche** :
   - Si vous préférez avoir un historique plus linéaire, vous pouvez utiliser `git rebase` au lieu de `git merge`. Pour cela, basculez à nouveau vers la branche `feature` :
     ```bash
     git checkout feature
     ```
   - Utilisez la commande `git rebase` pour appliquer les commits de la branche `main` avant les vôtres :
     ```bash
     git rebase main
     ```
   - Cela vous permettra de réorganiser l’historique des commits sans créer de commit de fusion.

---

### Étape 4 : Utiliser `git worktree` pour travailler sur plusieurs branches en parallèle
1. **Créer un nouvel espace de travail** :
   - Parfois, vous devez travailler sur plusieurs branches en même temps, sans basculer constamment entre elles. `git worktree` vous permet de créer un autre répertoire de travail pour une branche spécifique. Utilisez la commande suivante pour créer un nouveau répertoire de travail pour la branche `feature` :
     ```bash
     git worktree add ../feature_worktree feature
     ```
   - Cela créera un nouveau dossier `feature_worktree` où vous pourrez travailler sur la branche `feature` tout en gardant le dépôt principal sur une autre branche.

2. **Travailler dans le nouvel espace de travail** :
   - Vous pouvez maintenant naviguer dans ce nouveau répertoire et y effectuer des modifications spécifiques à la branche `feature` :
     ```bash
     cd ../feature_worktree
     ```

---

### Étape 5 : Résoudre un conflit de merge ou de rebase
1. **Générer un conflit** :
   - Dans la branche `main`, modifiez un fichier que vous avez également modifié dans la branche `feature`. Par exemple :
     ```bash
     echo "Changement dans main" >> file1.txt
     git commit -am "Modification dans main"
     ```
   - Ensuite, basculez à nouveau vers la branche `feature` et tentez de la fusionner ou de la réorganiser avec `main` :
     ```bash
     git rebase main
     ```
   - Git devrait vous avertir d’un conflit.

2. **Résoudre le conflit** :
   - Git va marquer les lignes conflictuelles dans le fichier concerné. Modifiez le fichier pour conserver les bonnes parties et supprimez les marqueurs de conflit. Une fois le conflit résolu, terminez le rebase :
     ```bash
     git add file1.txt
     git rebase --continue
     ```

---

### Résultat attendu
À la fin de cet exercice, vous saurez :
- Sauvegarder des modifications temporairement avec `git stash`.
- Combiner plusieurs branches avec `git merge`.
- Réorganiser des commits avec `git rebase`.
- Travailler simultanément sur plusieurs branches grâce à `git worktree`.
- Résoudre des conflits lors de fusions ou de rebase.

### Questions à Répondre
1. **Quelles différences y a-t-il entre `git merge` et `git rebase` ?**
2. **Dans quel contexte est-il utile d’utiliser `git worktree` ?**
3. **Quand est-il plus pertinent d’utiliser `git stash` plutôt que de committer les modifications en cours ?**

