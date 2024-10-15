# 05 git workflow commands



# **Commandes de Workflow Git**

Les **commandes de workflow Git** permettent de gérer un projet localement et de le synchroniser avec un dépôt distant comme GitHub. Ce guide vous montrera les différentes étapes pour gérer un dépôt Git local, effectuer des commits, et pousser le code vers GitHub.

## **Dépôt Local** : `Git`

## **Dépôt Distant** : `GitHub` ([https://github.com](https://github.com))

Prenons l'exemple d'un développeur qui travaille sur un projet Java nommé **SpringBootMicroservice**. Ce projet contient plusieurs fichiers (nous allons créer des fichiers fictifs avec l'extension `.java`). Le projet est d'abord géré localement avant d'être synchronisé avec GitHub.

---

## **Étapes du workflow Git**

### **Étape 1 : Créer un dossier pour le projet**
Créez un dossier pour contenir votre projet.
```bash
mkdir SpringBootMicroservice
```

### **Étape 2 : Créer les fichiers nécessaires**
Naviguez dans le dossier et créez quelques fichiers Java.
```bash
cd SpringBootMicroservice
touch restapi.java dao.java services.java
```

### **Étape 3 : Initialiser le dépôt Git**
Initialisez le dépôt Git dans le dossier du projet.
```bash
git init
```

### **Étape 4 : Vérifier la création du répertoire `.git`**
Après l'initialisation, un dossier `.git` est créé. Ce dossier est responsable de la gestion des versions du projet.
```bash
ls -la
ls .git
```

### **Étape 5 : Configurer le nom de l'auteur et l'adresse email au niveau local**
Configurez le nom et l'email de l'auteur pour ce projet localement.
```bash
git config --local user.name "Haythem"
git config --local user.email "rehoumahaythem@gmail.com"
```

### **Étape 6 : Vérifier la configuration locale**
Vérifiez que le nom et l'email sont correctement configurés dans le fichier `.git/config`.
```bash
cat .git/config
```

### **Étape 7 : Vérifier l'état du dépôt local**
Vérifiez l'état du dépôt pour voir quels fichiers ne sont pas suivis (fichiers non trackés).
```bash
git status
```

### **Étape 8 : Ajouter un fichier dans la zone de staging**
Ajoutez un fichier spécifique (par exemple, `dao.java`) à la zone de staging.
```bash
git add dao.java
git status
```

### **Étape 9 : Retirer un fichier de la zone de staging**
Si vous souhaitez retirer un fichier de la zone de staging (le rendre non tracké), utilisez la commande suivante :
```bash
git rm --cached dao.java
git status
```

### **Étape 10 : Ajouter tous les fichiers à la zone de staging**
Ajoutez tous les fichiers à la zone de staging en une seule commande.
```bash
git add .   # ou git add -A
git status
```

### **Étape 11 : Commiter un fichier spécifique dans le dépôt local**
Commitez un fichier spécifique (par exemple, `dao.java`) dans le dépôt local.
```bash
git commit -m "dao.java est ajouté"
git log
```

### **Étape 12 : Commiter tous les fichiers dans le dépôt local**
Commitez tous les fichiers dans le dépôt local.
```bash
git commit -m "Ajout des fichiers restapi.java et services.java"
git status
git log
git log --oneline
```

---

## **Synchronisation avec GitHub**

### **Étape 1 : Créer un dépôt sur GitHub**
1. Rendez-vous sur [GitHub](https://github.com) et connectez-vous.
2. Cliquez sur **"New"** ou **"Start a project"** pour créer un nouveau dépôt.
3. Donnez un nom à votre dépôt (par exemple **SpringBootMicroservice**), sélectionnez l'option **Public**, puis cliquez sur **"Create Repository"**.

### **Étape 2 : Créer un token GitHub**
1. Allez dans les **Settings** de votre compte GitHub.
2. Sélectionnez **Developer Settings**, puis **Personal Access Tokens**.
3. Cliquez sur **Generate new token** et remplissez les informations :
   - **Note** : `token1`
   - **Expiration** : 7 jours
   - **Permissions** : cochez les options **repo** et **admin:org**.
4. Cliquez sur **Generate token** et notez le numéro du token.

### **Étape 3 : Ajouter le dépôt distant (GitHub)**
1. Copiez l'URL HTTPS du dépôt GitHub.
2. Dans votre projet local, exécutez les commandes suivantes pour configurer la branche principale et ajouter le dépôt distant :
   ```bash
   git branch -M main
   git remote add origin <URL-HTTPS>
   git push origin main
   ```
3. Lorsqu'on vous le demande, fournissez votre nom d'utilisateur GitHub et le **token** comme mot de passe.

### **Étape 4 : Vérifier la synchronisation**
Vérifiez sur GitHub que la branche principale (`main`) a bien été créée et que tous les fichiers locaux sont disponibles sur le dépôt distant.

---

## **Connexion à GitHub via des clés SSH**

### **Étape 1 : Créer des clés SSH sur le système local**
Générez une paire de clés SSH sur votre système.
```bash
ssh-keygen
```
Copiez le contenu du fichier public :
```bash
cat ~/.ssh/id_rsa.pub
```

### **Étape 2 : Ajouter la clé SSH sur GitHub**
1. Allez dans les paramètres de votre dépôt GitHub.
2. Dans **Settings**, sélectionnez **Deploy Keys**.
3. Cliquez sur **Add key**, collez la clé publique SSH, cochez **Allow write access**, puis cliquez sur **Add key**.

### **Étape 3 : Modifier la configuration du dépôt local**
Remplacez l'URL HTTPS par l'URL SSH dans le fichier `.git/config` du dépôt local.
```bash
vi .git/config
```
Remplacez l'URL par celle en SSH : `git@github.com:<username>/<repository>.git`.

### **Étape 4 : Ajouter un nouveau fichier et pousser les changements**
1. Créez un nouveau fichier dans votre dépôt local :
   ```bash
   touch bal.java
   git add bal.java
   git commit -m "Ajout du fichier bal.java"
   ```
2. Poussez les modifications sur GitHub via SSH :
   ```bash
   git push origin main
   ```

---

## **Conclusion**

Ce guide vous a montré les commandes essentielles du workflow Git pour créer un dépôt local, gérer les commits, et synchroniser avec un dépôt distant comme GitHub, en utilisant HTTPS ou SSH. Avec ces étapes, vous pouvez efficacement gérer vos projets et collaborer avec d'autres développeurs sur GitHub.

---

Ce cours couvre les commandes de base du workflow Git et vous guide à travers les processus locaux et distants.
