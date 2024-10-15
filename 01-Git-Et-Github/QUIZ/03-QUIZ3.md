# QUIZ 3 (30 QUESTIONS)

### 1. **Quel est le rôle de la commande `git init` ?**
   - A. Initialiser un nouveau dépôt Git.
   - B. Ajouter un fichier au suivi de Git.
   - C. Fusionner des branches.
   - D. Supprimer un dépôt Git.

### 2. **Comment ajouter tous les fichiers modifiés et nouveaux fichiers au staging area (zone d'indexation) ?**
   - A. `git add *`
   - B. `git add .`
   - C. `git add -A`
   - D. `git commit -a`

### 3. **Quelle commande permet de commiter des changements avec un message ?**
   - A. `git save -m "message"`
   - B. `git commit -m "message"`
   - C. `git commit`
   - D. `git save`

### 4. **Que fait la commande `git pull` ?**
   - A. Elle envoie les modifications locales vers le dépôt distant.
   - B. Elle fusionne le dépôt distant avec le dépôt local.
   - C. Elle récupère les changements du dépôt distant et les fusionne dans la branche courante.
   - D. Elle crée une nouvelle branche.

### 5. **Comment basculer vers une autre branche dans Git ?**
   - A. `git change [branch-name]`
   - B. `git branch [branch-name]`
   - C. `git checkout [branch-name]`
   - D. `git switch [branch-name]`

### 6. **Quelle commande permet de lister toutes les branches, locales et distantes ?**
   - A. `git branch`
   - B. `git branch --all`
   - C. `git branch --list`
   - D. `git checkout`

### 7. **Quelle commande fusionne les changements d'une branche dans la branche courante ?**
   - A. `git pull`
   - B. `git merge [branch-name]`
   - C. `git rebase [branch-name]`
   - D. `git checkout [branch-name]`

### 8. **Comment appliquer les modifications enregistrées temporairement avec `git stash` ?**
   - A. `git stash apply`
   - B. `git stash pop`
   - C. `git stash pull`
   - D. `git stash push`

### 9. **Comment annuler le dernier commit sans supprimer les modifications locales ?**
   - A. `git reset --soft HEAD~1`
   - B. `git reset --hard HEAD~1`
   - C. `git revert HEAD`
   - D. `git reset HEAD~1`

### 10. **Quelle commande permet de réécrire l'historique Git en combinant plusieurs commits en un seul ?**
   - A. `git squash`
   - B. `git rebase -i`
   - C. `git merge --squash`
   - D. `git commit --amend`

### 11. **Comment récupérer les modifications du dépôt distant sans les fusionner ?**
   - A. `git fetch`
   - B. `git pull`
   - C. `git merge`
   - D. `git sync`

### 12. **Quel est le rôle de la commande `git checkout -b [branch-name]` ?**
   - A. Créer une nouvelle branche et y basculer.
   - B. Supprimer une branche.
   - C. Afficher l'historique des commits.
   - D. Fusionner une branche dans la branche courante.

### 13. **Quelle commande permet de lister toutes les modifications enregistrées par `git stash` ?**
   - A. `git stash list`
   - B. `git stash show`
   - C. `git stash logs`
   - D. `git stash view`

### 14. **Comment supprimer une branche locale ?**
   - A. `git branch -d [branch-name]`
   - B. `git branch --delete [branch-name]`
   - C. `git remove [branch-name]`
   - D. `git branch -rm [branch-name]`

### 15. **Comment ajouter un tag annoté à un commit pour indiquer une version ?**
   - A. `git tag -a v1.0 -m "Version 1.0"`
   - B. `git tag v1.0`
   - C. `git commit --tag v1.0`
   - D. `git tag --annotate v1.0`

### 16. **Quelle est la différence entre `git merge` et `git rebase` ?**
   - A. `git merge` crée un commit de fusion, `git rebase` réapplique les commits sur la branche cible.
   - B. `git merge` supprime l'historique, `git rebase` le conserve.
   - C. `git merge` réécrit l'historique, `git rebase` non.
   - D. `git merge` ne peut être utilisé que pour les branches locales, `git rebase` pour les branches distantes.

### 17. **Que se passe-t-il lorsque vous utilisez `git rebase` sur une branche avec des conflits ?**
   - A. Git résout automatiquement les conflits.
   - B. Git vous demande de résoudre les conflits manuellement.
   - C. Git annule le rebase et revient à l'état précédent.
   - D. Git crée une nouvelle branche.

### 18. **Quelle commande est utilisée pour combiner des commits dans un dépôt sans changer leur ordre ?**
   - A. `git merge`
   - B. `git rebase`
   - C. `git cherry-pick`
   - D. `git commit --amend`

### 19. **Comment supprimer définitivement des modifications locales sans les commiter ?**
   - A. `git reset --hard`
   - B. `git reset --soft`
   - C. `git stash`
   - D. `git checkout`

### 20. **Quelle commande permet de faire un commit rapide de tous les fichiers modifiés et suivis ?**
   - A. `git commit -a -m "message"`
   - B. `git commit -m "message"`
   - C. `git commit -A`
   - D. `git add . && git commit -m "message"`

### 21. **Comment forcer le push d'une branche vers le dépôt distant en écrasant l'historique distant ?**
   - A. `git push --force`
   - B. `git push --force-with-lease`
   - C. `git push origin --all`
   - D. `git push -f`

### 22. **Comment résoudre un conflit de fusion dans Git ?**
   - A. Modifier les fichiers concernés, puis utiliser `git add` et `git commit`.
   - B. Utiliser `git reset --hard` pour annuler la fusion.
   - C. Utiliser `git stash` pour ignorer les changements.
   - D. Supprimer le fichier en conflit.

### 23. **Quelle commande permet de supprimer tous les changements locaux non suivis ?**
   - A. `git clean -f`
   - B. `git reset --hard`
   - C. `git stash clear`
   - D. `git remove --untracked`

### 24. **Comment cloner un dépôt Git distant vers votre machine locale ?**
   - A. `git init [URL]`
   - B. `git clone [URL]`
   - C. `git pull [URL]`
   - D. `git checkout [URL]`

### 25. **Que fait la commande `git log --oneline` ?**
   - A. Affiche tous les commits avec une vue simplifiée.
   - B. Affiche le détail de chaque commit.
   - C. Affiche uniquement les branches.
   - D. Montre les différences entre les branches.

### 26. **Comment voir la différence entre deux commits dans un projet ?**
   - A. `git diff`
   - B. `git log`
   - C. `git merge`
   - D. `git status`

### 27. **Comment renommer une branche Git locale ?**
   - A. `git rename [old-name] [new-name]`
   - B. `git branch -m [new-name]`
   - C. `git branch --move [new-name]`
   - D. `git change [new-name]`

### 28. **Quelle commande permet de visualiser l’état actuel des fichiers suivis et non suivis dans le dépôt local ?**
   - A. `git status`
   - B. `git diff`
   - C. `git log`
   - D. `git show`

### 29. **Que fait la commande `git cherry-pick` ?**
   - A. Elle permet de sélectionner un ou plusieurs commits spécifiques à appliquer sur une autre branche.
   - B. Elle crée une nouvelle branche à partir d’un commit spécifique.
   - C. Elle permet de fusionner des commits en conflit.
   - D. Elle supprime un commit spécifique.

### 30. **Quelle commande est utilisée pour rétablir un fichier supprimé dans un dépôt local avant un commit ?**
   - A. `git reset --hard`


   - B. `git restore [file]`
   - C. `git checkout -- [file]`
   - D. `git revert [file]`

