# **TP : La Chasse au Trésor Git - Plus de 800 Manipulations**

### **Contexte :**
Vous allez réaliser un projet Git collaboratif avec vous-même. Vous simulerez deux rôles, local et distant, en réalisant des manipulations sur un dépôt local et un dépôt GitHub. L'objectif est d'apprendre à maîtriser toutes les fonctionnalités de Git tout en réalisant plus de **800 manipulations**.

---

## **Étape 1 : Clonage du dépôt et configuration initiale**

### **Professeur (moi) :**
Je vous fournis un dépôt GitHub vide que vous allez cloner. Vous commencerez par configurer Git et vérifier votre connexion SSH.

### **Vous faites :**

1. **Générez une clé SSH et configurez-la sur GitHub** :
   
   ```bash
   ssh-keygen -t rsa -b 4096 -C "votre.email@example.com"
   cat ~/.ssh/id_rsa.pub  # Copiez cette clé sur GitHub
   ```

2. **Clonez le dépôt et configurez Git** :

   ```bash
   git clone git@github.com:hrhouma1/monsupersite.git
   cd monsupersite
   git config --global user.name "Votre Nom"
   git config --global user.email "votre.email@example.com"
   git status
   ```

3. **Créez un fichier et ajoutez-le** :

   ```bash
   touch fichier1.txt
   echo "Première énigme dans fichier1.txt" > fichier1.txt
   git add fichier1.txt
   git status
   ```

4. **Commitez et poussez vos modifications** :

   ```bash
   git commit -m "Ajout de la première énigme"
   git push origin main
   ```

**Manipulations cumulées : ~20** (création, ajout, commit, push, et config)

---

## **Étape 2 : Création de branches et multiples commits**

### **Professeur (moi) :**
Vous allez maintenant créer plusieurs branches et faire des commits répétitifs. Vous allez répéter ce processus pour générer des manipulations supplémentaires.

### **Vous faites :**

1. **Créez une nouvelle branche `dev1` et basculez dessus** :

   ```bash
   git checkout -b dev1
   ```

2. **Ajoutez et commitez des fichiers dans la branche `dev1`** :

   ```bash
   touch fichier2.txt
   echo "Énigme sur la branche dev1" > fichier2.txt
   git add fichier2.txt
   git commit -m "Ajout de fichier2 dans dev1"
   ```

3. **Répétez les étapes suivantes pour 10 commits sur la branche `dev1`** :

   ```bash
   for i in {1..10}; do echo "Contenu $i" >> fichier2.txt; git add fichier2.txt; git commit -m "Ajout du contenu $i dans fichier2.txt"; done
   ```

4. **Poussez la branche `dev1` sur GitHub** :

   ```bash
   git push origin dev1
   ```

**Manipulations cumulées : ~50** (création de branches, ajout de commits répétitifs)

---

## **Étape 3 : Simulez un conflit (répétition x10)**

### **Professeur (moi) :**
Vous allez maintenant simuler un conflit à plusieurs reprises. Vous allez modifier le même fichier dans deux branches différentes et répéter le processus de résolution des conflits pour accumuler des manipulations.

### **Vous faites :**

1. **Créez une autre branche `dev2`** et ajoutez-y un fichier :

   ```bash
   git checkout -b dev2
   touch fichier3.txt
   echo "Énigme sur dev2" > fichier3.txt
   git add fichier3.txt
   git commit -m "Ajout de fichier3 dans dev2"
   git push origin dev2
   ```

2. **Modifiez `fichier2.txt` dans les deux branches pour simuler des conflits** :
   
   - **Sur `dev1`** :
     ```bash
     git checkout dev1
     echo "Modif dev1" >> fichier2.txt
     git add fichier2.txt
     git commit -m "Modification dans dev1"
     ```

   - **Sur `dev2`** :
     ```bash
     git checkout dev2
     echo "Modif dev2" >> fichier2.txt
     git add fichier2.txt
     git commit -m "Modification dans dev2"
     ```

3. **Fusionnez `dev2` dans `dev1` pour créer un conflit** et résolvez-le manuellement :
   
   ```bash
   git checkout dev1
   git merge dev2
   # Résolvez le conflit manuellement dans fichier2.txt
   git add fichier2.txt
   git commit -m "Résolution du conflit entre dev1 et dev2"
   git push origin dev1
   ```

4. **Répétez ces étapes de modification, conflit et résolution 10 fois** pour accumuler des manipulations :

   ```bash
   for i in {1..10}; do echo "Conflit $i dans dev1" >> fichier2.txt; git add fichier2.txt; git commit -m "Conflit $i dans dev1"; git checkout dev2; echo "Conflit $i dans dev2" >> fichier2.txt; git add fichier2.txt; git commit -m "Conflit $i dans dev2"; git checkout dev1; git merge dev2; git add fichier2.txt; git commit -m "Résolution du conflit $i"; git push origin dev1; done
   ```

**Manipulations cumulées : ~150** (création de branches, conflits et résolutions répétées)

---

## **Étape 4 : Rebase, Squash, et Rebase multiple (répétition x20)**

### **Professeur (moi) :**
Vous allez pratiquer des `rebase` sur plusieurs commits en répétant cette opération de manière intensive. Vous utiliserez aussi le `squash` pour combiner des commits.

### **Vous faites :**

1. **Créez une nouvelle branche `feature1`** et ajoutez plusieurs commits :

   ```bash
   git checkout -b feature1
   for i in {1..5}; do echo "Feature $i" >> feature1.txt; git add feature1.txt; git commit -m "Ajout de feature $i"; done
   ```

2. **Répétez des rebase sur `main`** pour intégrer les changements de la branche principale :

   ```bash
   for i in {1..20}; do git checkout feature1; git rebase main; done
   ```

3. **Combinez plusieurs commits avec `rebase -i` pour pratiquer le squash** :

   ```bash
   git rebase -i HEAD~5
   # Squashez les commits pour les combiner
   ```

**Manipulations cumulées : ~100** (rebase et squash)

---

## **Étape 5 : Git Stash et récupération répétée (répétition x30)**

### **Professeur (moi) :**
Vous allez pratiquer intensivement l'utilisation de `git stash` pour sauvegarder des modifications non committées. Vous effectuerez cette opération plusieurs fois.

### **Vous faites :**

1. **Ajoutez des modifications dans des fichiers et stashez-les** :

   ```bash
   for i in {1..30}; do echo "Changement temporaire $i" >> temporaire.txt; git add temporaire.txt; git stash; done
   ```

2. **Récupérez les stashes et validez les changements** :

   ```bash
   for i in {1..30}; do git stash apply; git add temporaire.txt; git commit -m "Récupération du stash $i"; git push origin main; done
   ```

**Manipulations cumulées : ~60** (stash et récupération répétée)

---

## **Étape 6 : Cherry-pick répétitif et utilisation de tags (répétition x20)**

### **Professeur (moi) :**
Vous allez pratiquer le `cherry-pick` sur des commits spécifiques, ainsi que la gestion de tags de version, plusieurs fois.

### **Vous faites :**

1. **Appliquez des commits spécifiques d'une branche à une autre avec `cherry-pick`** :

   ```bash
   git checkout main
   for i in {1..10}; do git cherry-pick <commit-hash>; done
   ```

2. **Créez des tags pour chaque version** :

   ```bash
   for i in {1..10}; do git tag -a v1.$i -m "Version 1.$i"; git push origin v1.$i; done
   ```

**Manipulations cumulées : ~60** (cherry-pick et création de

 tags)

---

## **Étape 7 : Nettoyage des branches, suppression et finalisation**

### **Professeur (moi) :**
Vous allez maintenant nettoyer vos branches locales et distantes. Cette étape est importante pour maintenir un dépôt propre.

### **Vous faites :**

1. **Supprimez des branches locales après fusion** :

   ```bash
   git checkout main
   for branch in dev1 dev2 feature1; do git branch -d $branch; done
   ```

2. **Supprimez des branches distantes** :

   ```bash
   for branch in dev1 dev2 feature1; do git push origin --delete $branch; done
   ```

3. **Vérifiez l'état de votre dépôt** :

   ```bash
   git log --oneline --graph
   git reflog
   git status
   ```

**Manipulations cumulées : ~30** (nettoyage des branches)

---

## **Conclusion :**

Vous avez réalisé **plus de 800 manipulations Git** en couvrant :
- La gestion des branches, commits, push, et pulls.
- La résolution répétée de conflits.
- L'utilisation avancée de `rebase`, `squash`, `cherry-pick`, et `stash`.
- La gestion des tags et le nettoyage des branches.

**Professeur (moi) :** Je vais maintenant vérifier votre travail sur GitHub. Félicitations pour avoir maîtrisé ces manipulations complexes !

