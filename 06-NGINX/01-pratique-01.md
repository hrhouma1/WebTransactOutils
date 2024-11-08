# Pratique-01

### 🌐 Étape 1 : Créer et configurer la VM Azure

1. **Connectez-vous à Azure** et accédez au **Portail Azure**.

2. **Créer une nouvelle VM** :
   - Allez dans **Créer une ressource** > **Machine virtuelle**.
   - Remplissez les informations :
     - **Nom de la VM** : choisissez un nom (ex. `wordpress-vm`).
     - **Région** : choisissez une région proche de vous.
     - **Image** : sélectionnez **Ubuntu Server 22.04 LTS**.
     - **Taille** : sélectionnez une taille appropriée (ex. Standard B1s).
     - **Authentification** : choisissez `SSH` pour la connexion (générez une clé SSH si nécessaire).

3. **Configurer les paramètres réseau** :
   - Assurez-vous que **Port HTTP (80)** et **Port HTTPS (443)** sont ouverts dans le groupe de sécurité réseau pour le trafic Web.

4. **Créer la VM** et notez l’**adresse IP publique** fournie après sa création.

5. **Se connecter à la VM** :
   - Utilisez SSH pour accéder à la VM depuis votre terminal local :

     ```bash
     ssh azureuser@<adresse_ip_publique>
     ```

---

### 2️⃣ Mettre à jour le système

Une fois connecté à la VM, mettez à jour le système avec les commandes suivantes :

```bash
sudo apt update -y
```

---

### 3️⃣ Installer les composants nécessaires

Installez Nginx, PostgreSQL, et les modules PHP pour WordPress :

```bash
sudo apt install -y nginx postgresql postgresql-contrib php8.1-fpm php8.1-pgsql php8.1-xml php8.1-mbstring php8.1-curl unzip
```

---

### 4️⃣ Configurer PostgreSQL pour WordPress

1. **Configurer PostgreSQL** :
   - Connectez-vous en tant qu’utilisateur PostgreSQL :

     ```bash
     sudo -u postgres psql
     ```

2. **Créer une base de données et un utilisateur** pour WordPress :

   ```sql
   CREATE USER wpuser WITH PASSWORD 'yourpassword';
   CREATE DATABASE wordpress_db OWNER wpuser;
   \q
   ```

   > Remplacez `yourpassword` par un mot de passe sécurisé.

---

### 5️⃣ Télécharger et configurer WordPress

1. **Télécharger WordPress** :

   ```bash
   cd /tmp
   wget https://wordpress.org/latest.zip
   unzip latest.zip
   sudo mv wordpress /var/www/wordpress
   ```

2. **Configurer les permissions** pour le dossier WordPress :

   ```bash
   sudo chown -R www-data:www-data /var/www/wordpress
   sudo chmod -R 755 /var/www/wordpress
   ```

3. **Installer le plugin PostgreSQL pour WordPress** :

   WordPress n’a pas de support PostgreSQL natif, donc un plugin est requis.

   ```bash
   wget https://github.com/kevinoid/postgresql-for-wordpress/archive/refs/heads/main.zip -O wp-pgsql.zip
   unzip wp-pgsql.zip
   sudo mv postgresql-for-wordpress-main /var/www/wordpress/wp-content/plugins/postgresql-for-wordpress
   ```

4. **Configurer `wp-config.php`** :

   Créez un fichier `wp-config.php` à partir du fichier exemple :

   ```bash
   sudo cp /var/www/wordpress/wp-config-sample.php /var/www/wordpress/wp-config.php
   sudo nano /var/www/wordpress/wp-config.php
   ```

   Modifiez les lignes suivantes :

   ```php
   define('DB_NAME', 'wordpress_db');
   define('DB_USER', 'wpuser');
   define('DB_PASSWORD', 'yourpassword');
   define('DB_HOST', 'localhost');
   define('DB_CHARSET', 'utf8');
   define('DB_COLLATE', '');

   // Pour PostgreSQL
   define('DB_DRIVER', 'pgsql');
   ```

   **Ajoutez les clés de sécurité WordPress** en générant les valeurs [ici](https://api.wordpress.org/secret-key/1.1/salt/).

---

### 6️⃣ Configurer Nginx pour WordPress

1. **Créer un fichier de configuration Nginx pour WordPress** :

   ```bash
   sudo nano /etc/nginx/sites-available/wordpress
   ```

2. **Ajouter la configuration suivante** :

   ```nginx
   server {
       listen 80;
       server_name your_domain.com;

       root /var/www/wordpress;
       index index.php index.html index.htm;

       location / {
           try_files $uri $uri/ /index.php?$args;
       }

       location ~ \.php$ {
           include snippets/fastcgi-php.conf;
           fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
           fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
           include fastcgi_params;
       }

       location ~ /\.ht {
           deny all;
       }
   }
   ```

   > Remplacez `your_domain.com` par l'adresse IP de votre VM Azure ou votre nom de domaine.

3. **Activer la configuration** et redémarrer Nginx :

   ```bash
   sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/
   sudo nginx -t
   sudo systemctl restart nginx
   ```

---

### 7️⃣ Configurer HTTPS (facultatif) avec Let's Encrypt

Si vous avez un nom de domaine, configurez HTTPS avec Let's Encrypt pour sécuriser votre site.

1. **Installer Certbot** :

   ```bash
   sudo apt install certbot python3-certbot-nginx -y
   ```

2. **Générer un certificat SSL** :

   ```bash
   sudo certbot --nginx -d your_domain.com
   ```

3. **Configurer le renouvellement automatique du certificat** :

   ```bash
   sudo systemctl enable certbot.timer
   ```

---

### 8️⃣ Finaliser l’installation de WordPress

1. **Accédez à votre site WordPress** en ouvrant `http://<adresse_ip_publique>` ou `http://your_domain.com` dans un navigateur.

2. **Suivez les instructions d’installation de WordPress** :
   - Sélectionnez la langue.
   - Configurez le titre de votre site, nom d’utilisateur admin, mot de passe, et email.

---

### 🔒 Sécuriser la VM

1. **Configurer le pare-feu** :

   ```bash
   sudo ufw allow 'Nginx Full'
   sudo ufw enable
   ```

2. **Restreindre les accès SSH** (optionnel) pour plus de sécurité :
   - **Modifier le port SSH** dans `/etc/ssh/sshd_config` si besoin.
   - **Désactiver l'accès root SSH** pour renforcer la sécurité.

---

### 🎉 Votre site WordPress est prêt
