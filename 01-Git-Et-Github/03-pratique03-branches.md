# L'histoire de Sébastien et ses coéquipiers : Collaborer avec Git pour créer un projet ensemble

Sébastien, un étudiant en programmation, est très motivé par la gestion de projets en groupe. Il décide de créer un projet avec l'aide de ses amis Eric et Michael. Le projet consiste à développer une application web qui permet aux étudiants de partager leurs idées et ressources pour améliorer leur apprentissage.

Sébastien, en tant que chef de projet, initie la première version du projet, et chaque membre de l'équipe travaille sur une fonctionnalité distincte à travers différentes branches Git. Voici comment Sébastien et son équipe collaborent pour mener à bien ce projet.

---

## Projet : Application de partage pour les étudiants

### 1. Créer un nouveau répertoire pour le projet

Sébastien commence par créer un répertoire pour l'application web :

```bash
mkdir partageEtudiants
cd partageEtudiants
```

### 2. Initialiser un dépôt Git

Il initialise ensuite un dépôt Git pour suivre l'évolution du projet :

```bash
git init
```

### 3. Configurer Git pour Sébastien

Sébastien configure Git avec son nom d'utilisateur et son email :

```bash
git config --global user.name "sgag-2-6"
git config --global user.email "seb.s.gag@gmail.com"
```

### 4. Créer la branche principale

Sébastien crée une branche `main` pour représenter la version stable du projet :

```bash
git branch -M main
```

### 5. Ajouter le premier fichier README

Il crée un fichier README pour décrire le projet :

```bash
echo "# Application de partage pour les étudiants" > README.md
git add README.md
git commit -m "Initial commit: Added README file"
```

### 6. Publier le projet sur un dépôt distant

Sébastien configure un dépôt distant et pousse la branche `main` :

```bash
git remote add origin <url-du-depot>
git push -u origin main
```

---

# Poste de Sébastien : Chef de projet

### 7. Création d'une branche pour une nouvelle fonctionnalité par Sébastien

Sébastien crée une nouvelle branche `interface` pour développer l'interface utilisateur de l'application :

```bash
git checkout -b interface
```

### 8. Sébastien commence à travailler sur l'interface utilisateur

Dans la branche `interface`, Sébastien crée les fichiers nécessaires pour l'interface utilisateur :

```bash
mkdir ui
echo "<html><body><h1>Bienvenue sur notre application de partage</h1></body></html>" > ui/index.html
git add ui/index.html
git commit -m "Created the initial UI for the homepage"
```

### 9. Sébastien pousse ses changements sur la branche distante

Sébastien pousse la branche `interface` vers le dépôt distant pour que les autres membres de l'équipe puissent y accéder :

```bash
git push -u origin interface
```

---

# Poste d'Eric : Gestion des utilisateurs


### 10. Cloner le dépôt et créer une branche

Eric, qui est responsable de la gestion des utilisateurs, doit d'abord cloner le dépôt avant de commencer :

```bash
git clone <url-du-depot>
cd partageEtudiants
```

### 11. Configurer Git pour Eric

Avant de commencer, Eric configure Git avec son nom d'utilisateur et son email :

```bash
git config --global user.name "eric-michaud"
git config --global user.email "michaud_e@hotmail.com"
```

Ensuite, il met à jour sa copie locale de la branche `main` avant de créer une nouvelle branche `gestion-utilisateurs` :

```bash
git pull origin main
git checkout -b gestion-utilisateurs
```

### 12. Eric ajoute la gestion des utilisateurs

Dans la branche `gestion-utilisateurs`, Eric ajoute un fichier pour la gestion des utilisateurs :

```bash
mkdir users
echo "module.exports = function registerUser() { console.log('User registered'); };" > users/user.js
git add users/user.js
git commit -m "Added user registration functionality"
git push -u origin gestion-utilisateurs
```

---

# Poste de Michael : Fonctionnalité de messagerie


### 13. Cloner le dépôt et créer une branche

Michael suit les mêmes étapes pour cloner le dépôt et se synchroniser avec la branche `main` avant de créer sa propre branche `messaging` :

```bash
git clone <url-du-depot>
cd partageEtudiants
git pull origin main
git checkout -b messaging
```

### 14. Configurer Git pour Michael

Michael configure Git avec son nom d'utilisateur et son email :

```bash
git config --global user.name "HashMapScreft"
git config --global user.email "screft@hotmail.com"
```

### 15. Michael ajoute la fonctionnalité de messagerie

Il commence à travailler sur le backend de la messagerie :

```bash
mkdir messaging
echo "module.exports = function sendMessage() { console.log('Message sent'); };" > messaging/message.js
git add messaging/message.js
git commit -m "Added messaging functionality"
git push -u origin messaging
```

---

# Poste de Sébastien : Chef de projet

### 16. Mise à jour et fusion des branches dans `main`

Avant de fusionner les branches de ses coéquipiers, Sébastien met à jour la branche `main` et se rébase sur les différentes branches créées par ses coéquipiers si nécessaire :

```bash
git checkout main
git pull origin main
git rebase interface
git rebase gestion-utilisateurs
git rebase database
git rebase messaging
```

### 17. Sébastien fusionne les branches dans `main`

Sébastien commence ensuite la fusion des branches dans `main` :

```bash
git checkout main
git merge interface
git merge gestion-utilisateurs
git merge database
git merge messaging
```

### 18. Résolution des conflits (si nécessaire)

Sébastien pourrait rencontrer des conflits lors de la fusion. Il résout les conflits et finalise la fusion.

### 19. Pousser la version finale du projet

Sébastien pousse la version finale sur la branche `main` :

```bash
git push origin main
```

---

### Conclusion

Grâce à cette approche collaborative utilisant des branches et des mises à jour régulières via `git pull` et `rebase`, Sébastien et son équipe ont réussi à créer une application de partage pour les étudiants. Chaque membre a pu travailler de manière indépendante sur sa fonctionnalité, puis les intégrer harmonieusement dans une version stable du projet.

