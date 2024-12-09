
# 05-comment-diagnostiquer-un-probleme ?

- Comment diagnostiquer et corriger un problème par exemple un problème d'accès au site principal **http://elastic.local** ?


---

### **Étape 1 : Vérification de la configuration Nginx**

1. **Tester la syntaxe des fichiers de configuration Nginx** :

   ```bash
   sudo nginx -t
   ```

   Si vous voyez une erreur, vérifiez le fichier `/etc/nginx/sites-available/elastic.local` pour d'éventuelles fautes de syntaxe.

   - Commande pour ouvrir et éditer :
     ```bash
     sudo nano /etc/nginx/sites-available/elastic.local
     ```

   - Une fois corrigé, redémarrez Nginx :
     ```bash
     sudo systemctl restart nginx
     ```

---

### **Étape 2 : Vérification des permissions des répertoires**

1. **Vérifier si Nginx a accès au répertoire du site** :

   ```bash
   ls -ld /var/www/elastic.local
   ```

   La sortie devrait montrer que le propriétaire est `www-data` et que les permissions sont correctes (755 pour les dossiers, 644 pour les fichiers).

   Si ce n'est pas le cas, exécutez les commandes suivantes pour corriger les permissions :

   ```bash
   sudo chown -R www-data:www-data /var/www/elastic.local
   sudo find /var/www/elastic.local -type d -exec chmod 755 {} \;
   sudo find /var/www/elastic.local -type f -exec chmod 644 {} \;
   ```

---

### **Étape 3 : Vérification du fichier hosts**

1. **Assurez-vous que le domaine `elastic.local` est correctement mappé** :

   Ouvrez le fichier `/etc/hosts` pour vérifier :

   ```bash
   sudo nano /etc/hosts
   ```

   La ligne suivante doit être présente :

   ```plaintext
   127.0.0.1   elastic.local
   ```

   Si elle manque, ajoutez-la, puis sauvegardez et quittez.

---

### **Étape 4 : Vérification des erreurs de Nginx**

1. **Consultez le fichier des journaux d'erreurs de Nginx** :

   ```bash
   sudo tail -f /var/log/nginx/error.log
   ```

   - Vérifiez si une erreur spécifique est signalée, par exemple des permissions ou des problèmes de fichier `index.php`.

2. **Consultez également le journal d'accès Nginx** :

   ```bash
   sudo tail -f /var/log/nginx/access.log
   ```

   Cela permet de vérifier si les requêtes HTTP atteignent le serveur.

---

### **Étape 5 : Vérification de PHP**

1. **Assurez-vous que PHP-FPM fonctionne correctement** :

   Vérifiez l'état de PHP-FPM :

   ```bash
   sudo systemctl status php8.1-fpm
   ```

   Si le service est arrêté, redémarrez-le :

   ```bash
   sudo systemctl restart php8.1-fpm
   ```

2. **Tester l'exécution de PHP** :

   Créez un fichier de test PHP dans le répertoire `/var/www/elastic.local` :

   ```bash
   echo "<?php phpinfo(); ?>" | sudo tee /var/www/elastic.local/info.php
   ```

   Ensuite, accédez à **http://elastic.local/info.php** dans votre navigateur pour vérifier si PHP fonctionne.

   Une fois confirmé, supprimez le fichier pour des raisons de sécurité :

   ```bash
   sudo rm /var/www/elastic.local/info.php
   ```

---

### **Étape 6 : Vérification de la configuration WordPress**

1. **Vérifiez le fichier `wp-config.php`** :

   ```bash
   sudo nano /var/www/elastic.local/wp-config.php
   ```

   - Confirmez que les informations de connexion à la base de données sont correctes :

     ```php
     define('DB_NAME', 'elastic_local_db');
     define('DB_USER', 'elastic_user');
     define('DB_PASSWORD', 'mot_de_passe_elastic');
     define('DB_HOST', 'localhost');
     ```

   - Assurez-vous que les clés de sécurité sont définies.

2. **Tester la connexion à la base de données** :

   Utilisez la commande suivante pour tester la connexion MySQL :

   ```bash
   mysql -u elastic_user -p -D elastic_local_db
   ```

   Entrez le mot de passe `mot_de_passe_elastic` lorsque demandé.

   Si la connexion échoue, vérifiez les privilèges et les utilisateurs dans MySQL :

   ```sql
   SHOW GRANTS FOR 'elastic_user'@'localhost';
   ```

   Si nécessaire, corrigez-les :

   ```sql
   GRANT ALL PRIVILEGES ON elastic_local_db.* TO 'elastic_user'@'localhost';
   FLUSH PRIVILEGES;
   ```

---

### **Étape 7 : Redémarrer les services**

Parfois, redémarrer tous les services liés résout le problème :

```bash
sudo systemctl restart nginx
sudo systemctl restart php8.1-fpm
sudo systemctl restart mysql
```

---

### **Étape 8 : Debugging avancé**

1. **Activer les logs de débogage pour WordPress** :

   Ajoutez les lignes suivantes à `wp-config.php` :

   ```php
   define('WP_DEBUG', true);
   define('WP_DEBUG_LOG', true);
   define('WP_DEBUG_DISPLAY', false);
   ```

   Ensuite, consultez le fichier de log WordPress pour les erreurs :

   ```bash
   sudo tail -f /var/www/elastic.local/wp-content/debug.log
   ```

2. **Utiliser `curl` pour tester la réponse de Nginx** :

   ```bash
   curl -I http://elastic.local
   ```

   Cela vous montrera les en-têtes HTTP renvoyés par Nginx.

---

### Résolution fréquente des problèmes

- **Erreur 403 (Forbidden)** :
  - Vérifiez les permissions sur `/var/www/elastic.local`.
  - Assurez-vous qu'il existe un fichier `index.php` ou `index.html`.

- **Erreur 404 (Not Found)** :
  - Vérifiez que la directive `try_files $uri $uri/ /index.php?$args;` est présente dans le fichier de configuration Nginx.

- **Erreur 500 (Internal Server Error)** :
  - Vérifiez les logs Nginx et WordPress pour des erreurs PHP ou de configuration.
