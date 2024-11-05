

### Schéma : `git merge` de `branche_merge` dans `branche2`

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
