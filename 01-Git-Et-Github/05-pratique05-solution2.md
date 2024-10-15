# SOLUTION - VARIANTE II (Avec un Conflit Garanti)

---

### La Chasse au Trésor Git avec Rebase

----


# Objectif :  Garantir un conflit à 100%, je vous propose un scénario qui illustre comment cela peut se produire :

1. **Marc et Paul clonent le dépôt à peu près au même moment, mais ils travaillent indépendamment sur leurs branches sans se synchroniser avec `main` après que l'enseignant a fusionné la branche de Paul.**

2. **Marc ne fait pas de `git pull` pour mettre à jour sa branche avant de faire son rebase ou son push.** 

3. **Marc pousse sa branche après que l'enseignant a fusionné la branche de Paul, ce qui provoquera un conflit lors de la fusion de la branche de Marc avec `main`.**

---

# Étapes: 

----

# 1. Création des énigmes

- Chaque étudiant crée sa propre énigme en suivant les étapes ci-dessous :

**Léa :**

```bash
git clone https://github.com/hrhouma/ChasseAuTresor.git
cd ChasseAuTresor
git checkout -b enigme_Lea
echo "Je suis plein la journée, vide la nuit. Qui suis-je ?" > Lea.txt
git add Lea.txt
git commit -m "Ajout de l'énigme de Léa"
git push origin enigme_Lea
```

L'enseignant fusionne ensuite l'énigme de Léa avec la branche `main`.

**Paul :**

Paul suit les mêmes étapes pour créer et ajouter son énigme.

```bash
git clone https://github.com/hrhouma/ChasseAuTresor.git
cd ChasseAuTresor
git checkout -b enigme_Paul
echo "Plus je sèche, plus je deviens humide. Qui suis-je ?" > Paul.txt
git add Paul.txt
git commit -m "Ajout de l'énigme de Paul"
git push origin enigme_Paul
```

# 2. Fusion de la Branche de Paul par l'Enseignant

- L'enseignant fusionne la branche de Paul dans `main` pour intégrer sa solution avant que Marc ne pousse son travail.

```bash
git checkout main
git pull origin main
git merge enigme_Paul
git push origin main
```

# 3. Marc Réalise sa Réponse sans Mise à Jour

**Marc clone le dépôt et commence à travailler sur sa branche en même temps que Paul ou avant la fusion de la branche de Paul dans `main`.** Marc ne fait **pas** de `pull` ou de `fetch` pour se synchroniser avec `main` avant de pousser sa branche.

```bash
git clone https://github.com/hrhouma/ChasseAuTresor.git
cd ChasseAuTresor
git checkout -b enigme_Marc
echo "Je vole sans ailes. Je pleure sans yeux. Partout je vais. Qui suis-je ?" > Marc.txt
git add Marc.txt
git commit -m "Ajout de l'énigme de Marc"
```

---

# TRÈS IMPORTANT  : 

----

- Ces manipulations doivent se faire avant que l'ensignant fasse un pull request ou merge des changements de Paul dans la branche principale main !!!!

**À ce stade, Marc n'est pas au courant des changements apportés par Paul, car il n'a pas mis à jour sa branche avec les derniers changements de `main`.**

Marc ajoute ensuite sa réponse à l'énigme de Léa :

```bash
echo "Réponse de Marc : un sac" >> Lea.txt
git add Lea.txt
git commit -m "Marc résout l'énigme de Léa"
```

##### 4. Marc Pousse sa Branche sans Rebase

Marc pousse sa branche directement sans rebase ni pull :

```bash
git push origin enigme_Marc
```

##### 5. Conflit lors de la Fusion par l'Enseignant

- L'enseignant essaie de fusionner la branche de Marc avec `main`. Cependant, un conflit survient parce que les réponses de Paul et Marc modifient toutes deux `Lea.txt` à partir de versions de `main` qui sont différentes.

```bash
git checkout main
git pull origin main
git merge enigme_Marc
# Conflit détecté dans Lea.txt !
```

**Résolution du Conflit :**

L'enseignant doit ouvrir `Lea.txt`, identifier les changements de Paul et Marc, et résoudre le conflit manuellement.

```bash
nano Lea.txt  # L'enseignant résout le conflit manuellement
git add Lea.txt
git commit -m "Résolution du conflit entre les réponses de Paul et Marc"
git push origin main
```

### Conclusion

Dans ce scénario, le conflit est garanti car Marc n'a pas mis à jour sa branche avec les derniers changements de `main` avant de pousser son travail. Comme Marc et Paul ont tous deux modifié le même fichier (`Lea.txt`) dans des branches dérivées de versions différentes de `main`, cela provoque un conflit lorsqu'on tente de fusionner la branche de Marc avec `main`.










---

# Annexe : Rebase ?

---


# Question : 
- Même si Marc effectue un rebase, n'est-ce pas qu'il va simplement se rebaser sur sa propre branche, sans intégrer les modifications de Paul, puisqu'il n'a pas fait de pull pour mettre à jour sa branche avec les derniers changements de `main` ?

# Réponse: 

- Si Marc fait un `rebase` après avoir fait des modifications sans avoir d'abord mis à jour sa branche avec les derniers changements de `main`, le `rebase` se fera essentiellement sur lui-même, car sa branche n'aura pas les derniers changements de `main`. Cela ne résoudra pas le problème et ne préviendra pas le conflit. Pour garantir un conflit, voici ce qui se passe :



##### 3. Marc Réalise sa Réponse sans Mise à Jour

**Marc clone le dépôt et commence à travailler sur sa branche en même temps que Paul ou avant la fusion de la branche de Paul dans `main`.** 

Marc ne fait **pas** de `pull` ou de `fetch` pour se synchroniser avec `main` avant de faire son rebase ou son push.

```bash
git clone https://github.com/hrhouma/ChasseAuTresor.git
cd ChasseAuTresor
git checkout -b enigme_Marc
echo "Je vole sans ailes. Je pleure sans yeux. Partout je vais. Qui suis-je ?" > Marc.txt
git add Marc.txt
git commit -m "Ajout de l'énigme de Marc"
```

- Marc ajoute ensuite sa réponse à l'énigme de Léa :

```bash
echo "Réponse de Marc : un sac" >> Lea.txt
git add Lea.txt
git commit -m "Marc résout l'énigme de Léa"
```


- Marc fait un `rebase`, mais comme il n'a pas mis à jour sa branche avec `main`, son `rebase` est inutile. Il se base seulement sur les changements de sa propre branche, sans intégrer les changements de Paul :

```bash
git rebase origin/main  # Ce rebase ne fait rien d'utile car il n'a pas fait de pull
git push origin enigme_Marc
```

**Même avec un `rebase`, Marc se rebase uniquement sur sa propre branche sans inclure les changements de `main`, ce qui garantit un conflit lors de la fusion.**



### Conclusion

En conclusion, même si Marc fait un `rebase`, tant qu'il n'a pas fait un `pull` ou un `fetch` pour se synchroniser avec la branche `main` après que Paul a poussé ses modifications, il y aura un conflit. Cela est dû au fait que Marc travaillera sur une ancienne version de `main`, et son `rebase` n'inclura pas les derniers changements, garantissant ainsi un conflit lors de la tentative de fusion par l'enseignant.
