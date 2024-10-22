# 17 git tags


### **Objectif :**
Ce guide vous apprendra à utiliser les **tags Git** pour marquer des points spécifiques dans l'historique de votre projet, comme des versions, des releases, ou des milestones importantes. Vous apprendrez à créer, lister, et supprimer des tags, ainsi qu’à les pousser vers un dépôt distant comme GitHub.

---

## **Partie 1 : Théorie**

### **Qu'est-ce qu'un tag Git ?**

- **Un tag Git** est un marqueur ou une étiquette que vous pouvez appliquer à un commit spécifique pour signaler un point important dans l'historique de votre projet, comme une version de release (par exemple, `v1.0`). Les tags sont souvent utilisés pour marquer les versions stables d’un projet.

### **Pourquoi utiliser des tags ?**

- **Marquer les releases** : Vous pouvez utiliser les tags pour indiquer des versions spécifiques (ex: `v1.0`, `v2.0`) de votre projet.
- **Faciliter la navigation** : Les tags permettent de retrouver facilement un commit particulier ou une version stable dans l'historique du projet.
- **Suivi des versions** : Lors du développement de logiciels, il est courant d'utiliser des tags pour gérer les versions et les releases publiées.

### **Deux types de tags :**

1. **Les tags légers (lightweight tags)** : Un simple pointeur vers un commit particulier sans informations supplémentaires. Ils sont utilisés pour un marquage rapide.
2. **Les tags annotés (annotated tags)** : Contiennent des informations supplémentaires comme un message, un nom, une date, et sont signés. Ils sont généralement utilisés pour les releases officielles.

---

## **Partie 2 : Pratique**

Nous allons maintenant utiliser **`git tag`** dans le cadre du projet **site-php-1** pour créer, lister, et supprimer des tags, ainsi que les pousser vers GitHub.

### **Étape 1 : Cloner le projet existant depuis GitHub**

Si vous n'avez pas encore de dépôt local, commencez par cloner le projet **site-php-1** depuis GitHub.

1. Ouvrez votre terminal et tapez cette commande pour cloner le projet :

   ```bash
   git clone https://github.com/hrhouma1/site-php-1.git
   ```

2. Entrez dans le répertoire du projet cloné :

   ```bash
   cd site-php-1
   ```

---

### **Étape 2 : Créer un tag léger (lightweight tag)**

Un tag léger est simplement un pointeur vers un commit particulier. C'est la façon la plus simple de taguer un commit.

1. **Vérifier l'historique des commits** :

   Tapez la commande suivante pour voir les commits récents et sélectionner celui que vous voulez taguer :

   ```bash
   git log --oneline
   ```

   Cela vous donnera une liste de commits récents, chacun avec son ID. Choisissez l'ID du commit que vous souhaitez taguer.

2. **Créer un tag léger** :

   Utilisez la commande suivante pour créer un tag léger nommé `v1.0` :

   ```bash
   git tag v1.0
   ```

   Cela crée un tag sur le dernier commit de la branche actuelle.

---

### **Étape 3 : Créer un tag annoté (annotated tag)**

Les tags annotés contiennent des informations supplémentaires, comme un message de tag, une date, et sont souvent utilisés pour des versions officielles.

1. **Créer un tag annoté** :

   Utilisez la commande suivante pour créer un tag annoté nommé `v1.0` avec un message décrivant la version :

   ```bash
   git tag -a v1.0 -m "Version 1.0 - Première release stable du projet"
   ```

   - **`-a`** : Indique qu'il s'agit d'un tag annoté.
   - **`-m`** : Spécifie un message pour le tag.

2. **Vérifier les informations du tag annoté** :

   Vous pouvez afficher les détails d'un tag annoté avec la commande suivante :

   ```bash
   git show v1.0
   ```

   Cela affichera des informations supplémentaires sur le commit tagué, ainsi que le message de tag que vous avez ajouté.

---

### **Étape 4 : Lister tous les tags**

Vous pouvez lister tous les tags de votre dépôt avec la commande suivante :

```bash
git tag
```

Cela affichera tous les tags créés jusqu'à présent dans votre projet.

---

### **Étape 5 : Pousser les tags vers GitHub**

Par défaut, les tags ne sont pas automatiquement poussés vers GitHub. Vous devez les pousser explicitement.

1. **Pousser un tag spécifique** :

   Pour pousser un tag spécifique vers GitHub (par exemple `v1.0`), utilisez la commande suivante :

   ```bash
   git push origin v1.0
   ```

2. **Pousser tous les tags à la fois** :

   Si vous avez plusieurs tags à pousser, vous pouvez tous les envoyer en une seule commande :

   ```bash
   git push origin --tags
   ```

---

### **Étape 6 : Supprimer un tag**

Si vous avez créé un tag par erreur ou si vous voulez supprimer un tag spécifique, voici comment faire.

1. **Supprimer un tag localement** :

   Utilisez la commande suivante pour supprimer un tag localement :

   ```bash
   git tag -d v1.0
   ```

   Cela supprime uniquement le tag dans votre dépôt local.

2. **Supprimer un tag sur GitHub** :

   Si vous voulez supprimer un tag également sur GitHub, vous devez d'abord le supprimer localement, puis pousser cette suppression vers GitHub :

   ```bash
   git push origin --delete v1.0
   ```

---

### **Étape 7 : Taguer un commit spécifique**

Si vous voulez taguer un commit particulier (pas le dernier), vous pouvez spécifier l'ID du commit lors de la création du tag.

1. **Lister les commits récents** :

   Utilisez la commande suivante pour voir l'ID des commits récents :

   ```bash
   git log --oneline
   ```

2. **Créer un tag pour un commit spécifique** :

   Si vous avez choisi un commit avec l'ID `abc1234`, vous pouvez créer un tag pour ce commit spécifique :

   ```bash
   git tag -a v2.0 abc1234 -m "Version 2.0 - Nouvelle fonctionnalité"
   ```

3. **Pousser le tag vers GitHub** :

   Poussez ce tag spécifique vers GitHub avec :

   ```bash
   git push origin v2.0
   ```

---

### **Étape 8 : Résumé des commandes `git tag`**

1. **Créer un tag léger** :
   ```bash
   git tag v1.0
   ```

2. **Créer un tag annoté avec un message** :
   ```bash
   git tag -a v1.0 -m "Version 1.0 - Première release stable"
   ```

3. **Lister tous les tags** :
   ```bash
   git tag
   ```

4. **Afficher les détails d'un tag annoté** :
   ```bash
   git show v1.0
   ```

5. **Pousser un tag spécifique vers GitHub** :
   ```bash
   git push origin v1.0
   ```

6. **Pousser tous les tags vers GitHub** :
   ```bash
   git push origin --tags
   ```

7. **Supprimer un tag localement** :
   ```bash
   git tag -d v1.0
   ```

8. **Supprimer un tag sur GitHub** :
   ```bash
   git push origin --delete v1.0
   ```

---

### **Conclusion**

Ce guide vous a montré comment utiliser **`git tag`** pour marquer des points spécifiques dans l'historique de votre projet. Vous avez appris à créer des tags légers et annotés, à les pousser vers GitHub, et à les supprimer si nécessaire. Les tags sont particulièrement utiles pour suivre les versions de votre projet et indiquer les releases importantes.

En utilisant les tags, vous pouvez facilement naviguer dans l'historique de votre projet et revenir à des versions spécifiques pour des déploiements ou des corrections de bugs.

-----------
# Annexe 1 :  Gérer les tags à distance (remote) :
-----------

### **Lister les tags à distance :**
```bash
git ls-remote --tags origin
```

### **Pousser un tag spécifique vers le dépôt distant :**
```bash
git push origin <nom_du_tag>
```

### **Pousser tous les tags vers le dépôt distant :**
```bash
git push origin --tags
```

### **Supprimer un tag à distance :**
```bash
git push origin --delete <nom_du_tag>
```

### **Récupérer les tags à partir du dépôt distant :**
```bash
git fetch --tags
```


-----------
# Annexe 2 :  Gérer les tags à distance (remote) dans une branche spécifique :
-----------


*Git ne permet pas directement de lister les **tags** par branche, car les **tags** sont globaux et non spécifiques à une branche. Cependant, voici une méthode pour lister les tags associés à une branche spécifique ainsi que pour récupérer les branches avec `git fetch`.*

### **Lister les tags dans une branche spécifique :**
Pour afficher les tags dans une branche spécifique, utilisez cette combinaison de commandes :

```bash
git log --oneline --decorate --tags --simplify-by-decoration <nom_de_branche>
```

Cela affichera les commits de la branche spécifiée avec les tags associés.

### **Lister toutes les branches et récupérer les informations à distance :**

1. **Récupérer toutes les branches et les tags avec `fetch` :**
   ```bash
   git fetch --all --tags
   ```

2. **Lister toutes les branches distantes :**
   ```bash
   git branch -r
   ```

Ces commandes vous permettent de gérer les tags et branches à distance efficacement.
