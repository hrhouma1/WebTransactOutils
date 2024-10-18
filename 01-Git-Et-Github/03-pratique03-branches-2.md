# Automatisation du Push des Branches avec Upstream

# Questions  :

# 1. **Comment faire une push général de toutes les branches ?**
   Pour faire un push général de toutes les branches, vous pouvez utiliser la commande `git push --all`. Cependant, cela fonctionne uniquement si les branches ont déjà un upstream configuré. Si vous avez des nouvelles branches, vous devrez d'abord les configurer.

# 2. **Dois-je utiliser `git push --set-upstream` pour chaque branche si je fais un push général ?**
   Oui, si une branche n'a pas encore d'upstream configuré, vous devez utiliser `git push --set-upstream origin <nom_de_la_branche>` pour chaque nouvelle branche avant de pouvoir faire un push général avec `git push --all`.

# 3. **Est-ce que `git push --all` fonctionnera pour des branches qui n'ont pas encore d'upstream ?**
   Non, si une branche n'a pas encore d'upstream configuré, `git push --all` ne fonctionnera pas pour cette branche. Vous devez d'abord configurer l'upstream avec `git push --set-upstream origin <nom_de_la_branche>`.

# 4. **Comment puis-je pousser plusieurs branches en même temps si elles n'ont pas encore d'upstream ?**
   Pour pousser plusieurs branches en même temps et configurer leur upstream en une seule fois, vous pouvez utiliser un script bash qui automatise le processus. Voir ci-dessous pour un exemple de script.

---

## Script pour Pousser Toutes les Branches et Configurer l'Upstream

Si vous avez plusieurs branches locales qui n'ont pas encore de dépôt distant configuré (upstream), voici un script bash pour automatiser le processus.

### Script Bash :

```bash
#!/bin/bash

# Ce script configure l'upstream pour toutes les branches locales
# et les pousse vers le dépôt distant.

for branch in $(git branch | sed 's/\*//'); do
  echo "Configuration de l'upstream pour la branche: $branch"
  git push --set-upstream origin $branch
done

echo "Push terminé pour toutes les branches."
```

# Explication du Script :
- **Étape 1** : Le script récupère toutes les branches locales en utilisant `git branch` et supprime les étoiles (`*`) qui indiquent la branche active.
- **Étape 2** : Pour chaque branche, le script exécute `git push --set-upstream origin <nom_branche>` pour configurer l'upstream.
- **Étape 3** : Il affiche un message de confirmation une fois que le push est terminé pour toutes les branches.

# Comment Utiliser le Script :

1. **Créer un fichier de script** :
   - Sauvegardez le script ci-dessus dans un fichier nommé `push_all_branches.sh`.

2. **Donner des permissions d'exécution au script** :
   - Dans votre terminal, donnez des permissions au script pour qu'il puisse s'exécuter :
     ```bash
     chmod +x push_all_branches.sh
     ```

3. **Exécuter le script** :
   - Pour exécuter le script, utilisez simplement la commande suivante :
     ```bash
     ./push_all_branches.sh
     ```

   Le script va configurer l'upstream pour chaque branche locale et pousser chaque branche vers le dépôt distant.

---

# Rappel des Commandes Utiles

- **Pousser toutes les branches avec upstream configuré** :
  ```bash
  git push --all
  ```

- **Configurer l'upstream pour une branche spécifique** :
  ```bash
  git push --set-upstream origin <nom_de_la_branche>
  ```

- **Lister toutes les branches locales** :
  ```bash
  git branch
  ```


---------------------------
# Annexe 1 -  pousser plusieurs branches en une seule commande
---------------------------

Pour pousser plusieurs branches en une seule commande, tout en configurant leur upstream pour la première fois, vous pouvez utiliser la méthode suivante :

# Étapes :
1. **Utiliser la commande `git push --set-upstream` pour plusieurs branches** :
   Vous pouvez spécifier plusieurs branches en une seule ligne avec la commande `git push --set-upstream`, mais cela nécessite de spécifier chaque branche manuellement pour lier l'upstream. Cependant, il n'y a pas de commande native Git qui configure automatiquement plusieurs upstreams en une seule commande.

2. **Automatisation via un script** :
   Vous pouvez utiliser un script pour automatiser la configuration des upstreams pour plusieurs branches d'un coup. Voici un exemple de script bash que vous pouvez utiliser pour automatiser ce processus :

   ```bash
   for branch in $(git branch | sed 's/\*//'); do
     git push --set-upstream origin $branch
   done
   ```

   Ce script :
   - Récupère la liste de toutes vos branches locales.
   - Exécute `git push --set-upstream origin <nom_branche>` pour chaque branche.

3. **Push manuel pour chaque branche** :
   Si vous préférez ne pas utiliser de script, vous pouvez configurer chaque branche manuellement :

   ```bash
   git push --set-upstream origin dev1
   git push --set-upstream origin dev2
   git push --set-upstream origin dev3
   git push --set-upstream origin master
   ```

Une fois que toutes les branches ont un upstream configuré, vous pourrez utiliser `git push --all` pour pousser toutes vos branches locales en une seule fois pour les mises à jour futures.

# Alternative : GitKraken
Dans **GitKraken**, après avoir créé de nouvelles branches, vous pouvez également sélectionner manuellement chaque branche et utiliser l'option "Push" avec l'upstream, puis passer à la branche suivante pour faire de même.


