

-----------------------------------------------------------------------
# Annexe : Différence entre `git merge` et `git rebase`. 
-----------------------------------------------------------------------

### Historique initial

Imaginons un projet où la branche principale est `master` avec trois commits initiaux :

```plaintext
(master)
A---B---C
```

Ensuite, on crée deux nouvelles branches depuis `master` :

1. **`feature-merge`** : pour tester `git merge`
2. **`feature-rebase`** : pour tester `git rebase`

### Travail dans chaque branche

Dans chaque branche, nous ajoutons trois nouveaux commits. Voici ce que cela donne :

```plaintext
(master)
A---B---C

(feature-merge)
       \
        D---E---F   # Commits sur feature-merge

(feature-rebase)
       \
        G---H---I   # Commits sur feature-rebase
```

### Étape 1 : Fusion de `feature-merge` dans `master` avec `git merge`

Pour `feature-merge`, nous utilisons la commande `git merge` sur la branche `master`. Cela crée un **commit de merge** qui garde un historique complet avec toutes les branches, sans réorganiser les commits. 

Voici l’historique après le `merge` :

```plaintext
(master)
A---B---C-------J      # J est le commit de merge
       |       /
       |      /
(feature-merge)
        D---E---F      # feature-merge garde son historique séparé
```

- **Explication** : `git merge` ajoute les commits de `feature-merge` (`D`, `E`, `F`) à l’historique de `master` sans les déplacer ni les modifier. Il crée simplement un nouveau commit `J` pour indiquer la fusion.
- **Observation** : Avec `git merge`, on voit un "point de jonction" dans l'historique où les deux branches se rencontrent. Cela permet de voir que `feature-merge` a été fusionnée avec `master`, tout en conservant l’historique distinct.

### Étape 2 : Fusion de `feature-rebase` dans `master` avec `git rebase`

Pour `feature-rebase`, nous utilisons `git rebase`. Au lieu de créer un commit de merge, `git rebase` déplace les commits (`G`, `H`, `I`) comme s'ils avaient été créés après `C` dans `master`. Voici l’historique après le `rebase` :

```plaintext
(master)
A---B---C---G'---H'---I'
```

- **Explication** : `git rebase` applique les commits de `feature-rebase` (`G`, `H`, `I`) à la suite des commits de `master` (après `C`). Les commits sont "rejoués" comme s’ils avaient été créés directement après `C`, donc ils apparaissent dans un ordre linéaire.
- **Observation** : Avec `git rebase`, l’historique est plus propre et linéaire, mais on perd le point de jonction qui montre l'existence d'une branche séparée.

### Comparaison finale

Pour résumer les différences observées dans le log Git :

- **git merge** : 
  - Garde l’historique complet avec les branches distinctes.
  - Crée un commit de fusion qui montre visuellement le moment où les deux branches se rejoignent.
  - **Avantage** : Idéal pour suivre un historique complet, particulièrement dans les projets collaboratifs.

- **git rebase** :
  - Réorganise l’historique pour le rendre linéaire, en plaçant les commits de `feature-rebase` comme s’ils avaient été faits après `C`.
  - **Avantage** : Rend l’historique plus propre, utile pour les projets où on veut minimiser les points de jonction dans le log.

En résumé :

```plaintext
git merge   ->  Historique complet avec commit de fusion
git rebase  ->  Historique linéaire sans commit de fusion
```

