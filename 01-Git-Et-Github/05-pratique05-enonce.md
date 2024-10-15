# TP #1 : La Chasse au Trésor Git

## Contexte

Dans ce projet, chaque étudiant contribuera à un dépôt Git partagé appelé **"La Chasse au Trésor"**. Le but est de placer des indices (ou des énigmes) dans le dépôt, que les autres étudiants devront résoudre pour progresser dans la chasse. Chaque indice mène au suivant. Les étudiants devront collaborer, résoudre des conflits Git, et interagir avec le dépôt tout en s'amusant !

## Prérequis

- Connaissance de base de Git
- Accès au dépôt Git du projet "La Chasse au Trésor"
- Token fourni par le professeur

## Instructions

### 1. Préparation

- Clonez le dépôt :
  ```bash
  git clone https://github.com/hrhouma/ChasseAuTresor.git
  ```
- Placez-vous dans le répertoire du projet :
  ```bash
  cd ChasseAuTresor
  ```

### 2. Création de votre Énigme

- Basculez vers une nouvelle branche avec votre nom :
  ```bash
  git checkout -b enigme_[votreNom]
  ```
- Créez un nouveau fichier avec votre nom :
  ```bash
  nano [votreNom].txt
  ```
- Écrivez une énigme amusante et sauvegardez.

### 3. Publication de votre Énigme

- Ajoutez et validez votre énigme :
  ```bash
  git add [votreNom].txt 
  git commit -m "Ajout de l'énigme de [votreNom]"
  ```
- Poussez votre branche vers le dépôt distant :
  ```bash
  git push origin enigme_[votreNom]
  ```

### 4. Création d'une Pull Request

- Accédez à votre dépôt GitHub et créez une pull request pour que votre branche soit fusionnée avec la branche `main`.
- Attendez que le chef de projet examine et fusionne votre pull request.

### 5. Résolution d'Épreuves

- Après que le chef de projet a fusionné votre pull request, basculez vers la branche `main` :
  ```bash
  git checkout main
  ```
- Mettez à jour votre branche :
  ```bash
  git pull origin main
  ```
- Tentez de résoudre au moins une énigme ajoutée par un camarade de classe. Lorsque vous trouvez la réponse, ajoutez-la à la fin du fichier correspondant.

### 6. Scénario de Conflit

- Imaginez que plusieurs étudiants travaillent simultanément sur le même fichier et que des conflits surviennent lors de la fusion des branches via une pull request. Le but est d'expérimenter la gestion des conflits Git dans un cadre collaboratif.

## Objectifs d'Apprentissage

- Comprendre les bases du travail collaboratif avec Git et GitHub.
- Expérimenter le processus de résolution de conflits.
- Encourager la communication et la collaboration entre étudiants.
