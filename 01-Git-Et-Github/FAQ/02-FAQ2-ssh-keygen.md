# Tutoriel détaillé sur l’utilisation de `ssh-keygen`

Ce tutoriel vous guide pas à pas dans l'utilisation de `ssh-keygen` pour configurer une authentification sécurisée avec des clés SSH pour interagir avec GitHub, sans avoir besoin d’entrer votre mot de passe à chaque fois.

--------
# Étape 1 : Générer une paire de clés SSH
--------

**Commande :**
```bash
ssh-keygen
```
Cette commande génère une paire de clés RSA, composée d'une **clé publique** et d'une **clé privée**. Ces clés sont utilisées pour l'authentification SSH sécurisée. La **clé publique** peut être partagée librement tandis que la **clé privée** doit rester secrète et sécurisée sur votre machine.

Vous allez être invité à :
- **Choisir l'emplacement** où enregistrer la clé. Par défaut, elle est enregistrée dans le dossier suivant : `/root/.ssh/id_rsa`. Si une clé existe déjà, vous pouvez choisir de la **remplacer** en tapant `y`.
- **Définir une passphrase** (facultatif). Si vous souhaitez sécuriser davantage la clé privée, vous pouvez définir une passphrase. Vous pouvez également laisser le champ vide si vous ne souhaitez pas de passphrase.

Après la génération, les fichiers seront enregistrés ici :
- **Clé privée** : `/root/.ssh/id_rsa`
- **Clé publique** : `/root/.ssh/id_rsa.pub`

--------
# Étape 2 : Afficher la clé publique
--------

Une fois les clés générées, vous devrez copier la clé publique pour l’ajouter à GitHub.

**Commande :**
```bash
cat /root/.ssh/id_rsa.pub
```
Cela affichera le contenu de votre fichier de clé publique. Vous devez copier la sortie pour l'utiliser dans l'étape suivante.


--------
# Étape 3 : Ajouter la clé publique à GitHub
--------

1. Allez dans les **paramètres** de votre dépôt GitHub.
2. Sélectionnez **Deploy keys** dans la barre de navigation gauche.
3. Cliquez sur **Add deploy key**.
4. Collez la clé publique que vous avez copiée dans le champ **Key**.
5. Donnez un titre à votre clé, par exemple **KeyProjetJava**.
6. Activez l'option **Allow write access** si vous avez besoin de pousser des changements vers ce dépôt.
7. Cliquez sur **Add key** pour enregistrer.

--------
# Étape 4 : Cloner le dépôt en utilisant SSH
--------

Maintenant que la clé SSH est ajoutée à GitHub, vous pouvez cloner votre dépôt sans avoir besoin de saisir de nom d'utilisateur ni de mot de passe.

**Commande :**
```bash
git clone git@github.com:<nom_utilisateur>/<nom_repertoire>.git
```
Par exemple :
```bash
git clone git@github.com:hrhouma/ProjetJava.git
```
Remplacez `<nom_utilisateur>` et `<nom_repertoire>` par vos propres informations.

--------
# Étape 5 : Effectuer des opérations Git
--------

Une fois le dépôt cloné, naviguez dans le dossier du projet :
```bash
cd ProjetJava/
```

Créez ou modifiez des fichiers, par exemple :
```bash
touch clara.json
```

Ajoutez et validez vos modifications :
```bash
git add clara.json
git commit -m "Ajout du fichier clara.json"
```

Poussez les modifications vers GitHub :
```bash
git push origin main
```
Grâce à l'authentification par clé SSH, Git ne vous demandera plus de mot de passe.

---
# Annexe : Explication du fonctionnement des clés SSH
--------
L'authentification par clé SSH repose sur une **clé publique** et une **clé privée**. Ce mécanisme de chiffrement asymétrique garantit une communication sécurisée entre deux systèmes.

# 1. **Clé publique** et **Clé privée**

- **Clé publique** : Elle est utilisée pour **chiffrer** les informations envoyées à un serveur. Vous pouvez la partager sans risque, car seule la clé privée correspondante peut déchiffrer les messages chiffrés avec la clé publique.
  
- **Clé privée** : Elle reste sur votre machine et **ne doit jamais être partagée**. Cette clé privée sert à **décrypter** les messages chiffrés avec la clé publique, assurant ainsi que vous êtes le seul à pouvoir accéder aux données chiffrées.

# 2. **Comment cela fonctionne-t-il ?**

Imaginons un scénario où vous vous connectez à un serveur GitHub via SSH :

1. Vous générez une paire de clés publique et privée avec `ssh-keygen`.
2. Vous **ajoutez la clé publique** sur GitHub. Elle sera utilisée pour chiffrer les demandes de connexion que GitHub vous enverra.
3. Lorsque vous essayez de vous connecter, GitHub envoie un message chiffré avec votre **clé publique**.
4. Vous utilisez votre **clé privée** pour déchiffrer ce message. Si le message est correctement déchiffré, cela prouve que vous possédez la clé privée correspondante à la clé publique, et GitHub vous autorise à accéder à votre dépôt.

Ce système est extrêmement sécurisé, car même si quelqu'un intercepte la clé publique, il ne pourra pas déchiffrer les messages ou usurper votre identité sans la clé privée.

# 3. **Avantages de l'authentification SSH avec des clés**

- **Sécurité accrue** : Il est beaucoup plus difficile de compromettre une clé privée que de deviner un mot de passe.
- **Pas besoin de mot de passe** : Une fois configurée, l'authentification SSH par clé permet de se connecter sans mot de passe, ce qui est plus rapide et plus pratique.
- **Adapté pour l’automatisation** : Lors de l’utilisation de scripts ou d’outils automatisés (par exemple, CI/CD), l’authentification par clé SSH est plus pratique qu'un mot de passe.

