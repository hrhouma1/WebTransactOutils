# **TP #1 : La Chasse au Trésor Git — 600 Manipulations**

### **Contexte :**
Vous allez participer à un projet Git collaboratif nommé **"La Chasse au Trésor Git"**. Chaque étudiant va jouer un rôle actif dans la gestion de branches, la création d'énigmes, la résolution de conflits, et bien plus encore, tout en travaillant dans un dépôt partagé. Le but est de manipuler Git de manière approfondie et amusante.

---

## **Étape 1 : Clonage et configuration initiale (Professeur et Étudiants)**

### **Professeur (moi) :**
Je vous ai fourni un dépôt GitHub que vous allez cloner sur vos machines pour commencer.

### **Vous faites :**

1. **Tous les étudiants (Léa, Marc, Paul)** : Clonez le dépôt et configurez Git avec vos informations personnelles.

   - **Commandes** :
     ```bash
     git clone git@github.com:hrhouma/ChasseAuTresor.git
     cd ChasseAuTresor
     git config --global user.name "Votre Nom"
     git config --global user.email "votre.email@example.com"
     ```

2. **Vérifiez la connexion SSH à GitHub** :

   ```bash
   ssh -T git@github.com
   ```

3. **Vérifiez les branches et l’état du dépôt** :

   ```bash
   git branch -a
   git status
   ```

---

## **Étape 2 : Création des branches locales et des énigmes**

### **Professeur (moi) :**
Chacun d'entre vous va maintenant créer une branche portant votre nom pour travailler dessus. Vous allez créer une énigme amusante dans un fichier texte qui sera résolu par un autre étudiant.

### **Vous faites :**

1. **Marc crée sa branche et son énigme** :
   
   ```bash
   git checkout -b enigme_Marc
   echo "Qu’est-ce qui est invisible et qui sent mauvais ?" > Marc.txt
   git add Marc.txt
   git commit -m "Ajout de l'énigme de Marc"
   ```

2. **Léa crée sa branche et son énigme** :
   
   ```bash
   git checkout -b enigme_Lea
   echo "Je suis un légume, mais je suis aussi une couleur. Qui suis-je ?" > Lea.txt
   git add Lea.txt
   git commit -m "Ajout de l'énigme de Léa"
   ```

3. **Paul crée sa branche et son énigme** :
   
   ```bash
   git checkout -b enigme_Paul
   echo "Je suis toujours dans le futur mais je n’arrive jamais. Qui suis-je ?" > Paul.txt
   git add Paul.txt
   git commit -m "Ajout de l'énigme de Paul"
   ```

4. **Vérifiez l’historique des commits :**

   ```bash
   git log --oneline --graph
   ```

---

## **Étape 3 : Pousser vos branches vers le dépôt distant**

### **Professeur (moi) :**
Vous allez maintenant pousser vos branches vers le dépôt distant. Ce dépôt contient la branche principale (`main`), et chaque étudiant travaille sur sa propre branche pour éviter les conflits au début.

### **Vous faites :**

1. **Marc pousse sa branche :**

   ```bash
   git push origin enigme_Marc
   ```

2. **Léa pousse sa branche :**

   ```bash
   git push origin enigme_Lea
   ```

3. **Paul pousse sa branche :**

   ```bash
   git push origin enigme_Paul
   ```

4. **Vérifiez les branches distantes :**

   ```bash
   git branch -r
   ```

---

## **Étape 4 : Création des Pull Requests (Professeur)**

### **Professeur (moi) :**
Je vais maintenant fusionner vos branches dans la branche `main`. Vous ne devez pas fusionner directement, mais créer des **pull requests** sur GitHub. Une fois que vous avez créé votre pull request, je vais les examiner et les fusionner.

### **Vous faites :**

1. **Créez une pull request pour votre branche :**
   - **Marc** : crée une pull request pour `enigme_Marc` sur GitHub.
   - **Léa** : crée une pull request pour `enigme_Lea` sur GitHub.
   - **Paul** : crée une pull request pour `enigme_Paul` sur GitHub.

### **Professeur (moi) :**
Je vais maintenant fusionner chaque pull request après avoir examiné vos modifications. Une fois cela fait, vous devrez mettre à jour vos dépôts locaux.

---

## **Étape 5 : Résolution d'énigmes et commits supplémentaires**

### **Professeur (moi) :**
Après la fusion de vos branches dans `main`, chacun d’entre vous va résoudre l’énigme d’un autre étudiant, ajouter la réponse dans le fichier correspondant, puis faire un commit.

### **Vous faites :**

1. **Marc résout l'énigme de Léa :**
   
   ```bash
   git checkout main
   git pull origin main
   echo "Réponse de Marc : la carotte" >> Lea.txt
   git add Lea.txt
   git commit -m "Marc résout l'énigme de Léa"
   git push origin main
   ```

2. **Léa résout l'énigme de Paul :**
   
   ```bash
   git checkout main
   git pull origin main
   echo "Réponse de Léa : demain" >> Paul.txt
   git add Paul.txt
   git commit -m "Léa résout l'énigme de Paul"
   git push origin main
   ```

3. **Paul résout l'énigme de Marc :**
   
   ```bash
   git checkout main
   git pull origin main
   echo "Réponse de Paul : un pet" >> Marc.txt
   git add Marc.txt
   git commit -m "Paul résout l'énigme de Marc"
   git push origin main
   ```

---

## **Étape 6 : Scénario de conflit garanti et résolution**

### **Professeur (moi) :**
Pour vous enseigner comment résoudre des conflits, je vais demander à **Marc** et **Paul** de modifier le même fichier en même temps, ce qui va provoquer un conflit. Vous allez ensuite résoudre ce conflit localement.

### **Vous faites :**

1. **Marc modifie le fichier `Lea.txt` :**

   ```bash
   git checkout enigme_Marc
   echo "Nouvelle réponse de Marc : un brocoli" >> Lea.txt
   git add Lea.txt
   git commit -m "Marc modifie Lea.txt"
   git push origin enigme_Marc
   ```

2. **Paul modifie également le fichier `Lea.txt` :**

   ```bash
   git checkout enigme_Paul
   echo "Nouvelle réponse de Paul : un concombre" >> Lea.txt
   git add Lea.txt
   git commit -m "Paul modifie Lea.txt"
   git push origin enigme_Paul
   ```

3. **Professeur (moi) :** En fusionnant les branches de Marc et Paul dans `main`, un conflit va apparaître. Je vais assigner à **Marc** la tâche de résoudre ce conflit localement.

### **Marc fait :**

1. **Récupérez la dernière version de `main` :**

   ```bash
   git checkout main
   git pull origin main
   ```

2. **Fusionnez votre branche avec `main` et détectez le conflit :**

   ```bash
   git checkout enigme_Marc
   git merge main
   # Conflit détecté dans Lea.txt
   ```

3. **Ouvrez le fichier `Lea.txt`, résolvez manuellement le conflit :**

   ```bash
   nano Lea.txt
   ```

4. **Après avoir résolu le conflit, ajoutez et validez :**

   ```bash
   git add Lea.txt
   git commit -m "Résolution du conflit dans Lea.txt"
   git push origin enigme_Marc
   ```

### **Professeur (moi) :**
Je vais maintenant examiner le travail de **Marc** pour vérifier si le conflit a bien été résolu et fusionner sa branche dans `main`.

---

## **Étape 7 : Rebase et Squash**

### **Professeur (moi) :**
Pour garder l’historique des commits propre, nous allons pratiquer le rebase et le squash. Cela vous permettra de combiner plusieurs commits en un seul.

### **Vous faites :**

1. **Marc intègre les changements récents de `main` dans sa branche avec `rebase` :**

   ```bash
   git checkout enigme_Marc
   git rebase main
   ```

2. **Squash : Combinez plusieurs commits en un seul :**

   ```bash
   git rebase -i HEAD
   ```



### **Étape 7 : Rebase et Squash (suite)**

### **Vous faites :**

1. **Marc combine plusieurs commits en un seul (Squash)** :
   
   ```bash
   git rebase -i HEAD~3
   # Choisissez 'squash' pour les commits que vous voulez combiner
   ```

   **Note** : Marc va maintenant choisir les trois derniers commits et les combiner en un seul pour simplifier l'historique.

2. **Marc vérifie l'historique des commits après le rebase et le squash** :

   ```bash
   git log --oneline --graph
   ```

3. **Léa et Paul font de même pour leurs branches respectives :**

   - **Léa** :
     ```bash
     git checkout enigme_Lea
     git rebase main
     git rebase -i HEAD~3
     ```

   - **Paul** :
     ```bash
     git checkout enigme_Paul
     git rebase main
     git rebase -i HEAD~3
     ```

4. **Une fois que vous avez terminé le rebase et le squash**, poussez vos branches modifiées sur le dépôt distant :

   - **Marc** :
     ```bash
     git push origin enigme_Marc --force
     ```

   - **Léa** et **Paul** font de même :
     ```bash
     git push origin enigme_Lea --force
     git push origin enigme_Paul --force
     ```

### **Professeur (moi) :**
Je vais maintenant examiner vos modifications et vérifier que l’historique des commits est propre après le squash.

---

## **Étape 8 : Utilisation de Git avancée (Stash, Cherry-pick, Tags)**

### **Professeur (moi) :**
Vous allez maintenant explorer des fonctionnalités avancées comme `stash` pour sauvegarder des modifications temporaires, `cherry-pick` pour appliquer des commits spécifiques d'une branche à une autre, et `tags` pour marquer des versions importantes.

### **Vous faites :**

1. **Sauvegardez vos modifications temporaires avec `git stash` :**
   
   - **Marc** :
     ```bash
     git checkout enigme_Marc
     echo "Nouvelle modification temporaire" >> Marc.txt
     git stash
     ```

   - **Vérifiez que la modification a été stashed :**
     ```bash
     git stash list
     ```

   - **Restaurez la modification stashed :**
     ```bash
     git stash apply
     git commit -am "Ajout de la modification après restauration du stash"
     git push origin enigme_Marc
     ```

2. **Appliquez un commit spécifique à une autre branche avec `cherry-pick` :**
   
   - **Paul** veut appliquer un commit spécifique de la branche de Léa :
     ```bash
     git checkout enigme_Paul
     git cherry-pick <commit-hash-de-Lea>
     ```

   - Une fois le commit appliqué, Paul fait un commit supplémentaire pour valider :
     ```bash
     git commit -m "Application du commit de Léa via cherry-pick"
     git push origin enigme_Paul
     ```

3. **Créez et poussez des `tags` pour marquer une version stable du projet :**

   - **Marc** marque une version importante de son projet :
     ```bash
     git tag -a v1.0 -m "Version stable 1.0 de Marc"
     git push origin v1.0
     ```

   - **Léa** et **Paul** créent également leurs tags :
     ```bash
     git tag -a v1.0 -m "Version stable 1.0 de Léa"
     git push origin v1.0

     git tag -a v1.0 -m "Version stable 1.0 de Paul"
     git push origin v1.0
     ```

---

## **Étape 9 : Nettoyage et gestion des branches (Avancé)**

### **Professeur (moi) :**
Maintenant que vous avez terminé la majorité des manipulations, vous allez nettoyer vos branches locales et distantes, et utiliser des fonctionnalités avancées de Git pour explorer davantage.

### **Vous faites :**

1. **Supprimez une branche locale après sa fusion dans `main` :**
   
   - **Marc** :
     ```bash
     git checkout main
     git branch -d enigme_Marc
     ```

   - **Léa** et **Paul** :
     ```bash
     git checkout main
     git branch -d enigme_Lea
     git branch -d enigme_Paul
     ```

2. **Supprimez une branche distante après la fusion (optionnel) :**
   
   ```bash
   git push origin --delete enigme_Marc
   git push origin --delete enigme_Lea
   git push origin --delete enigme_Paul
   ```

3. **Utilisez `git reflog` pour examiner tout l’historique des actions :**

   ```bash
   git reflog
   ```

4. **Vérifiez l’historique complet du dépôt avec des statistiques :**
   
   ```bash
   git log --stat
   ```

5. **Examinez les différences entre les branches avant la suppression :**
   
   ```bash
   git diff enigme_Marc main
   ```

---

## **Conclusion**

Vous avez réalisé **plus de 600 manipulations Git** en couvrant les aspects suivants :
- Création et gestion des branches, des pull requests et des fusions.
- Résolution de conflits localement et au niveau du dépôt distant.
- Utilisation avancée de `rebase`, `squash`, `stash`, `cherry-pick` et `tags`.
- Nettoyage des branches et gestion avancée de l’historique avec `reflog`.

### **Professeur (moi) :**
Je vais maintenant faire un dernier récapitulatif et m’assurer que chaque étape a été bien comprise. Vous avez fait un excellent travail à travers ces multiples manipulations. 





------------------
# Annexe 2 - Toutes les commandes
------------------


### **LEA**

```bash
git clone git@github.com:hrhouma/ChasseAuTresor.git
cd ChasseAuTresor
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
ssh -T git@github.com
git branch -a
git status
git checkout -b enigme_Lea
echo "Je suis un légume, mais je suis aussi une couleur. Qui suis-je ?" > Lea.txt
git add Lea.txt
git commit -m "Ajout de l'énigme de Léa"
git push origin enigme_Lea
git branch -r
git checkout main
git pull origin main
echo "Réponse de Léa : demain" >> Paul.txt
git add Paul.txt
git commit -m "Léa résout l'énigme de Paul"
git push origin main
git checkout enigme_Lea
git rebase main
git rebase -i HEAD~3
git push origin enigme_Lea --force
git stash
git stash list
git stash apply
git add Lea.txt
git commit -am "Ajout de la modification après restauration du stash"
git push origin enigme_Lea
git tag -a v1.0 -m "Version stable 1.0 de Léa"
git push origin v1.0
git checkout main
git branch -d enigme_Lea
git push origin --delete enigme_Lea
git reflog
git log --stat
git diff enigme_Lea main
```

---

### **MARC**

```bash
git clone git@github.com:hrhouma/ChasseAuTresor.git
cd ChasseAuTresor
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
ssh -T git@github.com
git branch -a
git status
git checkout -b enigme_Marc
echo "Qu’est-ce qui est invisible et qui sent mauvais ?" > Marc.txt
git add Marc.txt
git commit -m "Ajout de l'énigme de Marc"
git push origin enigme_Marc
git branch -r
git checkout main
git pull origin main
echo "Réponse de Marc : la carotte" >> Lea.txt
git add Lea.txt
git commit -m "Marc résout l'énigme de Léa"
git push origin main
git checkout enigme_Marc
git rebase main
git rebase -i HEAD~3
git push origin enigme_Marc --force
git stash
git stash list
git stash apply
git add Marc.txt
git commit -am "Ajout de la modification après restauration du stash"
git push origin enigme_Marc
git tag -a v1.0 -m "Version stable 1.0 de Marc"
git push origin v1.0
git checkout main
git branch -d enigme_Marc
git push origin --delete enigme_Marc
git reflog
git log --stat
git diff enigme_Marc main
```

---

### **PAUL**

```bash
git clone git@github.com:hrhouma/ChasseAuTresor.git
cd ChasseAuTresor
git config --global user.name "Votre Nom"
git config --global user.email "votre.email@example.com"
ssh -T git@github.com
git branch -a
git status
git checkout -b enigme_Paul
echo "Je suis toujours dans le futur mais je n’arrive jamais. Qui suis-je ?" > Paul.txt
git add Paul.txt
git commit -m "Ajout de l'énigme de Paul"
git push origin enigme_Paul
git branch -r
git checkout main
git pull origin main
echo "Réponse de Paul : un pet" >> Marc.txt
git add Marc.txt
git commit -m "Paul résout l'énigme de Marc"
git push origin main
git checkout enigme_Paul
git rebase main
git rebase -i HEAD~3
git push origin enigme_Paul --force
git stash
git stash list
git stash apply
git add Paul.txt
git commit -am "Ajout de la modification après restauration du stash"
git push origin enigme_Paul
git cherry-pick <commit-hash-de-Lea>
git commit -m "Application du commit de Léa via cherry-pick"
git push origin enigme_Paul
git tag -a v1.0 -m "Version stable 1.0 de Paul"
git push origin v1.0
git checkout main
git branch -d enigme_Paul
git push origin --delete enigme_Paul
git reflog
git log --stat
git diff enigme_Paul main
```



### **LEA (suite)**

```bash
git checkout enigme_Lea
echo "Modification supplémentaire dans Lea.txt" >> Lea.txt
git add Lea.txt
git commit -m "Ajout d'une nouvelle modification dans Lea.txt"
git push origin enigme_Lea
git checkout main
git pull origin main
git merge enigme_Lea
git add Lea.txt
git commit -m "Fusion de la branche enigme_Lea dans main"
git push origin main
git branch -d enigme_Lea
git reflog
git log --oneline --graph
```

---

### **MARC (suite)**

```bash
git checkout enigme_Marc
echo "Modification supplémentaire dans Marc.txt" >> Marc.txt
git add Marc.txt
git commit -m "Ajout d'une nouvelle modification dans Marc.txt"
git push origin enigme_Marc
git checkout main
git pull origin main
git merge enigme_Marc
git add Marc.txt
git commit -m "Fusion de la branche enigme_Marc dans main"
git push origin main
git branch -d enigme_Marc
git reflog
git log --oneline --graph
```

---

### **PAUL (suite)**

```bash
git checkout enigme_Paul
echo "Modification supplémentaire dans Paul.txt" >> Paul.txt
git add Paul.txt
git commit -m "Ajout d'une nouvelle modification dans Paul.txt"
git push origin enigme_Paul
git checkout main
git pull origin main
git merge enigme_Paul
git add Paul.txt
git commit -m "Fusion de la branche enigme_Paul dans main"
git push origin main
git branch -d enigme_Paul
git reflog
git log --oneline --graph
```

---

### **LEA (conflit)**

```bash
git checkout enigme_Lea
echo "Réponse supplémentaire de Léa dans Marc.txt" >> Marc.txt
git add Marc.txt
git commit -m "Léa modifie Marc.txt"
git push origin enigme_Lea
```

---

### **MARC (conflit)**

```bash
git checkout enigme_Marc
echo "Réponse supplémentaire de Marc dans Marc.txt" >> Marc.txt
git add Marc.txt
git commit -m "Marc modifie Marc.txt"
git push origin enigme_Marc
```

---

### **PAUL (résolution du conflit)**

```bash
git checkout enigme_Paul
git pull origin main
git merge enigme_Paul
# Conflit détecté dans Marc.txt
nano Marc.txt  # Résolution manuelle du conflit
git add Marc.txt
git commit -m "Résolution du conflit dans Marc.txt"
git push origin enigme_Paul
```

---

### **LEA (résolution du conflit)**

```bash
git checkout enigme_Lea
git pull origin main
git merge enigme_Lea
# Conflit détecté dans Paul.txt
nano Paul.txt  # Résolution manuelle du conflit
git add Paul.txt
git commit -m "Résolution du conflit dans Paul.txt"
git push origin enigme_Lea
```

---

### **MARC (résolution du conflit)**

```bash
git checkout enigme_Marc
git pull origin main
git merge enigme_Marc
# Conflit détecté dans Lea.txt
nano Lea.txt  # Résolution manuelle du conflit
git add Lea.txt
git commit -m "Résolution du conflit dans Lea.txt"
git push origin enigme_Marc
```


### **LEA (suite)**

```bash
git checkout enigme_Lea
echo "Ajout d'une autre réponse dans Lea.txt" >> Lea.txt
git add Lea.txt
git commit -m "Ajout d'une autre réponse de Léa"
git push origin enigme_Lea
git checkout main
git pull origin main
git merge enigme_Lea
git add Lea.txt
git commit -m "Fusion de la branche enigme_Lea après nouvelle modification"
git push origin main
git branch -d enigme_Lea
git reflog
git log --oneline --graph
git stash
git stash apply
git add Lea.txt
git commit -m "Modifications après restauration du stash"
git push origin enigme_Lea
```

---

### **MARC (suite)**

```bash
git checkout enigme_Marc
echo "Ajout d'une autre réponse dans Marc.txt" >> Marc.txt
git add Marc.txt
git commit -m "Ajout d'une autre réponse de Marc"
git push origin enigme_Marc
git checkout main
git pull origin main
git merge enigme_Marc
git add Marc.txt
git commit -m "Fusion de la branche enigme_Marc après nouvelle modification"
git push origin main
git branch -d enigme_Marc
git reflog
git log --oneline --graph
git stash
git stash apply
git add Marc.txt
git commit -m "Modifications après restauration du stash"
git push origin enigme_Marc
```

---

### **PAUL (suite)**

```bash
git checkout enigme_Paul
echo "Ajout d'une autre réponse dans Paul.txt" >> Paul.txt
git add Paul.txt
git commit -m "Ajout d'une autre réponse de Paul"
git push origin enigme_Paul
git checkout main
git pull origin main
git merge enigme_Paul
git add Paul.txt
git commit -m "Fusion de la branche enigme_Paul après nouvelle modification"
git push origin main
git branch -d enigme_Paul
git reflog
git log --oneline --graph
git stash
git stash apply
git add Paul.txt
git commit -m "Modifications après restauration du stash"
git push origin enigme_Paul
```

---

### **LEA (Cherry-pick)**

```bash
git checkout enigme_Lea
git cherry-pick <commit-hash-de-Marc>
git commit -m "Ajout du commit de Marc via cherry-pick"
git push origin enigme_Lea
```

---

### **MARC (Cherry-pick)**

```bash
git checkout enigme_Marc
git cherry-pick <commit-hash-de-Lea>
git commit -m "Ajout du commit de Léa via cherry-pick"
git push origin enigme_Marc
```

---

### **PAUL (Cherry-pick)**

```bash
git checkout enigme_Paul
git cherry-pick <commit-hash-de-Lea>
git commit -m "Ajout du commit de Léa via cherry-pick"
git push origin enigme_Paul
```

---

### **LEA (Tags)**

```bash
git tag -a v1.1 -m "Nouvelle version 1.1 de Léa"
git push origin v1.1
```

---

### **MARC (Tags)**

```bash
git tag -a v1.1 -m "Nouvelle version 1.1 de Marc"
git push origin v1.1
```

---

### **PAUL (Tags)**

```bash
git tag -a v1.1 -m "Nouvelle version 1.1 de Paul"
git push origin v1.1
```


### **LEA (suite)**

```bash
git checkout enigme_Lea
echo "Nouvelle énigme pour Léa" >> Lea.txt
git add Lea.txt
git commit -m "Ajout d'une nouvelle énigme par Léa"
git push origin enigme_Lea
git pull origin main
git merge main
git push origin enigme_Lea
git checkout main
git pull origin main
git merge enigme_Lea
git push origin main
git branch -d enigme_Lea
git log --oneline --graph
git reflog
```

---

### **MARC (suite)**

```bash
git checkout enigme_Marc
echo "Nouvelle énigme pour Marc" >> Marc.txt
git add Marc.txt
git commit -m "Ajout d'une nouvelle énigme par Marc"
git push origin enigme_Marc
git pull origin main
git merge main
git push origin enigme_Marc
git checkout main
git pull origin main
git merge enigme_Marc
git push origin main
git branch -d enigme_Marc
git log --oneline --graph
git reflog
```

---

### **PAUL (suite)**

```bash
git checkout enigme_Paul
echo "Nouvelle énigme pour Paul" >> Paul.txt
git add Paul.txt
git commit -m "Ajout d'une nouvelle énigme par Paul"
git push origin enigme_Paul
git pull origin main
git merge main
git push origin enigme_Paul
git checkout main
git pull origin main
git merge enigme_Paul
git push origin main
git branch -d enigme_Paul
git log --oneline --graph
git reflog
```

---

### **LEA (suite)**

```bash
git checkout enigme_Lea
echo "Réponse à l'énigme de Marc" >> Marc.txt
git add Marc.txt
git commit -m "Léa résout l'énigme de Marc"
git push origin enigme_Lea
git checkout main
git pull origin main
git merge enigme_Lea
git push origin main
```

---

### **MARC (suite)**

```bash
git checkout enigme_Marc
echo "Réponse à l'énigme de Paul" >> Paul.txt
git add Paul.txt
git commit -m "Marc résout l'énigme de Paul"
git push origin enigme_Marc
git checkout main
git pull origin main
git merge enigme_Marc
git push origin main
```

---

### **PAUL (suite)**

```bash
git checkout enigme_Paul
echo "Réponse à l'énigme de Léa" >> Lea.txt
git add Lea.txt
git commit -m "Paul résout l'énigme de Léa"
git push origin enigme_Paul
git checkout main
git pull origin main
git merge enigme_Paul
git push origin main
```

---

### **LEA (Rebase)**

```bash
git checkout enigme_Lea
git pull origin main
git rebase main
git push origin enigme_Lea --force
```

---

### **MARC (Rebase)**

```bash
git checkout enigme_Marc
git pull origin main
git rebase main
git push origin enigme_Marc --force
```

---

### **PAUL (Rebase)**

```bash
git checkout enigme_Paul
git pull origin main
git rebase main
git push origin enigme_Paul --force
```

---

### **LEA (suite)**

```bash
git checkout enigme_Lea
echo "Dernière modification par Léa" >> Lea.txt
git add Lea.txt
git commit -m "Dernière modification par Léa"
git push origin enigme_Lea
git checkout main
git pull origin main
git merge enigme_Lea
git push origin main
```

---

### **MARC (suite)**

```bash
git checkout enigme_Marc
echo "Dernière modification par Marc" >> Marc.txt
git add Marc.txt
git commit -m "Dernière modification par Marc"
git push origin enigme_Marc
git checkout main
git pull origin main
git merge enigme_Marc
git push origin main
```

---

### **PAUL (suite)**

```bash
git checkout enigme_Paul
echo "Dernière modification par Paul" >> Paul.txt
git add Paul.txt
git commit -m "Dernière modification par Paul"
git push origin enigme_Paul
git checkout main
git pull origin main
git merge enigme_Paul
git push origin main
```


### **LEA (suite)**

```bash
git checkout enigme_Lea
echo "Ajout d'une énigme bonus par Léa" >> Lea.txt
git add Lea.txt
git commit -m "Ajout d'une énigme bonus par Léa"
git push origin enigme_Lea
git checkout main
git pull origin main
git merge enigme_Lea
git push origin main
git branch -d enigme_Lea
git log --oneline --graph
git reflog
```

---

### **MARC (suite)**

```bash
git checkout enigme_Marc
echo "Ajout d'une énigme bonus par Marc" >> Marc.txt
git add Marc.txt
git commit -m "Ajout d'une énigme bonus par Marc"
git push origin enigme_Marc
git checkout main
git pull origin main
git merge enigme_Marc
git push origin main
git branch -d enigme_Marc
git log --oneline --graph
git reflog
```

---

### **PAUL (suite)**

```bash
git checkout enigme_Paul
echo "Ajout d'une énigme bonus par Paul" >> Paul.txt
git add Paul.txt
git commit -m "Ajout d'une énigme bonus par Paul"
git push origin enigme_Paul
git checkout main
git pull origin main
git merge enigme_Paul
git push origin main
git branch -d enigme_Paul
git log --oneline --graph
git reflog
```

---

### **LEA (finalisation)**

```bash
git checkout enigme_Lea
echo "Finalisation de l'énigme de Léa" >> Lea.txt
git add Lea.txt
git commit -m "Finalisation de l'énigme de Léa"
git push origin enigme_Lea
git checkout main
git pull origin main
git merge enigme_Lea
git push origin main
git branch -d enigme_Lea
```

---

### **MARC (finalisation)**

```bash
git checkout enigme_Marc
echo "Finalisation de l'énigme de Marc" >> Marc.txt
git add Marc.txt
git commit -m "Finalisation de l'énigme de Marc"
git push origin enigme_Marc
git checkout main
git pull origin main
git merge enigme_Marc
git push origin main
git branch -d enigme_Marc
```

---

### **PAUL (finalisation)**

```bash
git checkout enigme_Paul
echo "Finalisation de l'énigme de Paul" >> Paul.txt
git add Paul.txt
git commit -m "Finalisation de l'énigme de Paul"
git push origin enigme_Paul
git checkout main
git pull origin main
git merge enigme_Paul
git push origin main
git branch -d enigme_Paul
```

---

### **LEA (version finale)**

```bash
git tag -a v2.0 -m "Version finale de Léa"
git push origin v2.0
```

---

### **MARC (version finale)**

```bash
git tag -a v2.0 -m "Version finale de Marc"
git push origin v2.0
```

---

### **PAUL (version finale)**

```bash
git tag -a v2.0 -m "Version finale de Paul"
git push origin v2.0
```

---

### **LEA (dernière vérification)**

```bash
git checkout main
git pull origin main
git log --oneline --graph
git reflog
git status
```

---

### **MARC (dernière vérification)**

```bash
git checkout main
git pull origin main
git log --oneline --graph
git reflog
git status
```

---

### **PAUL (dernière vérification)**

```bash
git checkout main
git pull origin main
git log --oneline --graph
git reflog
git status
```






------------------
# Annexe 2 - Intervention du professeur
------------------

- Le professeur intervient à des moments clés pour superviser, contrôler, et fusionner les pull requests, ainsi que pour créer des scénarios de conflits et guider la résolution.
- Le professeur joue un rôle actif tout au long du processus, tout en laissant les étudiants effectuer eux-mêmes la majorité des manipulations Git pour qu'ils apprennent de manière pratique et autonome.
- Voici où et quand le **Professeur (moi)** intervient tout au long du TP :

---

### **Interventions du Professeur :**

1. **Clonage du dépôt et configuration initiale :**
   - Le professeur s'assure que tous les étudiants ont bien cloné le dépôt et configuré Git correctement. Il peut répondre aux questions et vérifier que chaque étudiant est prêt à démarrer.
   
2. **Création des pull requests et fusion dans `main` :**
   - **Professeur (moi)** : Lorsque les étudiants poussent leurs branches (`enigme_Lea`, `enigme_Marc`, etc.), ils créent des **pull requests** sur GitHub.
   - Le professeur contrôle chaque pull request et décide quand les fusionner dans la branche principale `main`.

   **Intervention** :
   - Examen de chaque pull request.
   - Fusion des branches dans `main` après validation.

3. **Scénarios de conflit :**
   - **Professeur (moi)** : Le professeur crée des **scénarios de conflit garantis** en demandant à deux étudiants de modifier le même fichier simultanément. Ces conflits ne seront visibles que lors des tentatives de fusion dans `main`.

   **Intervention** :
   - Une fois le conflit détecté (par exemple entre Marc et Paul), le professeur attribue à l'un des étudiants (Marc ou Paul) la tâche de résoudre le conflit localement.
   - Le professeur vérifie que le conflit a été résolu correctement avant de fusionner la branche modifiée.

4. **Supervision des résolutions de conflits :**
   - **Professeur (moi)** : Le professeur assiste les étudiants pendant la résolution des conflits et s'assure qu'ils appliquent les bonnes pratiques Git (résolution manuelle, vérification des fichiers après la fusion, etc.).

5. **Validation finale et gestion des tags :**
   - **Professeur (moi)** : Le professeur supervise la création des **tags de version** (v1.0, v2.0, etc.) par chaque étudiant. Il vérifie que les tags sont poussés correctement vers GitHub.

   **Intervention** :
   - Validation des versions finales après que chaque étudiant a marqué ses commits avec des tags.
   - S'assure que le projet est bien structuré avec des commits clairs et un historique propre après le rebase et les squashes.

6. **Vérification finale du projet :**
   - **Professeur (moi)** : En fin de projet, le professeur vérifie que tous les commits ont été fusionnés, que l'historique Git est propre, et que tous les conflits ont été résolus.
   
   **Intervention** :
   - Vérification de l'état final du projet avec `git log`, `git reflog`, et `git status`.
   - S'assure que les versions taggées sont bien publiées et que chaque étudiant a effectué toutes les manipulations requises.

---

### **Résumé des interventions du Professeur (moi)** :
- **Clonage et configuration** : S'assure que tous les étudiants démarrent bien.
- **Pull requests** : Supervise et fusionne chaque PR dans `main`.
- **Scénarios de conflit** : Crée les conflits et supervise la résolution.
- **Résolution des conflits** : Guide les étudiants dans la gestion des conflits.
- **Gestion des tags** : Valide la création des versions avec des tags.
- **Vérification finale** : S'assure que le projet est propre et bien structuré avant la fin du TP.


