# Concepts :

- `git squash`, `git reset`, `git revert`, `git diff`, etc.


### Exercice Git : Combinaison de `git reset`, `git revert`, `git diff`, et `git cherry-pick`

#### Contexte de l’exercice
Dans cet exercice, vous allez simuler une série d'erreurs et de corrections dans un dépôt Git pour comprendre comment les commandes `git reset`, `git revert`, `git diff`, et `git cherry-pick` interagissent. Vous apprendrez à corriger des erreurs de commits, à annuler des changements, et à fusionner des commits spécifiques dans d’autres branches.

---

### Étape 1 : Créer un dépôt Git et faire quelques commits
1. **Créer un nouveau dépôt** :
   - Ouvrez votre terminal, puis créez un nouveau dépôt Git dans un dossier vide :
     ```bash
     git init
     ```
2. **Créer des fichiers et les committer** :
   - Créez plusieurs fichiers (`file1.txt`, `file2.txt`, `file3.txt`), ajoutez du contenu à chacun d’eux, puis effectuez trois commits :
     ```bash
     echo "Contenu de file1" > file1.txt
     git add file1.txt
     git commit -m "Ajout de file1"
     
     echo "Contenu de file2" > file2.txt
     git add file2.txt
     git commit -m "Ajout de file2"
     
     echo "Contenu de file3" > file3.txt
     git add file3.txt
     git commit -m "Ajout de file3"
     ```

---

### Étape 2 : Utiliser `git reset` pour revenir à un commit précédent
1. **Revenir au commit de `file2.txt`** :
   - Utilisez `git reset` pour revenir à l’état du dépôt juste après l’ajout de `file2.txt` :
     ```bash
     git reset --hard HEAD~1
     ```
   - Cela annulera le dernier commit (l'ajout de `file3.txt`).
   - Vérifiez l’état actuel de votre dépôt avec :
     ```bash
     git status
     ```

---

### Étape 3 : Utiliser `git revert` pour annuler un commit sans changer l’historique
1. **Annuler l’ajout de `file2.txt`** :
   - Utilisez `git revert` pour annuler le commit où `file2.txt` a été ajouté, sans affecter les autres commits :
     ```bash
     git revert HEAD
     ```
   - Cela créera un nouveau commit qui annule les modifications introduites par `file2.txt`.

---

### Étape 4 : Utiliser `git diff` pour comparer les changements
1. **Comparer l’état du dépôt avant et après une modification** :
   - Modifiez `file1.txt` en ajoutant une nouvelle ligne :
     ```bash
     echo "Nouvelle ligne" >> file1.txt
     ```
   - Utilisez `git diff` pour voir les différences entre l’état actuel et le dernier commit :
     ```bash
     git diff
     ```

---

### Étape 5 : Utiliser `git cherry-pick` pour copier un commit spécifique dans une autre branche
1. **Créer une nouvelle branche** :
   - Créez une nouvelle branche nommée `feature` :
     ```bash
     git checkout -b feature
     ```
2. **Récupérer un commit spécifique à partir de la branche principale** :
   - Utilisez `git cherry-pick` pour copier le commit de l'ajout de `file3.txt` dans la branche `feature` :
     ```bash
     git cherry-pick <ID_du_commit_file3>
     ```
   - Vous pouvez obtenir l'ID du commit correspondant en utilisant `git log`.

---

### Résultat attendu
À la fin de cet exercice, vous aurez appris à :
- Revenir à un état précédent avec `git reset`.
- Annuler un commit en créant un nouveau commit avec `git revert`.
- Comparer les modifications en cours avec `git diff`.
- Fusionner des commits spécifiques dans une autre branche avec `git cherry-pick`.

### Questions à Répondre
1. **Quand est-il préférable d’utiliser `git reset` plutôt que `git revert` ?**
2. **Quelles différences remarquez-vous entre `git reset --hard` et `git revert` ?**
3. **Comment `git cherry-pick` peut-il être utile dans un projet collaboratif ?**


