# **Question :**

Vous travaillez avec deux branches dans votre projet Git : `branche1` et `branche_rebase`. Sur `branche_rebase`, vous avez effectué trois commits pour apporter des modifications. Vous souhaitez intégrer ces modifications dans `branche1`, alors vous basculez sur `branche1` et effectuez un `rebase` sur `branche_rebase`.

1. **Avant** le rebase, vous exécutez `git log` sur `branche_rebase` et voyez les trois commits avec leurs identifiants de commit (*hashes*).
2. **Après** le rebase, vous exécutez `git log` sur `branche1` et vous vous attendez à voir les trois commits de `branche_rebase`, mais avec des identifiants de commit modifiés. Cependant, vous remarquez que les *hashes* des trois commits sont restés inchangés dans `branche1`.

**Expliquez pourquoi les identifiants de commits n'ont pas été modifiés après le rebase.**

**Points de réflexion pour guider votre réponse :**
1. Pourquoi Git ne réécrit-il pas toujours les identifiants de commits lors d'un rebase ?
2. Dans quelles conditions Git peut-il effectuer un *fast-forward* pendant un rebase, laissant les identifiants de commits inchangés ?


# Réponse : 
Cela se produit probablement parce que le `rebase` que vous avez effectué était en réalité un *fast-forward rebase*, ou parce qu'il n'y a eu aucun changement entre la branche de base et la branche rebased.

Voici les scénarios pour lesquels les identifiants de commits ne changent pas après un `rebase` :

1. **Fast-Forward Rebase** : Si la branche de base n'a pas de nouveaux commits par rapport à la branche rebased (c'est-à-dire qu'elle est déjà alignée ou en avance), Git fait un *fast-forward* de la branche. Dans ce cas, aucun historique n'est réécrit, et les commits apparaissent inchangés, avec les mêmes *hashes*.

2. **Pas de Conflits ou Changements dans la Branche de Base** : Si la branche de base n’a aucun nouveau commit ou conflit par rapport à la branche rebased, Git peut garder les *hashes* inchangés car il n’y a pas eu de réécriture de l’historique pour intégrer les commits de la base.

### Vérification et Solution

Si vous souhaitez forcer Git à réécrire les commits, vous pouvez essayer un `rebase -i` (rebase interactif), même sans modifier quoi que ce soit. Cela forcera Git à recréer chaque commit, générant ainsi de nouveaux identifiants :

```bash
git rebase -i <base-branch>
```

Ensuite, enregistrez et fermez l'éditeur sans modifier l’ordre des commits. Cela peut forcer une réécriture complète et générer de nouveaux *hashes*.

Vérifiez alors l’historique avec `git log` pour constater que les *hashes* ont changé.
