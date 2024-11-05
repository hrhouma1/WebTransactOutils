# Travail Pratique N°2 : Étapes pratiques

# **Instructions :**  
Suivez chaque étape dans l'ordre et effectuez les manipulations demandées sur votre dépôt Git. Le professeur validera certaines étapes pour attribuer les points correspondants.

---

1) Cloner le dépôt  
2) Configurer le dépôt avec vos informations globales et locales  
3) Vérifier `.git/config`  
4) Générer votre clé SSH avec `ssh-keygen`  
5) Partager la clé avec le professeur  
6) Ajouter un fichier nommé `<votre_prenom.txt>`  
7) Pousser sur la branche `main`

---

# 🛑 **STOP - ÉTAPE 1 : LE PROF VALIDE dès qu'il reçoit votre push sur `main`**

---

9) Créer une branche `<br_votreprenom>`  
10) Chacun.e parmi vous créera sa branche. Vous allez ajouter votre branche et vous placer sur cette nouvelle branche `<br_votreprenom>`  
11) Créez votre propre énigme dans un fichier nommé `enigme_<votreprenom>.txt`  
12) Faites un push de votre branche  

---

# 🛑 **STOP - ÉTAPE 2 : LE PROF VALIDE et VOUS CONFIRME L'AJOUT DE BRANCHES**

---

14) **Règle 1 :** Le premier étudiant qui fait un push de sa branche ne fait rien à cette étape ! (supposons Mathieu)  

# 🛑 **STOP - ÉTAPE 3 : LE PROFESSEUR FAIT UN PULL REQUEST SEULEMENT DE LA PREMIÈRE BRANCHE REÇUE À CE STADE**

   - Chaque étudiant doit faire un pull de la branche `main` pour récupérer les dernières modifications.
   - Chaque étudiant doit résoudre l'énigme du premier étudiant (Mathieu) sur sa propre branche.

17) Une fois que l'énigme de Mathieu est résolue sur votre branche locale `<br_votreprenom>`, chaque étudiant doit faire un push de sa branche locale vers sa branche distante.

⚠️ **Attention : Ne faites pas de changements directement dans `main` ! (sinon, il y a une pénalité)**

### ➡️ Processus recommandé :

➡️ `br_votreprenom (MATHIEU POSTE LOCAL)` ➡️ `br_votreprenom (MATHIEU GITHUB)` ➡️ *Pull request avec*➡️ `main (GITHUB)` ➡️ `pull` ➡️*VERS*➡️ `main (POSTE LOCAL)`➡️ *ALLER À* ➡️ `br_votreprenom (VOTRE BRANCHE LOCAL)` ➡️ `merge` avec `ton main LOCAL qui est mise à jour depuis MAIN de GITHUB`

- **Ajoutez et committez les modifications**  
- **Effectuez un pull/push de votre branche locale vers votre branche distante**

---

# 🛑 **STOP - ÉTAPE 4 : LE PROFESSEUR FAIT UN PULL REQUEST DE TOUTES LES BRANCHES DANS `MAIN`**

   **Remarque :** À ce stade, le professeur résout les conflits. Vous aurez un `main` consolidé avec tous les changements de chaque étudiant.

---

19) **Chaque étudiant** doit maintenant apporter toutes les branches en local dans son dépôt local. Suivez les étapes ci-dessous pour récupérer les branches :

   - Passez à la branche `main`
   - Récupérez toutes les branches du dépôt distant
   - Vérifiez les branches locales et distantes
   - Passez sur chaque branche des autres étudiants pour effectuer un pull de leurs modifications

### ➡️ **Processus recommandé :**

```bash
git checkout main
git fetch --all
git branch
git branch -r
git branch -a
```

Ensuite, pour chaque branche d’étudiant, passez à la branche et faites un pull, par exemple pour Elodie :

```bash
git checkout br_elodie
git pull origin br_elodie
```

Répétez ces étapes pour chaque branche (par exemple, `br_mathieu`, `enigme_samaneh`, `br_marcolivier`).

Terminez en revenant sur **votre propre branche** et effectuez un pull pour récupérer les dernières modifications :

```bash
git checkout <VOTRE_BRANCHE>
git pull origin <VOTRE_BRANCHE>
```

---

# 🛑 **STOP - ÉTAPE 5 : LE PROFESSEUR RÉPOND À VOS ÉNIGMES SUR VOTRE BRANCHE**

---

20) **Chaque étudiant** doit également répondre à **sa propre énigme** sur sa branche.

21) **Chaque étudiant** effectue un push de sa branche locale avec son nom vers sa branche distante, avec toutes ses modifications et réponses.

