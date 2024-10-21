# 1 - Différences entre `git merge` et `git rebase`  :

![image](https://github.com/user-attachments/assets/2cd31f13-b077-4b93-935c-5f4bb193825e)

### Git Merge
- **Opération :** `git merge develop`
- **Objectif :** Intégrer les modifications d'une branche (`develop`) dans une autre (`feature/login`).
- **Processus :** Git crée un nouveau "commit de fusion" qui a deux parents, un pour le dernier commit de chaque branche. Cela préserve l'historique tel qu'il s'est produit.
- **Résultat :** L'historique de la branche `feature/login` montre une structure avec une bifurcation, où le commit de fusion combine les historiques des deux branches.

### Git Rebase
- **Opération :** `git rebase develop`
- **Objectif :** Appliquer de nouveau les commits sur le sommet d'une autre branche de base.
- **Processus :** Rebaser prend les modifications faites dans la branche `feature/login` et les réapplique sur le sommet de la branche `develop`.
- **Résultat :** Cela rend l'historique linéaire, comme si les modifications avaient été faites juste après les dernières modifications dans `develop`.

### Différences Clés
- **Préservation de l'historique :** Merge ne modifie pas l'historique existant, tandis que rebase réécrit l'historique des commits pour le rendre linéaire.
- **Résolution de conflits :** Avec merge, les conflits sont résolus à la fin du processus de fusion, tandis que rebase peut nécessiter de résoudre des conflits tout au long du processus à mesure que chaque commit est réappliqué.

En bref, `merge` est utilisé pour conserver un historique précis des changements, tandis que `rebase` est préféré pour simplifier l'historique avant l'intégration d'une branche de fonctionnalités.


# 2 - Encore pas claire ?


# Git Merge
- **Ce que ça fait :** Fusionne les changements de deux branches en une seule. Il combine les chemins de développement.
- **Comment ça fonctionne :** Il crée un nouveau commit qui a deux parents. Chaque parent représente le dernier commit de chaque branche avant la fusion.
- **Historique des commits :** L'historique montre clairement quand les branches ont divergé et fusionné. Cela ressemble à un graphique avec un point où deux lignes se rejoignent pour former une seule.

# Git Rebase
- **Ce que ça fait :** Change la base de votre branche de fonctionnalités pour qu'elle apparaisse comme si elle avait été créée à partir du dernier commit de la branche `develop`.
- **Comment ça fonctionne :** Il prend les commits de la branche de fonctionnalités et les "rejoue" un par un sur le sommet de la branche `develop`.
- **Historique des commits :** L'historique devient linéaire. On ne voit pas de bifurcation comme avec `merge`. Cela donne l'impression que tous les changements ont été faits dans l'ordre, sans développement parallèle.

# Pourquoi choisir l'un ou l'autre ?
- **Merge :** Utilisé pour préserver l'historique complet et explicite de votre projet. C'est utile lorsque vous voulez voir les points précis où les changements ont été combinés.
- **Rebase :** Utilisé pour créer un historique plus propre et plus simple. C'est pratique si vous voulez que votre historique semble avoir une séquence de développement directe sans branches secondaires.

En gros, si vous voulez que l'historique de votre projet montre comment les fonctionnalités ont été développées en parallèle et combinées, utilisez `merge`. Si vous préférez que votre historique soit simple et direct (comme si tout avait été développé dans un ordre linéaire), utilisez `rebase`.
