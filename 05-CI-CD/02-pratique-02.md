
# Objectif: 

- Héberger votre site web HTML sur GitHub Pages à l'aide de GitHub Actions.
- Voici un guide complet de A à Z, détaillé, depuis la création de votre projet HTML en local jusqu'à la mise en ligne sur GitHub Pages.

### Prérequis 📝
- Avoir un compte GitHub (inscription gratuite sur [https://github.com](https://github.com)).
- Installer **Git** sur votre ordinateur (téléchargeable depuis [https://git-scm.com/](https://git-scm.com/)).
- Avoir un éditeur de code, comme **Visual Studio Code** (téléchargeable depuis [https://code.visualstudio.com/](https://code.visualstudio.com/)).

---

### Étape 1 : Créer votre projet HTML en local 💻

1. **Créer un dossier pour votre projet** :
   ```bash
   mkdir mon-site-web
   cd mon-site-web
   ```

2. **Créer un fichier `index.html`** dans ce dossier avec votre code HTML :
   ```html
   <!DOCTYPE html>
   <html lang="fr">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Mon Site Web</title>
   </head>
   <body>
       <h1>Bienvenue sur mon site hébergé avec GitHub Pages !</h1>
       <p>Ceci est une page web simple hébergée à l'aide de GitHub Actions et GitHub Pages.</p>
   </body>
   </html>
   ```

3. **Initialiser un dépôt Git** dans votre dossier :
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Ajout de index.html"
   ```

---

### Étape 2 : Créer un dépôt sur GitHub 🏢

1. **Aller sur GitHub** et cliquer sur le bouton **New** pour créer un nouveau dépôt.
2. **Nommer votre dépôt** (ex. : `mon-site-web`) et cliquer sur **Create repository**.
3. **Lier votre dépôt local à GitHub** en ajoutant l'URL de votre dépôt :
   ```bash
   git remote add origin https://github.com/votre-nom-utilisateur/mon-site-web.git
   git branch -M main
   git push -u origin main
   ```

---

### Étape 3 : Configurer GitHub Actions pour déployer sur GitHub Pages ⚙️

1. **Créer un fichier de workflow GitHub Actions** :
   - Allez dans votre dépôt sur GitHub, cliquez sur l'onglet **Actions**, puis sur **Set up a workflow yourself**.
   - Nommez le fichier `.github/workflows/deploy.yml`.

2. **Ajouter le code YAML suivant** pour configurer le déploiement sur GitHub Pages :
   ```yaml
   name: Deploy to GitHub Pages

   on:
     push:
       branches:
         - main

   jobs:
     build:
       runs-on: ubuntu-latest

       steps:
       - name: Checkout code
         uses: actions/checkout@v3

       - name: Deploy to GitHub Pages
         uses: peaceiris/actions-gh-pages@v3
         with:
           github_token: ${{ secrets.GITHUB_TOKEN }}
           publish_dir: ./
   ```

   Ce fichier déclenche le workflow chaque fois qu’un push est effectué sur la branche `main`. Il déploie le contenu du dossier racine `./` sur GitHub Pages.

3. **Commitez et poussez le fichier de workflow** :
   ```bash
   git add .github/workflows/deploy.yml
   git commit -m "Ajout du workflow GitHub Actions pour déployer sur GitHub Pages"
   git push
   ```

---

### Étape 4 : Activer GitHub Pages 🌐

1. **Accéder aux paramètres de votre dépôt** sur GitHub.
2. Dans l'onglet **Pages**, sous **Source**, sélectionnez `GitHub Actions` pour activer le déploiement via votre workflow.
3. Attendez quelques instants pour que le déploiement se termine.

---

### Étape 5 : Vérifier la publication de votre site 🎉

1. Une fois le workflow exécuté, votre site sera accessible à l'adresse :
   ```
   https://votre-nom-utilisateur.github.io/mon-site-web/
   ```
2. **Vérifiez que votre page s'affiche correctement** en visitant l'URL.

---

### Résumé 🚀

1. Créez un projet HTML localement.
2. Initialisez un dépôt Git et poussez-le sur GitHub.
3. Configurez un workflow GitHub Actions pour déployer sur GitHub Pages.
4. Activez GitHub Pages dans les paramètres du dépôt.
5. Vérifiez votre site à l'URL fournie.

