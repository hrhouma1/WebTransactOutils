----------------------
# Note et références:
----------------------

- Ce tutoriel est basé sur les concepts expliqués par Amit Prajapati dans son article original.
- https://medium.com/mindorks/understanding-git-merge-git-rebase-88e2afd42671



![image](https://github.com/user-attachments/assets/1ff0f9f6-7a2e-4323-bb47-0b71e25ff416)

![image](https://github.com/user-attachments/assets/16dc5225-874c-4f56-b212-40125bbfec3b)

![image](https://github.com/user-attachments/assets/cdd3f8f1-bddb-4099-bf57-80236f754f57)

![image](https://github.com/user-attachments/assets/da9214b0-caae-4eea-b09d-f9f109bf86ad)

![image](https://github.com/user-attachments/assets/dc0af3a2-c303-44a9-a6df-a878b78a2dec)

![image](https://github.com/user-attachments/assets/fee99673-69e0-4bc3-8547-45a4585d4e76)

![image](https://github.com/user-attachments/assets/1f5d2902-b2d7-40c9-907f-6d9485e270c2)

![image](https://github.com/user-attachments/assets/4bc7ae2a-1d8b-44dd-bc2e-ed98f40b0e0a)

![image](https://github.com/user-attachments/assets/3e27c46f-6d32-43f8-ab55-d573cd14b240)

![image](https://github.com/user-attachments/assets/f84d7c1d-95dc-45c1-bdb7-55db7c625168)

![image](https://github.com/user-attachments/assets/a7519d06-4d91-4f4a-b01d-630f15da504e)

![image](https://github.com/user-attachments/assets/9ab6ceff-b2fd-4122-838d-c0cb5c021d76)

![image](https://github.com/user-attachments/assets/4595ddb3-31f3-479f-ad9c-001fb14fa65f)

![image](https://github.com/user-attachments/assets/5f1fc559-2530-419f-93dd-e860f807a67e)

![image](https://github.com/user-attachments/assets/a79124d1-4a9f-438a-9e16-f11456fb73d2)

![image](https://github.com/user-attachments/assets/8f4219eb-25b7-441d-adf7-2fcc05f5dcb0)

![image](https://github.com/user-attachments/assets/f3de7f3e-08d4-460d-a88f-f60285260aa4)

![image](https://github.com/user-attachments/assets/e88adfd4-980c-4ebd-bbb0-1acd84509cfc)

![image](https://github.com/user-attachments/assets/88998c50-8947-4c0c-ab45-ba4e7ff1800d)

![image](https://github.com/user-attachments/assets/30ce7735-2d09-4faa-b39f-458ce354ba7c)

![image](https://github.com/user-attachments/assets/98d6967c-5a26-4dde-ae92-94648135e939)

![image](https://github.com/user-attachments/assets/3c9309fa-00a6-4d01-80be-285d8d664fc6)

![image](https://github.com/user-attachments/assets/0bae4384-19b0-41e1-8f44-5dca3391666e)

![image](https://github.com/user-attachments/assets/19ff3ab2-ebc3-4465-a45b-96ff5952dfa6)

![image](https://github.com/user-attachments/assets/d4840573-23ed-4872-845a-7c069d1e08af)

![image](https://github.com/user-attachments/assets/309d151e-d595-4e03-9364-d8bbbdab2ff4)


![image](https://github.com/user-attachments/assets/43b0882e-1a71-46d9-bad8-33c14b201ac4)

![image](https://github.com/user-attachments/assets/8e7bca6a-c763-46ab-aeee-e949b50c6827)

![image](https://github.com/user-attachments/assets/939a646a-7cc9-43f8-9bd7-0a4c58b31208)

![image](https://github.com/user-attachments/assets/7d40310c-6d0e-4e46-89ea-75e3af6ba0b5)

![image](https://github.com/user-attachments/assets/c06bee13-9d65-42e6-94c0-366a68d974e3)

![image](https://github.com/user-attachments/assets/9afda69b-5584-4359-bd9c-d93681b101cf)

![image](https://github.com/user-attachments/assets/bdefa406-cb14-4570-a66e-2c4ca1d2ca50)

![image](https://github.com/user-attachments/assets/12cda280-b527-4bda-a0d5-b1c2152da274)

![image](https://github.com/user-attachments/assets/053390f0-19e2-4402-8dac-adadec2a51eb)

































## Comprendre **Git Merge** et **Git Rebase**

### **Motivation d'aujourd'hui :**

*"Le progrès est impossible sans changement et ceux qui ne peuvent pas changer d'avis ne peuvent rien changer."*

Commençons ! 😊

---

### **Quelle est l'utilité de `git merge` ?**

Séparer les fonctionnalités dans différentes branches est une pratique essentielle pour tout développeur sérieux. En séparant chaque fonctionnalité, correction de bug, ou expérimentation, vous éviterez de nombreux problèmes et garderez vos branches de développement propres.

À un moment donné, une partie du code atteindra un état où vous voudrez l'intégrer avec le reste du projet. C'est là que la commande `git merge` entre en jeu.

---

### **Préparation à la fusion**

Supposons que vous voulez fusionner la branche `hotfix` dans votre branche `master`. Voici comment vous assurer que vous êtes prêt à effectuer cette fusion :

1. **Mettre à jour votre dépôt local** : Vérifiez si votre dépôt local est à jour avec les derniers changements du serveur distant en utilisant `git fetch`.
2. **Passer à la branche `master`** : Une fois la mise à jour effectuée, faites un `git checkout master` pour vous assurer que vous travaillez sur la bonne branche.
3. **Récupérer les dernières mises à jour** : Exécutez `git pull` pour vous assurer que la branche `master` contient bien les dernières mises à jour.
4. **Fusionner les branches** : Utilisez `git merge <nom_branche>` pour intégrer les modifications de la branche `hotfix` dans `master`.

---

### **Fusion rapide (Fast-forward Merge)**

Une fusion rapide peut se produire lorsqu'il existe un chemin linéaire entre les branches que vous souhaitez fusionner. Si la branche `master` n'a pas divergé, au lieu de créer un nouveau commit, Git fera simplement pointer la branche `master` vers le dernier commit de la branche `hotfix`.

### **Fusion à trois voies (Three-way Merge)**

Lorsque les branches ont divergé, Git n'a pas d'autre choix que de combiner les branches via une fusion à trois voies. Cette fusion utilise un commit supplémentaire pour relier les deux branches.

---

### **Comment résoudre les conflits de fusion**

Un conflit de fusion se produit lorsque deux branches que vous essayez de fusionner ont modifié la même partie du même fichier. Git ne pourra pas déterminer quelle version utiliser. Voici comment résoudre un conflit de fusion :

1. **Ouvrir le fichier en conflit** : Lorsque vous essayez de fusionner les branches, Git marque les zones conflictuelles avec des indicateurs visuels :
   - `<<<<<<<` : Indicateur de début de conflit.
   - `=======` : Sépare vos changements de ceux de l'autre branche.
   - `>>>>>>>` : Indique la fin des lignes en conflit.

2. **Résoudre le conflit manuellement** : Décidez si vous voulez conserver uniquement vos changements ou ceux de l'autre branche, ou bien écrire du code entièrement nouveau. Ensuite, supprimez les marqueurs de conflit.

3. **Appliquer et committer les changements** : Après avoir résolu les conflits, utilisez `git add <fichier>` pour dire à Git que les conflits sont résolus, puis créez un commit avec `git commit`.

---

### **Meilleure pratique avec `git rebase`**

L'objectif du **merge** et du **rebase** est le même : prendre des commits d'une branche de fonctionnalité et les appliquer à une autre branche. Cependant, le rebase permet de "rejouer" les commits d'une branche sur une autre, créant ainsi un historique plus linéaire.

---

### **La règle d'or du rebase**

La règle d'or du **rebase** est de **ne jamais l'utiliser sur des branches publiques**. En effet, le rebase réécrit l'historique des commits, ce qui peut entraîner des divergences avec d'autres développeurs travaillant sur les mêmes branches.

---

### **Conclusion**

Dans ce tutoriel, nous avons couvert les notions essentielles de **Git merge** et **Git rebase**, ainsi que la gestion des conflits de fusion. Le merge est une manière plus simple de combiner des branches, mais le rebase permet de maintenir un historique propre et linéaire. Assurez-vous de bien comprendre les différences entre ces deux approches avant de les utiliser dans vos projets.

Si vous avez trouvé ce tutoriel utile, partagez-le et mettez-le en pratique dans vos projets pour mieux maîtriser ces concepts.


