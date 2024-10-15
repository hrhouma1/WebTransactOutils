# pratique 01 - Guide de démarrage rapide avec Git

# Objectif

- Ce guide fournit une série de commandes Git de base pour initialiser un dépôt, ajouter des fichiers, configurer les informations d'utilisateur, et pousser les changements vers un dépôt distant.

# Étapes

# 0. Installez git :

- https://phoenixnap.com/kb/how-to-install-git-windows 

# 1. Initialiser un dépôt Git

Commencez par initialiser un nouveau dépôt Git dans votre répertoire de projet :

```bash
git init
```

# 2. Vérifier l'état du dépôt

Vous pouvez vérifier l'état de votre dépôt à tout moment avec :

```bash
git status
```

# 3. Créer des fichiers

Créez trois fichiers nommés `page1.txt`, `page2.txt`, et `page3.txt` :

```bash
touch page1.txt page2.txt page3.txt
```

# 4. Vérifier à nouveau l'état

Après avoir créé les fichiers, vérifiez l'état du dépôt :

```bash
git status
```

# 5. Ajouter les fichiers à l'index

Ajoutez tous les fichiers créés à l'index (staging area) :

```bash
git add .
```

# 6. Vérifier l'état après ajout

Vérifiez l'état du dépôt après avoir ajouté les fichiers :

```bash
git status
```

# 7. Configurer les informations utilisateur globales

Configurez votre nom et email utilisateur globalement :

```bash
git config --global user.name "hrhouma"
git config --global user.email "rehoumahaythem@gmail.com"
```

## Remarque :
- Vous pouvez remplacer "hrhouma" et "rehoumahaythem@gmail.com" par votre utilisateur global à vous

# 8. Configurer les informations utilisateur locales

Configurez des informations utilisateur spécifiques à ce dépôt :

```bash
git config --local user.name "dev"
git config --local user.email "dev_alex@gmail.com"
```
- Vous pouvez remplacer "dev" et "dev_alex@gmail.com" par votre utilisateur local à vous

# 9. Commit des fichiers

Enregistrez les modifications avec un message de commit :

```bash
git commit -m "Ajout des pages page1.txt page2.txt page3.txt"
```

# 10. Vérifier l'état après le commit

Vérifiez l'état de votre dépôt après avoir effectué le commit :

```bash
git status
```

# 11. Ajouter un dépôt distant

Ajoutez un dépôt distant nommé `origin` :

```bash
git remote add origin https://github.com/hrhouma/monsupersite.git
```
- Vous pouvez remplacer "https://github.com/hrhouma/monsupersite.git" par votre URL à vous

# 12. Renommer la branche principale

Renommez la branche principale en `master` :

```bash
git branch -M master
```

# 13. Pousser les changements vers le dépôt distant

Poussez vos changements vers la branche `master` sur le dépôt distant :

```bash
git push -u origin master
```

# 14. Vérifier la configuration Git

Pour voir la configuration actuelle de votre dépôt, utilisez :

```bash
cat .git/config
```



# point de vulgarisation:


- Ajouter des fichiers à l'index dans Git (git add . ou ce que nous appelons le staging area), c'est un peu comme préparer une valise avant un voyage.
- Imaginons que tu prépares un voyage (le commit) et que tu as plusieurs objets (les fichiers) éparpillés dans ta chambre. Avant de partir, tu veux t'assurer que tous les objets que tu veux emporter sont bien dans ta valise.
- Ajouter des fichiers à l'index avec `git add`, c'est comme mettre ces objets dans la valise. Cela signifie que tu es prêt à les emporter avec toi lors de ton voyage, c'est-à-dire lors du commit.
- Donc, l'index (ou "staging area") est comme ta valise de préparation : tu y mets tout ce que tu veux emporter dans ton prochain voyage, et une fois que tout est prêt, tu fermes la valise et tu pars, c'est-à-dire que tu fais le commit.

En résumé :
- **Git add** = Mettre des fichiers dans la valise (index).
- **Git commit** = Fermer la valise et partir en voyage (enregistrer les changements).

- Cela permet d'avoir un contrôle sur ce que tu veux vraiment inclure ou non dans le commit final, exactement comme tu choisirais soigneusement ce que tu veux emporter pour ton voyage.


- Le `git push`, c'est comme envoyer ta valise à la maison de vacances (le dépôt distant).
- Continuons avec l'analogie du voyage. Après avoir fermé ta valise (fait le commit), tu dois l'envoyer à ta destination finale, par exemple, une maison de vacances (ton dépôt distant, comme GitHub). Le `git push`, c'est l'action d'envoyer ta valise (tes changements) à cette destination.
- En d'autres termes, `git push` prend toutes les modifications que tu as préparées et enregistrées (dans ta valise) et les envoie à un endroit accessible à d'autres personnes (comme un dépôt sur GitHub), pour que tout le monde puisse y accéder, les voir, ou les utiliser.

Donc, en résumé :
- **Git add** = Mettre des fichiers dans la valise (préparer les changements).
- **Git commit** = Fermer la valise (enregistrer les changements).
- **Git push** = Envoyer la valise à ta destination (partager les changements avec tout le monde).

C'est comme si tu avais travaillé sur un projet dans ta chambre (ton dépôt local), puis que tu envoyais tout ton travail (les fichiers) à l'endroit où tes collègues peuvent le récupérer et continuer à travailler dessus.



| **Commande Git** | **Action Git**                         | **Analogie de la valise**                                           | **Description en vrai vie**                                   |
|------------------|----------------------------------------|---------------------------------------------------------------------|---------------------------------------------------------------|
| `git add`        | Ajouter les fichiers à l'index         | Mettre des objets dans la valise                                    | Préparer les fichiers à être inclus dans le prochain commit    |
| `git commit`     | Enregistrer les changements            | Fermer la valise et la préparer pour le voyage                      | Enregistrer définitivement les changements dans le dépôt local |
| `git push`       | Envoyer les changements vers un dépôt distant | Envoyer la valise à la maison de vacances (destination finale) | Partager les changements avec d'autres en les envoyant sur un dépôt distant (comme GitHub) |

### Explication détaillée :

- **Git add** : Imagine que tu choisis des vêtements et des objets pour un voyage. En les mettant dans la valise, tu te prépares à emporter ces articles. Avec `git add`, tu fais la même chose pour tes fichiers : tu les "prépares" à être inclus dans le commit.

- **Git commit** : Une fois ta valise bien remplie, tu la fermes et la prépares à être envoyée. Cela signifie que tout ce que tu as mis dans la valise est prêt et ne peut plus être changé. En faisant `git commit`, tu enregistres tous les fichiers ajoutés pour qu'ils soient une partie permanente de l'historique de ton projet.

- **Git push** : Enfin, tu envoies ta valise à ta destination de vacances. Tes amis ou ta famille peuvent ouvrir la valise et utiliser ce que tu y as mis. Avec `git push`, tu envoies tes commits vers un dépôt distant, comme GitHub, où d'autres peuvent accéder à ton travail.


# Résumé : l'analogie de la valise :

```
         +------------------+
         |  Dossier Projet   |             +------------------+
         |  (Local)          |             | Maison de Vacances|
         +--------+----------+             | (Dépôt Distant)   |
                  |                        +---------+--------+
                  |                                  |
        git init  |                                  |
                  V                                  |
         +--------+----------+                       |
         |  Répertoire Git   |                       |
         |  Initialisé       |                       |
         +--------+----------+                       |
                  |                                  |
        Créer     |                                  |
      des fichiers|                                  |
                  V                                  |
     +------------+-------------+                   |
     |   page1.txt, page2.txt,   |                  |
     |   page3.txt               |                  |
     +------------+-------------+                   |
                  |                                  |
        git add   |                                  |
        .         |                                  |
                  V                                  |
     +------------+-------------+                   |
     |  Fichiers ajoutés dans    |                  |
     |  l'index (valise)         |                  |
     +------------+-------------+                   |
                  |                                  |
     git commit   |                                  |
     -m "Ajout des|                                  |
     pages"       V                                  |
     +------------+-------------+                   |
     |  Valise (commit) fermée   |                  |
     |  et prête pour le voyage  |                  |
     +------------+-------------+                   |
                  |                                  |
     git push     |                                  |
                  V                                  V
         +--------+----------+            +---------+--------+
         |  Fichiers envoyés |------------| Fichiers reçus   |
         |  à la destination |            | à la destination |
         |  (Dépôt Distant)  |            | (Dépôt Distant)  |
         +------------------+             +------------------+
```

### Légende :
- **Dossier Projet (Local)** : Le répertoire où vous travaillez sur votre projet localement.
- **Maison de Vacances (Dépôt Distant)** : Le dépôt distant comme GitHub où vous envoyez votre travail.
- **Répertoire Git Initialisé** : Le dossier de projet qui a été initialisé pour utiliser Git.
- **Fichiers** : Les fichiers que vous créez et ajoutez à votre projet.
- **Index (Valise)** : L’endroit où vous préparez les fichiers pour les commits.
- **Commit** : L'action de fermer la valise, enregistrant définitivement les changements.
- **Push** : L'action d'envoyer la valise (vos commits) à la destination finale, où d'autres peuvent y accéder.

Ce schéma vous aide à visualiser comment chaque commande Git fonctionne dans le processus de gestion des fichiers et des versions dans un projet.
