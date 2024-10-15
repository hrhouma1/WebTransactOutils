# FAQ sur la configuration Git

### Question :
Si j'utilise la commande `git config --local user.name`, est-ce sécuritaire ? Une personne qui connaît mon nom d'utilisateur et mon email peut-elle se faire passer pour moi ?

### Réponse :
Utiliser la commande `git config --local user.name` ou `git config --local user.email` n'est pas en soi une faille de sécurité. Ces commandes définissent des métadonnées dans votre dépôt local pour identifier qui a effectué des commits. Cependant, cela ne concerne pas l'authentification pour des actions telles que pousser des changements vers un dépôt distant comme GitHub.

Voici les points à garder en tête :

- **Authentification nécessaire** : Même si quelqu'un connaît votre nom d'utilisateur et votre email, il ne pourra pas accéder à votre compte GitHub sans une authentification, comme un jeton d'accès personnel ou une clé SSH.
  
- **Commits falsifiés** : Si une personne a accès à votre dépôt local, elle peut théoriquement effectuer des commits sous votre nom. Cependant, pour pousser ces commits sur GitHub, elle aurait toujours besoin de vos identifiants d'authentification.

- **Sécurité locale** : La sécurisation de votre environnement local (mot de passe fort, chiffrement des disques, etc.) est essentielle pour éviter toute modification non autorisée dans vos dépôts locaux.

En résumé, connaître votre nom d'utilisateur et votre email ne permet pas à quelqu'un de se faire passer pour vous sur GitHub sans avoir également accès à vos mécanismes d'authentification. Assurez-vous de bien protéger vos identifiants et l'accès à votre machine.

