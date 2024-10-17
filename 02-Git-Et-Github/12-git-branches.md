# 12 git branches


### **Objectif :**
Ce guide vous apprendra à utiliser les branches dans Git. Les branches sont un élément essentiel de Git qui vous permettent de travailler sur des fonctionnalités distinctes sans affecter la branche principale de votre projet. Vous apprendrez à créer, changer, fusionner, et supprimer des branches, ainsi qu'à gérer plusieurs branches dans un projet Git.

---

## **Partie 1 : Théorie**

### **Qu'est-ce qu'une branche Git ?**

- **Une branche** est une version parallèle de votre projet. Par défaut, Git utilise la branche principale appelée **`main`**. Vous pouvez créer plusieurs branches pour travailler sur différentes fonctionnalités, puis fusionner ces branches dans `main` une fois que votre travail est terminé et testé.

### **Pourquoi utiliser les branches ?**
- **Travail en parallèle** : Vous pouvez créer une branche pour chaque nouvelle fonctionnalité ou correction de bug sans affecter la version stable de votre projet.
- **Collaboration** : Chaque développeur peut travailler sur sa propre branche, puis fusionner son travail dans `main` ou une autre branche lorsque tout est prêt.
- **Expérimentations** : Les branches permettent d'essayer des idées sans toucher au projet principal.

---

## **Partie 2 : Pratique**

Nous allons maintenant créer plusieurs branches dans le cadre du projet **site-php-1**, et vous apprendrez à manipuler ces branches avec des exemples concrets.

### **Étape 1 : Cloner le projet existant depuis GitHub**

Comme toujours, nous allons commencer par cloner le projet **site-php-1** pour travailler dessus.

1. Ouvrez votre terminal et tapez cette commande pour cloner le projet :

   ```bash
   git clone https://github.com/hrhouma1/site-php-1.git
   ```

2. Ensuite, entrez dans le répertoire du projet cloné :

   ```bash
   cd site-php-1
   ```

---

### **Étape 2 : Créer une nouvelle branche**

Nous allons maintenant créer une nouvelle branche pour travailler sur une nouvelle fonctionnalité, sans toucher à la branche principale.

1. **Créer une nouvelle branche** :

   La commande pour créer une nouvelle branche est :

   ```bash
   git checkout -b feature-1
   ```

   - **`checkout -b`** : Cela crée une nouvelle branche nommée `feature-1` et bascule automatiquement dessus.
   - Vous travaillez maintenant sur une branche distincte, `feature-1`.

2. **Vérifier sur quelle branche vous êtes** :

   Pour voir sur quelle branche vous travaillez, tapez :

   ```bash
   git branch
   ```

   La branche sur laquelle vous êtes actuellement sera marquée avec une étoile (`*`). Vous devriez voir quelque chose comme ceci :

   ```
   * feature-1
     main
   ```

---

### **Étape 3 : Faire des modifications dans la nouvelle branche**

Nous allons maintenant faire des modifications dans la branche `feature-1`.

#### **1. Modifier `app.js` :**

1. Ouvrez le fichier `app.js` et ajoutez cette ligne :

   ```javascript
   console.log("Modification dans feature-1");
   ```

2. **Ajouter les modifications à la zone de staging et créer un commit** :

   - Ajoutez le fichier modifié à la zone de staging :
   
     ```bash
     git add app.js
     ```

   - Créez un commit pour cette modification :

     ```bash
     git commit -m "Ajout de console log dans app.js sur feature-1"
     ```

---

### **Étape 4 : Créer plusieurs branches pour différentes fonctionnalités**

Nous allons maintenant créer d'autres branches pour illustrer comment travailler sur plusieurs fonctionnalités en parallèle.

#### **1. Créer une branche `feature-2` et faire des modifications :**

1. **Créer une nouvelle branche `feature-2`** :

   ```bash
   git checkout -b feature-2
   ```

2. **Modifier `index.php`** :

   Ouvrez le fichier `index.php` et ajoutez cette ligne :

   ```php
   echo "Modification dans feature-2";
   ```

3. **Ajouter et committer les modifications dans `feature-2`** :

   - Ajoutez `index.php` à la zone de staging :

     ```bash
     git add index.php
     ```

   - Créez un commit pour cette modification :

     ```bash
     git commit -m "Ajout d'un echo dans index.php sur feature-2"
     ```

#### **2. Créer une branche `feature-3` et faire des modifications :**

1. **Créer une nouvelle branche `feature-3`** :

   ```bash
   git checkout -b feature-3
   ```

2. **Modifier `connection.php`** :

   Ouvrez le fichier `connection.php` et ajoutez cette ligne :

   ```php
   echo "Modification dans feature-3";
   ```

3. **Ajouter et committer les modifications dans `feature-3`** :

   - Ajoutez `connection.php` à la zone de staging :

     ```bash
     git add connection.php
     ```

   - Créez un commit pour cette modification :

     ```bash
     git commit -m "Ajout d'un echo dans connection.php sur feature-3"
     ```

---

### **Étape 5 : Fusionner les branches dans `main`**

Maintenant que nous avons travaillé sur plusieurs branches, nous allons fusionner certaines de ces branches dans `main`.

1. **Basculer sur la branche principale (`main`)** :

   Avant de fusionner une branche, il faut se positionner sur la branche dans laquelle vous voulez fusionner les changements. Dans ce cas, nous allons fusionner dans `main` :

   ```bash
   git checkout main
   ```

2. **Fusionner `feature-1` dans `main`** :

   Fusionnez la branche `feature-1` dans `main` avec la commande suivante :

   ```bash
   git merge feature-1
   ```

3. **Fusionner `feature-2` dans `main`** :

   Répétez la même commande pour fusionner `feature-2` dans `main` :

   ```bash
   git merge feature-2
   ```

---

### **Étape 6 : Supprimer des branches**

Après avoir fusionné les branches, vous pouvez supprimer les branches locales pour garder votre environnement propre.

1. **Supprimer la branche `feature-1`** :

   ```bash
   git branch -d feature-1
   ```

2. **Supprimer la branche `feature-2`** :

   ```bash
   git branch -d feature-2
   ```

Si vous avez une branche non fusionnée mais que vous voulez tout de même la supprimer, utilisez l'option `-D` pour forcer la suppression :

```bash
git branch -D feature-3
```

---

### **Étape 7 : Pousser les branches vers GitHub**

Maintenant que vous avez travaillé sur vos branches localement, vous pouvez pousser ces modifications vers GitHub.

1. **Pousser les modifications de `main` vers GitHub** :

   Après avoir fusionné les branches dans `main`, poussez les changements sur GitHub :

   ```bash
   git push origin main
   ```

2. **Pousser une branche spécifique (comme `feature-3`) vers GitHub** :

   Si vous voulez pousser une branche spécifique (comme `feature-3`), vous pouvez utiliser cette commande :

   ```bash
   git push -u origin feature-3
   ```

---

### **Étape 8 : Résumé des commandes de gestion des branches**

1. **Créer une nouvelle branche** :
   ```bash
   git checkout -b feature-1
   ```

2. **Vérifier la branche actuelle** :
   ```bash
   git branch
   ```

3. **Basculer vers une autre branche** :
   ```bash
   git checkout main
   ```

4. **Fusionner une branche dans `main`** :
   ```bash
   git merge feature-1
   ```

5. **Supprimer une branche** :
   ```bash
   git branch -d feature-1
   ```

6. **Pousser une branche vers GitHub** :
   ```bash
   git push -u origin feature-3
   ```

---

### **Conclusion**

Ce guide vous a montré comment utiliser les branches dans Git pour travailler sur différentes fonctionnalités en parallèle. Vous avez appris à créer, committer, fusionner, et supprimer des branches. Travailler avec des branches est une pratique essentielle pour maintenir un projet propre et bien organisé, en particulier lorsque plusieurs personnes collaborent sur un même projet.
