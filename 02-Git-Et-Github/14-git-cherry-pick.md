# 14 git cherry pick



### **Objectif :**
Ce guide vous apprendra à utiliser la commande **`git cherry-pick`**, qui permet de sélectionner des commits spécifiques d'une branche pour les appliquer à une autre. Vous apprendrez quand et comment utiliser cette commande dans un projet Git.

---

## **Partie 1 : Théorie**

### **Qu'est-ce que `git cherry-pick` ?**

- **`git cherry-pick`** est une commande Git qui permet d'appliquer un ou plusieurs commits spécifiques d'une branche à une autre sans fusionner toute la branche. Cela peut être utile lorsque vous souhaitez intégrer des modifications précises sans fusionner l'intégralité de l'historique.

### **Quand utiliser `git cherry-pick` ?**

- **Sélection de modifications spécifiques** : Si une branche contient des commits importants que vous voulez appliquer à une autre branche, mais que vous ne souhaitez pas fusionner tout le contenu de la branche, `git cherry-pick` vous permet de le faire.
- **Corrections de bugs** : Lorsque vous avez corrigé un bug dans une branche et que vous voulez appliquer cette correction à d'autres branches sans fusionner toutes les autres modifications.
  
### **Comment fonctionne `git cherry-pick` ?**

- `git cherry-pick` applique un ou plusieurs commits d'une branche source à une autre branche. Chaque commit spécifié par son **ID** sera appliqué à la branche actuelle sans toucher aux autres commits de la branche source.

---

## **Partie 2 : Pratique**

Nous allons maintenant utiliser **`git cherry-pick`** dans le cadre du projet **site-php-1** pour appliquer des commits spécifiques d'une branche à une autre.

### **Étape 1 : Cloner le projet existant depuis GitHub**

Si vous n'avez pas encore de dépôt local, commencez par cloner le projet **site-php-1** depuis GitHub.

1. Ouvrez votre terminal et tapez cette commande pour cloner le projet :

   ```bash
   git clone https://github.com/hrhouma1/site-php-1.git
   ```

2. Entrez dans le répertoire du projet cloné :

   ```bash
   cd site-php-1
   ```

---

### **Étape 2 : Créer deux branches et faire des commits**

Nous allons créer deux branches, `feature-A` et `feature-B`, et faire des commits dans `feature-A` que nous appliquerons ensuite à `feature-B` avec `git cherry-pick`.

1. **Créer la branche `feature-A`** :

   ```bash
   git checkout -b feature-A
   ```

2. **Modifier `app.js` dans `feature-A`** :

   Ouvrez le fichier `app.js` et ajoutez cette ligne :

   ```javascript
   console.log("Modification 1 dans feature-A");
   ```

3. **Ajouter et committer la modification** :

   - Ajoutez le fichier à la zone de staging :
   
     ```bash
     git add app.js
     ```

   - Créez un commit pour cette modification :
   
     ```bash
     git commit -m "Ajout de la modification 1 dans app.js sur feature-A"
     ```

4. **Faire un deuxième commit dans `feature-A`** :

   Faites une deuxième modification dans `app.js` :

   ```javascript
   console.log("Modification 2 dans feature-A");
   ```

5. **Ajouter et committer la modification** :

   - Ajoutez le fichier à la zone de staging :
   
     ```bash
     git add app.js
     ```

   - Créez un commit pour cette modification :
   
     ```bash
     git commit -m "Ajout de la modification 2 dans app.js sur feature-A"
     ```

6. **Créer une nouvelle branche `feature-B`** :

   Maintenant, basculez sur la branche `main` et créez une nouvelle branche `feature-B` :

   ```bash
   git checkout main
   git checkout -b feature-B
   ```

---

### **Étape 3 : Utiliser `git cherry-pick` pour appliquer des commits spécifiques**

Nous allons maintenant appliquer les commits de `feature-A` à `feature-B` en utilisant `git cherry-pick`.

1. **Obtenir l'ID des commits dans `feature-A`** :

   Basculez sur `feature-A` pour voir les commits que vous voulez appliquer à `feature-B` :

   ```bash
   git checkout feature-A
   ```

2. **Lister les commits de `feature-A`** :

   Utilisez la commande suivante pour voir les commits de la branche `feature-A` :

   ```bash
   git log --oneline
   ```

   Vous devriez voir quelque chose comme ceci :

   ```
   a2f5e8d Ajout de la modification 2 dans app.js sur feature-A
   1c8b4f2 Ajout de la modification 1 dans app.js sur feature-A
   ```

3. **Appliquer un commit spécifique avec `git cherry-pick`** :

   Basculez sur `feature-B`, puis appliquez le commit de `feature-A` que vous voulez :

   ```bash
   git checkout feature-B
   git cherry-pick a2f5e8d
   ```

   Cela applique le commit `a2f5e8d` (la modification 2) à la branche `feature-B`.

4. **Vérifier le résultat dans `feature-B`** :

   Ouvrez `app.js` pour vérifier que la modification 2 a bien été appliquée dans `feature-B`.

5. **Appliquer plusieurs commits avec `git cherry-pick`** :

   Si vous voulez appliquer plusieurs commits à la fois, vous pouvez spécifier une plage de commits :

   ```bash
   git cherry-pick 1c8b4f2..a2f5e8d
   ```

   Cela appliquera tous les commits entre `1c8b4f2` et `a2f5e8d` (inclus) à `feature-B`.

---

### **Étape 4 : Gérer les conflits lors du `cherry-pick`**

Si des conflits surviennent pendant le `cherry-pick`, Git vous demandera de les résoudre.

1. **Résoudre le conflit manuellement** :

   Ouvrez les fichiers en conflit dans votre éditeur de texte et résolvez les conflits comme vous le feriez lors d'un merge. Les sections en conflit seront marquées ainsi :

   ```
   <<<<<<< HEAD
   Votre version locale
   =======
   La version du commit que vous appliquez
   >>>>>>> <commit_id>
   ```

   Choisissez quelle version conserver et enregistrez le fichier.

2. **Ajouter les fichiers résolus** :

   Après avoir résolu les conflits, ajoutez les fichiers modifiés à la zone de staging :

   ```bash
   git add <nom_du_fichier>
   ```

3. **Continuer le `cherry-pick`** :

   Après avoir ajouté les fichiers, continuez le `cherry-pick` :

   ```bash
   git cherry-pick --continue
   ```

   Si vous décidez d'abandonner le `cherry-pick` à cause de conflits trop complexes, vous pouvez l'annuler avec :

   ```bash
   git cherry-pick --abort
   ```

---

### **Étape 5 : Pousser les changements vers GitHub**

Après avoir appliqué les commits avec `git cherry-pick`, vous pouvez pousser les modifications vers GitHub.

1. **Pousser la branche `feature-B` vers GitHub** :

   ```bash
   git push origin feature-B
   ```

---

### **Étape 6 : Résumé des commandes `git cherry-pick`**

1. **Créer une nouvelle branche** :
   ```bash
   git checkout -b feature-A
   ```

2. **Voir les commits d'une branche** :
   ```bash
   git log --oneline
   ```

3. **Appliquer un commit spécifique à une autre branche** :
   ```bash
   git cherry-pick <commit_id>
   ```

4. **Appliquer plusieurs commits à une autre branche** :
   ```bash
   git cherry-pick <commit_id1>..<commit_id2>
   ```

5. **Résoudre un conflit lors d'un `cherry-pick`** :
   - Résoudre le conflit dans l'éditeur de texte.
   - Ajouter les fichiers résolus :
     ```bash
     git add <nom_du_fichier>
     ```
   - Continuer le `cherry-pick` :
     ```bash
     git cherry-pick --continue
     ```

6. **Annuler un `cherry-pick`** :
   ```bash
   git cherry-pick --abort
   ```

---

### **Conclusion**

Dans ce guide, vous avez appris à utiliser la commande **`git cherry-pick`** pour appliquer des commits spécifiques d'une branche à une autre sans fusionner toute la branche. Vous avez également vu comment gérer les conflits qui peuvent survenir pendant un `cherry-pick` et comment pousser les modifications vers GitHub.

Cette technique est particulièrement utile lorsque vous devez appliquer des corrections ou des modifications spécifiques à d'autres branches sans inclure toutes les autres modifications. Elle vous permet de travailler avec précision tout en gardant un contrôle total sur les commits que vous appliquez.
