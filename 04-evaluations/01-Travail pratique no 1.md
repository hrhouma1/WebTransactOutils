# **Travail Pratique N°1 : Différence entre `git merge` et `git rebase`**

**Cours** : Gestion de versions avec Git  
**Objectifs pédagogiques :**
- Comprendre les différences fondamentales entre `git merge` et `git rebase`.
- Observer les effets des deux commandes sur l’historique Git.
- Documenter les manipulations avec des captures d’écran et des explications claires.

---

## Objectifs du TP

À la fin de ce TP, vous serez capable de :
1. Utiliser `git merge` et `git rebase` pour intégrer des modifications de branches.
2. Analyser les différences entre les deux commandes dans la structure de l'historique.
3. Identifier les cas d'utilisation idéaux pour `merge` et `rebase`.

---

## Instructions et étapes détaillées

### Préparation

1. **Créez un dossier de travail pour ce TP** :
   - Dans votre terminal, tapez les commandes suivantes pour préparer votre environnement :
     ```bash
     mkdir git-evaluation-1
     cd git-evaluation-1
     git init
     ```

2. **Capture d’écran** : Prenez une capture d’écran montrant l’initialisation du dépôt (`git init`).

---

## Étape 1 : Initialisation du dépôt et création de la branche principale

1. **Création du fichier initial**  
   Créez un fichier nommé `fichier1.txt` (fichier original) et ajoutez un commit de base sur la branche principale `main` :
   ```bash
   echo "Contenu initial dans fichier1" > fichier1.txt
   git add fichier1.txt
   git commit -m "Initialisation du projet avec fichier1.txt"
   ```

2. **Renommez la branche principale en `main` (si nécessaire)** :
   ```bash
   git branch -M main
   ```

3. **Capture d’écran** : Montrez l’ajout du fichier et le premier commit.

---

## Étape 2 : Création des branches pour le rebase et le merge

1. **Créez les branches `branche1` et `branche2` à partir de `main`** :
   - Créez `branche1` :
     ```bash
     git checkout -b branche1
     ```
   - Revenez sur `main` et créez `branche2` :
     ```bash
     git checkout main
     git checkout -b branche2
     ```

2. **Création des branches de travail** :
   - Créez `branche-rebase` à partir de `branche1` :
     ```bash
     git checkout branche1
     git checkout -b branche-rebase
     ```
   - Créez `branche-merge` à partir de `branche2` :
     ```bash
     git checkout branche2
     git checkout -b branche-merge
     ```

3. **Capture d’écran** : Montrez la création des branches avec la commande `git branch`.

---

## Étape 3 : Ajout de commits identiques sur `branche-rebase` et `branche-merge`

> **Note :** Nous allons utiliser des fichiers différents (`fichier-2-rebase.txt` et `fichier-2-merge.txt`) et effectuer les mêmes modifications pour pouvoir comparer les effets de `merge` et `rebase`.

1. **Travail sur `branche-rebase`** :
   - **Premier commit** :
     ```bash
     git checkout branche-rebase
     echo "Modification 1 dans branche-rebase" > fichier-2-rebase.txt
     git add fichier-2-rebase.txt
     git commit -m "Ajout de fichier-2-rebase.txt avec modification 1"
     ```

   - **Deuxième commit** :
     ```bash
     echo "Modification 2 dans branche-rebase" >> fichier-2-rebase.txt
     git add fichier-2-rebase.txt
     git commit -m "Ajout de modification 2 dans fichier-2-rebase.txt"
     ```

   - **Troisième commit** :
     ```bash
     echo "Modification 3 dans branche-rebase" >> fichier-2-rebase.txt
     git add fichier-2-rebase.txt
     git commit -m "Ajout de modification 3 dans fichier-2-rebase.txt"
     ```

2. **Travail sur `branche-merge`** :
   - **Premier commit** :
     ```bash
     git checkout branche-merge
     echo "Modification 1 dans branche-merge" > fichier-2-merge.txt
     git add fichier-2-merge.txt
     git commit -m "Ajout de fichier-2-merge.txt avec modification 1"
     ```

   - **Deuxième commit** :
     ```bash
     echo "Modification 2 dans branche-merge" >> fichier-2-merge.txt
     git add fichier-2-merge.txt
     git commit -m "Ajout de modification 2 dans fichier-2-merge.txt"
     ```

   - **Troisième commit** :
     ```bash
     echo "Modification 3 dans branche-merge" >> fichier-2-merge.txt
     git add fichier-2-merge.txt
     git commit -m "Ajout de modification 3 dans fichier-2-merge.txt"
     ```

3. **Capture d’écran** : Montrez les commits réalisés dans chaque branche avec `git log`.

---

## Étape 4 : Intégration des branches avec `merge` et `rebase`

1. **Rebase de `branche-rebase` dans `branche1`** :
   - Basculez sur `branche1` :
     ```bash
     git checkout branche1
     ```
   - Rebasez `branche-rebase` dans `branche1` :
     ```bash
     git rebase branche-rebase
     ```

   - **Capture d’écran** : Utilisez `git log --oneline --graph --all` pour montrer l’historique linéaire créé par le rebase.

2. **Merge de `branche-merge` dans `branche2`** :
   - Basculez sur `branche2` :
     ```bash
     git checkout branche2
     ```
   - Fusionnez `branche-merge` dans `branche2` :
     ```bash
     git merge branche-merge -m "Fusion de branche-merge dans branche2"
     ```

   - **Capture d’écran** : Utilisez `git log --oneline --graph --all` pour montrer l’historique avec le commit de fusion.

---

## Étape 5 : Comparaison finale et questions de réflexion

### Questions de réflexion

1. **Comparer les historiques** :
   - Que remarquez-vous dans la différence entre l’historique de `branche1` (avec `rebase`) et celui de `branche2` (avec `merge`) ?
   - Prenez une capture d’écran de chaque historique et expliquez les différences observées.

2. **Arguments pour chaque méthode** :
   - Dans quels cas serait-il préférable d’utiliser `rebase` pour intégrer des modifications ?
   - Dans quels cas le `merge` est-il plus avantageux ?

3. **Scénarios d’application** :
   - Imaginez un projet en équipe. Expliquez un cas concret où `merge` pourrait causer des conflits dans l'historique, et comment `rebase` pourrait résoudre ce problème.
   - Inversement, décrivez un cas où l’utilisation excessive de `rebase` pourrait poser des difficultés de suivi dans un projet collaboratif.

---

## Résumé et soumission

**Pour soumettre ce TP** :
1. Compilez vos réponses et captures d’écran dans un document (PDF ou Word).
2. Répondez aux questions de réflexion en bas du document.
3. Soumettez votre fichier sur la plateforme de cours.

---

**Note aux étudiants** : Ce TP est conçu pour vous permettre de pratiquer Git en profondeur. N'hésitez pas à expérimenter et à documenter toute difficulté rencontrée dans vos réponses.
