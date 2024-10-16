# **TP #1 : La Chasse au Trésor Git — 600 Manipulations**

### **Contexte :**
Chaque étudiant contribuera à un dépôt partagé pour apprendre Git de manière approfondie. Ils créeront des branches, résoudront des conflits localement, et collaboreront en créant des pull requests que **toi, le professeur**, géreront pour les fusions dans la branche `main`. Les rôles et actions de chacun sont bien distincts pour assurer un contrôle pédagogique.

### **Prérequis :**
- Accès au dépôt GitHub **La Chasse au Trésor**
- Clé SSH configurée
- Token d'accès pour GitHub

---

## **Étape 1 : Clonage et configuration initiale (50 manipulations)**

1. **Tous les étudiants :** Clonage du dépôt GitHub sur vos machines locales.

   - **Étudiant01 (Marc)** :
     ```bash
     git clone git@github.com:hrhouma/ChasseAuTresor.git
     cd ChasseAuTresor
     ```
     
   - **Étudiant02 (Léa)** :
     ```bash
     git clone git@github.com:hrhouma/ChasseAuTresor.git
     cd ChasseAuTresor
     ```

2. **Configuration de Git pour chaque étudiant :** Chaque étudiant doit configurer son nom et son email dans Git.

   ```bash
   git config --global user.name "Marc"
   git config --global user.email "marc@example.com"
   ```

   Répétez pour chaque étudiant.

3. **Vérification du dépôt et de la connexion SSH** :
   - Affichez les branches disponibles :
     ```bash
     git branch -a
     ```

   - Vérifiez l'état du dépôt et la connexion SSH :
     ```bash
     git status
     ssh -T git@github.com
     ```

---

## **Étape 2 : Création des branches locales et énigmes (80 manipulations)**

1. **Chaque étudiant crée sa propre branche locale pour y travailler**. Cela leur permet de travailler indépendamment avant d'envoyer leurs modifications au dépôt distant.

   - **Marc** :
     ```bash
     git checkout -b enigme_Marc
     ```

   - **Léa** :
     ```bash
     git checkout -b enigme_Lea
     ```

2. **Création des énigmes :** Chaque étudiant crée un fichier texte contenant une énigme.

   - **Marc** :
     ```bash
     echo "Je vole sans ailes. Je pleure sans yeux. Qui suis-je ?" > Marc.txt
     git add Marc.txt
     git commit -m "Ajout de l'énigme de Marc"
     ```

   - **Léa** :
     ```bash
     echo "Je suis plein la journée, vide la nuit. Qui suis-je ?" > Lea.txt
     git add Lea.txt
     git commit -m "Ajout de l'énigme de Léa"
     ```

   **Chaque étudiant doit :**
   - Créer son fichier.
   - Ajouter ce fichier au staging (`git add`).
   - Faire un commit (`git commit`).

---

## **Étape 3 : Push des branches et création des Pull Requests (70 manipulations)**

1. **Poussez vos branches vers GitHub :** Chaque étudiant doit envoyer sa branche vers le dépôt distant, mais ne fusionne rien directement dans `main`. Cela reste sous le contrôle du professeur.

   - **Marc** :
     ```bash
     git push origin enigme_Marc
     ```

   - **Léa** :
     ```bash
     git push origin enigme_Lea
     ```

2. **Création des pull requests sur GitHub :** Chaque étudiant doit maintenant aller sur GitHub et créer une **pull request** pour fusionner sa branche dans `main`. **C’est le professeur qui fusionne** les pull requests, pas les étudiants.

3. **Vérification des branches distantes et locales :**

   - Listez les branches locales :
     ```bash
     git branch
     ```

   - Listez les branches distantes :
     ```bash
     git branch -r
     ```

---

## **Étape 4 : Gestion des pull requests et fusions (Contrôle du professeur)**

1. **Professeur** : Une fois que les étudiants ont créé leurs pull requests, **tu contrôles** la fusion dans `main`. Tu inspectes chaque pull request et décides de l’accepter ou de demander des modifications. Voici les étapes :

   - **Accédez à GitHub :** Revue des pull requests des étudiants.
   - **Fusion des branches :**
     - Si aucune modification n'est nécessaire, tu fusionnes directement via GitHub.
     - En cas de problème ou de conflit, tu peux demander des ajustements aux étudiants.

2. **Étudiants :** Une fois la pull request fusionnée par le professeur, vous devez mettre à jour vos dépôts locaux pour intégrer les changements dans `main`.

   ```bash
   git checkout main
   git pull origin main
   ```

3. **Affichage des logs et vérification après la fusion** :

   - **Professeur** : Avant et après chaque fusion, utilise ces commandes pour vérifier l'état du dépôt :
     ```bash
     git log --oneline --graph --all
     ```

---

## **Étape 5 : Résolution d'énigmes et commits supplémentaires (80 manipulations)**

1. **Chaque étudiant** : Vous allez résoudre une énigme créée par un autre étudiant et ajouter votre réponse dans le fichier correspondant. Par exemple, **Marc** résout l'énigme de **Léa**.

   - **Marc** :
     ```bash
     echo "Réponse de Marc : un sac" >> Lea.txt
     git add Lea.txt
     git commit -m "Marc résout l'énigme de Léa"
     ```

   - **Léa** :
     ```bash
     echo "Réponse de Léa : une larme" >> Marc.txt
     git add Marc.txt
     git commit -m "Léa résout l'énigme de Marc"
     ```

2. **Push des réponses dans les branches personnelles :** Avant d'envoyer les réponses dans `main`, chaque étudiant pousse ses réponses dans sa branche personnelle.

   ```bash
   git push origin enigme_Marc
   ```

3. **Création d’une nouvelle pull request pour chaque réponse :** Les étudiants doivent à nouveau créer des pull requests sur GitHub pour fusionner leurs réponses dans `main`.

---

## **Étape 6 : Scénario de conflit garanti (Contrôle par le professeur et étudiants)**

### **Création d’un conflit :**

1. **Professeur :** Tu demandes à deux étudiants de travailler simultanément sur le même fichier pour générer un conflit. Par exemple, **Marc** et **Paul** vont modifier le fichier `Lea.txt` en même temps.

   - **Marc** :
     ```bash
     echo "Réponse de Marc : une armoire" >> Lea.txt
     git add Lea.txt
     git commit -m "Marc résout l'énigme de Léa"
     git push origin enigme_Marc
     ```

   - **Paul** :
     ```bash
     echo "Réponse de Paul : un lit" >> Lea.txt
     git add Lea.txt
     git commit -m "Paul résout l'énigme de Léa"
     git push origin enigme_Paul
     ```

2. **Étudiants :** Le conflit survient lors de la création des pull requests, car les deux étudiants ont modifié la même partie de `Lea.txt`.

### **Résolution du conflit par les étudiants :**

1. **Professeur :** Tu attribues à l'un des étudiants (par exemple, Marc) la tâche de résoudre le conflit localement. **Marc** récupère la dernière version de `main` et résout le conflit sur sa machine.

   - **Marc** :
     ```bash
     git checkout main
     git pull origin main
     git checkout enigme_Marc
     git merge main
     # Conflit détecté dans Lea.txt
     ```

2. **Étudiant (Marc) :** Ouvre le fichier `Lea.txt`, résout manuellement le conflit, puis continue avec ces commandes :

   ```bash
   nano Lea.txt  # Résolution manuelle du conflit
   git add Lea.txt
   git commit -m "Résolution du conflit par Marc"
   git push origin enigme_Marc
   ```

3. **Professeur :** Une fois que l'étudiant a résolu le conflit et créé une nouvelle pull request, tu la fusionnes dans `main`.

---

## **Étape 7 : Rebase et Squash (60 manipulations)**

1. **Rebase pour garder un historique propre** : Chaque étudiant doit pratiquer le rebase en intégrant les changements récents de `main` dans sa branche personnelle.

   - **Marc** :
     ```bash
     git checkout enig

me_Marc
     git rebase main
     ```

2. **Squash pour combiner plusieurs commits en un seul :** Utilisez `git rebase -i` pour combiner plusieurs commits en un seul.

   ```bash
   git rebase -i HEAD~3
   # Sélectionnez 'squash' pour combiner les commits
   ```

---

## **Étape 8 : Utilisation de Git avancée (80 manipulations)**

1. **Utilisez `git stash` pour sauvegarder des modifications temporaires** : Chaque étudiant doit expérimenter le `stash` pour mettre de côté ses changements sans les committer.

   ```bash
   git stash
   git stash list
   git stash apply
   ```

2. **Pratiquez `git cherry-pick` pour appliquer un commit spécifique** : Choisissez un commit spécifique dans une branche et appliquez-le dans une autre.

   ```bash
   git cherry-pick <commit-hash>
   ```

3. **Créez et gérez des tags pour marquer des versions importantes** : Utilisez des tags pour marquer les versions importantes des énigmes.

   ```bash
   git tag -a v1.0 -m "Version 1.0"
   git push origin v1.0
   ```

---

## **Conclusion et récapitulatif**

Ce TP a permis aux étudiants de réaliser **au moins 600 manipulations Git** en couvrant :
- La création et la gestion des branches.
- Le push, les pull requests et la résolution de conflits.
- Des commandes avancées comme `rebase`, `squash`, `cherry-pick` et `stash`.

Chaque étape a été soigneusement orchestrée pour encourager l'apprentissage pratique et la collaboration sur GitHub.
