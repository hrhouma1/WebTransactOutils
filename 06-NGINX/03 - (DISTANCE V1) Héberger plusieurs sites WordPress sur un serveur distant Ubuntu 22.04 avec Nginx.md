### Tutoriel complet : Héberger plusieurs sites WordPress sur un serveur distant Ubuntu 22.04 avec Nginx

---

**Objectif :** Apprendre à installer et configurer plusieurs sites WordPress sur un serveur distant (par exemple, une instance Hostinger ou Vultr) exécutant Ubuntu 22.04. Nous utiliserons des noms de domaine imaginaires tels que **worldnews.com**, **soccernews.com**, et **hockeynews.com**. Chaque site aura son propre répertoire et sa propre configuration. Ce guide est destiné aux débutants et détaillera chaque étape sans rien omettre.

---

#### **Pré-requis :**

- Un serveur distant exécutant Ubuntu 22.04 (par exemple, sur Hostinger ou Vultr).
- Accès root ou sudo au serveur.
- Noms de domaine enregistrés (vous pouvez utiliser des domaines réels ou configurer des domaines de test via un fichier hosts local ou un service DNS).
- Un client SSH pour se connecter au serveur (par exemple, PuTTY ou Terminal).

---

#### **Étape 1 : Connexion au serveur**

1. **Obtenir les informations de connexion :**

   Après avoir créé votre instance Ubuntu 22.04 sur Hostinger ou Vultr, vous recevrez une adresse IP, un nom d'utilisateur (généralement `root`), et un mot de passe ou une clé SSH.

2. **Se connecter au serveur via SSH :**

   Sur votre terminal, exécutez :

   ```bash
   ssh root@IP_DU_SERVEUR
   ```

   Remplacez `IP_DU_SERVEUR` par l'adresse IP de votre serveur.

---

#### **Étape 2 : Mettre à jour le serveur**

1. **Mettre à jour la liste des paquets :**

   ```bash
   sudo apt update
   ```

2. **Mettre à niveau les paquets installés :**

   ```bash
   sudo apt upgrade -y
   ```

---

#### **Étape 3 : Installer le serveur web Nginx**

1. **Installer Nginx :**

   ```bash
   sudo apt install nginx -y
   ```

2. **Vérifier que Nginx est en cours d'exécution :**

   ```bash
   sudo systemctl status nginx
   ```

   Vous devriez voir qu'il est **active (running)**.

---

#### **Étape 4 : Installer MySQL pour la gestion des bases de données**

1. **Installer MySQL :**

   ```bash
   sudo apt install mysql-server -y
   ```

2. **Sécuriser l'installation de MySQL :**

   ```bash
   sudo mysql_secure_installation
   ```

   **Pendant le script :**

   - **Configurer le VALIDATE PASSWORD plugin ?** Tapez **N** pour non (pour simplifier en environnement de test).
   - **Définir un mot de passe root ?** Tapez **Y** puis entrez un mot de passe sécurisé.
   - **Supprimer les utilisateurs anonymes ?** Tapez **Y**.
   - **Interdire la connexion root à distance ?** Tapez **Y**.
   - **Supprimer la base de données de test ?** Tapez **Y**.
   - **Recharger les tables de privilèges ?** Tapez **Y**.

3. **Se connecter à MySQL en tant que root :**

   ```bash
   sudo mysql -u root -p
   ```

   Entrez le mot de passe root que vous venez de définir.

---

#### **Étape 5 : Créer des bases de données pour chaque site**

**Pour chaque site, nous allons créer une base de données, un utilisateur et accorder les privilèges nécessaires.**

**5.1. Site worldnews.com**

```sql
CREATE DATABASE worldnews_db;
CREATE USER 'worldnews_user'@'localhost' IDENTIFIED BY 'password_worldnews';
GRANT ALL PRIVILEGES ON worldnews_db.* TO 'worldnews_user'@'localhost';
FLUSH PRIVILEGES;
```

**5.2. Site soccernews.com**

```sql
CREATE DATABASE soccernews_db;
CREATE USER 'soccernews_user'@'localhost' IDENTIFIED BY 'password_soccernews';
GRANT ALL PRIVILEGES ON soccernews_db.* TO 'soccernews_user'@'localhost';
FLUSH PRIVILEGES;
```

**5.3. Site hockeynews.com**

```sql
CREATE DATABASE hockeynews_db;
CREATE USER 'hockeynews_user'@'localhost' IDENTIFIED BY 'password_hockeynews';
GRANT ALL PRIVILEGES ON hockeynews_db.* TO 'hockeynews_user'@'localhost';
FLUSH PRIVILEGES;
```

**5.4. Quitter MySQL :**

```sql
EXIT;
```

---

#### **Étape 6 : Installer PHP et les extensions nécessaires**

1. **Installer PHP et les extensions :**

   ```bash
   sudo apt install php-fpm php-mysql php-curl php-gd php-xml php-mbstring -y
   ```

2. **Vérifier la version de PHP installée :**

   ```bash
   php -v
   ```

   Vous devriez voir quelque chose comme **PHP 8.1.x**.

---

#### **Étape 7 : Télécharger et configurer WordPress pour chaque site**

**7.1. Créer un répertoire pour télécharger WordPress :**

```bash
cd /tmp
wget https://fr.wordpress.org/latest-fr_FR.tar.gz
tar -xzf latest-fr_FR.tar.gz
```

**7.2. Créer les répertoires pour chaque site dans `/var/www` :**

```bash
sudo mkdir -p /var/www/worldnews.com
sudo mkdir -p /var/www/soccernews.com
sudo mkdir -p /var/www/hockeynews.com
```

**7.3. Copier les fichiers WordPress dans chaque répertoire :**

- **Pour worldnews.com :**

  ```bash
  sudo cp -r wordpress/* /var/www/worldnews.com/
  ```

- **Pour soccernews.com :**

  ```bash
  sudo cp -r wordpress/* /var/www/soccernews.com/
  ```

- **Pour hockeynews.com :**

  ```bash
  sudo cp -r wordpress/* /var/www/hockeynews.com/
  ```

**7.4. Définir les permissions appropriées :**

```bash
sudo chown -R www-data:www-data /var/www/worldnews.com
sudo chown -R www-data:www-data /var/www/soccernews.com
sudo chown -R www-data:www-data /var/www/hockeynews.com

sudo find /var/www/ -type d -exec chmod 755 {} \;
sudo find /var/www/ -type f -exec chmod 644 {} \;
```

---

#### **Étape 8 : Configurer Nginx pour chaque site**

**8.1. Créer un fichier de configuration pour worldnews.com**

```bash
sudo nano /etc/nginx/sites-available/worldnews.com
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name worldnews.com www.worldnews.com;
    root /var/www/worldnews.com;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**8.2. Créer un fichier de configuration pour soccernews.com**

```bash
sudo nano /etc/nginx/sites-available/soccernews.com
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name soccernews.com www.soccernews.com;
    root /var/www/soccernews.com;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**8.3. Créer un fichier de configuration pour hockeynews.com**

```bash
sudo nano /etc/nginx/sites-available/hockeynews.com
```

**Contenu du fichier :**

```nginx
server {
    listen 80;
    server_name hockeynews.com www.hockeynews.com;
    root /var/www/hockeynews.com;

    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass unix:/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

**8.4. Activer les sites en créant des liens symboliques :**

```bash
sudo ln -s /etc/nginx/sites-available/worldnews.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/soccernews.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/hockeynews.com /etc/nginx/sites-enabled/
```

**8.5. Vérifier la configuration de Nginx et redémarrer le service :**

```bash
sudo nginx -t
sudo systemctl restart nginx
```

---

#### **Étape 9 : Configurer les enregistrements DNS pour chaque domaine**

**Note importante :** Pour que les domaines pointent vers votre serveur, vous devez configurer les enregistrements DNS chez votre registraire de domaine.

**9.1. Ajouter un enregistrement A pour chaque domaine :**

- **worldnews.com**

  - Type : A
  - Nom : @
  - Valeur : IP_DU_SERVEUR

  - Type : A
  - Nom : www
  - Valeur : IP_DU_SERVEUR

- **soccernews.com**

  - Type : A
  - Nom : @
  - Valeur : IP_DU_SERVEUR

  - Type : A
  - Nom : www
  - Valeur : IP_DU_SERVEUR

- **hockeynews.com**

  - Type : A
  - Nom : @
  - Valeur : IP_DU_SERVEUR

  - Type : A
  - Nom : www
  - Valeur : IP_DU_SERVEUR

**9.2. Attendre la propagation DNS :**

La propagation des enregistrements DNS peut prendre de quelques minutes à 24 heures. Vous pouvez vérifier la propagation en utilisant des outils comme [WhatsMyDNS](https://www.whatsmydns.net/).

---

#### **Étape 10 : Installer Certbot pour les certificats SSL (Optionnel mais recommandé)**

**10.1. Installer Certbot et le plugin Nginx :**

```bash
sudo apt install certbot python3-certbot-nginx -y
```

**10.2. Obtenir des certificats SSL pour chaque domaine :**

- **Pour worldnews.com :**

  ```bash
  sudo certbot --nginx -d worldnews.com -d www.worldnews.com
  ```

- **Pour soccernews.com :**

  ```bash
  sudo certbot --nginx -d soccernews.com -d www.soccernews.com
  ```

- **Pour hockeynews.com :**

  ```bash
  sudo certbot --nginx -d hockeynews.com -d www.hockeynews.com
  ```

**10.3. Configurer le renouvellement automatique :**

Certbot ajoute automatiquement une tâche cron pour renouveler les certificats. Vous pouvez tester le renouvellement avec :

```bash
sudo certbot renew --dry-run
```

---

#### **Étape 11 : Configurer WordPress pour chaque site**

**11.1. Créer le fichier `wp-config.php` pour chaque site**

- **Pour worldnews.com :**

  ```bash
  sudo cp /var/www/worldnews.com/wp-config-sample.php /var/www/worldnews.com/wp-config.php
  ```

- **Pour soccernews.com :**

  ```bash
  sudo cp /var/www/soccernews.com/wp-config-sample.php /var/www/soccernews.com/wp-config.php
  ```

- **Pour hockeynews.com :**

  ```bash
  sudo cp /var/www/hockeynews.com/wp-config-sample.php /var/www/hockeynews.com/wp-config.php
  ```

**11.2. Modifier le fichier `wp-config.php` pour chaque site**

- **Pour worldnews.com :**

  ```bash
  sudo nano /var/www/worldnews.com/wp-config.php
  ```

  **Modifications à apporter :**

  ```php
  define('DB_NAME', 'worldnews_db');
  define('DB_USER', 'worldnews_user');
  define('DB_PASSWORD', 'password_worldnews');
  define('DB_HOST', 'localhost');
  ```

  **Générer des clés de sécurité :**

  Rendez-vous sur [https://api.wordpress.org/secret-key/1.1/salt/](https://api.wordpress.org/secret-key/1.1/salt/) et copiez les clés générées. Remplacez les lignes correspondantes dans `wp-config.php`.

- **Pour soccernews.com :**

  ```bash
  sudo nano /var/www/soccernews.com/wp-config.php
  ```

  **Modifications à apporter :**

  ```php
  define('DB_NAME', 'soccernews_db');
  define('DB_USER', 'soccernews_user');
  define('DB_PASSWORD', 'password_soccernews');
  define('DB_HOST', 'localhost');
  ```

  **Générer et insérer les clés de sécurité comme précédemment.**

- **Pour hockeynews.com :**

  ```bash
  sudo nano /var/www/hockeynews.com/wp-config.php
  ```

  **Modifications à apporter :**

  ```php
  define('DB_NAME', 'hockeynews_db');
  define('DB_USER', 'hockeynews_user');
  define('DB_PASSWORD', 'password_hockeynews');
  define('DB_HOST', 'localhost');
  ```

  **Générer et insérer les clés de sécurité comme précédemment.**

---

#### **Étape 12 : Finaliser l'installation de WordPress via le navigateur**

**12.1. Accéder à chaque site dans le navigateur :**

- **worldnews.com** : [https://worldnews.com](https://worldnews.com)
- **soccernews.com** : [https://soccernews.com](https://soccernews.com)
- **hockeynews.com** : [https://hockeynews.com](https://hockeynews.com)

**12.2. Suivre les étapes de l'installation WordPress :**

Pour chaque site :

- **Choisir la langue** : Sélectionnez **Français** et cliquez sur **Continuer**.
- **Bienvenue** : Cliquez sur **C'est parti !**
- **Informations de base de données** : Cette étape est déjà configurée, vous pouvez passer.
- **Informations sur le site** :

  - **Titre du site** : Entrez le nom approprié (par exemple, **World News**, **Soccer News**, **Hockey News**).
  - **Nom d'utilisateur** : Choisissez un nom d'utilisateur pour l'administrateur.
  - **Mot de passe** : Choisissez un mot de passe sécurisé.
  - **Adresse e-mail** : Entrez votre adresse e-mail.
  - **Visibilité pour les moteurs de recherche** : Décochez si vous ne souhaitez pas que le site soit indexé pour le moment.
  - Cliquez sur **Installer WordPress**.

- **Installation réussie** : Cliquez sur **Se connecter** pour accéder au tableau de bord.

---

#### **Étape 13 : Désactiver un site (Optionnel)**

Supposons que vous souhaitiez désactiver le site **hockeynews.com** après l'avoir installé.

**13.1. Supprimer le lien symbolique du site :**

```bash
sudo rm /etc/nginx/sites-enabled/hockeynews.com
```

**13.2. Redémarrer Nginx :**

```bash
sudo systemctl restart nginx
```

Le site **hockeynews.com** ne sera plus accessible. Pour le réactiver, recréez le lien symbolique :

```bash
sudo ln -s /etc/nginx/sites-available/hockeynews.com /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

---

#### **Étape 14 : Conseils supplémentaires**

- **Sécurité :**

  - Gardez votre serveur à jour en exécutant régulièrement `sudo apt update && sudo apt upgrade`.
  - Utilisez des mots de passe forts pour les bases de données et les comptes administrateurs WordPress.
  - Installez des plugins de sécurité tels que Wordfence pour protéger vos sites.

- **Sauvegardes :**

  - Configurez des sauvegardes régulières de vos bases de données et fichiers WordPress.
  - Vous pouvez utiliser des plugins comme **UpdraftPlus** pour automatiser les sauvegardes.

- **Optimisation :**

  - Utilisez des plugins de mise en cache comme **WP Super Cache** pour améliorer les performances.
  - Optimisez les images avec des plugins comme **Smush**.

- **Certificats SSL :**

  - Les certificats Let's Encrypt expirent tous les 90 jours. Assurez-vous que le renouvellement automatique est configuré.
  - Vérifiez régulièrement que vos sites sont accessibles via HTTPS.

---

#### **Conclusion**

Félicitations ! Vous avez appris à configurer plusieurs sites WordPress sur un serveur distant Ubuntu 22.04 avec Nginx. Chaque site fonctionne indépendamment avec son propre domaine, sa base de données et ses fichiers. Ce type de configuration est idéal pour héberger plusieurs sites sur un seul serveur tout en les maintenant isolés les uns des autres.

N'hésitez pas à personnaliser davantage vos sites, à installer des thèmes et des plugins, et à explorer les nombreuses possibilités offertes par WordPress.

Si vous avez des questions ou rencontrez des difficultés, n'hésitez pas à demander de l'aide.

Bon courage et bonne continuation dans votre apprentissage !
