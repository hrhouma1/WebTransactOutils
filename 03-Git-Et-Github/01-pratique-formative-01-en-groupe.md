# **TP #1 : La Chasse au Trésor Git — 200 Manipulations Git**

### **Contexte :**
Vous allez travailler sur un dépôt partagé où chaque étudiant crée une énigme. Le but est d'apprendre à utiliser Git dans un cadre collaboratif tout en manipulant diverses fonctionnalités : création de branches, pull requests, résolution de conflits, rebase, merge, etc.

### **Prérequis :**
- Connaissance basique de Git
- Clé SSH configurée
- Accès au dépôt **La Chasse au Trésor**

---

## **Étape 1 : Clonage du dépôt et configuration initiale (20 manipulations)**

1. **Tous les étudiants :** Commencez par cloner le dépôt GitHub sur vos machines locales.
   
   ```bash
   git clone git@github.com:hrhouma/ChasseAuTresor.git
   cd ChasseAuTresor
   ```

2. **Configuration de l'utilisateur :** Assurez-vous que votre configuration Git est correcte (votre nom et votre email).

   ```bash
   git config --global user.name "Votre Nom"
   git config --global user.email "votre.email@example.com"
   ```

3. **Vérification de la connexion à GitHub via SSH :**
   
   ```bash
   ssh -T git@github.com
   ```

4. **Vérifiez l'état de votre dépôt local :**
   
   ```bash
   git status
   git branch
   ```

5. **Affichez les dernières modifications du projet :**
   
   ```bash
   git log --oneline --graph --decorate --all
   ```

---

## **Étape 2 : Création et gestion des branches (30 manipulations)**

1. **Chaque étudiant crée une nouvelle branche pour son énigme :**

   - **Étudiant01 (Marc)** :
     ```bash
     git checkout -b enigme_Marc
     ```

   - **Étudiant02 (Léa)** :
     ```bash
     git checkout -b enigme_Lea
     ```

   Continuez ainsi pour chaque étudiant.

2. **Vérifiez que vous êtes sur la bonne branche avec :**

   ```bash
   git branch
   ```

3. **Renommez une branche existante (juste pour la pratique) :**

   ```bash
   git branch -m nouvelle_branche
   ```

4. **Listez toutes les branches (locales et distantes) :**
   
   ```bash
   git branch -a
   ```

---

## **Étape 3 : Création des énigmes et commit initial (40 manipulations)**

1. **Créez un fichier texte pour votre énigme :**

   - **Marc** :
     ```bash
     echo "Je vole sans ailes. Je pleure sans yeux. Qui suis-je ?" > Marc.txt
     ```

   - **Léa** :
     ```bash
     echo "Je suis plein la journée, vide la nuit. Qui suis-je ?" > Lea.txt
     ```

   - Continuez ainsi pour chaque étudiant.

2. **Ajoutez votre fichier au suivi Git (staging) :**

   ```bash
   git add Marc.txt
   ```

3. **Vérifiez les fichiers suivis et non suivis :**

   ```bash
   git status
   ```

4. **Créez un commit pour enregistrer vos modifications :**

   ```bash
   git commit -m "Ajout de l'énigme de Marc"
   ```

5. **Affichez l'historique des commits avec les différences :**

   ```bash
   git log -p
   ```

---

## **Étape 4 : Pousser votre branche et créer une Pull Request (20 manipulations)**

1. **Poussez votre branche sur le dépôt distant :**

   ```bash
   git push origin enigme_Marc
   ```

   Répétez cela pour tous les étudiants.

2. **Accédez à GitHub et créez une Pull Request :**
   - Vous allez fusionner votre branche `enigme_[Nom]` avec la branche `main`.

3. **Inspectez vos branches distantes :**

   ```bash
   git branch -r
   ```

4. **Supprimez une branche locale (après fusion, par exemple) :**

   ```bash
   git branch -d enigme_Marc
   ```

---

## **Étape 5 : Synchronisation avec le dépôt (30 manipulations)**

1. **Mettez à jour votre dépôt local avec les dernières modifications de `main` :**

   ```bash
   git fetch origin
   git pull origin main
   ```

2. **Examinez les différences entre votre branche locale et `main` :**

   ```bash
   git diff main
   ```

3. **Fusionnez la branche `main` dans votre branche si nécessaire :**

   ```bash
   git merge main
   ```

4. **Résolvez les conflits si nécessaire (voir Étape 7 pour plus de détails).**

5. **Réaffichez le statut après la synchronisation :**

   ```bash
   git status
   ```

---

## **Étape 6 : Résolution d'énigmes et ajout de réponses (20 manipulations)**

1. **Chaque étudiant résout une énigme créée par un camarade.**

   - **Marc** : Ajoute ta réponse à l'énigme de Léa.
     
     ```bash
     echo "Réponse de Marc : un sac" >> Lea.txt
     git add Lea.txt
     git commit -m "Marc résout l'énigme de Léa"
     git push origin main
     ```

   - **Léa** : Ajoute ta réponse à l'énigme de Marc.
     
     ```bash
     echo "Réponse de Léa : une larme" >> Marc.txt
     git add Marc.txt
     git commit -m "Léa résout l'énigme de Marc"
     git push origin main
     ```

   **Répétez cette procédure pour chaque étudiant.**

---

## **Étape 7 : Gestion des conflits (30 manipulations)**

1. **Création d’un conflit garanti :**

   - **Marc** et **Paul** travaillent tous deux sur le fichier `Lea.txt` sans se synchroniser.

   - **Marc** :
     ```bash
     echo "Réponse de Marc : une armoire" >> Lea.txt
     git add Lea.txt
     git commit -m "Marc résout l'énigme de Léa"
     ```

   - **Paul** :
     ```bash
     echo "Réponse de Paul : un lit" >> Lea.txt
     git add Lea.txt
     git commit -m "Paul résout l'énigme de Léa"
     ```

2. **Professeur (moi) :** Lorsque je tente de fusionner ces branches, un conflit apparaît. Vous allez le résoudre ensemble.

3. **Affichage des conflits dans Git :**

   ```bash
   git merge enigme_Marc
   # Conflit détecté !
   ```

4. **Résolution manuelle du conflit :**

   ```bash
   nano Lea.txt
   ```

   Vous devrez conserver les deux réponses et ajuster le fichier.

5. **Ajoutez et commitez la résolution :**

   ```bash
   git add Lea.txt
   git commit -m "Résolution du conflit entre Marc et Paul"
   ```

---

## **Étape 8 : Rebase et Squash (30 manipulations)**

1. **Rebase :** Pour maintenir un historique linéaire, vous allez rebaser votre branche sur `main`.

   - **Marc** :
     ```bash
     git checkout enigme_Marc
     git rebase main
     ```

   - **Vérifiez les résultats du rebase :**

     ```bash
     git log --oneline --graph
     ```

2. **Squash :** Combinez plusieurs commits en un seul pour simplifier l’historique de votre branche.

   ```bash
   git rebase -i HEAD~3
   # Sélectionnez 'squash' pour les commits que vous voulez combiner
   ```

---

## **Étape 9 : Utilisation avancée de Git (30 manipulations)**

1. **Utilisation de `git stash` :** Sauvegardez temporairement votre travail sans faire de commit.
   
   ```bash
   git stash
   git stash list
   git stash apply
   ```

2. **Affichage des différences dans des fichiers spécifiques :**
   
   ```bash
   git diff Lea.txt
   ```

3. **Utilisation de `git cherry-pick` pour appliquer un commit spécifique :**

   ```bash
   git cherry-pick <commit-hash>
   ```

4. **Gestion des tags :** Créez un tag pour marquer une version importante.
   
   ```bash
   git tag -a v1.0 -m "Version 1.0"
   git push origin v1.0
   ```

---

## **Étape 10 : Conclusion et bonnes pratiques (20 manipulations)**



1. **Nettoyage des branches locales et distantes :**

   ```bash
   git branch -d enigme_Marc
   git push origin --delete enigme_Marc
   ```

2. **Examinez et révisez l’historique de votre dépôt :**

   ```bash
   git log --stat
   ```

3. **Utilisez `git reflog` pour revoir toutes vos actions récentes :**

   ```bash
   git reflog
   ```

4. **Partagez votre expérience avec l’équipe :**

   ```bash
   git push origin main
   ```

---

## **Objectif atteint : 200 manipulations Git**

À travers cet exercice, vous avez appris à utiliser Git de manière collaborative, en réalisant au moins 200 manipulations. Vous avez exploré les branches, les conflits, les pull requests, le rebase, et bien plus encore.
