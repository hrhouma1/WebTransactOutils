-----------
# Divers - partie 01 (supression d'un fichier)
-----------

### Exercice Git : Récupérer un Fichier Supprimé dans un Dépôt GitHub

Bonjour à tous,

Pour cet exercice, je vais vous guider pas à pas. L'objectif est d'apprendre comment utiliser l'historique Git pour récupérer un fichier supprimé dans un dépôt collaboratif. Voici les étapes à suivre :

---

#### Contexte
1. **Création du dépôt**  
   - J'ai créé un dépôt sur GitHub avec plusieurs fichiers, dont certains contiennent des informations importantes pour votre travail.

2. **Clonage du dépôt**  
   - Pour commencer, vous allez cloner ce dépôt afin d’avoir une copie locale sur votre machine.

3. **Suppression d'un fichier par le professeur**  
   - Une fois que vous avez cloné le dépôt, je vais supprimer un fichier important du dépôt et pousser ce changement. Vous devrez ensuite récupérer ce fichier supprimé en utilisant les outils Git.

---

### Étapes de l'Exercice

#### Étape 1 : Cloner le dépôt GitHub
1. **Ouvrez votre terminal ou interface Git de votre choix**.
2. Clonez le dépôt avec la commande suivante (remplacez `<url_du_depot>` par l'URL du dépôt que je vous fournirai) :
   ```bash
   git clone <url_du_depot>
   ```
3. Une fois le dépôt cloné, naviguez dans le répertoire du dépôt local :
   ```bash
   cd <nom_du_dossier_du_depot>
   ```

---

#### Étape 2 : Vérification du contenu du dépôt
- Vous verrez plusieurs fichiers dans ce dépôt, notamment un fichier `file2.txt` (ou un autre fichier qui sera supprimé plus tard).
- Familiarisez-vous avec le contenu du dépôt et vérifiez bien la présence du fichier.

---

#### Étape 3 : Mise à jour du dépôt après la suppression
1. **Suppression du fichier par le professeur**  
   - Je vais maintenant supprimer un fichier dans le dépôt GitHub et pousser ce changement. Vous serez informés une fois la suppression effectuée.
   
2. **Mise à jour locale**  
   - Pour voir cette suppression dans votre dépôt local, exécutez la commande suivante pour synchroniser votre dépôt local avec le dépôt GitHub :
     ```bash
     git pull
     ```
   - Après cette opération, vous constaterez que le fichier a été supprimé dans votre dépôt local.

---

#### Étape 4 : Récupérer le fichier supprimé
1. **Trouver l'ID du commit**  
   - Pour récupérer le fichier supprimé, il nous faut le dernier commit où le fichier existait encore.
   - Utilisez la commande suivante pour afficher l'historique des commits et identifier le commit précédant la suppression :
     ```bash
     git log
     ```
   - Trouvez l’ID du commit où le fichier supprimé était encore présent (juste avant le commit de suppression).

2. **Récupérer le fichier à l'aide de Git**  
   - Utilisez la commande suivante en remplaçant `<commit_id>` par l'ID du commit identifié et `<nom_du_fichier>` par le nom du fichier supprimé (par exemple, `file2.txt`) :
     ```bash
     git checkout <commit_id> -- <nom_du_fichier>
     ```
   - Cette commande ramènera le fichier supprimé dans votre version locale.

---

#### Étape 5 : Vérification
- Une fois le fichier restauré, vérifiez qu'il est bien réapparu dans votre répertoire local.
- Vous pouvez également faire un `git status` pour voir l'état de votre dépôt et constater que le fichier est de retour dans la zone de travail.

---

#### Résultat attendu
À la fin de cet exercice, vous devriez être capables de :
- Utiliser `git log` pour retrouver l'historique des commits.
- Utiliser `git checkout <commit_id> -- <nom_du_fichier>` pour récupérer un fichier supprimé à partir d'un commit antérieur.

### Questions à Répondre
1. **Quelles étapes avez-vous suivies pour récupérer le fichier ?**
2. **Pourquoi est-il important de connaître ces commandes lors d’un travail collaboratif ?**



---------------
# Divers - partie 02 (supression d'un dossier)
---------------


### Exercice Git : Récupérer un Dossier Supprimé dans un Dépôt GitHub

Bonjour à tous,

Dans cet exercice, vous allez apprendre à restaurer un dossier entier supprimé dans un dépôt collaboratif Git. Je vais effectuer la suppression dans le dépôt GitHub, et votre objectif sera de récupérer ce dossier en utilisant les commandes Git.

---

#### Contexte
1. **Création du dépôt**  
   - J'ai mis en place un dépôt GitHub avec plusieurs fichiers et dossiers, dont un dossier nommé `documents`.

2. **Clonage du dépôt**  
   - Vous allez cloner ce dépôt pour l’avoir en local. Une fois que vous aurez terminé cette étape, je vais supprimer le dossier `documents` du dépôt et pousser ce changement.

3. **Récupération du dossier supprimé**  
   - Vous devrez ensuite récupérer ce dossier supprimé en utilisant l'historique Git.

---

### Étapes de l'Exercice

#### Étape 1 : Cloner le dépôt GitHub
1. **Ouvrez votre terminal ou interface Git de votre choix**.
2. Clonez le dépôt en utilisant la commande suivante (remplacez `<url_du_depot>` par l’URL du dépôt) :
   ```bash
   git clone <url_du_depot>
   ```
3. Une fois le dépôt cloné, entrez dans le répertoire du dépôt :
   ```bash
   cd <nom_du_dossier_du_depot>
   ```

---

#### Étape 2 : Vérification du contenu du dépôt
- Dans votre dépôt local, vérifiez la présence du dossier `documents`.
- Familiarisez-vous avec le contenu de ce dossier et notez que ce dossier est crucial pour la suite.

---

#### Étape 3 : Mise à jour après la suppression du dossier par le professeur
1. **Suppression du dossier par le professeur**  
   - Je vais maintenant supprimer le dossier `documents` dans le dépôt GitHub et pousser cette modification. Je vous informerai une fois la suppression terminée.

2. **Synchroniser votre dépôt local avec le dépôt GitHub**  
   - Après que j'ai supprimé le dossier, vous devrez mettre à jour votre copie locale pour refléter cette suppression. Exécutez la commande suivante :
     ```bash
     git pull
     ```
   - Vous verrez que le dossier `documents` a été supprimé de votre copie locale.

---

#### Étape 4 : Récupérer le dossier supprimé
1. **Identifier le commit où le dossier existait encore**  
   - Pour récupérer le dossier, il faut revenir au dernier commit où le dossier `documents` était encore présent.
   - Utilisez cette commande pour voir l'historique des commits :
     ```bash
     git log
     ```
   - Trouvez l’ID du commit juste avant la suppression du dossier.

2. **Récupérer le dossier à l’aide de Git**  
   - Une fois que vous avez l’ID de ce commit, utilisez la commande suivante pour restaurer l'intégralité du dossier `documents` dans votre dépôt local :
     ```bash
     git checkout <commit_id> -- documents
     ```
   - Cela ramènera le dossier `documents` dans votre copie locale.

---

#### Étape 5 : Vérification
- Confirmez que le dossier `documents` est bien restauré en local.
- Exécutez `git status` pour vérifier l’état de votre dépôt et vous assurer que le dossier est bien revenu.

---

#### Résultat attendu
À la fin de cet exercice, vous devriez être capables de :
- Utiliser `git log` pour localiser un commit spécifique.
- Utiliser `git checkout <commit_id> -- <nom_du_dossier>` pour récupérer un dossier supprimé à partir d'un commit antérieur.

### Questions à Répondre
1. **Décrivez les étapes que vous avez suivies pour restaurer le dossier.**
2. **Pourquoi cette méthode est-elle utile dans un projet collaboratif ?**

