# Configuration de plusieurs clés SSH pour différents projets GitHub et GitLab

Ce guide détaille la configuration de plusieurs clés SSH pour accéder à différents projets sur GitHub et GitLab, en associant chaque clé à un dépôt spécifique.

# Objectif : 
 - Configurer plusieurs clés SSH en fonction de différents projets, vous pouvez utiliser le fichier `~/.ssh/config` pour associer chaque clé à un projet ou dépôt spécifique.
   


## 1. Générer des clés SSH pour chaque projet

Pour chaque projet, générez une clé SSH avec un nom unique.

### Exemple de commandes pour chaque projet

1. **Projet GitHub 1**
   ```bash
   ssh-keygen -t rsa -b 4096 -C "rhoumahaythem@gmail.com" -f ~/.ssh/id_rsa_projet1_github
   ```

2. **Projet GitHub 2**
   ```bash
   ssh-keygen -t rsa -b 4096 -C "rhoumahaythem@gmail.com" -f ~/.ssh/id_rsa_projet2_github
   ```

3. **Projet GitLab**
   ```bash
   ssh-keygen -t rsa -b 4096 -C "rhoumahaythem@gmail.com" -f ~/.ssh/id_rsa_projet_gitlab
   ```

Chaque commande crée une paire de clés SSH avec des noms spécifiques :
- `id_rsa_projet1_github`, `id_rsa_projet1_github.pub`
- `id_rsa_projet2_github`, `id_rsa_projet2_github.pub`
- `id_rsa_projet_gitlab`, `id_rsa_projet_gitlab.pub`

## 2. Ajouter les clés SSH aux services GitHub et GitLab

### Pour GitHub

1. Connectez-vous à [GitHub](https://github.com).
2. Allez dans **Settings** > **SSH and GPG keys**.
3. Ajoutez chaque clé publique (`.pub`) pour les projets concernés.

### Pour GitLab

1. Connectez-vous à [GitLab](https://gitlab.com).
2. Allez dans **Settings** > **SSH Keys**.
3. Collez la clé publique de `~/.ssh/id_rsa_projet_gitlab.pub`.

## 3. Configurer le fichier `~/.ssh/config`

Pour associer chaque clé à un dépôt spécifique, vous pouvez utiliser des noms d’hôtes personnalisés dans le fichier `~/.ssh/config`.

### Ouvrez ou créez `~/.ssh/config`

```bash
nano ~/.ssh/config
```

### Ajouter une configuration pour chaque projet

Ajoutez les configurations suivantes pour chaque projet GitHub et GitLab.

```config
# Configuration pour le projet GitHub 1
Host github-projet1
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_projet1_github

# Configuration pour le projet GitHub 2
Host github-projet2
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_projet2_github

# Configuration pour le projet GitLab
Host gitlab-projet
  HostName gitlab.com
  User git
  IdentityFile ~/.ssh/id_rsa_projet_gitlab
```

Dans ce fichier :
- `Host` : Nom personnalisé que vous utiliserez lors du clonage de chaque projet (ex. `github-projet1`).
- `IdentityFile` : Chemin vers la clé SSH dédiée à ce projet.

### Cloner les projets en utilisant les noms d’hôtes configurés

1. **Cloner le projet GitHub 1**
   ```bash
   git clone git@github-projet1:username/projet1.git
   ```

2. **Cloner le projet GitHub 2**
   ```bash
   git clone git@github-projet2:username/projet2.git
   ```

3. **Cloner le projet GitLab**
   ```bash
   git clone git@gitlab-projet:username/projet.git
   ```

Remplacez `username` et `projet` par les noms d'utilisateur et de dépôt appropriés pour chaque projet.

## 4. Tester la connexion SSH pour chaque projet

Pour vérifier que la configuration est correcte, vous pouvez tester la connexion SSH avec chaque nom d’hôte :

1. **Tester GitHub Projet 1**
   ```bash
   ssh -T git@github-projet1
   ```

2. **Tester GitHub Projet 2**
   ```bash
   ssh -T git@github-projet2
   ```

3. **Tester GitLab Projet**
   ```bash
   ssh -T git@gitlab-projet
   ```

Chaque commande devrait afficher un message de bienvenue si la connexion fonctionne correctement.

---

## Résolution de problèmes

Si vous rencontrez des erreurs de permissions, assurez-vous que les fichiers de clé ont les bonnes permissions :

```bash
chmod 600 ~/.ssh/id_rsa_projet1_github
chmod 600 ~/.ssh/id_rsa_projet2_github
chmod 600 ~/.ssh/id_rsa_projet_gitlab
```

## Ressources

- [Documentation GitHub sur les clés SSH](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/about-ssh)
- [Documentation GitLab sur les clés SSH](https://docs.gitlab.com/ee/ssh/)

---

Cela permet de gérer plusieurs projets GitHub et GitLab en utilisant des clés SSH spécifiques pour chaque dépôt.
