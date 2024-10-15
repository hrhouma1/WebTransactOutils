# SOLUTION - VARIANTE I (SANS CONFLITS)

---

### La Chasse au Trésor Git avec Rebase

----


##### 1. Énigmes Individuelles

Chaque étudiant crée sa propre énigme en suivant les étapes ci-dessous :

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

##### 2. Fusion de la Branche de Paul par l'Enseignant

- L'enseignant fusionne la branche de Paul dans `main` pour intégrer sa solution avant que Marc ne commence à travailler.

```bash
git checkout main
git pull origin main
git merge enigme_Paul
git push origin main
```

##### 3. Marc Réalise sa Réponse avec Rebase

**Marc veut répondre à l'énigme de Léa.** Avant d'ajouter sa réponse, il met à jour sa branche avec `main`.

- **Marc fait un `pull` pour s'assurer que sa branche est à jour** :

```bash
git checkout enigme_Marc
git pull origin main  # Mise à jour de sa branche avec les derniers changements de main
```

- Ensuite, **Marc effectue son rebase** pour s'assurer que son travail est basé sur la dernière version de `main` :

```bash
git rebase origin/main
```

Dans ce cas, **comme Marc a fait un `git pull` suivi d'un `git rebase` sur la branche `main`, il n'y aura pas de conflit** lors de son travail, car sa branche est déjà alignée avec la dernière version de `main` contenant la réponse de Paul.

**Marc ajoute ensuite sa réponse :**

```bash
echo "Réponse de Marc : un sac" >> Lea.txt
git add Lea.txt
git commit -m "Marc résout l'énigme de Léa"
git push origin enigme_Marc
```

##### 4. Fusion de la Branche de Marc par l'Enseignant

- Après que Marc a poussé sa solution, l'enseignant devra à nouveau fusionner cette branche dans `main`.

```bash
git checkout main
git pull origin main
git merge enigme_Marc
git push origin main
```

---

**Conclusion :**  
En résumé, si Marc met bien à jour sa branche avec `git pull origin main` avant de faire son rebase, il ne devrait pas rencontrer de conflits majeurs, car sa branche serait déjà alignée avec les changements récents intégrés par l'enseignant, y compris ceux de Paul. L'utilisation de `pull` suivie d'un `rebase` aide à maintenir une branche propre et minimise les conflits, rendant le processus de travail plus fluide.
