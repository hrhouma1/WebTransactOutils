# Introduction à GitHub Actions : Guide pour les débutants 🚀

## Introduction: 

CI/CD, pour **Continuous Integration** et **Continuous Delivery/Deployment**, est un ensemble de pratiques qui automatise les processus de développement et de livraison de logiciels. En **Continuous Integration** (CI), les développeurs intègrent fréquemment leur code dans un dépôt partagé. Ce code est ensuite automatiquement testé et validé pour détecter rapidement les erreurs, assurant ainsi la qualité du code dès les premières étapes. **Continuous Delivery** (CD) va un peu plus loin en préparant le code testé pour le déploiement dans différents environnements, tandis que **Continuous Deployment** pousse ce code jusqu’en production automatiquement après chaque modification validée. Ensemble, ces pratiques permettent des cycles de développement plus rapides, une meilleure qualité de code et des livraisons de logiciels plus fiables.

## 1. Qu'est-ce que GitHub Actions ? 🤔

**GitHub Actions** est une fonctionnalité intégrée à GitHub qui permet d’automatiser des tâches dans votre dépôt de code. Il facilite la création de workflows pour **construire, tester et déployer** du code directement depuis GitHub, en déclenchant des actions basées sur des événements comme des pull requests ou des push sur certaines branches.

Les actions sont définies via des fichiers **YAML** dans le répertoire `.github/workflows` de votre dépôt. Un workflow peut comprendre plusieurs étapes, comme l’exécution de tests, le déploiement de code ou l’envoi de notifications.

### Avantages de GitHub Actions
1. **Automatisation des workflows** : automatisation des tâches répétitives (tests, déploiements).
2. **Intégration avec GitHub** : actions déclenchées par les événements GitHub (push, pull request, etc.).
3. **Écosystème large** : des actions disponibles pour automatiser de nombreuses tâches.
4. **Sécurité et fiabilité** : exécution des workflows dans des environnements isolés.
5. **Support de multiples langages et plateformes** : compatible avec différents projets et langages.

---

## 2. Comment démarrer avec GitHub Actions 🎬

### Étape 1 : Créer un dépôt GitHub
Si vous n’avez pas encore de compte, inscrivez-vous gratuitement. Ensuite, créez un nouveau dépôt pour y gérer vos workflows.

### Étape 2 : Ajouter un fichier de workflow
Accédez à l’onglet **Actions** de votre dépôt et cliquez sur **New workflow** pour créer un nouveau workflow. Vous pouvez partir d’un modèle ou créer votre propre fichier YAML.

**Exemple de fichier YAML pour un workflow simple :**
1. Dans le répertoire racine de votre dépôt, créez un dossier `.github/workflows` s'il n'existe pas.
2. Créez un fichier `test.yml` avec le contenu suivant :

```yaml
name: Test
on:
  push:
    branches:
      - main
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - name: Install dependencies
      run: npm install
    - name: Run tests
      run: npm test
```

Ce code déclenche un workflow nommé "Test" à chaque push sur la branche `main`. Le job `test` s’exécute sur Ubuntu et comprend trois étapes : vérifier le code, installer les dépendances et lancer les tests.

---

## 3. Comment fonctionne GitHub Actions ? 🛠️

Les workflows GitHub Actions sont des fichiers **YAML** qui contiennent des **jobs** et des **steps**.
- **Jobs** : ensemble d'actions exécutées en parallèle ou en séquence.
- **Steps** : actions individuelles au sein d’un job, comme exécuter un script, installer des dépendances, ou déployer le code.

Les workflows peuvent être déclenchés par divers **événements**, comme :
- **push** ou **pull_request** : exécution du workflow lorsqu’un code est poussé ou lorsqu’une pull request est créée.
- **schedule** : exécution du workflow selon un calendrier (ex. : tous les jours à minuit).
- **workflow_dispatch** : déclenchement manuel par l’utilisateur.

---

## 4. Cas d'utilisation courants pour GitHub Actions 📝

### 1. CI/CD (Intégration et Déploiement Continus)
GitHub Actions est parfait pour mettre en place des pipelines CI/CD, permettant de tester et de déployer du code automatiquement pour garantir la qualité avant de le mettre en production.

### 2. Tests automatisés
À chaque commit, des tests peuvent être lancés pour vérifier que le code fonctionne correctement et éviter les erreurs lors de l'intégration dans la branche principale.

### 3. Notifications
Les workflows peuvent envoyer des notifications par e-mail ou sur Slack lorsque certaines actions se produisent (ex. : un test échoue).

### 4. Analyse du code
GitHub Actions peut intégrer des outils de qualité de code comme ESLint pour garantir que le code respecte les standards.

---

## 5. Exemple de workflow complet 🚀

Essayons un exemple de workflow pour tester du code React à chaque push sur `main` :

1. **Créer le fichier `test.yml` :**
    ```yaml
    name: Test React App
    on:
      push:
        branches:
          - main
    jobs:
      test:
        runs-on: ubuntu-latest
        steps:
        - uses: actions/checkout@v2
        - name: Install dependencies
          run: npm install
        - name: Run tests
          run: npm test
    ```

2. **Commiter et pousser le fichier :** Une fois votre workflow en place, committez-le et poussez-le sur GitHub.

3. **Visualiser le workflow :** Dans l’onglet **Actions**, vous pouvez voir le workflow "Test React App" s’exécuter chaque fois que vous faites un push sur `main`.

---

## 6. Conclusion 🎉

GitHub Actions est un outil puissant pour l’automatisation des workflows de développement. Il permet de simplifier les pipelines CI/CD, d’automatiser les tests et le déploiement, et de s'intégrer facilement avec GitHub. En combinant les workflows disponibles et en créant vos propres actions personnalisées, vous pouvez gérer de manière efficace tous les aspects de l’automatisation de vos projets.

### Références
- [Documentation officielle de GitHub Actions](https://docs.github.com/en/actions)
- [Créer des actions personnalisées](https://docs.github.com/en/actions/creating-actions)
- [Marketplace GitHub Actions](https://github.com/marketplace)

GitHub Actions offre de grandes possibilités pour améliorer la productivité et la qualité du code, alors n’hésitez pas à l’explorer pour optimiser vos projets !
