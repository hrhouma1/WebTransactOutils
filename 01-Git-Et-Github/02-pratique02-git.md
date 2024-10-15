# L'histoire d'Eric : Un développeur passionné et ses amis

Eric (vous dans cet exercice) est un développeur passionné par la technologie. Désireux de créer un CV qui reflète son parcours professionnel et ses compétences, il décide de se lancer dans ce projet. Mais Eric n'est pas seul dans cette aventure : ses amis, à gauche et à droite, l'accompagnent pour lui donner des recommandations et des conseils précieux tout au long du processus.

- Voici comment Eric et ses amis construisent ensemble un CV remarquable à travers les commandes Git.

## Projet : La création du CV d'Eric

### 1. Créer un nouveau répertoire appelé `monCV`

Eric commence par créer un nouvel espace de travail pour son projet de CV :

```bash
mkdir monCV
```

### 2. Naviguer dans le répertoire `monCV`

Il entre ensuite dans ce répertoire pour commencer à travailler :

```bash
cd monCV
```

### 3. Initialiser un dépôt Git

Pour suivre l'évolution de son CV, Eric initialise un dépôt Git local dans ce répertoire :

```bash
git init
```

### 4. Vérifier l'état du dépôt

Il vérifie l'état actuel du dépôt pour voir ce qui est suivi ou non :

```bash
git status
```

### 5. Configurer les informations utilisateur globales

Eric configure son nom et son email utilisateur globalement afin que chaque changement qu'il apportera à son CV soit correctement identifié :

```bash
git config --global user.name "votreUserGithub"
git config --global user.email "votreVraiEmailGithub"
```

### exemple : 

Pour Eric :
```bash
git config --global user.name "eric-michaud"
git config --global user.email "michaud_e@hotmail.com"
```

Remplacez les commandes ci-dessus par les informations d'utilisateur appropriées lorsque vous changez d'utilisateur. Si vous avez besoin de changer fréquemment d'utilisateur, vous pouvez créer différents profils Git ou utiliser un script pour automatiser les changements de configuration (**Voir** *Annexe1*).

### 6. Créer un fichier pour commencer à rédiger le CV

Il crée un fichier appelé `cvEric.txt` pour commencer à raconter son histoire professionnelle :

```bash
touch cvEric.txt
```

### 7. Vérifier à nouveau l'état du dépôt

Après avoir créé le fichier, Eric vérifie l'état du dépôt pour voir où il en est :

```bash
git status
```

### 8. Ajouter le fichier à l'index

Eric ajoute le fichier `cvEric.txt` à l'index pour que son travail soit sauvegardé et prêt à être partagé :

```bash
git add cvEric.txt
```

### 9. Vérifier l'état après ajout

Il vérifie l'état du dépôt après avoir ajouté le fichier pour s'assurer que tout est en ordre :

```bash
git status
```

### 10. Configurer les informations utilisateur locales

Eric configure des informations utilisateur spécifiques à ce dépôt pour personnaliser davantage son projet :

```bash
git config --local user.name "votreUserGithub"
git config --local user.email "votreVraiEmailGithub"
```

### 11. Commit des fichiers

Il enregistre les modifications avec un message de commit, scellant ainsi la première version de son CV :

```bash
git commit -m "The journey begins: First draft of my CV added"
```

### 12. Ajouter un dépôt distant

Eric ajoute un dépôt distant pour partager son CV avec le monde :

```bash
git remote add origin VOTRE_URL
```
- Remplacez "VOTRE_URL" par l'URL de votre dépôt GitHub.

### 13. Renommer la branche principale

Il renomme la branche principale en `main`, marquant le début officiel de son projet :

```bash
git branch -M main
```

### 14. Pousser les changements vers le dépôt distant

Eric pousse ses changements vers la branche `main` sur le dépôt distant, lançant ainsi son CV dans l'univers numérique :

```bash
git push -u origin main
```

### 15. Écrire une introduction avec l'aide de son ami à gauche

Eric commence à écrire une introduction pour que les lecteurs puissent mieux le connaître. Son ami à gauche lui donne des conseils pour rendre cette introduction plus captivante :

```bash
echo "Bonjour, je suis Sébastien et je recommande Eric. C'est un développeur passionné par la technologie." >> cvEric.txt
```

### 16. Configurer les informations utilisateur de son ami à gauche

Pour refléter l'aide précieuse de son ami à gauche, Eric configure les informations utilisateur de ce dernier :

```bash
git config --local user.name "usernameamiacotedevousa-gauche"
git config --local user.email "EmailGithubdevotreamiacotedevousa-gauche"
```

### exemple : 


Pour Sébastien (sgag-2-6):
```bash
git config --global user.name "sgag-2-6"
git config --global user.email "seb.s.gag@gmail.com"
```


### 17. Commit de l'introduction ajoutée

Il scelle cette belle introduction dans un commit, honorant l'aide de son ami :

```bash
git add .
git status
git commit -m "A friend's touch: Introduction added by l'ami à gauche"
git status
```

### 18. Pousser les changements vers le dépôt distant

Eric pousse ces nouveaux changements vers le dépôt distant pour que cette introduction soit partagée avec tous :

```bash
git push origin main
```

### 19. Ajouter des certifications et mises à jour des diplômes avec l'aide de son ami à droite

Eric ajoute maintenant ses réalisations les plus significatives avec l'aide de son ami à droite, montrant ainsi ses compétences et qualifications :

```bash
echo "Je suis Michael. Je vais ajouter des certifications au CV d'ERIC - AWS Certified Solutions Architect" >> cvEric.txt
```

### 20. Configurer les informations utilisateur de son ami à droite

Pour refléter l'aide de son ami à droite, Eric configure les informations utilisateur de ce dernier :

```bash
git config --local user.name "usernameamiacotedevousa-DROITE"
git config --local user.email "EmailGithubdevotreamiacotedevousa-DROITE"
```

### exemple : 

Pour Michael (HashMapScreft):
```bash
git config --global user.name "HashMapScreft"
git config --global user.email "screft@hotmail.com"
```

### 21. Commit des certifications et diplômes ajoutés

Eric scelle cette étape importante dans un commit, posant une pierre angulaire dans l'édifice de sa carrière :

```bash
git add .
git status
git commit -m "Milestones achieved: Certifications and diplomas added by l'ami à droite"
git status
```

### 22. Pousser les changements vers le dépôt distant

Enfin, Eric pousse ces nouvelles réalisations vers le dépôt distant, complétant ainsi son CV pour qu'il soit prêt à impressionner le monde :

```bash
git push origin main
```

---

Ainsi, Eric, avec l'aide de ses amis, a réussi à créer un CV qui non seulement reflète ses compétences et réalisations, mais aussi l'amitié et le soutien dont il a bénéficié tout au long de son parcours. Ce script raconte une histoire à travers les commandes Git, où chaque commit capture un moment significatif dans l'évolution du CV d'Eric. Les descriptions des commits ajoutent une touche narrative, transformant un simple projet technique en une aventure collaborative et enrichissante.

# Résumé 

```bash
# Créer un nouveau répertoire appelé monCV
mkdir monCV

# Naviguer dans le répertoire monCV
cd monCV

# Initialiser un dépôt Git local dans le répertoire monCV
git init

# Vérifier l'état actuel du dépôt Git (affiche les fichiers suivis et non suivis)
git status

# Configurer votre nom d'utilisateur global pour Git
git config --global user.name "votreUserGithub"

# Configurer votre adresse email globale pour Git
git config --global user.email "votreVraiEmailGithub"

# Créer un nouveau fichier texte appelé cvEric.txt pour commencer à rédiger votre CV
touch cvEric.txt

# Vérifier à nouveau l'état du dépôt Git (le fichier cvEric.txt apparaîtra comme non suivi)
git status

# Ajouter le fichier cvEric.txt au suivi dans Git pour que votre travail soit sauvegardé et prêt à être partagé
git add cvEric.txt

# Vérifier l'état du dépôt Git pour confirmer que cvEric.txt est maintenant suivi
git status

# Configurer votre nom d'utilisateur local pour ce dépôt Git
git config --local user.name "votreUserGithub"

# Configurer votre adresse email locale pour ce dépôt Git
git config --local user.email "votreVraiEmailGithub"

# Effectuer un commit pour immortaliser la première version de votre CV, comme si vous graviez votre premier chapitre dans l'histoire de votre carrière
git commit -m "The journey begins: First draft of my CV added"

# Ajouter une nouvelle origine distante pointant vers votre dépôt GitHub, où votre histoire numérique sera partagée avec le monde
git remote add origin VOTRE_URL

# Renommer la branche actuelle en 'main' pour symboliser le début officiel de votre voyage
git branch -M main

# Pousser le contenu de la branche 'main' vers l'origine distante, lançant ainsi votre CV dans l'univers numérique
git push -u origin main

# Modification 1 : Vous commencez à écrire votre introduction, un premier aperçu de qui vous êtes et de vos aspirations
echo "Bonjour, je m'appelle Eric, et je suis un développeur passionné par la technologie. Voici une brève introduction sur moi." >> cvEric.txt

# Configurer le nom d'utilisateur de votre ami à votre gauche pour ce dépôt Git
git config --local user.name "usernameamiacotedevousa-gauche"

# Configurer l'adresse email de votre ami à votre gauche pour ce dépôt Git
git config --local user.email "EmailGithubdevotreamiacotedevousa-gauche"

# Effectuer un commit pour capturer ce moment où votre ami vous aide à raconter votre histoire
git add .
git commit -m "A friend's touch: Introduction added by l'ami à gauche"

# Pousser le contenu de la branche 'main' vers l'origine distante avec le nom de votre ami à gauche
git push origin main

# Modification 2 : Vous ajoutez vos réalisations, les

 fruits de votre travail, pour montrer au monde ce que vous avez accompli
echo "Ajout des certifications : AWS Certified Solutions Architect, Google Cloud Professional Data Engineer. Mise à jour des diplômes : Master en Informatique." >> cvEric.txt

# Configurer le nom d'utilisateur de votre ami à votre droite pour ce dépôt Git
git config --local user.name "usernameamiacotedevousa-DROITE"

# Configurer l'adresse email de votre ami à votre droite pour ce dépôt Git
git config --local user.email "EmailGithubdevotreamiacotedevousa-DROITE"

# Effectuer un commit pour immortaliser ces ajouts, comme si vous posiez une pierre angulaire dans l'édifice de votre carrière
git add .
git commit -m "Milestones achieved: Certifications and diplomas added by l'ami à droite"

# Pousser le contenu de la branche 'main' vers l'origine distante avec le nom de votre ami à droite
git push origin main
```



# Exemple de configurations : 

Pour Eric :
```bash
git config --global user.name "eric-michaud"
git config --global user.email "michaud_e@hotmail.com"
```

Pour Sébastien (sgag-2-6):
```bash
git config --global user.name "sgag-2-6"
git config --global user.email "seb.s.gag@gmail.com"
```

Pour Michael (HashMapScreft):
```bash
git config --global user.name "HashMapScreft"
git config --global user.email "screft@hotmail.com"
```

----

# Annexe 1 : Automatiser la création des profils

----


Je vous propose un exemple de création de différents profils Git et d'un script pour automatiser les changements de configuration.

### 1. Création de différents profils Git

Vous pouvez créer des fichiers de configuration Git spécifiques à chaque utilisateur dans votre répertoire personnel. Par exemple :

- **~/.gitconfig_eric**
```bash
[user]
    name = eric-michaud
    email = michaud_e@hotmail.com
```

- **~/.gitconfig_sebastien**
```bash
[user]
    name = sgag-2-6
    email = seb.s.gag@gmail.com
```

- **~/.gitconfig_michael**
```bash
[user]
    name = HashMapScreft
    email = screft@hotmail.com
```

### 2. Script pour changer de profil

Créez un script bash pour automatiser le changement de profil. Par exemple :

**~/.change_git_profile.sh**
```bash
#!/bin/bash

if [ "$1" == "eric" ]; then
    cp ~/.gitconfig_eric ~/.gitconfig
    echo "Profil Git changé pour Eric (eric-michaud)."
elif [ "$1" == "sebastien" ]; then
    cp ~/.gitconfig_sebastien ~/.gitconfig
    echo "Profil Git changé pour Sébastien (sgag-2-6)."
elif [ "$1" == "michael" ]; then
    cp ~/.gitconfig_michael ~/.gitconfig
    echo "Profil Git changé pour Michael (HashMapScreft)."
else
    echo "Usage : $0 {eric|sebastien|michael}"
fi
```

### 3. Utilisation du script

Donnez des permissions d'exécution au script et utilisez-le pour changer de profil :

```bash
chmod +x ~/.change_git_profile.sh

# Pour changer de profil à Eric
~/.change_git_profile.sh eric

# Pour changer de profil à Sébastien
~/.change_git_profile.sh sebastien

# Pour changer de profil à Michael
~/.change_git_profile.sh michael
```

Avec ce script, vous pouvez facilement changer de profil Git en exécutant une simple commande, ce qui est particulièrement utile si vous travaillez régulièrement avec plusieurs comptes GitHub.

----

# Annexe 2 : Méthode 2

----


- *Objectif* :  créer les fichiers de configuration et le script nécessaire pour gérer plusieurs profils Git, en utilisant `sh ~/change_git_profile.sh` pour exécuter le script.

### 1. Création des fichiers de configuration pour chaque profil
Ouvrez votre terminal et exécutez les commandes suivantes pour créer les fichiers de configuration pour chaque profil Git.

**Pour Eric :**
```bash
cd ~
cat << EOF > .gitconfig_eric
[user]
    name = eric-michaud
    email = michaud_e@hotmail.com
EOF
```

**Pour Sébastien :**
```bash
cat << EOF > .gitconfig_sebastien
[user]
    name = sgag-2-6
    email = seb.s.gag@gmail.com
EOF
```

**Pour Michael :**
```bash
cat << EOF > .gitconfig_michael
[user]
    name = HashMapScreft
    email = screft@hotmail.com
EOF
```

### 2. Création du script pour changer de profil
Créez un script bash qui vous permettra de changer facilement de profil Git en fonction de l'utilisateur.

```bash
cd ~
cat << EOF > change_git_profile.sh
#!/bin/bash

# Vérification de l'argument passé au script
if [ "\$1" == "eric" ]; then
    cp ~/.gitconfig_eric ~/.gitconfig
    echo "Profil Git changé pour Eric (eric-michaud)."
elif [ "\$1" == "sebastien" ]; then
    cp ~/.gitconfig_sebastien ~/.gitconfig
    echo "Profil Git changé pour Sébastien (sgag-2-6)."
elif [ "\$1" == "michael" ]; then
    cp ~/.gitconfig_michael ~/.gitconfig
    echo "Profil Git changé pour Michael (HashMapScreft)."
else
    echo "Usage : \$0 {eric|sebastien|michael}"
fi
EOF
```

### 3. Rendre le script exécutable
Assurez-vous que le script est exécutable en utilisant la commande suivante :

```bash
chmod +x ~/change_git_profile.sh
```

### 4. Utilisation du script
Vous pouvez maintenant utiliser le script pour changer de profil Git rapidement. Par exemple :

**Pour changer au profil de Eric :**
```bash
sh ~/change_git_profile.sh eric
```

**Pour changer au profil de Sébastien :**
```bash
sh ~/change_git_profile.sh sebastien
```

**Pour changer au profil de Michael :**
```bash
sh ~/change_git_profile.sh michael
```

### 5. Validation de la configuration actuelle
Pour vérifier la configuration Git en cours après avoir changé de profil, vous pouvez exécuter :

```bash
git config --global --list
```

Ce processus vous permet de gérer plusieurs profils Git de manière simple et efficace, avec la possibilité de passer d'un utilisateur à l'autre en fonction de vos besoins.
