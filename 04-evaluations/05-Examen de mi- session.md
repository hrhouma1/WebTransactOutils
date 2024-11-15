### **Examen de mi-session sur Git**

---

### **Partie 1 : Quiz (20 points)**

**Instructions** : Choisissez la meilleure réponse pour chaque question. Chaque question vaut **1 points**.

#### Questions :
1. Quelle commande permet de cloner un dépôt Git ?
   - a) `git copy`
   - b) `git clone`
   - c) `git download`
   - d) `git fetch`

2. Quelle commande permet de voir l'état actuel des fichiers dans un dépôt ?
   - a) `git status`
   - b) `git check`
   - c) `git log`
   - d) `git show`

3. Quelle est la commande pour créer une nouvelle branche nommée "feature" ?
   - a) `git branch feature`
   - b) `git new feature`
   - c) `git create branch feature`
   - d) `git switch feature`

4. Que fait la commande `git add` ?
   - a) Elle enregistre les changements dans le dépôt distant.
   - b) Elle ajoute les modifications dans l'index (staging area).
   - c) Elle crée un nouveau commit.
   - d) Elle supprime un fichier du dépôt.

5. Quelle commande permet d'annuler les modifications d'un fichier non encore indexé ?
   - a) `git reset`
   - b) `git checkout -- <fichier>`
   - c) `git revert`
   - d) `git undo`

6. Quelle est la différence principale entre `git merge` et `git rebase` ?
   - a) `git merge` combine les branches avec un commit de fusion, `git rebase` réécrit l'historique.
   - b) `git rebase` est plus rapide que `git merge`.
   - c) `git merge` ne fonctionne pas avec des branches distantes.
   - d) Il n’y a aucune différence.

7. Comment vérifier l'historique des commits d'un dépôt ?
   - a) `git show`
   - b) `git log`
   - c) `git history`
   - d) `git inspect`

8. Quelle commande est utilisée pour télécharger des modifications d’un dépôt distant sans les intégrer ?
   - a) `git pull`
   - b) `git fetch`
   - c) `git clone`
   - d) `git update`

9. Quelle est la fonction d’un fichier `.gitignore` ?
   - a) Ignorer les commits effectués sur certaines branches.
   - b) Ignorer les fichiers listés pour qu’ils ne soient pas suivis par Git.
   - c) Supprimer les fichiers du dépôt.
   - d) Restaurer les fichiers supprimés.

10. Que signifie "HEAD" dans Git ?
    - a) Le dernier commit sur la branche principale.
    - b) Le pointeur vers le commit courant dans la branche active.
    - c) Un alias pour le dépôt distant.
    - d) Une commande pour récupérer l'état précédent.

11. Quelle commande permet de comparer les différences entre la branche actuelle et une autre ?
    - a) `git compare`
    - b) `git diff`
    - c) `git inspect`
    - d) `git branch --compare`

12. Que fait `git stash` ?
    - a) Supprime définitivement des fichiers.
    - b) Sauvegarde temporairement les changements non validés.
    - c) Réinitialise l’état du dépôt.
    - d) Annule le dernier commit.

13. Quelle commande permet de supprimer une branche locale nommée "old-feature" ?
    - a) `git delete old-feature`
    - b) `git branch -d old-feature`
    - c) `git remove branch old-feature`
    - d) `git rm old-feature`

14. Quelle commande permet de configurer le nom d'utilisateur pour un dépôt ?
    - a) `git config --local username`
    - b) `git config --global user.name "<nom>"`
    - c) `git setup username "<nom>"`
    - d) `git user set "<nom>"`

15. Comment ajouter un message à un commit ?
    - a) `git commit --add-message`
    - b) `git commit -m "<message>"`
    - c) `git message "<message>"`
    - d) `git add -m "<message>"`

16. Quelle commande affiche les informations sur un commit spécifique ?
    - a) `git inspect`
    - b) `git show <commit-id>`
    - c) `git details <commit-id>`
    - d) `git info <commit-id>`

17. Quel est le rôle de `git push` ?
    - a) Envoyer les modifications locales vers un dépôt distant.
    - b) Télécharger les modifications du dépôt distant.
    - c) Fusionner deux branches.
    - d) Annuler les derniers changements locaux.

18. Quelle commande permet de restaurer un fichier supprimé accidentellement avant un commit ?
    - a) `git undo`
    - b) `git restore <fichier>`
    - c) `git reset`
    - d) `git stash`

19. Que signifie "detached HEAD" dans Git ?
    - a) Une branche sans nom pointant vers un commit spécifique.
    - b) Une erreur dans le dépôt.
    - c) Une branche inactive.
    - d) Un commit abandonné.

20. Quelle commande permet de récupérer les modifications distantes et de les intégrer automatiquement dans la branche locale ?
    - a) `git pull`
    - b) `git fetch`
    - c) `git sync`
    - d) `git merge`

---

### **Partie 2 : Questions de Développement (40 points)**

**Instructions** : Répondez aux questions suivantes en écrivant le code ou en expliquant les étapes nécessaires. Chaque question vaut **20 points**.

1. **Scénario** : Vous avez modifié un fichier `README.md` mais vous avez commis une erreur dans la description. Comment corriger le dernier commit tout en gardant les modifications actuelles dans l'index ?  
   *(Indiquez les commandes et expliquez chaque étape.)*

2. **Scénario** : Vous travaillez sur une branche nommée "dev". Vous souhaitez intégrer ses modifications dans la branche principale "main" sans créer de commit de fusion.  
   *(Décrivez les étapes nécessaires pour effectuer un rebase, en indiquant les commandes exactes.)*


---

### **Partie 3 : Différences entre `git merge` et `git rebase` (40 points)**

**Instructions** :  
- Expliquez les différences entre **`git merge`** et **`git rebase`** en termes de fonctionnement et d'impact sur l'historique Git.  
- Indiquez dans quels cas utiliser l’un ou l’autre (avantages et inconvénients).  
- Fournissez un exemple clair et simple des commandes pour illustrer ces concepts.  
- Vous pouvez vous inspirer du TP que nous avons réalisé ou proposer une amélioration.  


