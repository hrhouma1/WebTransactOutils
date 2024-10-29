
# **Annexe : Différence entre `git merge` et `git rebase`**

---

### Contexte

Dans cet exemple, nous avons un dépôt avec une branche principale `main` contenant un fichier de base `fichier1.txt` et un premier commit initial. À partir de `main`, nous créons deux branches, `branche1` et `branche2`, chacune étant destinée à tester respectivement `rebase` et `merge`. Ensuite, deux branches de travail supplémentaires sont créées, `branche-rebase` depuis `branche1` et `branche-merge` depuis `branche2`, pour y ajouter des modifications.

### Historique initial

Le projet commence avec un dépôt contenant un seul commit sur `main`, correspondant à la création du fichier `fichier1.txt` :

```plaintext
(main)
A               # Commit initial avec fichier1.txt
```

Dans le commit `A`, nous avons ajouté le fichier `fichier1.txt` avec du contenu initial.

Ensuite, deux nouvelles branches sont créées à partir de `main` :

1. **`branche1`** : destinée à accueillir `branche-rebase` pour tester `git rebase`.
2. **`branche2`** : destinée à accueillir `branche-merge` pour tester `git merge`.

---

### Travail dans chaque branche de travail

Dans chaque branche de travail (`branche-rebase` et `branche-merge`), nous effectuons trois commits distincts. Voici les commits en détail pour chaque branche :

```plaintext
(main)
A

(branche-rebase)
       \
        D---E---F   # Commits ajoutés sur branche-rebase

(branche-merge)
       \
        G---H---I   # Commits ajoutés sur branche-merge
```

1. **Commits sur `branche-rebase` :**
   - **Commit D** : Création du fichier `fichier-2-rebase.txt` avec le contenu initial "Modification 1 dans branche-rebase".
   - **Commit E** : Ajout de "Modification 2 dans branche-rebase" dans le même fichier `fichier-2-rebase.txt`.
   - **Commit F** : Ajout de "Modification 3 dans branche-rebase" dans le même fichier `fichier-2-rebase.txt`.

2. **Commits sur `branche-merge` :**
   - **Commit G** : Création du fichier `fichier-2-merge.txt` avec le contenu initial "Modification 1 dans branche-merge".
   - **Commit H** : Ajout de "Modification 2 dans branche-merge" dans le même fichier `fichier-2-merge.txt`.
   - **Commit I** : Ajout de "Modification 3 dans branche-merge" dans le même fichier `fichier-2-merge.txt`.

Ces commits ajoutent du contenu identique, mais dans des fichiers différents (`fichier-2-rebase.txt` et `fichier-2-merge.txt`), pour permettre une comparaison claire entre `merge` et `rebase`.

---

### Étape 1 : Fusion de `branche-merge` dans `branche2` avec `git merge`

Pour intégrer les modifications de `branche-merge` dans `branche2`, nous utilisons la commande `git merge` sur `branche2`. Cette opération crée un **commit de fusion** qui conserve un historique complet et inclut les commits de la branche de travail sans les réorganiser.

L’historique après le `merge` :

```plaintext
(branche2)
A-------J        # J est le commit de fusion
 \       |
  \      |
   G---H---I     # branche-merge conserve son historique distinct
```

- **Explication des commits** : 
   - **Commit J** : Commit de fusion qui combine le contenu de `branche2` avec les modifications de `branche-merge` (`G`, `H`, `I`) sans les déplacer ni modifier leur ordre.
- **Observation** : Avec `git merge`, l'historique montre un "point de jonction" qui indique visuellement où `branche-merge` a été fusionnée dans `branche2`. Cela conserve un historique complet et distinct pour chaque branche, ce qui est souvent utile dans des projets collaboratifs.

---

### Étape 2 : Intégration de `branche-rebase` dans `branche1` avec `git rebase`

Pour intégrer les modifications de `branche-rebase` dans `branche1`, nous utilisons la commande `git rebase`. Contrairement à `merge`, `rebase` repositionne les commits (`D`, `E`, `F`) de `branche-rebase` comme s'ils avaient été créés après le dernier commit de `branche1` (`A`).

L’historique après le `rebase` :

```plaintext
(branche1)
A---D'---E'---F'   # Commits de branche-rebase réappliqués en fin de branche1
```

- **Explication des commits** :
   - **Commits D', E', F'** : Commits rejoués de `branche-rebase` appliqués linéairement à la suite de `A` sur `branche1`.
- **Observation** : Avec `git rebase`, les commits de `branche-rebase` sont réorganisés pour former un historique linéaire sans "point de jonction", comme s’ils avaient été ajoutés directement après le commit initial `A`. Cela simplifie l'historique en le rendant plus propre, mais il peut masquer le chemin des branches de travail initiales.

---

### Comparaison finale

Les différences observées dans les logs Git permettent de mieux comprendre les usages spécifiques de `merge` et `rebase`.

- **git merge** :
  - **Effet** : Maintient un historique complet avec un commit de fusion qui marque la jonction des branches.
  - **Avantage** : Idéal pour suivre un historique complet dans des projets collaboratifs, car chaque jonction est visible.
  - **Inconvénient** : L’historique peut devenir complexe avec de nombreuses jonctions, surtout dans les projets avec plusieurs branches.

- **git rebase** :
  - **Effet** : Réorganise les commits pour les placer linéairement en fin de la branche principale, sans créer de commit de fusion.
  - **Avantage** : Idéal pour un historique linéaire et propre, en minimisant les jonctions. Cela est souvent préféré dans les petits projets ou pour nettoyer l'historique avant de le partager.
  - **Inconvénient** : Peut masquer le chemin des branches de travail, ce qui peut poser problème si plusieurs personnes travaillent sur les mêmes branches.

---

### Résumé

| Commande        | Historique                             | Cas d'utilisation idéal                   |
|-----------------|---------------------------------------|-------------------------------------------|
| `git merge`     | Historique complet avec point de jonction | Projets collaboratifs avec plusieurs branches |
| `git rebase`    | Historique linéaire sans points de jonction | Nettoyage de l’historique avant un merge partagé |

En résumé :

```plaintext
git merge   ->  Historique complet avec commit de fusion
git rebase  ->  Historique linéaire sans commit de fusion
```

Ce guide vous permet de comprendre et visualiser les différences entre `git merge` et `git rebase`, et de choisir la méthode la plus adaptée en fonction de votre contexte de projet.
