-------------------------------------
# 04 git configuration
-------------------------------------

# **Configuration de Git**

La **configuration de Git** permet de définir les paramètres globaux ou locaux pour un projet Git. Lorsque vous créez un projet et que vous l'enregistrez dans un dépôt local, il est essentiel de spécifier le nom de l'auteur et son adresse email. Ces informations peuvent être stockées dans un fichier de configuration qui peut être global ou local.

## **Configuration globale**

Le fichier de configuration globale est commun à tous les projets Git sur un même système local. Si aucune configuration locale n'est définie, Git utilise la configuration globale. Un fichier `.gitconfig` est créé dans le dossier de l'utilisateur.

### Exemple : Créer un nom d'utilisateur et une adresse email dans le fichier de configuration globale

#### Étape 1 : Trouver le répertoire de l'utilisateur
Exécutez la commande suivante pour localiser le répertoire de l'utilisateur :
```bash
echo $HOME
```

#### Étape 2 : Créer un fichier de configuration globale et définir un auteur
Utilisez les commandes suivantes pour créer un fichier de configuration globale (le fichier `.gitconfig` dans le répertoire de l'utilisateur) et définir un nom et une adresse email pour l'auteur :
```bash
git config --global user.name "Haythem"
git config --global user.email "rehoumahaythem@gmail.com"
```

#### Étape 3 : Vérification du fichier de configuration
Après avoir exécuté ces commandes, vous pouvez vérifier le contenu du fichier `.gitconfig` en utilisant la commande suivante :
```bash
cat ~/.gitconfig
```

Le contenu du fichier `.gitconfig` ressemblera à ceci :
```
[user]
    name = Haythem
    email = rehoumahaythem@gmail.com
```

## **Étude de cas 1 : Configuration globale**

### Contexte :
Haythem est développeur de logiciels et travaille sur un projet appelé **MyProj** sur son ordinateur portable. Il utilise Git pour gérer le dépôt de son projet. Haythem souhaite définir son nom et son adresse email dans la configuration globale pour que ses contributions soient correctement enregistrées.

### Solution :
1. **Initialiser le dépôt Git pour le projet MyProj** :
   ```bash
   cd MyProj
   git init
   ```

2. **Définir le nom de l'auteur et l'email au niveau global** :
   ```bash
   git config --global user.name "Haythem"
   git config --global user.email "haythem@gmail.com"
   ```

3. **Créer un fichier de projet** (par exemple, `myfile_1.txt`) :
   ```bash
   touch myfile_1.txt
   ```

4. **Vérifier le statut Git du fichier** (il sera marqué comme non suivi) :
   ```bash
   git status
   ```

5. **Ajouter et committer les changements** :
   ```bash
   git add myfile_1.txt
   git commit -m "Ajout du fichier myfile_1.txt"
   ```

6. **Vérifier l'historique des commits** :
   ```bash
   git log
   ```
   L'historique montrera l'auteur comme "Haythem" et l'adresse email associée.

---

## **Configuration locale**

La configuration locale est spécifique à un projet Git particulier. Si plusieurs développeurs travaillent sur une même machine, chaque projet peut avoir ses propres paramètres de nom et d'email. La configuration locale est stockée dans le fichier `.git/config` du projet.

### Exemple : Créer un nom d'utilisateur et une adresse email dans la configuration locale

#### Étape 1 : Initialiser un projet Git
```bash
cd LocalConfigProj
git init
```

#### Étape 2 : Définir le nom de l'auteur et l'email au niveau local
Utilisez les commandes suivantes pour définir le nom de l'auteur et l'adresse email spécifiques à ce projet :
```bash
git config --local user.name "Haythem Local"
git config --local user.email "localhaythem@gmail.com"
```

#### Étape 3 : Vérifier le fichier de configuration locale
Le fichier `.git/config` du projet contiendra :
```
[user]
    name = Haythem Local
    email = localhaythem@gmail.com
```

## **Étude de cas 2 : Configuration locale**

### Contexte :
Haythem doit désormais travailler sur un serveur de développement où plusieurs développeurs collaborent. Il ne souhaite pas utiliser la configuration globale, mais préfère définir un nom et une adresse email spécifiques au projet pour que ses contributions soient correctement enregistrées.

### Solution :
1. **Initialiser le dépôt Git pour le projet LocalConfigProj** :
   ```bash
   cd LocalConfigProj
   git init
   ```

2. **Définir le nom de l'auteur et l'email au niveau local** :
   ```bash
   git config --local user.name "Haythem_dev"
   git config --local user.email "dev_haythem@company.com"
   ```

3. **Créer un fichier de projet** (par exemple, `myfile_1.txt`) :
   ```bash
   touch myfile_1.txt
   ```

4. **Vérifier le statut Git du fichier** :
   ```bash
   git status
   ```

5. **Ajouter et committer les changements** :
   ```bash
   git add myfile_1.txt
   git commit -m "Ajout du fichier myfile_1.txt"
   ```

6. **Vérifier l'historique des commits** :
   ```bash
   git log
   ```
   L'historique montrera l'auteur comme "Haythem_dev" avec l'email correspondant.

---

## **Conclusion**

La configuration Git est une étape essentielle pour assurer que chaque commit est correctement attribué à l'auteur avec les informations appropriées. Il est possible de configurer Git au niveau global ou local, en fonction du contexte de développement. La configuration globale est utile pour les projets personnels ou sur une machine dédiée, tandis que la configuration locale est pratique lorsque plusieurs développeurs partagent un même environnement.

---

Ce cours vous a montré comment configurer Git aussi bien au niveau global que local, avec des études de cas pour illustrer les différents scénarios d'utilisation.
