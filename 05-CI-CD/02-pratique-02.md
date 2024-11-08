## Pratique-02 : Héberger un site HTML sur GitHub Pages avec GitHub Actions de A à Z 🚀

# Prérequis 📝
- Avoir un compte GitHub (inscription gratuite sur [https://github.com](https://github.com)).
- Installer **Git** sur votre ordinateur (téléchargeable depuis [https://git-scm.com/](https://git-scm.com/)).
- Avoir un éditeur de code, comme **Visual Studio Code** (téléchargeable depuis [https://code.visualstudio.com/](https://code.visualstudio.com/)).

---

### Étape 1 : Créer votre projet HTML en local 💻

1. **Créer un dossier pour votre projet** :
   - Ouvrez votre terminal et exécutez les commandes suivantes :
     ```bash
     mkdir mon-site-web
     cd mon-site-web
     ```

2. **Créer un fichier `index.html`** dans ce dossier avec votre code HTML :
   - Exemple de contenu pour `index.html` :
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
   - Tapez les commandes suivantes pour initialiser Git et créer un premier commit :
     ```bash
     git init
     git add .
     git commit -m "Initial commit: Ajout de index.html"
     ```

---

### Étape 2 : Créer un dépôt sur GitHub 🏢

1. **Allez sur GitHub** et cliquez sur le bouton **New** pour créer un nouveau dépôt.
2. **Nommer votre dépôt** (par exemple : `mon-site-web`) et cliquez sur **Create repository**.
3. **Lier votre dépôt local à GitHub** :
   - Exécutez les commandes suivantes en remplaçant `<votre-nom-utilisateur>` par votre nom d'utilisateur GitHub :
     ```bash
     git remote add origin https://github.com/<votre-nom-utilisateur>/mon-site-web.git
     git branch -M main
     git push -u origin main
     ```

---

### Étape 3 : Créer la Branche `gh-pages` et Forcer le Push

1. **Créer la branche `gh-pages`** :
   - Dans le terminal, exécutez ces commandes pour créer une branche `gh-pages` vide :
     ```bash
     git checkout --orphan gh-pages
     git rm -rf .
     touch index.html
     git add index.html
     git commit -m "Initial gh-pages commit"
     ```

2. **Forcer le push de la branche `gh-pages`** :
   - Cette commande force le push pour créer la branche `gh-pages` sur GitHub, ce qui est nécessaire pour le déploiement sur GitHub Pages.
     ```bash
     git push --force origin gh-pages
     ```

3. **Revenir à la branche `main`** :
   ```bash
   git checkout main
   ```

---

### Étape 4 : Configurer le fichier de workflow GitHub Actions

1. **Créer un dossier et un fichier pour GitHub Actions** :
   - Dans le terminal, exécutez ces commandes pour créer un dossier `.github/workflows` et un fichier `deploy.yml` :
     ```bash
     mkdir -p .github/workflows
     touch .github/workflows/deploy.yml
     ```

2. **Ajouter le contenu suivant au fichier `deploy.yml`** :
   - Ouvrez le fichier `deploy.yml` dans votre éditeur de code et collez le code suivant :
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
             publish_branch: gh-pages
             publish_dir: ./
     ```

   - Ce fichier YAML configure un workflow GitHub Actions qui se déclenche à chaque push sur la branche `main` et déploie le contenu vers la branche `gh-pages`.

3. **Pousser les modifications vers GitHub** :
   - Sauvegardez, puis poussez le fichier de workflow vers votre dépôt GitHub :
     ```bash
     git add .github/workflows/deploy.yml
     git commit -m "Ajout du workflow GitHub Actions pour déployer sur GitHub Pages"
     git push
     ```

---

### Étape 5 : Configurer les Permissions pour GitHub Actions

1. **Accédez aux paramètres de votre dépôt** :
   - Allez sur votre dépôt GitHub, puis cliquez sur **Settings** (Paramètres) en haut de la page.

2. **Configurer les permissions d'accès pour les actions** :
   - Dans le menu de gauche, descendez jusqu’à **Actions** sous **Code and automation**.
   - Dans la section **General**, assurez-vous que les permissions sont définies sur **Read and write permissions**.
   - Cela permet aux workflows GitHub Actions de pousser des modifications vers la branche `gh-pages`.

---

### Étape 6 : Activer GitHub Pages 🌐

1. **Allez dans les paramètres de GitHub Pages** :
   - Toujours dans l'onglet **Settings** de votre dépôt, descendez jusqu’à **Pages** sous **Code and automation**.

2. **Configurer la source de GitHub Pages** :
   - Dans la section **Source**, sélectionnez la branche `gh-pages`.
   - Cliquez sur **Save** pour enregistrer.

3. **Vérifiez que le message indique que le site sera publié** à l’URL suivante :
   ```
   https://<votre-nom-utilisateur>.github.io/mon-site-web/
   ```

---

### Étape 7 : Tester et Vérifier le Déploiement 🎉

1. **Attendez quelques minutes** pour que GitHub Pages termine le déploiement. Cela peut prendre un moment.
2. **Accédez à l’URL** : Rendez-vous sur l’URL indiquée (par exemple, `https://<votre-nom-utilisateur>.github.io/mon-site-web/`) pour vérifier que votre site s’affiche correctement.

3. **Si le site ne s’affiche pas immédiatement** :
   - Allez dans l’onglet **Actions** de votre dépôt et assurez-vous que le workflow a réussi.
   - Si tout fonctionne, rafraîchissez l’URL ou videz le cache de votre navigateur.

---

### Résumé 🚀

1. **Créez un dépôt GitHub** et configurez votre projet HTML en local.
2. **Créez et configurez la branche `gh-pages`** pour le déploiement.
3. **Ajoutez un workflow GitHub Actions** pour automatiser le déploiement sur GitHub Pages.
4. **Configurez les permissions et les paramètres de GitHub Pages** pour activer le site.
5. **Vérifiez votre site** à l'URL fournie.
