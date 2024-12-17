# Sécurisation d'un site WordPress: 

Ce document décrit les mesures de sécurité essentielles pour protéger un site WordPress. Utilisant l'exemple du site /inkcrown.com(https://inkcrown.com), nous explorerons les fichiers critiques, les pratiques recommandées, et les configurations de sécurité.

# 1 - Détection de WordPress

Pour déterminer si un site utilise WordPress, des outils comme /WPThemeDetector(https://www.wpthemedetector.com/) peuvent être utilisés. Ce site détecte automatiquement les thèmes et plugins WordPress actifs.

# 2 - Structure de Fichiers WordPress

WordPress possède une structure de fichiers typique :

- **Administration et Connexion :**
  -  /wp-admin (https://inkcrown.com/wp-admin)
  - /wp-login(https://inkcrown.com/wp-login)
  - /users(https://inkcrown.com/users)
  - /wp-json/wp/v2/users(https://inkcrown.com/wp-json/wp/v2/users)

- **Contenu et Inclusions :**
  - /wp-content(https://inkcrown.com/wp-content)
  - /wp-includes(https://inkcrown.com/wp-includes)

- **Maintenance et Configuration :**
  - /wp-cron.php(https://inkcrown.com/wp-cron.php)
  - /xmlrpc.php(https://inkcrown.com/xmlrpc.php)
  - /wp-signup.php(https://inkcrown.com/wp-signup.php)
  - /wp-activate.php(https://inkcrown.com/wp-activate.php)
  - /wp-comments-post.php(https://inkcrown.com/wp-comments-post.php)
  - /readme.html(https://inkcrown.com/readme.html)
  - /license.txt(https://inkcrown.com/license.txt)
  - /wp-config.php(https://inkcrown.com/wp-config.php)
  - /wp-load.php(https://inkcrown.com/wp-load.php)
  - /wp-trackback.php(https://inkcrown.com/wp-trackback.php)

- **Sitemaps et Installation :**
  - /sitemap.xml(https://inkcrown.com/sitemap.xml)
  - /sitemap_index.xml(https://inkcrown.com/sitemap_index.xml)
  - /wp-admin/install.php(https://inkcrown.com/wp-admin/install.php)

# 3 - Pratiques de Sécurité Recommandées

# 3-1- Supprimer `install.php`

Le fichier `install.php` peut être exploité par des pirates pour réinitialiser le site, entraînant la suppression de la base de données existante et une nouvelle installation de WordPress. Il est crucial de supprimer ou renommer ce fichier après l'installation initiale.

# 3-2- Protection des Utilisateurs

Vous pouvez visualiser les utilisateurs du site via l'API REST de WordPress. Par exemple :

```bash
curl -s https://inkcrown.com/wp-json/wp/v2/users
```

Cela retourne les informations des utilisateurs, par exemple :

```json
/
  {
    "id": 1,
    "name": "inkcrownstudio",
    "url": "",
    "description": ""
  }

```

Avec le nom d'utilisateur `inkcrownstudio`, des attaquants pourraient utiliser des attaques par force brute pour deviner le mot de passe. Cela souligne l'importance d'utiliser des mots de passe forts et uniques, ainsi que des mesures de sécurité supplémentaires comme l'authentification à deux facteurs (2FA) et la limitation des tentatives de connexion.

# 3-4- Sécurisation de wp-admin avec .htaccess

Pour renforcer la sécurité de l'administration WordPress, vous pouvez utiliser un fichier `.htaccess` pour restreindre l'accès à `wp-admin`. Voici un exemple de configuration :

```apache
<Files wp-login.php>
    Order Deny,Allow
    Deny from all
    Allow from /YOUR IP ADDRESS
</Files>
```

Remplacez `/YOUR IP ADDRESS` par votre adresse IP. Cela permet seulement à l'adresse IP spécifiée d'accéder à la page de connexion de WordPress.

# 3-5- Importance de la Sécurité Web

Ces exemples montrent l'importance de sécuriser un site web, notamment ceux construits sur des plateformes largement utilisées comme WordPress. Voici quelques étapes essentielles :

- Mettre régulièrement à jour le noyau WordPress, les thèmes, et les plugins.
- Supprimer ou sécuriser les fichiers par défaut pouvant être utilisés de manière malveillante.
- Surveiller les comptes utilisateurs et les journaux d'accès.
- Utiliser des plugins de sécurité et imposer des mots de passe forts.

En suivant ces pratiques, vous pouvez réduire considérablement le risque de compromission de votre site WordPress.
