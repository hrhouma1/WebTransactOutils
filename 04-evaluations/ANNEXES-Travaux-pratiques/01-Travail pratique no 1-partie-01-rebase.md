


--------------------------
# Annexe Théorie1 -  Schéma : `git rebase` de `branche_rebase` sur `branche1`
--------------------------

1. **État initial :** Voici la structure des branches avant de faire le `rebase`. Les commits de `main` sont présents sur `branche1`, tandis que `branche_rebase` contient ses propres commits.

```
                       main
                         |
                         |
        o----------------o---------------------> bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
       (Initial commit)  |                     (Initialisation du projet)
                         |
                         |
                         o---------------------> aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                        (Modification dans main)

       branche1                    branche_rebase
         |                                |
         |                                |
         o--------------------------------|
        (même historique                  |
         que main)                        |
                                          |
                                          o----> 111111111111111111111111111111
                                         (Modification 1 dans branche_rebase)

                                          |
                                          o----> 222222222222222222222222222222
                                         (Modification 2 dans branche_rebase)

                                          |
                                          o----> 333333333333333333333333333333
                                         (Modification 3 dans branche_rebase)
```

2. **Rebase :** Nous basculons sur `branche1` et exécutons `git rebase branche_rebase`. Les commits de `branche_rebase` sont réécrits et ajoutés à `branche1` avec de nouveaux identifiants. Le résultat final est un historique linéaire intégrant toutes les modifications.

---

```
              branche1 après rebase (intégrant les commits de branche_rebase)
                         |
                         |
        o----------------o-------------------------------------> bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
       (Initial commit)  |                                    (Initialisation du projet)
                         |
                         |
                         o------------------------------------> aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                        (Modification dans main)
                         |
                         |
                         o------------------------------------> xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
                        (Modification 1 dans branche_rebase)
                         |
                         |
                         o------------------------------------> yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
                        (Modification 2 dans branche_rebase)
                         |
                         |
                         o------------------------------------> zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
                        (Modification 3 dans branche_rebase)
```

### Explication

- **Avant le rebase** : `branche1` contient les commits `bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb` et `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa` de `main`. De son côté, `branche_rebase` contient ses propres commits (`11111111...`, `22222222...`, `33333333...`), qui ne sont pas dans l’historique de `branche1`.

- **Après le rebase** : Les commits de `branche_rebase` sont ajoutés à `branche1`, mais ils ont de nouveaux identifiants (`xxxxxxxx...`, `yyyyyyyy...`, `zzzzzzzz...`). L’historique de `branche1` devient linéaire et inclut maintenant toutes les modifications de `branche_rebase` tout en préservant les commits de `main`.

Ce schéma illustre bien comment `rebase` permet d’obtenir un historique linéaire tout en intégrant les commits d'une autre branche, en modifiant leurs identifiants pour éviter des conflits d'historique.



--------------------------
# Annexe Théorie2 -  Exemple de rebase avec identifiants de commits fictifs
--------------------------

### Contexte de départ

Nous avons une branche `main` et une branche `branche_rebase` qui contient trois commits. Nous allons effectuer un `rebase` pour intégrer les modifications de `branche_rebase` dans une autre branche appelée `branche1`. Cette annexe théorique détaille chaque étape avec des identifiants de commits fictifs.

---

### Étapes détaillées

1. **Commits dans `branche_rebase`**

   Voici les trois commits présents sur la branche `branche_rebase` avant de faire le `rebase` :
   
   ```bash
   git log
   ```
   
   ```
   commit 111111111111111111111111111111
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 1 dans branche_rebase

   commit 222222222222222222222222222222
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 2 dans branche_rebase

   commit 333333333333333333333333333333
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 3 dans branche_rebase
   ```

2. **Affichage du `git log` dans `branche1` avant le rebase**

   Avant d’intégrer les commits de `branche_rebase` dans `branche1`, nous nous positionnons sur `branche1` et vérifions l’historique :

   ```bash
   git checkout branche1
   git log
   ```
   
   Supposons que l’historique de `branche1` ne contient que les commits de la branche principale `main`, sans les modifications de `branche_rebase`. Nous voyons alors :

   ```
   commit aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Modification dans main

   commit bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Initialisation du projet avec fichier1.txt
   ```

3. **Effectuer le `rebase` de `branche_rebase` sur `branche1`**

   À présent, nous effectuons un `rebase` pour intégrer les commits de `branche_rebase` dans `branche1` :

   ```bash
   git rebase branche_rebase
   ```

4. **Vérifier le `git log` après le rebase dans `branche1`**

   Après le `rebase`, nous visualisons de nouveau l’historique des commits sur `branche1` :

   ```bash
   git log
   ```

   L’historique de `branche1` contient désormais les commits de `branche_rebase`. Cependant, les identifiants de commits sont modifiés, car `rebase` crée de nouvelles copies des commits de `branche_rebase` avec de nouveaux identifiants. Voici l’historique après le rebase :

   ```
   commit xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 1 dans branche_rebase

   commit yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 2 dans branche_rebase

   commit zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 3 dans branche_rebase

   commit aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Modification dans main

   commit bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Initialisation du projet avec fichier1.txt
   ```

5. **Analyse et comparaison de l’historique avant et après le `rebase`**

   - **Avant le rebase** : L’historique de `branche1` ne contenait que les commits de `main` sans les modifications de `branche_rebase`.
   - **Après le rebase** : Les commits de `branche_rebase` apparaissent dans `branche1`, mais avec de nouveaux identifiants de commits (`xxxxxxxx`, `yyyyyyyy`, `zzzzzzzz`) au lieu des anciens identifiants (`11111111`, `22222222`, `33333333`). Cela est dû au fait que `rebase` copie les commits, créant des versions réécrites avec de nouveaux identifiants pour conserver un historique linéaire.

   Cette réécriture de l’historique est l’une des principales caractéristiques du `rebase`, créant une apparence linéaire et permettant de voir l’ensemble des commits d’une branche comme s’ils faisaient partie de l’historique de `branche1` depuis le début.

---

### Conclusion

Grâce à cet exemple théorique, nous observons que `rebase` conserve les modifications de `branche_rebase` mais modifie les identifiants de commits. Cela crée un historique linéaire qui peut simplifier la lecture de l’historique, mais nécessite de prêter attention aux changements d’identifiants de commits pour ne pas perdre le suivi des modifications dans des collaborations.


----------
# Correction du schéma visuel
-------------------

L'historique doit bien suivre l'ordre chronologique inverse : du plus récent en haut au plus ancien en bas. Voici le schéma corrigé avec les commits de `branche_rebase` et `branche1` dans le bon ordre, affichés du plus récent au plus ancien.

---

# Annexe Théorie1 - Schéma : `git rebase` de `branche_rebase` sur `branche1`

1. **État initial :** Voici la structure des branches avant de faire le `rebase`. Les commits de `main` sont présents sur `branche1`, tandis que `branche_rebase` contient ses propres commits, du plus récent en haut au plus ancien en bas.

```
                       main
                         |
                         |
        o----------------o---------------------> bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
       (Initial commit)  |                     (Initialisation du projet)
                         |
                         |
                         o---------------------> aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                        (Modification dans main)

       branche1                    branche_rebase
         |                                |
         |                                |
         o--------------------------------|
        (même historique                  |
         que main)                        |
                                          |
                                          o----> 333333333333333333333333333333
                                         (Modification 3 dans branche_rebase)
                                          |
                                          |
                                          o----> 222222222222222222222222222222
                                         (Modification 2 dans branche_rebase)
                                          |
                                          |
                                          o----> 111111111111111111111111111111
                                         (Modification 1 dans branche_rebase)
```

2. **Rebase :** Nous basculons sur `branche1` et exécutons `git rebase branche_rebase`. Les commits de `branche_rebase` sont réécrits et ajoutés à `branche1` avec de nouveaux identifiants. Le résultat final est un historique linéaire intégrant toutes les modifications.

---

```
              branche1 après rebase (intégrant les commits de branche_rebase)
                         |
                         |
        o------------------------------------> zzzzzzzzzzzzzzzzzzzzzzzzzzzzzzzz
       (Modification 3 dans branche_rebase)
                         |
                         |
                         o------------------------------------> yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy
                        (Modification 2 dans branche_rebase)
                         |
                         |
                         o------------------------------------> xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
                        (Modification 1 dans branche_rebase)
                         |
                         |
                         o-------------------------------------> aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                        (Modification dans main)
                         |
                         |
        o----------------o-------------------------------------> bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
       (Initial commit)                                     (Initialisation du projet)
```

### Explication

- **Avant le rebase** : `branche1` contient les commits `bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb` et `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa` de `main`. `branche_rebase` contient ses propres commits (`33333333...`, `22222222...`, `11111111...`) du plus récent au plus ancien.
  
- **Après le rebase** : Les commits de `branche_rebase` sont ajoutés à `branche1` avec de nouveaux identifiants (`zzzzzzzz...`, `yyyyyyyy...`, `xxxxxxxx...`). L'historique de `branche1` devient linéaire, avec les commits de `branche_rebase` apparaissant juste avant les commits initiaux de `main`.

Ce schéma reflète le résultat final d'un `rebase` : un historique linéaire intégrant tous les commits dans l'ordre du plus récent en haut au plus ancien en bas.
