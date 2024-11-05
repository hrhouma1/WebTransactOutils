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
