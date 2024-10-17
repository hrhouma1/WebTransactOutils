# **TP #3 : La Chasse au Trésor Git**

# **Contexte :**
Dans ce projet, chaque étudiant va travailler de manière autonome sur un dépôt Git individuel. Ils vont simuler une collaboration entre un contributeur local (eux-mêmes) et un autre contributeur distant (leur propre dépôt GitHub) pour réaliser toutes les manipulations Git. Vous jouerez donc deux rôles : **vous-même localement** et **vous-même sur GitHub**.

---

# **Étape 1 : Configuration initiale et génération de clé SSH (Professeur et Étudiant)**

## **Professeur (moi) :**
Je vous fournis un dépôt GitHub vide que vous allez cloner sur vos machines. Vous allez aussi configurer Git et générer votre clé SSH pour authentifier vos actions avec GitHub.

## **Vous faites :**

1. **Générez une clé SSH** pour interagir avec GitHub via SSH :
   
   - **Commandes** :
     ```bash
     ssh-keygen -t rsa -b 4096 -C "votre.email@example.com"
     ```

   - Copiez la clé publique SSH dans votre compte GitHub (Paramètres > SSH et GPG Keys > Ajouter une nouvelle clé SSH).

2. **Clonez le dépôt sur votre machine locale** et configurez vos informations Git :
   
   ```bash
   git clone git@github.com:hrhouma1/monsupersite.git
   cd monsupersite
   git config --global user.name "Votre Nom"
   git config --global user.email "votre.email@example.com"
   git config --local user.name "Votre Nom"
   git config --local user.email "votre.email@example.com"
   ```

3. **Vérifiez la connexion SSH à GitHub** :

   ```bash
   ssh -T git@github.com
   ```

4. **Vérifiez l'état de votre dépôt** :

   ```bash
   git status
   ```

---

# **Étape 2 : Simulation de collaboration (Local vs GitHub)**

## **Professeur (moi) :**
Vous allez maintenant créer une branche localement, ajouter des fichiers, et les committer, comme si vous travailliez avec une autre personne distante (GitHub). Vous allez pousser les changements vers GitHub, puis simuler des modifications à distance, comme si une autre personne travaillait sur le même dépôt.

## **Vous faites :**

1. **Créez un fichier sur votre dépôt local et ajoutez-le au staging** :

   ```bash
   touch VotreNom.txt
   echo "Ceci est une énigme : Je suis rond le matin et pointu le soir. Qui suis-je ?" > VotreNom.txt
   git add VotreNom.txt
   git status
   ```

2. **Commitez vos changements localement** :

   ```bash
   git commit -m "Ajout de l'énigme de Votre Nom"
   git log --oneline
   ```

3. **Poussez vos changements vers le dépôt distant sur GitHub** :

   ```bash
   git push origin main
   ```

4. **Simulez une modification à distance (sur GitHub)** :
   - Allez sur GitHub, modifiez le fichier **VotreNom.txt** directement via l'interface web.
   - Ajoutez une nouvelle ligne : "Modifié à distance sur GitHub."

---

# **Étape 3 : Récupération et fusion des modifications distantes (Local)**

## **Professeur (moi) :**
Maintenant, vous allez récupérer les modifications que vous avez simulées sur GitHub, comme si une autre personne avait travaillé à distance. Vous allez les fusionner avec vos modifications locales.

## **Vous faites :**

1. **Récupérez les modifications distantes** :

   ```bash
   git fetch origin
   git log --oneline --graph --all
   ```

2. **Fusionnez les modifications distantes avec votre dépôt local** :

   ```bash
   git pull origin main
   git status
   ```

3. **Résolvez les éventuels conflits (si vous modifiez en local et à distance le même fichier)** :

   ```bash
   git diff
   nano VotreNom.txt  # Résolvez les conflits manuellement si nécessaire
   git add VotreNom.txt
   git commit -m "Résolution du conflit entre local et GitHub"
   git push origin main
   ```

4. **Vérifiez l'historique de vos modifications** :

   ```bash
   git log --oneline --graph
   ```

---

# **Étape 4 : Création et gestion des branches locales et distantes**

## **Professeur (moi) :**
Vous allez maintenant créer des branches localement et les pousser vers GitHub. Cela vous permettra de simuler la gestion de plusieurs fonctionnalités sur des branches séparées, comme si vous travailliez en équipe avec un autre contributeur.

## **Vous faites :**

1. **Créez une nouvelle branche localement** :

   ```bash
   git checkout -b enigme_VotreNom
   ```

2. **Ajoutez un fichier dans cette nouvelle branche et validez-le** :

   ```bash
   echo "Nouvelle énigme dans la branche enigme_VotreNom" > enigme.txt
   git add enigme.txt
   git commit -m "Ajout d'une énigme dans la branche enigme_VotreNom"
   ```

3. **Poussez votre branche vers GitHub** :

   ```bash
   git push origin enigme_VotreNom
   ```

4. **Simulez une modification à distance sur GitHub sur cette branche** :
   - Modifiez **enigme.txt** directement sur GitHub, ajoutez une nouvelle ligne : "Modifié à distance sur GitHub."

5. **Récupérez et fusionnez les modifications distantes dans votre branche locale** :

   ```bash
   git fetch origin
   git checkout enigme_VotreNom
   git pull origin enigme_VotreNom
   ```

6. **Fusionnez cette branche dans `main`** :

   ```bash
   git checkout main
   git merge enigme_VotreNom
   git push origin main
   ```

---

# **Étape 5 : Simulation de conflits et résolution**

## **Professeur (moi) :**
Vous allez maintenant simuler des conflits en modifiant le même fichier localement et sur GitHub. Vous allez résoudre ces conflits manuellement.

## **Vous faites :**

1. **Modifiez le fichier `enigme.txt` localement** :

   ```bash
   echo "Modification locale avant le conflit" >> enigme.txt
   git add enigme.txt
   git commit -m "Modification locale avant le conflit"
   ```

2. **Modifiez également `enigme.txt` directement sur GitHub** :
   - Ajoutez une ligne : "Modification à distance avant le conflit."

3. **Tentez de pousser vos changements locaux et observez le conflit** :

   ```bash
   git push origin enigme_VotreNom
   # Un conflit apparaîtra lorsque vous essayez de pousser
   ```

4. **Résolvez le conflit** :

   ```bash
   git pull origin enigme_VotreNom
   nano enigme.txt  # Résolvez le conflit manuellement
   git add enigme.txt
   git commit -m "Résolution du conflit dans enigme.txt"
   git push origin enigme_VotreNom
   ```

---

# **Étape 6 : Rebase, Squash, et Cherry-pick**

## **Professeur (moi) :**
Pour garder un historique Git propre, vous allez pratiquer le `rebase`, le `squash` et utiliser `cherry-pick` pour appliquer des commits spécifiques d'une branche à une autre.

## **Vous faites :**

1. **Rebase votre branche `enigme_VotreNom` sur `main`** :

   ```bash
   git checkout enigme_VotreNom
   git rebase main
   ```

2. **Squash plusieurs commits en un seul** :

   ```bash
   git rebase -i HEAD~3
   # Choisissez 'squash' pour combiner les commits
   git push origin enigme_VotreNom --force
   ```

3. **Appliquez un commit spécifique d'une branche à une autre avec `cherry-pick`** :

   ```bash
   git checkout main
   git cherry-pick <commit-hash-de-enigme_VotreNom>
   git push origin main
   ```

---

# **Étape 7 : Stash, Tags, et nettoyage des branches**

## **Professeur (moi) :**
Pour gérer efficacement vos modifications temporaires et marquer des versions importantes, vous allez utiliser `git stash` et créer des tags de version.

## **Vous faites :**

1. **Utilisez `git stash` pour sauvegarder des modifications temporaires** :

   ```bash
   git checkout enigme_VotreNom
   echo "Modification temporaire non prête" >> temporaire.txt
   git stash
   git stash list
   ```

2. **Récupérez la modification stashed et commitez-la** :

   ```bash
   git stash apply
   git add temporaire.txt
   git commit -m "Ajout de la modification après restauration du stash"
   git push origin enigme_VotreNom
   ```

3. **Créez un tag pour marquer une version stable** :

   ```bash
   git tag -a v1.0 -m "Version stable 1.0"
   git push origin v1.0
   ```

4. **Nettoyez les branches locales et distantes après fusion** :

   ```bash
   git checkout main
   git branch -d enigme_VotreNom
   git push origin --delete enigme_VotreNom
   ```

---

# **Conclusion :**

En réalisant ces étapes, vous aurez complété les aspects suivants :
- Clonage, configuration, et gestion des clés SSH.
- Création et fusion de branches locales et distantes.
- Simulation de conflits et résolution manuelle.
- Utilisation de `rebase`, `squash`, `cherry-pick`, `stash`, et gestion des tags.

**Professeur (moi) :**
Je vais maintenant vérifier que toutes vos manipulations ont été correctement effectuées en validant vos dépôts sur GitHub. Vous avez ainsi simulé efficacement une collaboration tout en travaillant individuellement.
