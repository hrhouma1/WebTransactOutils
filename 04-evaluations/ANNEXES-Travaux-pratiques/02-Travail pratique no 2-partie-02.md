--------------------------
# Annexe Théorie1 -  Schéma : `git merge` de `branche_merge` dans `branche2`
--------------------------


1. **État initial :** Voici l’état initial des branches avant de faire le `merge`. La branche `branche2` contient les commits de `main`, tandis que `branche_merge` possède ses propres commits.

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

       branche2                    branche_merge
         |                                |
         |                                |
         o--------------------------------|
        (même historique                  |
         que main)                        |
                                          |
                                          o----> 111111111111111111111111111111
                                         (Modification 1 dans branche_merge)

                                          |
                                          o----> 222222222222222222222222222222
                                         (Modification 2 dans branche_merge)

                                          |
                                          o----> 333333333333333333333333333333
                                         (Modification 3 dans branche_merge)
```

2. **Merge :** Nous basculons sur `branche2` et exécutons `git merge branche_merge`. Cela crée un **commit de fusion** qui combine l’historique des deux branches sans réécrire les commits existants. Le résultat est un historique qui conserve les deux lignes de développement.

---

```
            branche2 après merge (avec commit de fusion)
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
                         |       branche_merge
                         |            |
                         |            |
                         |            o----> 111111111111111111111111111111
                         |           (Modification 1 dans branche_merge)
                         |
                         |            |
                         |            o----> 222222222222222222222222222222
                         |           (Modification 2 dans branche_merge)
                         |
                         |            |
                         |            o----> 333333333333333333333333333333
                         |           (Modification 3 dans branche_merge)
                         |
                         |
                         |
                         o-----------------------------------------> mmmmmmmmmmmmmmmmmmmmmmmmmmmmmm
                        (Commit de fusion entre branche2 et branche_merge)
```

### Explication

- **Avant le merge** : `branche2` contient uniquement les commits de `main`, c’est-à-dire `bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb` et `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa`. De son côté, `branche_merge` contient trois nouveaux commits (`11111111...`, `22222222...`, `33333333...`) qui ne sont pas dans l’historique de `branche2`.

- **Après le merge** : Un commit de fusion (`mmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm`) est créé pour intégrer les modifications de `branche_merge` dans `branche2`. Ce commit de fusion combine les historiques des deux branches sans les réécrire, ce qui préserve les identifiants des commits originaux.

Contrairement au `rebase`, le `merge` conserve les deux lignes d’historique, montrant que `branche2` et `branche_merge` avaient des évolutions distinctes avant d’être fusionnées. Cela peut être utile pour conserver la traçabilité des branches, surtout dans des projets collaboratifs où il est important de voir l’historique de chaque branche sans le réécrire.













---------------
# Annexe Théorie 2 - Exemple de merge avec identifiants de commits fictifs
---------------

### Contexte de départ

Nous avons une branche `main` et une branche `branche_merge` qui contient trois commits. Nous allons effectuer un `merge` pour intégrer les modifications de `branche_merge` dans une autre branche appelée `branche2`. Cette annexe théorique détaille chaque étape avec des identifiants de commits fictifs.

---

### Étapes détaillées

1. **Commits dans `branche_merge`**

   Voici les trois commits présents sur la branche `branche_merge` avant de faire le `merge` :
   
   ```bash
   git log
   ```
   
   ```
   commit 111111111111111111111111111111
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 1 dans branche_merge

   commit 222222222222222222222222222222
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 2 dans branche_merge

   commit 333333333333333333333333333333
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 3 dans branche_merge
   ```

2. **Affichage du `git log` dans `branche2` avant le merge**

   Avant d’intégrer les commits de `branche_merge` dans `branche2`, nous nous positionnons sur `branche2` et vérifions l’historique :

   ```bash
   git checkout branche2
   git log
   ```
   
   Supposons que l’historique de `branche2` ne contient que les commits de la branche principale `main`, sans les modifications de `branche_merge`. Nous voyons alors :

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

3. **Effectuer le `merge` de `branche_merge` dans `branche2`**

   À présent, nous effectuons un `merge` pour intégrer les commits de `branche_merge` dans `branche2`. Cela va créer un commit de fusion :

   ```bash
   git merge branche_merge -m "Fusion de branche_merge dans branche2"
   ```

4. **Vérifier le `git log` après le merge dans `branche2`**

   Après le `merge`, nous visualisons de nouveau l’historique des commits sur `branche2` :

   ```bash
   git log
   ```

   L’historique de `branche2` contient désormais les commits de `branche_merge`, ainsi qu’un nouveau commit de fusion pour indiquer la combinaison des deux branches. Voici l’historique après le merge :

   ```
   commit mmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm
   Merge: aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa 333333333333333333333333333333
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Fusion de branche_merge dans branche2

   commit 333333333333333333333333333333
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 3 dans branche_merge

   commit 222222222222222222222222222222
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 2 dans branche_merge

   commit 111111111111111111111111111111
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Ajout de modification 1 dans branche_merge

   commit aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Modification dans main

   commit bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
   Author: Utilisateur <utilisateur@example.com>
   Date:   ...

       Initialisation du projet avec fichier1.txt
   ```

5. **Analyse et comparaison de l’historique avant et après le `merge`**

   - **Avant le merge** : L’historique de `branche2` ne contenait que les commits de `main` sans les modifications de `branche_merge`.
   - **Après le merge** : Les commits de `branche_merge` apparaissent dans `branche2` avec leurs identifiants d’origine (`11111111`, `22222222`, `33333333`). Un nouveau commit de fusion (`mmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm`) a été créé pour indiquer le point de combinaison entre `branche2` et `branche_merge`. Ce commit de fusion permet de préserver un historique arborescent, montrant la provenance des modifications des différentes branches.

   Le `merge` conserve les deux lignes d’historique, ce qui peut être avantageux pour la traçabilité des modifications et la gestion de projets collaboratifs, car il montre visuellement que des branches distinctes ont été combinées.

---

### Conclusion

Cet exemple théorique montre que `merge` préserve l’intégrité de chaque branche en ajoutant un commit de fusion au lieu de réécrire les identifiants de commits. Cela crée un historique arborescent qui conserve la traçabilité des contributions de chaque branche sans modifier les commits originaux.


-------------

# Correction du schéma visuel :


Dans un affichage d'historique Git, le commit initial, tel que `bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb` ("Initialisation du projet"), doit apparaître en bas, car il est le tout premier commit. Voici le schéma final corrigé, qui respecte complètement l'ordre des commits, du plus récent au plus ancien.

---

### Schéma : `git merge` de `branche_merge` dans `branche2` (avec l'ordre final correct)

1. **État final après le merge :** Ce schéma montre l'historique après le merge de `branche_merge` dans `branche2`, avec le commit de fusion en haut et les commits des branches dans le bon ordre.

```
         branche2 après merge (avec commit de fusion en haut)
                         |
                         |
                         o-----------------------------------------> mmmmmmmmmmmmmmmmmmmmmmmmmmmmmm
                        (Commit de fusion entre branche2 et branche_merge)
                         |
                         |
                         |       branche_merge
                         |            |
                         |            |
                         |            o----> 333333333333333333333333333333
                         |           (Modification 3 dans branche_merge)
                         |
                         |            |
                         |            o----> 222222222222222222222222222222
                         |           (Modification 2 dans branche_merge)
                         |
                         |            |
                         |            o----> 111111111111111111111111111111
                         |           (Modification 1 dans branche_merge)
                         |
                         |
                         |
                         o-------------------------------------> aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa
                        (Modification dans main)
                         |
                         |
                         |
        o----------------o-------------------------------------> bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
       (Initial commit)                                      (Initialisation du projet)
```

### Explication

- **Ordre des commits dans l’historique** : Le commit de fusion `mmmmmmmmmmmmmmmmmmmmmmmmmmmmmmmm` apparaît en haut, car il est le plus récent après le merge.
- **Ordre dans `branche_merge`** : Les commits dans `branche_merge` suivent un ordre chronologique descendant, du plus récent `333333333333333333333333333333` au plus ancien `111111111111111111111111111111`.
- **Commits initiaux de `main`** : Les commits initiaux, `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa` ("Modification dans main") et `bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb` ("Initialisation du projet"), apparaissent en bas, avec le tout premier commit en dernier.

Ce schéma final reflète fidèlement l'historique d'un `git merge` tel qu'il apparaît dans `git log`, avec les commits les plus récents en haut et les plus anciens en bas.
