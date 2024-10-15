# Restauration du Répertoire `semaine3`

## Contexte

Haythem travaille sur un projet. Ce projet contient un répertoire nommé `semaine3` qui a été accidentellement supprimé dans un commit récent. Ce document décrit les étapes suivies pour restaurer ce répertoire à partir de l'historique Git.

## Étapes de Restauration

### 1. **Vérification de l'historique des commits**

La première étape a consisté à vérifier l'historique des commits pour identifier le commit dans lequel le répertoire `semaine3` a été supprimé.

```bash
git log -- semaine3/
```

Cette commande a révélé que le commit `4839147759c6d18e051fc5672213e6fab2681445` a supprimé le répertoire `semaine3`. Les commits précédents ont été examinés pour trouver celui dans lequel le répertoire existait encore.

### 2. **Identification du Dernier Commit où `semaine3` Existait**

Le commit `b2dce13edae91ac81f196b8fb859337dd415ec2c` a été identifié comme étant le dernier commit où le répertoire `semaine3` existait avant sa suppression.

### 3. **Restauration du Répertoire `semaine3`**

Pour restaurer le répertoire `semaine3`, la commande suivante a été exécutée :

```bash
git checkout b2dce13edae91ac81f196b8fb859337dd415ec2c -- semaine3/
```

Cette commande a restauré tout le contenu du répertoire `semaine3` tel qu'il était dans le commit `b2dce13edae91ac81f196b8fb859337dd415ec2c`.

### 4. **Vérification des Fichiers Restaurés**

Après avoir restauré le répertoire, une vérification manuelle a été effectuée pour s'assurer que tous les fichiers attendus étaient présents dans `semaine3`.

### 5. **Validation et Push des Changements**

Une fois la restauration confirmée, les fichiers ont été ajoutés à l'index de Git et un commit a été créé pour valider la restauration :

```bash
git add semaine3/
git commit -m "Restauration du répertoire semaine3"
git push origin main
```

Ce commit a été poussé vers le dépôt distant, rendant le répertoire `semaine3` à nouveau disponible dans le projet.

## Conclusion

Ces étapes ont permis de restaurer avec succès le répertoire `semaine3` dans le projet. L'historique Git reste intact, et le répertoire est maintenant de nouveau disponible dans l'état où il était avant sa suppression.

----
----
----

# ANNEXE PLUS DÉTAILLÉ - Histoire de la Restauration du Répertoire `semaine3`

## Contexte

Dans ce projet, le répertoire `semaine3`, contenant plusieurs fichiers importants, a été accidentellement supprimé dans un commit récent. Pour corriger cette erreur, nous avons utilisé les fonctionnalités de Git pour restaurer le répertoire à son état précédent. Ce document retrace les étapes suivies, les commandes exécutées, et les sorties obtenues lors de ce processus de restauration.

## Étape 1 : Vérification de l'Historique des Commits

Tout d'abord, il était nécessaire de comprendre quand et comment le répertoire `semaine3` avait été supprimé. Nous avons utilisé la commande suivante pour afficher l'historique des commits affectant ce répertoire :

```bash
git log -- semaine3/
```

### Sortie de la commande :
```plaintext
commit 4839147759c6d18e051fc5672213e6fab2681445 (HEAD -> main, origin/main, origin/HEAD)
Author: hrhouma1 <rhoumahaythem@gmail.com>
Date:   Sun Sep 1 20:22:43 2024 -0400

    Delete semaine3 directory

commit b2dce13edae91ac81f196b8fb859337dd415ec2c
Author: hrhouma1 <rhoumahaythem@gmail.com>
Date:   Sun Sep 1 20:22:30 2024 -0400

    Create 03-DRAFT.md

commit 40550a725338256a41048dec648093f83fbee3c9
Author: hrhouma1 <rhoumahaythem@gmail.com>
Date:   Sun Sep 1 20:12:48 2024 -0400

    Update and rename 02.md to 02-SMB et Sécurisation du Trafic SMB.md

commit de6e311f3724ccf9a01b8b66bb54cf4ed8d7a1b5
Author: hrhouma1 <rhoumahaythem@gmail.com>
Date:   Sun Sep 1 20:12:19 2024 -0400

    Create 02.md

commit 61b0b205885efaef93e6bc1cb5941841fb1c15af
Author: hrhouma1 <rhoumahaythem@gmail.com>
Date:   Sun Sep 1 20:11:45 2024 -0400

    Rename 01-cours.md to 01-Analyse des activités systèmes et réseaux.md
```

### Analyse :

- Le commit `4839147759c6d18e051fc5672213e6fab2681445` est celui où le répertoire `semaine3` a été supprimé.
- Le commit précédent, `b2dce13edae91ac81f196b8fb859337dd415ec2c`, est celui où les fichiers dans `semaine3` étaient encore présents.

## Étape 2 : Identification du Dernier Commit où `semaine3` Existait

Nous avons identifié que le dernier commit avant la suppression était `b2dce13edae91ac81f196b8fb859337dd415ec2c`. C'est à partir de ce commit que nous allons restaurer le répertoire.

## Étape 3 : Restauration du Répertoire `semaine3`

Pour restaurer le répertoire supprimé, nous avons utilisé la commande suivante :

```bash
git checkout b2dce13edae91ac81f196b8fb859337dd415ec2c -- semaine3/
```

### Sortie de la commande :

Cette commande ne produit pas de sortie visible si elle réussit, mais elle restaure les fichiers dans le répertoire `semaine3` dans l'état où ils étaient dans le commit `b2dce13edae91ac81f196b8fb859337dd415ec2c`.

## Étape 4 : Vérification des Fichiers Restaurés

Une fois le répertoire `semaine3` restauré, nous avons vérifié manuellement que tous les fichiers attendus étaient bien présents :

- `01-Analyse des activités systèmes et réseaux.md`
- `02-SMB et Sécurisation du Trafic SMB.md`
- `03-DRAFT.md`
- `readme.md`

Tous les fichiers ont été restaurés avec succès.

## Étape 5 : Validation et Push des Changements

Après avoir confirmé que tout était en ordre, nous avons ajouté les fichiers restaurés à l'index de Git et créé un nouveau commit pour valider ces changements :

```bash
git add semaine3/
git commit -m "Restauration du répertoire semaine3"
git push origin main
```

### Sortie de la commande `git commit` :
```plaintext
[main 789c1a7] Restauration du répertoire semaine3
 4 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 semaine3/01-Analyse des activités systèmes et réseaux.md
 create mode 100644 semaine3/02-SMB et Sécurisation du Trafic SMB.md
 create mode 100644 semaine3/03-DRAFT.md
 create mode 100644 semaine3/readme.md
```

### Sortie de la commande `git push` :
```plaintext
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (4/4), 465 bytes | 465.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To https://github.com/nom-utilisateur/nom-du-depot.git
   4839147..789c1a7  main -> main
```

## Conclusion

Grâce à ces manipulations, nous avons pu restaurer avec succès le répertoire `semaine3` qui avait été accidentellement supprimé. Cette démarche montre l'importance de bien comprendre l'historique des commits dans Git et comment utiliser les commandes appropriées pour restaurer des éléments supprimés. En suivant ces étapes, vous pouvez éviter la perte de données et maintenir l'intégrité de votre projet.
