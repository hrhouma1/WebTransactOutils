### Tutoriel : Création de plusieurs sous-sites WordPress sur Ubuntu 22.04 avec Nginx

---

**Objectif :** Configurer un serveur local avec Ubuntu 22.04 pour héberger un site principal **elastic.local** et trois sous-sites : **dev.elastic.local**, **test.elastic.local** et **prod.elastic.local**. Chaque site aura son propre répertoire. Nous allons activer les deux premiers sous-sites et désactiver le troisième après l'avoir installé.

---

#### **Étape 1 : Préparation du serveur**

**1.1. Mettre à jour le système**

Ouvrez un terminal et exécutez les commandes suivantes pour mettre à jour votre système :

```bash
sudo apt update
sudo apt upgrade -y
```

**1.2. Installer Nginx**

Installez le serveur web Nginx avec la commande suivante :

```bash
sudo apt install nginx -y
```

**1.3. Installer PHP et les extensions nécessaires**

Installez PHP et les extensions requises pour WordPress :

```bash
sudo apt install php-fpm php-mysql php-curl php-gd php-xml php-mbstring -y
```

**1.4. Installer MySQL**

Installez le serveur de base de données MySQL :

```bash
sudo apt install mysql-server -y
```

**1.5. Sécuriser l'installation MySQL**

Exécutez le script de sécurisation de MySQL :

```bash
sudo mysql_secure_installation
```

Répondez aux questions posées :

- **Configurer le plugin VALIDATE PASSWORD ?** Appuyez sur **Entrée** pour ignorer ou tapez **y** pour configurer.
- **Définir le mot de passe root ?** Tapez **y** puis entrez un mot de passe sécurisé.
- **Supprimer les utilisateurs anonymes ?** Tapez **y**.
- **Interdire la connexion root à distance ?** Tapez **y**.
- **Supprimer la base de données de test et y accéder ?** Tapez **y**.
- **Recharger les tables de privilèges maintenant ?** Tapez **y**.

---

#### **Étape 2 : Créer les bases de données pour chaque site**

**2.1. Se connecter à MySQL en tant que root**

```bash
sudo mysql -u root -p
```

Entrez le mot de passe root que vous avez défini précédemment.

**2.2. Créer la base de données et l'utilisateur pour le site principal**

```sql
CREATE DATABASE elastic_local_db;
CREATE USER 'elastic_user'@'localhost' IDENTIFIED BY 'mot_de_passe_elastic';
GRANT ALL PRIVILEGES ON elastic_local_db.* TO 'elastic_user'@'localhost';
```

**2.3. Créer la base de données et l'utilisateur pour le sous-site dev.elastic.local**

```sql
CREATE DATABASE dev_elastic_local_db;
CREATE USER 'dev_user'@'localhost' IDENTIFIED BY 'mot_de_passe_dev';
GRANT ALL PRIVILEGES ON dev_elastic_local_db.* TO 'dev_user'@'localhost';
```

**2.4. Créer la base de données et l'utilisateur pour le sous-site test.elastic.local**

```sql
CREATE DATABASE test_elastic_local_db;
CREATE USER 'test_user'@'localhost' IDENTIFIED BY 'mot_de_passe_test';
GRANT ALL PRIVILEGES ON test_elastic_local_db.* TO 'test_user'@'localhost';
```

**2.5. Créer la base de données et l'utilisateur pour le sous-site prod.elastic.local**

```sql
CREATE DATABASE prod_elastic_local_db;
CREATE USER 'prod_user'@'localhost' IDENTIFIED BY 'mot_de_passe_prod';
GRANT ALL PRIVILEGES ON prod_elastic_local_db.* TO 'prod_user'@'localhost';
```

**2.6. Appliquer les modifications et quitter MySQL**

```sql
FLUSH PRIVILEGES;
EXIT;
```

---

#### **Étape 3 : Télécharger WordPress et configurer les répertoires**

**3.1. Télécharger la dernière version de WordPress**

```bash
cd /tmp
wget https://fr.wordpress.org/latest-fr_FR.tar.gz
tar -xzf latest-fr_FR.tar.gz
```

**3.2. Créer les répertoires pour chaque site**

```bash
sudo mkdir -p /var/www/elastic.local
sudo mkdir -p /var/www/dev.elastic.local
sudo mkdir -p /var/www/test.elastic.local
sudo mkdir -p /var/www/prod.elastic.local
```

**3.3. Copier les fichiers WordPress dans le répertoire du site principal**

```bash
sudo cp -r wordpress/* /var/www/elastic.local/
```

**3.4. Copier les fichiers WordPress dans le répertoire du sous-site dev.elastic.local**

```bash
sudo cp -r wordpress/* /var/www/dev.elastic.local/
```

**3.5. Copier les fichiers WordPress dans le répertoire du sous-site test.elastic.local**

```bash
sudo cp -r wordpress/* /var/www/test.elastic.local/
```

**3.6. Copier les fichiers WordPress dans le répertoire du sous-site prod.elastic.local**

```bash
sudo cp -r wordpress/* /var/www/prod.elastic.local/
```

**3.7. Définir les permissions appropriées pour les répertoires**

```bash
sudo chown -R www-data:www-data /var/www/elastic.local
sudo chown -R www-data:www-data /var/www/dev.elastic.local
sudo chown -R www-data:www-data /var/www/test.elastic.local
sudo chown -R www-data:www-data /var/www/prod.elastic.local

sudo find /var/www/ -type d -exec chmod 755 {} \;
sudo find /var/www/ -type f -exec chmod 644 {} \;
```

---

#### **Étape 4 : Configurer Nginx pour chaque site**

**4.1. Créer le fichier de configuration pour le site principal**

```bash
sudo nano /etc/nginx/sites-available/elastic.local
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name elastic.local;
    root /var/www/elastic.local;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**4.2. Créer le fichier de configuration pour le sous-site dev.elastic.local**

```bash
sudo nano /etc/nginx/sites-available/dev.elastic.local
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name dev.elastic.local;
    root /var/www/dev.elastic.local;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**4.3. Créer le fichier de configuration pour le sous-site test.elastic.local**

```bash
sudo nano /etc/nginx/sites-available/test.elastic.local
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name test.elastic.local;
    root /var/www/test.elastic.local;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**4.4. Créer le fichier de configuration pour le sous-site prod.elastic.local**

```bash
sudo nano /etc/nginx/sites-available/prod.elastic.local
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name prod.elastic.local;
    root /var/www/prod.elastic.local;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**4.5. Activer les sites en créant des liens symboliques**

**Activer le site principal :**

```bash
sudo ln -s /etc/nginx/sites-available/elastic.local /etc/nginx/sites-enabled/
```

**Activer le sous-site dev.elastic.local :**

```bash
sudo ln -s /etc/nginx/sites-available/dev.elastic.local /etc/nginx/sites-enabled/
```

**Activer le sous-site test.elastic.local :**

```bash
sudo ln -s /etc/nginx/sites-available/test.elastic.local /etc/nginx/sites-enabled/
```

**Activer le sous-site prod.elastic.local (nous le désactiverons plus tard) :**

```bash
sudo ln -s /etc/nginx/sites-available/prod.elastic.local /etc/nginx/sites-enabled/
```

**4.6. Ajouter les domaines locaux au fichier hosts**

```bash
sudo nano /etc/hosts
```

**Ajoutez les lignes suivantes à la fin du fichier :**

```plaintext
127.0.0.1   elastic.local
127.0.0.1   dev.elastic.local
127.0.0.1   test.elastic.local
127.0.0.1   prod.elastic.local
```

**4.7. Tester la configuration Nginx et redémarrer le service**

```bash
sudo nginx -t
sudo systemctl restart nginx
```

---

#### **Étape 5 : Configurer WordPress pour chaque site**

**5.1. Créer le fichier `wp-config.php` pour le site principal**

```bash
sudo cp /var/www/elastic.local/wp-config-sample.php /var/www/elastic.local/wp-config.php
```

**5.2. Modifier le fichier `wp-config.php` du site principal**

```bash
sudo nano /var/www/elastic.local/wp-config.php
```

**Apportez les modifications suivantes :**

- **Définir les informations de connexion à la base de données :**

  ```php
  define('DB_NAME', 'elastic_local_db');
  define('DB_USER', 'elastic_user');
  define('DB_PASSWORD', 'mot_de_passe_elastic');
  define('DB_HOST', 'localhost');
  ```

- **Générer des clés de sécurité uniques**

  Visitez [https://api.wordpress.org/secret-key/1.1/salt/](https://api.wordpress.org/secret-key/1.1/salt/) et copiez les clés générées.

  Remplacez les lignes suivantes dans `wp-config.php` par les clés copiées :

  ```php
  define('AUTH_KEY',         '...');
  define('SECURE_AUTH_KEY',  '...');
  define('LOGGED_IN_KEY',    '...');
  define('NONCE_KEY',        '...');
  define('AUTH_SALT',        '...');
  define('SECURE_AUTH_SALT', '...');
  define('LOGGED_IN_SALT',   '...');
  define('NONCE_SALT',       '...');
  ```

**5.3. Répéter les étapes pour le sous-site dev.elastic.local**

**Créer le fichier `wp-config.php` :**

```bash
sudo cp /var/www/dev.elastic.local/wp-config-sample.php /var/www/dev.elastic.local/wp-config.php
```

**Modifier le fichier `wp-config.php` :**

```bash
sudo nano /var/www/dev.elastic.local/wp-config.php
```

**Apportez les modifications suivantes :**

- **Définir les informations de connexion à la base de données :**

  ```php
  define('DB_NAME', 'dev_elastic_local_db');
  define('DB_USER', 'dev_user');
  define('DB_PASSWORD', 'mot_de_passe_dev');
  define('DB_HOST', 'localhost');
  ```

- **Générer et insérer des clés de sécurité uniques comme précédemment.**

**5.4. Répéter les étapes pour le sous-site test.elastic.local**

**Créer le fichier `wp-config.php` :**

```bash
sudo cp /var/www/test.elastic.local/wp-config-sample.php /var/www/test.elastic.local/wp-config.php
```

**Modifier le fichier `wp-config.php` :**

```bash
sudo nano /var/www/test.elastic.local/wp-config.php
```

**Apportez les modifications suivantes :**

- **Définir les informations de connexion à la base de données :**

  ```php
  define('DB_NAME', 'test_elastic_local_db');
  define('DB_USER', 'test_user');
  define('DB_PASSWORD', 'mot_de_passe_test');
  define('DB_HOST', 'localhost');
  ```

- **Générer et insérer des clés de sécurité uniques comme précédemment.**

**5.5. Répéter les étapes pour le sous-site prod.elastic.local**

**Créer le fichier `wp-config.php` :**

```bash
sudo cp /var/www/prod.elastic.local/wp-config-sample.php /var/www/prod.elastic.local/wp-config.php
```

**Modifier le fichier `wp-config.php` :**

```bash
sudo nano /var/www/prod.elastic.local/wp-config.php
```

**Apportez les modifications suivantes :**

- **Définir les informations de connexion à la base de données :**

  ```php
  define('DB_NAME', 'prod_elastic_local_db');
  define('DB_USER', 'prod_user');
  define('DB_PASSWORD', 'mot_de_passe_prod');
  define('DB_HOST', 'localhost');
  ```

- **Générer et insérer des clés de sécurité uniques comme précédemment.**

---

#### **Étape 6 : Finaliser l'installation de WordPress via le navigateur**

**6.1. Accéder au site principal**

Ouvrez votre navigateur et rendez-vous sur [http://elastic.local](http://elastic.local).

**6.2. Suivre les instructions d'installation**

- **Choisir la langue** : Sélectionnez **Français** et cliquez sur **Continuer**.
- **Informations nécessaires** : Cliquez sur **Let's go!** (ou **C'est parti !**).
- **Informations de connexion** : Comme nous avons déjà configuré le fichier `wp-config.php`, cette étape est sautée.
- **Titre du site** : Entrez **Elastic Local**.
- **Nom d'utilisateur** : Choisissez un nom d'utilisateur pour l'administrateur.
- **Mot de passe** : Choisissez un mot de passe sécurisé.
- **Votre adresse de messagerie** : Entrez votre email.
- **Visibilité pour les moteurs de recherche** : Comme c'est un site local, cette option n'a pas d'impact.
- **Cliquer sur Installer WordPress**.

**6.3. Répéter les étapes pour le sous-site dev.elastic.local**

Rendez-vous sur [http://dev.elastic.local](http://dev.elastic.local) et suivez les mêmes étapes d'installation. Utilisez un titre de site approprié, par exemple **Dev Elastic Local**.

**6.4. Répéter les étapes pour le sous-site test.elastic.local**

Rendez-vous sur [http://test.elastic.local](http://test.elastic.local) et suivez les mêmes étapes d'installation. Utilisez un titre de site approprié, par exemple **Test Elastic Local**.

**6.5. Répéter les étapes pour le sous-site prod.elastic.local**

Rendez-vous sur [http://prod.elastic.local](http://prod.elastic.local) et suivez les mêmes étapes d'installation. Utilisez un titre de site approprié, par exemple **Prod Elastic Local**.

---

#### **Étape 7 : Désactiver le sous-site prod.elastic.local**

Après avoir installé le sous-site **prod.elastic.local**, nous allons le désactiver.

**7.1. Supprimer le lien symbolique pour prod.elastic.local**

```bash
sudo rm /etc/nginx/sites-enabled/prod.elastic.local
```

**7.2. Redémarrer Nginx pour appliquer les modifications**

```bash
sudo systemctl restart nginx
```

Le sous-site **prod.elastic.local** est maintenant désactivé. Si vous essayez d'y accéder via le navigateur, il ne sera plus disponible.

---

#### **Étape 8 : Vérification finale**

**8.1. Vérifier l'accès au site principal**

Rendez-vous sur [http://elastic.local](http://elastic.local) pour vous assurer que le site fonctionne correctement.

**8.2. Vérifier l'accès au sous-site dev.elastic.local**

Rendez-vous sur [http://dev.elastic.local](http://dev.elastic.local) pour vérifier son fonctionnement.

**8.3. Vérifier l'accès au sous-site test.elastic.local**

Rendez-vous sur [http://test.elastic.local](http://test.elastic.local) pour vérifier son fonctionnement.

**8.4. Vérifier que le sous-site prod.elastic.local est bien désactivé**

Essayez d'accéder à [http://prod.elastic.local](http://prod.elastic.local). Vous devriez obtenir une erreur indiquant que le site n'est pas accessible.

---

#### **Étape 9 : Conseils supplémentaires**

- **Réactiver le sous-site prod.elastic.local si nécessaire**

  Si vous souhaitez réactiver le sous-site **prod.elastic.local**, recréez le lien symbolique et redémarrez Nginx :

  ```bash
  sudo ln -s /etc/nginx/sites-available/prod.elastic.local /etc/nginx/sites-enabled/
  sudo systemctl restart nginx
  ```

- **Gestion des plugins et thèmes**

  Installez des plugins et des thèmes adaptés pour chaque site en fonction de vos besoins.

- **Sauvegardes**

  Même en environnement local, il est recommandé de sauvegarder régulièrement vos bases de données et fichiers.

- **Mises à jour**

  Gardez WordPress, les thèmes et les plugins à jour pour bénéficier des dernières fonctionnalités et correctifs de sécurité.

---

#### **Conclusion**

Vous avez maintenant configuré un serveur local avec plusieurs sites WordPress distincts, chacun dans son propre répertoire. Vous savez comment activer et désactiver des sites selon vos besoins. Cela vous permettra de travailler sur différents environnements (développement, test, production) de manière isolée.

N'hésitez pas à explorer davantage les fonctionnalités de WordPress et de Nginx pour optimiser vos sites. Si vous avez des questions ou des difficultés, je suis là pour vous aider.

Bon courage dans votre apprentissage !
