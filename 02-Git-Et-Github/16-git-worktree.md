# 16 git worktree



### **Objectif :**
Ce guide vous apprendra à utiliser la commande **`git worktree`**, qui permet de créer plusieurs répertoires de travail (worktrees) pour un même dépôt Git. Vous apprendrez comment utiliser cette fonctionnalité pour travailler sur plusieurs branches en parallèle sans avoir à changer constamment de branche dans le même répertoire.

---

## **Partie 1 : Théorie**

### **Qu'est-ce que `git worktree` ?**

- **`git worktree`** est une commande Git qui vous permet de **créer plusieurs répertoires de travail** pour un même dépôt. Cela signifie que vous pouvez travailler sur plusieurs branches simultanément dans différents répertoires sans avoir à basculer entre les branches dans un seul répertoire.

### **Quand utiliser `git worktree` ?**

- **Travail sur plusieurs branches** : Lorsque vous devez travailler sur plusieurs branches en parallèle et que vous ne voulez pas committer ou stasher vos modifications en cours pour changer de branche.
- **Tests simultanés** : Si vous voulez tester des branches différentes ou des versions spécifiques de votre projet sans perturber votre environnement de travail actuel.
- **Comparaison entre branches** : Pour pouvoir comparer directement deux branches de manière pratique en les ayant ouvertes dans deux répertoires différents.

### **Avantages de `git worktree` :**

- **Pas besoin de stasher ou de committer** : Vous pouvez simplement créer un nouveau répertoire de travail et continuer à travailler sur une autre branche sans perdre votre contexte actuel.
- **Facilite le multitâche** : Idéal pour ceux qui doivent jongler entre plusieurs branches pour les corrections de bugs, les nouvelles fonctionnalités, ou les tests.

---

## **Partie 2 : Pratique**

Nous allons maintenant voir comment utiliser **`git worktree`** dans le cadre du projet **site-php-1** pour travailler sur plusieurs branches en parallèle.

### **Étape 1 : Cloner le projet existant depuis GitHub**

Si vous n'avez pas encore de dépôt local, commencez par cloner le projet **site-php-1** depuis GitHub.

1. Ouvrez votre terminal et exécutez la commande suivante pour cloner le projet :

   ```bash
   git clone https://github.com/hrhouma1/site-php-1.git
   ```

2. Entrez dans le répertoire du projet cloné :

   ```bash
   cd site-php-1
   ```

---

### **Étape 2 : Créer un deuxième répertoire de travail avec `git worktree`**

Nous allons maintenant créer un deuxième répertoire de travail pour pouvoir travailler sur une autre branche sans quitter la branche actuelle.

1. **Créer un worktree pour une nouvelle branche** :

   Par exemple, si vous voulez travailler sur une branche `feature-X` tout en restant sur la branche `main` dans votre répertoire de travail actuel, vous pouvez créer un nouveau répertoire de travail pour `feature-X` avec la commande suivante :

   ```bash
   git worktree add ../feature-X feature-X
   ```

   - **`../feature-X`** : Spécifie le chemin vers le nouveau répertoire de travail.
   - **`feature-X`** : Indique la branche à utiliser dans ce nouveau répertoire.

2. **Vérifier le nouveau répertoire de travail** :

   Après avoir créé le worktree, allez dans le nouveau répertoire `feature-X` :

   ```bash
   cd ../feature-X
   ```

   Vous êtes maintenant dans un répertoire de travail distinct qui utilise la branche `feature-X`.

---

### **Étape 3 : Travailler sur plusieurs branches simultanément**

Nous allons maintenant faire des modifications dans la branche `feature-X` tout en gardant la branche `main` ouverte dans l'autre répertoire.

1. **Modifier `app.js` dans la branche `feature-X`** :

   Dans le répertoire `feature-X`, ouvrez le fichier `app.js` et ajoutez cette ligne :

   ```javascript
   console.log("Modification dans feature-X");
   ```

2. **Ajouter et committer les modifications** :

   - Ajoutez les modifications à la zone de staging :

     ```bash
     git add app.js
     ```

   - Créez un commit pour cette modification :

     ```bash
     git commit -m "Ajout d'un log dans app.js sur feature-X"
     ```

3. **Changer de répertoire de travail pour revenir à `main`** :

   Maintenant, revenez au répertoire de travail principal pour travailler sur la branche `main` :

   ```bash
   cd ../site-php-1
   ```

   Vous pouvez continuer à travailler sur la branche `main` ici, tandis que les modifications dans `feature-X` sont séparées dans l'autre répertoire.

---

### **Étape 4 : Supprimer un répertoire de travail avec `git worktree`**

Une fois que vous avez terminé votre travail dans le répertoire de travail `feature-X`, vous pouvez le supprimer.

1. **Supprimer le worktree** :

   Pour supprimer le répertoire de travail `feature-X`, tapez la commande suivante :

   ```bash
   git worktree remove ../feature-X
   ```

   Cette commande supprime le répertoire de travail tout en conservant l'historique Git dans le dépôt principal.

---

### **Étape 5 : Lister les répertoires de travail actifs**

Vous pouvez lister tous les worktrees actifs dans votre projet Git avec la commande suivante :

```bash
git worktree list
```

Cela affichera tous les répertoires de travail associés au dépôt, ainsi que la branche qui est utilisée dans chaque répertoire.

---

### **Étape 6 : Résumé des commandes `git worktree`**

1. **Créer un nouveau répertoire de travail pour une branche** :
   ```bash
   git worktree add ../feature-X feature-X
   ```

2. **Lister tous les répertoires de travail actifs** :
   ```bash
   git worktree list
   ```

3. **Supprimer un répertoire de travail** :
   ```bash
   git worktree remove ../feature-X
   ```

---

### **Conclusion**

Ce guide vous a montré comment utiliser **`git worktree`** pour travailler sur plusieurs branches en parallèle sans avoir à changer constamment de branche dans un seul répertoire. Cette fonctionnalité est très utile pour tester des branches différentes, travailler sur des corrections de bugs ou des fonctionnalités séparées, et garder vos environnements de travail propres et organisés.

Avec `git worktree`, vous pouvez travailler de manière plus flexible et éviter les interruptions de flux de travail lorsque vous devez passer d'une tâche à une autre.
