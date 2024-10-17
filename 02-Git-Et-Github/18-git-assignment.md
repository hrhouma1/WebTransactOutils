# 18 git assignment


### **Objectif :**
L’objectif de cet assignement est de tester votre compréhension et vos compétences dans l’utilisation des différentes commandes Git. Vous allez simuler un projet en plusieurs étapes qui nécessite l’utilisation des branches, des commits, des fusions, des tags, et des outils comme `stash`, `cherry-pick`, `reset`, et `rebase`. Vous devrez également synchroniser votre travail avec un dépôt distant (GitHub).

---

### **Étape 1 : Cloner le projet et préparer l’environnement**

1. **Cloner le projet depuis GitHub :**

   Pour commencer, vous devez cloner le projet depuis GitHub pour avoir un environnement de travail local.

   ```bash
   git clone https://github.com/hrhouma1/site-php-1.git
   ```

2. **Entrer dans le répertoire du projet :**

   Accédez au répertoire du projet cloné.

   ```bash
   cd site-php-1
   ```

---

### **Étape 2 : Configurer les branches de base**

1. **Créer deux nouvelles branches** :

   Créez deux branches pour travailler simultanément sur des fonctionnalités distinctes.

   ```bash
   git checkout -b feature-login
   git checkout -b feature-dashboard
   ```

2. **Modifications sur les branches :**

   - Sur la branche `feature-login`, modifiez `app.js` pour ajouter une fonctionnalité de connexion.
   - Sur la branche `feature-dashboard`, modifiez `index.php` pour ajouter un tableau de bord.

3. **Ajouter et committer les modifications dans chaque branche** :

   - Dans `feature-login` :
     ```bash
     git add app.js
     git commit -m "Ajout de la fonctionnalité login"
     ```

   - Dans `feature-dashboard` :
     ```bash
     git add index.php
     git commit -m "Ajout du tableau de bord"
     ```

---

### **Étape 3 : Fusionner et gérer les branches**

1. **Basculer sur la branche `main` et fusionner `feature-login`** :

   Revenez à la branche `main` et fusionnez `feature-login`.

   ```bash
   git checkout main
   git merge feature-login
   ```

2. **Utiliser `git rebase` pour appliquer `feature-dashboard`** :

   Au lieu de fusionner, rebasez `feature-dashboard` sur `main` pour maintenir un historique propre.

   ```bash
   git checkout feature-dashboard
   git rebase main
   ```

   Si un conflit survient, résolvez-le manuellement et continuez le rebase.

3. **Fusionner `feature-dashboard` dans `main`** :

   Basculez sur `main` et fusionnez la branche `feature-dashboard`.

   ```bash
   git checkout main
   git merge feature-dashboard
   ```

---

### **Étape 4 : Utiliser `git stash` pour sauvegarder les modifications en cours**

Supposons que vous travaillez sur une nouvelle fonctionnalité mais que vous devez passer temporairement à une autre tâche.

1. **Créer une nouvelle branche et commencer des modifications** :

   Créez une branche `feature-payment` et commencez à modifier `payment.php`.

   ```bash
   git checkout -b feature-payment
   ```

2. **Stasher les modifications** :

   Avant de basculer sur une autre branche, stashez les modifications non committées.

   ```bash
   git stash
   ```

3. **Récupérer les modifications plus tard avec `git stash pop`** :

   Après avoir terminé d'autres tâches, récupérez vos modifications.

   ```bash
   git stash pop
   ```

---

### **Étape 5 : Utiliser `git cherry-pick` pour appliquer des commits spécifiques**

1. **Créer une nouvelle branche `feature-report`** :

   Basculez sur la branche `main` et créez une nouvelle branche.

   ```bash
   git checkout main
   git checkout -b feature-report
   ```

2. **Lister les commits sur une autre branche** :

   Lister les commits de la branche `feature-dashboard` et choisissez un commit à appliquer.

   ```bash
   git log --oneline
   ```

3. **Appliquer un commit spécifique avec `git cherry-pick`** :

   Sélectionnez un commit et appliquez-le sur `feature-report`.

   ```bash
   git cherry-pick <commit_id>
   ```

---

### **Étape 6 : Taguer des versions de release**

1. **Créer un tag annoté pour une version release** :

   Lorsque vous êtes satisfait de l'état actuel du projet, taguez le commit comme étant la version 1.0.

   ```bash
   git tag -a v1.0 -m "Version 1.0 - Release initiale"
   ```

2. **Pousser le tag vers GitHub** :

   Envoyez ce tag vers GitHub.

   ```bash
   git push origin v1.0
   ```

---

### **Étape 7 : Utiliser `git worktree` pour travailler sur plusieurs branches**

1. **Créer un nouveau répertoire de travail pour une branche** :

   Utilisez `git worktree` pour créer un répertoire de travail distinct pour `feature-testing`.

   ```bash
   git worktree add ../feature-testing feature-testing
   ```

2. **Travailler dans ce répertoire** :

   Allez dans le répertoire `feature-testing` et apportez des modifications.

   ```bash
   cd ../feature-testing
   ```

---

### **Étape 8 : Réinitialiser des modifications avec `git reset` et `git revert`**

1. **Utiliser `git reset` pour réinitialiser des commits** :

   Supposons que vous avez committé quelque chose par erreur. Utilisez `git reset` pour annuler les derniers commits sans les supprimer.

   ```bash
   git reset --soft HEAD~1
   ```

2. **Utiliser `git revert` pour annuler un commit** :

   Si vous devez annuler un commit tout en conservant l'historique, utilisez `git revert`.

   ```bash
   git revert <commit_id>
   ```

---

### **Étape 9 : Pousser et synchroniser avec GitHub**

1. **Pousser les branches locales** :

   Poussez toutes les modifications de la branche `main` et des autres branches vers GitHub.

   ```bash
   git push origin main
   git push origin feature-login
   git push origin feature-dashboard
   ```

2. **Utiliser `git pull` pour synchroniser les dernières modifications** :

   Récupérez les modifications distantes si d'autres collaborateurs ont fait des modifications sur GitHub.

   ```bash
   git pull origin main
   ```

---

### **Étape 10 : Résumé des commandes dans cet assignment**

- **Créer et gérer des branches** : `git checkout -b <branch_name>`, `git merge`, `git rebase`
- **Travailler sur plusieurs répertoires avec `worktree`** : `git worktree add`, `git worktree list`
- **Gérer des modifications non committées** : `git stash`, `git stash pop`
- **Appliquer des commits spécifiques** : `git cherry-pick`
- **Créer et pousser des tags** : `git tag -a <tag_name> -m "message"`, `git push origin --tags`
- **Réinitialiser et annuler des commits** : `git reset`, `git revert`
- **Synchroniser avec GitHub** : `git push`, `git pull`

---

### **Conclusion**

Cet assignement est conçu pour vous faire pratiquer l'ensemble des commandes Git apprises dans vos cours précédents. Il vous permet de gérer efficacement des branches, des commits, des tags, ainsi que de naviguer entre les répertoires de travail. Assurez-vous de suivre chaque étape et de bien comprendre les raisons pour lesquelles chaque commande est utilisée, car cela vous préparera à travailler sur des projets Git plus complexes en équipe.
