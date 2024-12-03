### Tutoriel complet : Héberger plusieurs sites WordPress sur un serveur distant Ubuntu 22.04 avec Nginx

---

**Objectif :** Apprendre à installer et configurer plusieurs sites WordPress sur un serveur distant exécutant Ubuntu 22.04 avec Nginx. Nous allons créer un site principal avec le domaine **mywebsite.com** et trois sous-domaines : **blog.mywebsite.com**, **shop.mywebsite.com** et **forum.mywebsite.com**. Chaque site aura son propre répertoire. Ce guide détaillera chaque étape afin que vous puissiez suivre en copiant/collant les commandes sans rencontrer de problèmes.

---

#### **Prérequis :**

- Un serveur distant exécutant Ubuntu 22.04 (par exemple, une instance chez Hostinger ou Vultr).
- Accès root ou sudo au serveur.
- Noms de domaine enregistrés (ou des sous-domaines configurés) pointant vers l'adresse IP de votre serveur.
- Un client SSH pour se connecter au serveur (comme PuTTY ou Terminal).

---

#### **Étape 1 : Connexion au serveur**

**1.1.** **Obtenir les informations de connexion :**

- Adresse IP du serveur : `XXX.XXX.XXX.XXX` (remplacez par votre adresse IP réelle).
- Nom d'utilisateur : `root` (ou un autre utilisateur avec privilèges sudo).
- Mot de passe ou clé SSH pour l'authentification.

**1.2.** **Se connecter au serveur via SSH :**

- **Sur Linux ou macOS :**

  ```bash
  ssh root@XXX.XXX.XXX.XXX
  ```

- **Sur Windows :**

  - Téléchargez et installez [PuTTY](https://www.putty.org/).
  - Ouvrez PuTTY, entrez l'adresse IP dans le champ **Host Name**, et cliquez sur **Open**.
  - Entrez votre nom d'utilisateur et mot de passe lorsque vous y êtes invité.

---

#### **Étape 2 : Mettre à jour le serveur**

Avant d'installer de nouveaux paquets, il est important de mettre à jour la liste des paquets et les paquets installés.

**2.1.** **Mettre à jour la liste des paquets :**

```bash
sudo apt update
```

**2.2.** **Mettre à niveau les paquets installés :**

```bash
sudo apt upgrade -y
```

---

#### **Étape 3 : Installer Nginx**

Nginx est le serveur web que nous allons utiliser pour héberger nos sites.

**3.1.** **Installer Nginx :**

```bash
sudo apt install nginx -y
```

**3.2.** **Vérifier que Nginx est en cours d'exécution :**

```bash
sudo systemctl status nginx
```

Vous devriez voir un statut **active (running)**. Si ce n'est pas le cas, démarrez Nginx :

```bash
sudo systemctl start nginx
```

**3.3.** **Autoriser le trafic HTTP et HTTPS à travers le pare-feu :**

```bash
sudo ufw allow 'Nginx Full'
```

---

#### **Étape 4 : Installer MySQL**

Nous utiliserons MySQL pour gérer les bases de données de nos sites WordPress.

**4.1.** **Installer MySQL :**

```bash
sudo apt install mysql-server -y
```

**4.2.** **Sécuriser l'installation de MySQL :**

```bash
sudo mysql_secure_installation
```

**Pendant le script :**

- **Configurer le plugin VALIDATE PASSWORD ?** Tapez **N** pour non.
- **Définir un mot de passe root ?** Tapez **Y** puis entrez un mot de passe sécurisé. **Notez ce mot de passe**, vous en aurez besoin plus tard.
- **Supprimer les utilisateurs anonymes ?** Tapez **Y**.
- **Interdire la connexion root à distance ?** Tapez **Y**.
- **Supprimer la base de données de test ?** Tapez **Y**.
- **Recharger les tables de privilèges ?** Tapez **Y**.

**4.3.** **Vérifier que MySQL est en cours d'exécution :**

```bash
sudo systemctl status mysql
```

---

#### **Étape 5 : Installer PHP et les extensions nécessaires**

WordPress nécessite PHP pour fonctionner.

**5.1.** **Installer PHP et les extensions :**

```bash
sudo apt install php-fpm php-mysql php-curl php-gd php-xml php-mbstring php-xmlrpc php-soap php-intl php-zip -y
```

**5.2.** **Vérifier la version de PHP installée :**

```bash
php -v
```

Vous devriez voir quelque chose comme **PHP 8.1.x**.

---

#### **Étape 6 : Créer les bases de données pour chaque site**

Nous allons créer une base de données et un utilisateur MySQL pour chaque site.

**6.1.** **Se connecter à MySQL en tant que root :**

```bash
sudo mysql -u root -p
```

Entrez le mot de passe root que vous avez défini précédemment.

**6.2.** **Créer la base de données et l'utilisateur pour le site principal (mywebsite.com) :**

```sql
CREATE DATABASE mywebsite_db DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'mywebsite_user'@'localhost' IDENTIFIED BY 'MotDePasseMyWebsite';
GRANT ALL PRIVILEGES ON mywebsite_db.* TO 'mywebsite_user'@'localhost';
FLUSH PRIVILEGES;
```

**6.3.** **Créer la base de données et l'utilisateur pour le sous-domaine blog.mywebsite.com :**

```sql
CREATE DATABASE blog_db DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'blog_user'@'localhost' IDENTIFIED BY 'MotDePasseBlog';
GRANT ALL PRIVILEGES ON blog_db.* TO 'blog_user'@'localhost';
FLUSH PRIVILEGES;
```

**6.4.** **Créer la base de données et l'utilisateur pour le sous-domaine shop.mywebsite.com :**

```sql
CREATE DATABASE shop_db DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'shop_user'@'localhost' IDENTIFIED BY 'MotDePasseShop';
GRANT ALL PRIVILEGES ON shop_db.* TO 'shop_user'@'localhost';
FLUSH PRIVILEGES;
```

**6.5.** **Créer la base de données et l'utilisateur pour le sous-domaine forum.mywebsite.com :**

```sql
CREATE DATABASE forum_db DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'forum_user'@'localhost' IDENTIFIED BY 'MotDePasseForum';
GRANT ALL PRIVILEGES ON forum_db.* TO 'forum_user'@'localhost';
FLUSH PRIVILEGES;
```

**6.6.** **Quitter MySQL :**

```sql
EXIT;
```

---

#### **Étape 7 : Télécharger et configurer WordPress pour chaque site**

**7.1.** **Télécharger la dernière version de WordPress :**

```bash
cd /tmp
wget https://fr.wordpress.org/latest-fr_FR.tar.gz
tar -xzf latest-fr_FR.tar.gz
```

**7.2.** **Créer les répertoires pour chaque site :**

```bash
sudo mkdir -p /var/www/mywebsite.com
sudo mkdir -p /var/www/blog.mywebsite.com
sudo mkdir -p /var/www/shop.mywebsite.com
sudo mkdir -p /var/www/forum.mywebsite.com
```

**7.3.** **Copier les fichiers WordPress dans chaque répertoire :**

- **Pour mywebsite.com :**

  ```bash
  sudo cp -r /tmp/wordpress/* /var/www/mywebsite.com/
  ```

- **Pour blog.mywebsite.com :**

  ```bash
  sudo cp -r /tmp/wordpress/* /var/www/blog.mywebsite.com/
  ```

- **Pour shop.mywebsite.com :**

  ```bash
  sudo cp -r /tmp/wordpress/* /var/www/shop.mywebsite.com/
  ```

- **Pour forum.mywebsite.com :**

  ```bash
  sudo cp -r /tmp/wordpress/* /var/www/forum.mywebsite.com/
  ```

**7.4.** **Attribuer les permissions appropriées :**

```bash
sudo chown -R www-data:www-data /var/www/mywebsite.com
sudo chown -R www-data:www-data /var/www/blog.mywebsite.com
sudo chown -R www-data:www-data /var/www/shop.mywebsite.com
sudo chown -R www-data:www-data /var/www/forum.mywebsite.com

sudo find /var/www/ -type d -exec chmod 755 {} \;
sudo find /var/www/ -type f -exec chmod 644 {} \;
```

---

#### **Étape 8 : Configurer Nginx pour chaque site**

**8.1.** **Créer le fichier de configuration pour mywebsite.com :**

```bash
sudo nano /etc/nginx/sites-available/mywebsite.com
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name mywebsite.com www.mywebsite.com;
    root /var/www/mywebsite.com;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**8.2.** **Créer le fichier de configuration pour blog.mywebsite.com :**

```bash
sudo nano /etc/nginx/sites-available/blog.mywebsite.com
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name blog.mywebsite.com;
    root /var/www/blog.mywebsite.com;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**8.3.** **Créer le fichier de configuration pour shop.mywebsite.com :**

```bash
sudo nano /etc/nginx/sites-available/shop.mywebsite.com
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name shop.mywebsite.com;
    root /var/www/shop.mywebsite.com;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**8.4.** **Créer le fichier de configuration pour forum.mywebsite.com :**

```bash
sudo nano /etc/nginx/sites-available/forum.mywebsite.com
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name forum.mywebsite.com;
    root /var/www/forum.mywebsite.com;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**8.5.** **Activer les sites en créant des liens symboliques :**

```bash
sudo ln -s /etc/nginx/sites-available/mywebsite.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/blog.mywebsite.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/shop.mywebsite.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/forum.mywebsite.com /etc/nginx/sites-enabled/
```

**8.6.** **Vérifier la configuration de Nginx :**

```bash
sudo nginx -t
```

Si vous voyez **syntax is ok** et **test is successful**, vous pouvez redémarrer Nginx.

**8.7.** **Redémarrer Nginx :**

```bash
sudo systemctl restart nginx
```

---

#### **Étape 9 : Configurer les enregistrements DNS pour chaque domaine**

Pour que vos domaines pointent vers votre serveur, vous devez configurer les enregistrements DNS chez votre registraire de domaine.

**9.1.** **Ajouter un enregistrement A pour le domaine principal (mywebsite.com) :**

- **Type :** A
- **Nom :** @
- **Valeur :** `XXX.XXX.XXX.XXX` (adresse IP de votre serveur)

- **Type :** A
- **Nom :** www
- **Valeur :** `XXX.XXX.XXX.XXX`

**9.2.** **Ajouter des enregistrements A pour les sous-domaines :**

- **Pour blog.mywebsite.com :**

  - **Type :** A
  - **Nom :** blog
  - **Valeur :** `XXX.XXX.XXX.XXX`

- **Pour shop.mywebsite.com :**

  - **Type :** A
  - **Nom :** shop
  - **Valeur :** `XXX.XXX.XXX.XXX`

- **Pour forum.mywebsite.com :**

  - **Type :** A
  - **Nom :** forum
  - **Valeur :** `XXX.XXX.XXX.XXX`

**9.3.** **Attendre la propagation DNS :**

La propagation des enregistrements DNS peut prendre de quelques minutes à 24 heures. Vous pouvez vérifier la propagation en utilisant des outils comme [WhatsMyDNS](https://www.whatsmydns.net/).

---

#### **Étape 10 : Installer Certbot pour les certificats SSL (Optionnel mais recommandé)**

L'utilisation de certificats SSL permet d'établir une connexion sécurisée (HTTPS) vers vos sites.

**10.1.** **Installer Certbot et le plugin Nginx :**

```bash
sudo apt install certbot python3-certbot-nginx -y
```

**10.2.** **Obtenir des certificats SSL pour chaque domaine :**

- **Pour mywebsite.com :**

  ```bash
  sudo certbot --nginx -d mywebsite.com -d www.mywebsite.com
  ```

- **Pour blog.mywebsite.com :**

  ```bash
  sudo certbot --nginx -d blog.mywebsite.com
  ```

- **Pour shop.mywebsite.com :**

  ```bash
  sudo certbot --nginx -d shop.mywebsite.com
  ```

- **Pour forum.mywebsite.com :**

  ```bash
  sudo certbot --nginx -d forum.mywebsite.com
  ```

**10.3.** **Suivre les instructions de Certbot :**

- Entrez une adresse e-mail valide.
- Acceptez les conditions d'utilisation.
- Choisissez si vous souhaitez partager votre adresse e-mail avec l'EFF.

**10.4.** **Vérifier que les sites sont accessibles en HTTPS :**

Visitez vos sites en utilisant **https://** pour vous assurer que les certificats SSL fonctionnent correctement.

---

#### **Étape 11 : Configurer WordPress pour chaque site**

**11.1.** **Créer le fichier `wp-config.php` pour chaque site**

- **Pour mywebsite.com :**

  ```bash
  sudo cp /var/www/mywebsite.com/wp-config-sample.php /var/www/mywebsite.com/wp-config.php
  ```

- **Pour blog.mywebsite.com :**

  ```bash
  sudo cp /var/www/blog.mywebsite.com/wp-config-sample.php /var/www/blog.mywebsite.com/wp-config.php
  ```

- **Pour shop.mywebsite.com :**

  ```bash
  sudo cp /var/www/shop.mywebsite.com/wp-config-sample.php /var/www/shop.mywebsite.com/wp-config.php
  ```

- **Pour forum.mywebsite.com :**

  ```bash
  sudo cp /var/www/forum.mywebsite.com/wp-config-sample.php /var/www/forum.mywebsite.com/wp-config.php
  ```

**11.2.** **Modifier le fichier `wp-config.php` pour chaque site**

- **Pour mywebsite.com :**

  ```bash
  sudo nano /var/www/mywebsite.com/wp-config.php
  ```

  **Modifications à apporter :**

  ```php
  define('DB_NAME', 'mywebsite_db');
  define('DB_USER', 'mywebsite_user');
  define('DB_PASSWORD', 'MotDePasseMyWebsite');
  define('DB_HOST', 'localhost');
  define('DB_CHARSET', 'utf8mb4');
  define('DB_COLLATE', '');
  ```

  **Générer des clés de sécurité :**

  Rendez-vous sur [https://api.wordpress.org/secret-key/1.1/salt/](https://api.wordpress.org/secret-key/1.1/salt/) et copiez les clés générées. Remplacez les lignes correspondantes dans `wp-config.php`.

- **Pour blog.mywebsite.com :**

  ```bash
  sudo nano /var/www/blog.mywebsite.com/wp-config.php
  ```

  **Modifications à apporter :**

  ```php
  define('DB_NAME', 'blog_db');
  define('DB_USER', 'blog_user');
  define('DB_PASSWORD', 'MotDePasseBlog');
  define('DB_HOST', 'localhost');
  define('DB_CHARSET', 'utf8mb4');
  define('DB_COLLATE', '');
  ```

  **Générer et insérer les clés de sécurité comme précédemment.**

- **Pour shop.mywebsite.com :**

  ```bash
  sudo nano /var/www/shop.mywebsite.com/wp-config.php
  ```

  **Modifications à apporter :**

  ```php
  define('DB_NAME', 'shop_db');
  define('DB_USER', 'shop_user');
  define('DB_PASSWORD', 'MotDePasseShop');
  define('DB_HOST', 'localhost');
  define('DB_CHARSET', 'utf8mb4');
  define('DB_COLLATE', '');
  ```

  **Générer et insérer les clés de sécurité comme précédemment.**

- **Pour forum.mywebsite.com :**

  ```bash
  sudo nano /var/www/forum.mywebsite.com/wp-config.php
  ```

  **Modifications à apporter :**

  ```php
  define('DB_NAME', 'forum_db');
  define('DB_USER', 'forum_user');
  define('DB_PASSWORD', 'MotDePasseForum');
  define('DB_HOST', 'localhost');
  define('DB_CHARSET', 'utf8mb4');
  define('DB_COLLATE', '');
  ```

  **Générer et insérer les clés de sécurité comme précédemment.**

---

#### **Étape 12 : Finaliser l'installation de WordPress via le navigateur**

**12.1.** **Accéder à chaque site dans le navigateur :**

- **mywebsite.com** : [https://mywebsite.com](https://mywebsite.com)
- **blog.mywebsite.com** : [https://blog.mywebsite.com](https://blog.mywebsite.com)
- **shop.mywebsite.com** : [https://shop.mywebsite.com](https://shop.mywebsite.com)
- **forum.mywebsite.com** : [https://forum.mywebsite.com](https://forum.mywebsite.com)

**12.2.** **Suivre les étapes de l'installation WordPress pour chaque site :**

Pour chaque site :

- **Choisir la langue** : Sélectionnez **Français** et cliquez sur **Continuer**.
- **Informations nécessaires** : Comme nous avons déjà configuré le fichier `wp-config.php`, cette étape est sautée.
- **Informations sur le site** :

  - **Titre du site** : Entrez le nom approprié (par exemple, **Mon Site Web**, **Blog de Mon Site**, **Boutique de Mon Site**, **Forum de Mon Site**).
  - **Nom d'utilisateur** : Choisissez un nom d'utilisateur pour l'administrateur (par exemple, **admin**).
  - **Mot de passe** : Choisissez un mot de passe sécurisé.
  - **Adresse e-mail** : Entrez votre adresse e-mail.
  - **Visibilité pour les moteurs de recherche** : Décochez si vous ne souhaitez pas que le site soit indexé pour le moment.
  - Cliquez sur **Installer WordPress**.

- **Installation réussie** : Cliquez sur **Se connecter** pour accéder au tableau de bord.

---

#### **Étape 13 : Désactiver un site (Optionnel)**

Supposons que vous souhaitiez désactiver le sous-domaine **forum.mywebsite.com** après l'avoir installé.

**13.1.** **Supprimer le lien symbolique du site :**

```bash
sudo rm /etc/nginx/sites-enabled/forum.mywebsite.com
```

**13.2.** **Redémarrer Nginx :**

```bash
sudo systemctl restart nginx
```

Le site **forum.mywebsite.com** ne sera plus accessible. Pour le réactiver, recréez le lien symbolique :

```bash
sudo ln -s /etc/nginx/sites-available/forum.mywebsite.com /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

---

#### **Étape 14 : Conseils supplémentaires**

**14.1.** **Sécurité :**

- **Mettre à jour régulièrement :** Exécutez régulièrement `sudo apt update && sudo apt upgrade` pour garder le système à jour.
- **Mots de passe forts :** Utilisez des mots de passe complexes pour les utilisateurs de base de données et les comptes administrateur WordPress.
- **Plugins de sécurité :** Installez des plugins comme **Wordfence** pour renforcer la sécurité de vos sites.
- **Sauvegardes :** Configurez des sauvegardes régulières de vos bases de données et fichiers (plugins comme **UpdraftPlus**).
- **Limiter l'accès SSH :** Si possible, désactivez l'accès SSH pour l'utilisateur root et utilisez des clés SSH.

**14.2.** **Optimisation :**

- **Caching :** Utilisez des plugins de mise en cache comme **WP Super Cache** pour améliorer les performances.
- **Optimisation des images :** Utilisez des plugins comme **Smush** pour optimiser les images.
- **CDN :** Envisagez d'utiliser un CDN (Content Delivery Network) pour accélérer la distribution de contenu.

**14.3.** **Surveillance :**

- **Logs :** Consultez régulièrement les logs Nginx et PHP pour détecter les problèmes.
- **Monitoring :** Utilisez des outils de surveillance pour suivre les performances du serveur.

---

#### **Étape 15 : Nettoyage (Optionnel)**

Si vous avez téléchargé des fichiers temporaires ou installé des paquets inutiles, vous pouvez nettoyer le système.

**15.1.** **Supprimer les fichiers temporaires :**

```bash
sudo rm -rf /tmp/wordpress
sudo rm /tmp/latest-fr_FR.tar.gz
```

**15.2.** **Supprimer les paquets inutilisés :**

```bash
sudo apt autoremove -y
```

---

#### **Conclusion**

Vous avez maintenant un serveur configuré pour héberger plusieurs sites WordPress avec un domaine principal et trois sous-domaines, chacun dans son propre répertoire. Ce guide détaillé vous a permis de suivre chaque étape sans rien oublier, en appliquant les meilleures pratiques.

N'hésitez pas à personnaliser davantage vos sites, à installer des thèmes et des plugins, et à continuer d'apprendre pour améliorer vos compétences en administration de serveurs et en gestion de sites web.

Si vous rencontrez des problèmes, revérifiez chaque étape et assurez-vous d'avoir bien suivi toutes les instructions. En cas de doute, consultez les logs Nginx et PHP pour identifier les erreurs.

Bon courage et bonne continuation dans votre apprentissage !
