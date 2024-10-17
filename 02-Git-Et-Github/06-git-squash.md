# 06 git squash

--------------------------------------------
## Git Squash : Théorie et Pratique
--------------------------------------------

Dans cette section, nous allons apprendre ce qu'est **Git Squash**, à quoi cela sert, et comment l'utiliser dans un projet. Ensuite, nous mettrons cela en pratique sur le projet PHP **site-php-1**.

---

## **Partie 1 : Théorie**

### **Qu'est-ce que Git Squash ?**

Git Squash est une commande qui permet de combiner plusieurs commits en un seul. Cette commande est utile lorsqu’on souhaite simplifier l’historique Git ou regrouper plusieurs petits commits (comme des corrections ou des ajustements) en un seul commit plus propre et plus significatif. Cela est souvent fait avant de pousser les modifications vers un dépôt distant ou avant de fusionner une branche dans la branche principale.

**Quand utiliser Git Squash ?**
- **Nettoyage de l’historique Git** : Si vous avez plusieurs commits mineurs (comme des corrections orthographiques ou des ajustements de code), vous pouvez les regrouper en un seul commit.
- **Avant une pull request** : Il est souvent recommandé de combiner plusieurs commits en un seul avant d’ouvrir une pull request pour garder l’historique propre.
- **Travail en équipe** : Git Squash est souvent utilisé pour simplifier l’historique lors de travaux collaboratifs, notamment avant de fusionner des branches.

**Avantage de Git Squash :**
- Un historique plus propre et plus facile à lire.
- Meilleure organisation des commits (chaque commit ayant un sens plus global).

---

## **Partie 2 : Pratique**

### **Étape 1 : Cloner le projet existant**

Comme d'habitude, nous allons commencer par cloner le projet PHP **site-php-1**. Ouvrez votre terminal et exécutez cette commande pour récupérer le projet :

```bash
git clone https://github.com/hrhouma1/site-php-1.git
```

Ensuite, entrez dans le dossier du projet cloné :

```bash
cd site-php-1
```

### **Étape 2 : Créer une nouvelle branche et faire plusieurs commits**

Nous allons maintenant créer une nouvelle branche pour travailler dessus et faire plusieurs petits commits que nous combinerons ensuite avec Git Squash.

1. **Créer une nouvelle branche** :
   ```bash
   git checkout -b feature/update-functionality
   ```

2. **Effectuer plusieurs petites modifications** :
   
   - **Premier commit** : Ajoutez une ligne dans `app.js` pour afficher un message dans la console :
   
   Ouvrez le fichier `app.js`, puis ajoutez cette ligne au début du fichier :
   ```javascript
   console.log("Premier changement dans app.js");
   ```
   
   Ensuite, ajoutez le fichier et créez un commit :
   ```bash
   git add app.js
   git commit -m "Ajout d'un log dans app.js"
   ```

   - **Deuxième commit** : Ajoutez une autre ligne dans `index.php` :
   
   Ouvrez le fichier `index.php` et ajoutez ceci au début du fichier :
   ```php
   echo "Deuxième modification dans index.php";
   ```

   Ensuite, ajoutez le fichier et créez un commit :
   ```bash
   git add index.php
   git commit -m "Ajout d'un echo dans index.php"
   ```

   - **Troisième commit** : Modifiez encore une fois `connection.php` :
   
   Ouvrez le fichier `connection.php` et changez les informations de connexion (comme vu précédemment). Ensuite, créez un commit :
   ```bash
   git add connection.php
   git commit -m "Mise à jour des informations de connexion"
   ```

### **Étape 3 : Combiner les commits avec Git Squash**

Maintenant que nous avons fait plusieurs petits commits, nous allons les combiner en un seul commit pour avoir un historique plus propre.

1. **Voir l'historique des commits** :

   Avant de faire le squash, regardons l’historique des commits pour voir les trois derniers commits que nous avons créés :
   ```bash
   git log --oneline
   ```

   Vous devriez voir quelque chose comme ceci :
   ```
   3c5e2a1 Mise à jour des informations de connexion
   12a7f4b Ajout d'un echo dans index.php
   9a6e123 Ajout d'un log dans app.js
   ```

2. **Faire le squash des trois derniers commits** :

   Nous allons maintenant combiner ces trois commits en un seul. Pour cela, nous allons utiliser **git rebase** avec l'option **interactive**.

   Exécutez cette commande :
   ```bash
   git rebase -i HEAD~3
   ```

   Cette commande vous montrera les trois derniers commits. Vous allez voir une liste comme ceci dans votre éditeur :

   ```
   pick 9a6e123 Ajout d'un log dans app.js
   pick 12a7f4b Ajout d'un echo dans index.php
   pick 3c5e2a1 Mise à jour des informations de connexion
   ```

   **Modifier la liste pour faire un squash** :
   
   - Changez `pick` en `squash` ou simplement `s` pour les deux derniers commits, comme ceci :
     ```
     pick 9a6e123 Ajout d'un log dans app.js
     squash 12a7f4b Ajout d'un echo dans index.php
     squash 3c5e2a1 Mise à jour des informations de connexion
     ```

   - Enregistrez et fermez l'éditeur.

3. **Éditer le message du commit final** :

   Après avoir fermé l’éditeur, Git vous demandera de modifier le message du nouveau commit combiné. Vous verrez les messages des trois commits précédents, que vous pouvez modifier ou combiner.

   Exemple de message combiné :
   ```
   Ajout de plusieurs fonctionnalités dans app.js, index.php, et connection.php
   - Ajout d'un log dans app.js
   - Ajout d'un echo dans index.php
   - Mise à jour des informations de connexion
   ```

   Enregistrez et fermez l’éditeur pour finaliser le squash.

4. **Vérifier l’historique après le squash** :

   Une fois le squash effectué, vérifiez à nouveau l’historique des commits avec la commande suivante :

   ```bash
   git log --oneline
   ```

   Vous devriez maintenant voir un seul commit qui combine les trois précédents.

### **Étape 4 : Pousser la branche squashed vers GitHub**

Maintenant que nous avons effectué le squash, nous pouvons pousser la branche vers GitHub.

1. **Pousser la branche vers GitHub** :
   ```bash
   git push -u origin feature/update-functionality
   ```

2. **Créer une pull request** :

   Comme dans les étapes précédentes, vous pouvez maintenant créer une pull request sur GitHub pour fusionner ces changements dans la branche principale.

---

## **Résumé des commandes**

1. **Cloner le projet** :
   ```bash
   git clone https://github.com/hrhouma1/site-php-1.git
   cd site-php-1
   ```

2. **Créer une nouvelle branche** :
   ```bash
   git checkout -b feature/update-functionality
   ```

3. **Effectuer plusieurs commits** :
   - `git add app.js`
   - `git commit -m "Ajout d'un log dans app.js"`
   - `git add index.php`
   - `git commit -m "Ajout d'un echo dans index.php"`
   - `git add connection.php`
   - `git commit -m "Mise à jour des informations de connexion"`

4. **Faire un Git Squash** :
   ```bash
   git rebase -i HEAD~3
   ```

5. **Pousser la branche vers GitHub** :
   ```bash
   git push -u origin feature/update-functionality
   ```

---

- Ce guide vous a montré comment utiliser **Git Squash** pour combiner plusieurs commits en un seul, avec un exemple concret sur un projet PHP. 
- Vous pouvez désormais utiliser cette technique pour garder un historique Git propre et bien organisé.
