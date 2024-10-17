# 10 git diff command


### **Objectif :**
Ce guide vous apprendra à utiliser la commande `git diff`, qui permet de visualiser les différences entre deux états d'un fichier dans un projet Git. Vous verrez comment cette commande est utile pour comparer les modifications que vous avez apportées avant de les committer.

---

## **Partie 1 : Théorie**

### **Qu'est-ce que `git diff` ?**

- **`git diff`** est une commande Git qui permet de comparer les différences entre différentes versions d'un fichier. Cela peut inclure des modifications locales qui ne sont pas encore committées, des différences entre branches, ou des différences entre des commits dans l'historique.

### **Quand utiliser `git diff` ?**

- **Avant un commit** : Pour vérifier les changements que vous avez effectués dans vos fichiers avant de les ajouter à la zone de staging ou de les committer.
- **Entre branches** : Pour voir les différences entre deux branches avant de les fusionner.
- **Entre commits** : Pour comparer deux commits spécifiques dans l'historique Git.

### **Types de différences que vous pouvez comparer avec `git diff` :**
1. **Différences dans le répertoire de travail** : Comparez les fichiers modifiés mais non ajoutés à la zone de staging.
2. **Différences entre la zone de staging et le répertoire de travail** : Comparez les fichiers dans la zone de staging avec ceux du répertoire de travail.
3. **Différences entre commits** : Comparez des versions différentes de fichiers à travers les commits.

---

## **Partie 2 : Pratique**

Nous allons maintenant voir comment utiliser la commande `git diff` dans le projet **site-php-1** avec plusieurs exemples concrets.

### **Étape 1 : Cloner le projet existant depuis GitHub**

Comme d'habitude, nous allons commencer par cloner le projet **site-php-1** pour travailler dessus.

1. Ouvrez votre terminal et exécutez la commande suivante pour cloner le projet :

   ```bash
   git clone https://github.com/hrhouma1/site-php-1.git
   ```

2. Ensuite, entrez dans le répertoire du projet cloné :

   ```bash
   cd site-php-1
   ```

---

### **Étape 2 : Créer une nouvelle branche pour tester `git diff`**

Nous allons créer une nouvelle branche pour faire des modifications et tester la commande `git diff`.

1. Créez une nouvelle branche appelée `diff-test-branch` :

   ```bash
   git checkout -b diff-test-branch
   ```

---

### **Étape 3 : Faire des modifications dans plusieurs fichiers**

Nous allons faire quelques modifications dans différents fichiers afin de voir comment `git diff` nous permet de visualiser ces différences.

#### **1. Modifier `app.js` :**

1. Ouvrez le fichier `app.js` dans votre éditeur de texte et ajoutez cette ligne au début du fichier :

   ```javascript
   console.log("Test de git diff dans app.js");
   ```

2. **Ne commitez pas encore !** Nous allons comparer les différences dans le répertoire de travail avant d'ajouter le fichier à la zone de staging.

#### **2. Modifier `index.php` :**

1. Ouvrez le fichier `index.php` et ajoutez cette ligne en haut du fichier :

   ```php
   echo "Test de git diff dans index.php";
   ```

2. **Ne commitez pas encore non plus !** Nous utiliserons `git diff` pour voir les différences avant et après l'ajout à la zone de staging.

---

### **Étape 4 : Utiliser `git diff` pour comparer les modifications non ajoutées à la zone de staging**

Nous allons maintenant utiliser `git diff` pour voir les différences dans les fichiers modifiés mais non ajoutés à la zone de staging.

1. Tapez la commande suivante pour voir les différences dans **tous les fichiers modifiés** dans le répertoire de travail :

   ```bash
   git diff
   ```

   Vous verrez les changements que vous avez faits dans `app.js` et `index.php`. Chaque ligne modifiée sera affichée en **rouge** pour les suppressions et en **vert** pour les ajouts.

---

### **Étape 5 : Ajouter les modifications à la zone de staging**

Maintenant, nous allons ajouter les fichiers à la zone de staging pour voir comment `git diff` compare les fichiers dans la zone de staging avec ceux du répertoire de travail.

1. Ajoutez **uniquement `app.js`** à la zone de staging :

   ```bash
   git add app.js
   ```

---

### **Étape 6 : Utiliser `git diff` pour comparer la zone de staging et le répertoire de travail**

Après avoir ajouté `app.js` à la zone de staging, nous allons comparer la différence entre la version dans la zone de staging et la version non ajoutée dans le répertoire de travail.

1. Tapez la commande suivante pour comparer les fichiers dans la zone de staging et les fichiers modifiés dans le répertoire de travail :

   ```bash
   git diff
   ```

   Comme `app.js` est déjà dans la zone de staging, **aucune différence** ne sera affichée pour ce fichier. Cependant, les modifications dans `index.php` (qui ne sont pas encore ajoutées à la zone de staging) seront affichées.

2. Pour comparer uniquement ce qui est dans la zone de staging, utilisez :

   ```bash
   git diff --staged
   ```

   Cette commande vous montrera uniquement les différences des fichiers déjà ajoutés à la zone de staging, comme `app.js`.

---

### **Étape 7 : Utiliser `git diff` entre deux commits**

Nous allons maintenant committer nos modifications, puis comparer les différences entre deux commits spécifiques.

1. **Commettre les modifications** :

   - Ajoutez `index.php` à la zone de staging :
   
     ```bash
     git add index.php
     ```

   - Créez un commit avec les modifications dans `app.js` et `index.php` :
   
     ```bash
     git commit -m "Ajout des modifications dans app.js et index.php pour tester git diff"
     ```

2. **Vérifier l'historique des commits** :

   Tapez la commande suivante pour voir les ID des commits récents :

   ```bash
   git log --oneline
   ```

   Vous verrez les ID des commits récents dans votre dépôt. Choisissez deux commits à comparer.

3. **Comparer deux commits spécifiques** :

   Pour comparer deux commits, utilisez cette commande en remplaçant `<commit1>` et `<commit2>` par les IDs des commits que vous souhaitez comparer :

   ```bash
   git diff <commit1> <commit2>
   ```

   Cette commande vous montrera toutes les différences entre les deux commits spécifiés.

---

### **Étape 8 : Pousser la branche vers GitHub**

Si vous voulez pousser votre branche vers GitHub après avoir expérimenté avec `git diff`, utilisez la commande suivante :

```bash
git push -u origin diff-test-branch
```

Ensuite, vous pouvez créer une **pull request** pour fusionner vos modifications dans la branche principale si nécessaire.

---

## **Résumé des commandes**

1. **Cloner le projet** :
   ```bash
   git clone https://github.com/hrhouma1/site-php-1.git
   cd site-php-1
   ```

2. **Créer une nouvelle branche** :
   ```bash
   git checkout -b diff-test-branch
   ```

3. **Effectuer des modifications dans plusieurs fichiers** :
   - Modifier `app.js` :
     ```javascript
     console.log("Test de git diff dans app.js");
     ```
   - Modifier `index.php` :
     ```php
     echo "Test de git diff dans index.php";
     ```

4. **Utiliser `git diff` pour voir les différences avant d'ajouter à la zone de staging** :
   ```bash
   git diff
   ```

5. **Ajouter des fichiers à la zone de staging** :
   ```bash
   git add app.js
   ```

6. **Utiliser `git diff` pour voir les différences entre la zone de staging et le répertoire de travail** :
   ```bash
   git diff
   ```

7. **Utiliser `git diff` pour comparer uniquement la zone de staging** :
   ```bash
   git diff --staged
   ```

8. **Commettre les modifications** :
   ```bash
   git add index.php
   git commit -m "Ajout des modifications dans app.js et index.php pour tester git diff"
   ```

9. **Comparer deux commits spécifiques** :
   ```bash
   git diff <commit1> <commit2>
   ```

10. **Pousser la branche vers GitHub** :
    ```bash
    git push -u origin diff-test-branch
    ```

---

### **Conclusion**

Ce guide vous a montré comment utiliser la commande `git diff` pour visualiser les différences entre des fichiers modifiés, les fichiers dans la zone de staging, ou entre deux commits. Vous pouvez désormais utiliser `git diff` pour vérifier vos modifications avant de les committer ou pour comparer différentes versions de votre projet.
