------------------------
# Objectif: 
------------------------

- Illustrer la différence entre `git merge` et `git rebase`
- Nous allons créer un dépôt Git, deux branches, et travailler sur chacune avec les commandes exactes.

### Étape 1 : Initialiser le dépôt et créer des commits de base

1. **Initialisez le dépôt Git :**
   ```bash
   mkdir git-evaluation
   cd git-evaluation
   git init
   ```

2. **Créez un fichier `fichier1.txt` et ajoutez le premier commit :**
   ```bash
   echo "Première ligne dans fichier1" > fichier1.txt
   git add fichier1.txt
   git commit -m "Ajout du fichier1 avec la première ligne"
   ```

3. **Ajoutez un deuxième commit en modifiant `fichier1.txt` :**
   ```bash
   echo "Deuxième ligne dans fichier1" >> fichier1.txt
   git add fichier1.txt
   git commit -m "Ajout de la deuxième ligne dans fichier1"
   ```

4. **Ajoutez un troisième commit en ajoutant `fichier2.txt` :**
   ```bash
   echo "Contenu de fichier2" > fichier2.txt
   git add fichier2.txt
   git commit -m "Ajout du fichier2 avec son contenu"
   ```

   À ce stade, l'historique de `master` ressemble à ceci :
   ```plaintext
   (master)
   A---B---C
   ```

### Étape 2 : Créer les branches `feature-merge` et `feature-rebase`

1. **Créez la branche `feature-merge` et basculez dessus :**
   ```bash
   git checkout -b feature-merge
   ```

2. **Ajoutez trois commits dans `feature-merge` :**

   - **Premier commit :**
     ```bash
     echo "Contenu initial dans feature-merge" > merge-example.txt
     git add merge-example.txt
     git commit -m "Ajout de merge-example.txt avec contenu initial"
     ```

   - **Deuxième commit :**
     ```bash
     echo "Ligne additionnelle dans merge-example" >> merge-example.txt
     git add merge-example.txt
     git commit -m "Ajout d'une ligne additionnelle dans merge-example"
     ```

   - **Troisième commit :**
     ```bash
     echo "Dernière ligne dans merge-example" >> merge-example.txt
     git add merge-example.txt
     git commit -m "Ajout de la dernière ligne dans merge-example"
     ```

   L’historique de `feature-merge` est maintenant :
   ```plaintext
   (feature-merge)
       D---E---F
   ```

3. **Retournez à `master` et créez la branche `feature-rebase` :**
   ```bash
   git checkout master
   git checkout -b feature-rebase
   ```

4. **Ajoutez trois commits dans `feature-rebase` :**

   - **Premier commit :**
     ```bash
     echo "Contenu initial dans feature-rebase" > rebase-example.txt
     git add rebase-example.txt
     git commit -m "Ajout de rebase-example.txt avec contenu initial"
     ```

   - **Deuxième commit :**
     ```bash
     echo "Ligne additionnelle dans rebase-example" >> rebase-example.txt
     git add rebase-example.txt
     git commit -m "Ajout d'une ligne additionnelle dans rebase-example"
     ```

   - **Troisième commit :**
     ```bash
     echo "Dernière ligne dans rebase-example" >> rebase-example.txt
     git add rebase-example.txt
     git commit -m "Ajout de la dernière ligne dans rebase-example"
     ```

   L’historique de `feature-rebase` est maintenant :
   ```plaintext
   (feature-rebase)
       G---H---I
   ```

### Étape 3 : Fusion de `feature-merge` dans `master` avec `git merge`

1. **Revenez sur `master` :**
   ```bash
   git checkout master
   ```

2. **Fusionnez `feature-merge` dans `master` :**
   ```bash
   git merge feature-merge -m "Fusion de feature-merge dans master"
   ```

   L’historique avec `git merge` ressemble maintenant à ceci :
   ```plaintext
   (master)
   A---B---C-------J
          |       /
          D---E---F
   ```

   Ici, `J` est un commit de fusion qui conserve l'historique distinct de `feature-merge`.

### Étape 4 : Fusion de `feature-rebase` dans `master` avec `git rebase`

1. **Revenez sur `feature-rebase` :**
   ```bash
   git checkout feature-rebase
   ```

2. **Rebasez `feature-rebase` sur `master` :**
   ```bash
   git rebase master
   ```

   Cette commande applique les commits `G`, `H`, et `I` de `feature-rebase` après le commit `J` de `master`, créant un historique linéaire :

   ```plaintext
   (master)
   A---B---C---J---G'---H'---I'
   ```

   Les commits `G'`, `H'`, et `I'` sont les versions réappliquées de `G`, `H`, et `I` après `J`.

3. **Revenez sur `master` et faites un fast-forward merge de `feature-rebase` :**
   ```bash
   git checkout master
   git merge feature-rebase
   ```

   L’historique final sur `master` est donc linéaire grâce au rebase de `feature-rebase`.

### Étape 5 : Vérifier l'historique avec `git log`

Utilisez `git log --oneline --graph --all` pour observer la différence dans l'historique :

```bash
git log --oneline --graph --all
```

- Avec `git merge`, l’historique montrera une **jonction** avec un commit de fusion.
- Avec `git rebase`, l’historique est **linéaire** sans commit de fusion.

### Récapitulatif

| Commande                   | Action                                      |
|----------------------------|---------------------------------------------|
| `git checkout -b feature-merge` | Crée la branche `feature-merge` et y bascule |
| `git commit -m "...`       | Ajoute des commits dans chaque branche      |
| `git merge feature-merge`  | Fusionne `feature-merge` dans `master` avec un commit de fusion |
| `git rebase master`        | Rebase `feature-rebase` pour rendre l’historique linéaire |
| `git log --oneline --graph --all` | Visualise l'historique complet |

En suivant ces étapes, les étudiants comprendront clairement comment `git merge` et `git rebase` impactent l'historique Git, en ayant une vue pratique sur la différence entre un historique avec un commit de fusion et un historique linéaire.



-----------------------------------------------------------------------
# Annexe : Différence entre `git merge` et `git rebase`. 
-----------------------------------------------------------------------

### Historique initial

Imaginons un projet où la branche principale est `master` avec trois commits initiaux :

```plaintext
(master)
A---B---C
```

Ensuite, on crée deux nouvelles branches depuis `master` :

1. **`feature-merge`** : pour tester `git merge`
2. **`feature-rebase`** : pour tester `git rebase`

### Travail dans chaque branche

Dans chaque branche, nous ajoutons trois nouveaux commits. Voici ce que cela donne :

```plaintext
(master)
A---B---C

(feature-merge)
       \
        D---E---F   # Commits sur feature-merge

(feature-rebase)
       \
        G---H---I   # Commits sur feature-rebase
```

### Étape 1 : Fusion de `feature-merge` dans `master` avec `git merge`

Pour `feature-merge`, nous utilisons la commande `git merge` sur la branche `master`. Cela crée un **commit de merge** qui garde un historique complet avec toutes les branches, sans réorganiser les commits. 

Voici l’historique après le `merge` :

```plaintext
(master)
A---B---C-------J      # J est le commit de merge
       |       /
       |      /
(feature-merge)
        D---E---F      # feature-merge garde son historique séparé
```

- **Explication** : `git merge` ajoute les commits de `feature-merge` (`D`, `E`, `F`) à l’historique de `master` sans les déplacer ni les modifier. Il crée simplement un nouveau commit `J` pour indiquer la fusion.
- **Observation** : Avec `git merge`, on voit un "point de jonction" dans l'historique où les deux branches se rencontrent. Cela permet de voir que `feature-merge` a été fusionnée avec `master`, tout en conservant l’historique distinct.

### Étape 2 : Fusion de `feature-rebase` dans `master` avec `git rebase`

Pour `feature-rebase`, nous utilisons `git rebase`. Au lieu de créer un commit de merge, `git rebase` déplace les commits (`G`, `H`, `I`) comme s'ils avaient été créés après `C` dans `master`. Voici l’historique après le `rebase` :

```plaintext
(master)
A---B---C---G'---H'---I'
```

- **Explication** : `git rebase` applique les commits de `feature-rebase` (`G`, `H`, `I`) à la suite des commits de `master` (après `C`). Les commits sont "rejoués" comme s’ils avaient été créés directement après `C`, donc ils apparaissent dans un ordre linéaire.
- **Observation** : Avec `git rebase`, l’historique est plus propre et linéaire, mais on perd le point de jonction qui montre l'existence d'une branche séparée.

### Comparaison finale

Pour résumer les différences observées dans le log Git :

- **git merge** : 
  - Garde l’historique complet avec les branches distinctes.
  - Crée un commit de fusion qui montre visuellement le moment où les deux branches se rejoignent.
  - **Avantage** : Idéal pour suivre un historique complet, particulièrement dans les projets collaboratifs.

- **git rebase** :
  - Réorganise l’historique pour le rendre linéaire, en plaçant les commits de `feature-rebase` comme s’ils avaient été faits après `C`.
  - **Avantage** : Rend l’historique plus propre, utile pour les projets où on veut minimiser les points de jonction dans le log.

En résumé :

```plaintext
git merge   ->  Historique complet avec commit de fusion
git rebase  ->  Historique linéaire sans commit de fusion
```

