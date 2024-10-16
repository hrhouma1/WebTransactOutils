








------------------
# Annexe 2
------------------


#1
Voici l'ensemble des manipulations demandées sous forme de commandes, avec les noms des étudiants associés à chaque section.

---

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

#2
Voici la suite des manipulations avec les rôles de chaque étudiant.

---

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

#3
Voici la suite des manipulations avec les rôles de chaque étudiant.

---

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

#4
Voici la suite des manipulations avec les rôles de chaque étudiant.

---

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


#5

Voici la suite des manipulations avec les rôles de chaque étudiant.

---

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

#6


#7





------------------
# Annexe 3
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


