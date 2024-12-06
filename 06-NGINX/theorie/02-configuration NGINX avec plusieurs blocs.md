# **Exemple complet de configuration NGINX**

```nginx
# Bloc principal : HTTP settings globaux
http {
    # Redirection HTTP vers HTTPS
    server {
        listen 80;
        server_name example.com www.example.com;

        return 301 https://$host$request_uri;
    }

    # Bloc HTTPS principal
    server {
        listen 443 ssl;
        server_name example.com www.example.com;

        # Certificats SSL
        ssl_certificate /etc/nginx/ssl/example.com.crt;
        ssl_certificate_key /etc/nginx/ssl/example.com.key;

        # Emplacement racine
        root /var/www/example;
        index index.html index.htm;

        # Page d'erreur personnalisée pour 404
        error_page 404 /404.html;
        location = /404.html {
            root /var/www/errors;
        }

        # Bloc pour le contenu statique
        location /static/ {
            root /var/www/static;
            try_files $uri $uri/ =404;
        }

        # Bloc pour les images
        location ~* \.(png|jpg|jpeg|gif|svg)$ {
            root /var/www/images;
            expires 30d;
            access_log off;
        }

        # API backend (proxy vers une application Node.js)
        location /api/ {
            proxy_pass http://127.0.0.1:3000;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        # Réécriture d'URI
        location /old-path/ {
            rewrite ^/old-path/(.*)$ /new-path/$1 permanent;
        }

        # Page par défaut
        location / {
            try_files $uri $uri/ /index.html;
        }
    }

    # Serveur pour un sous-domaine (blog.example.com)
    server {
        listen 80;
        server_name blog.example.com;

        root /var/www/blog;
        index index.html index.php;

        # Redirection des requêtes PHP vers PHP-FPM
        location ~ \.php$ {
            include fastcgi_params;
            fastcgi_pass unix:/run/php/php7.4-fpm.sock;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        }

        # Page d'erreur personnalisée pour 500
        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
            root /var/www/errors;
        }
    }
}
```

---

### **Explications :**
1. **Redirection HTTP vers HTTPS :**
   - Le premier bloc `server` écoute sur le port 80 (HTTP) et redirige toutes les requêtes vers HTTPS.

2. **Bloc HTTPS principal :**
   - Utilise des certificats SSL pour sécuriser les connexions.
   - Définit les pages statiques et une page d'erreur personnalisée pour les 404.
   - Met en cache les fichiers d'images pendant 30 jours pour améliorer les performances.
   - Inclut un bloc pour servir un backend API via proxy.

3. **Réécritures d'URI :**
   - Redirige `/old-path/...` vers `/new-path/...` avec une redirection permanente.

4. **Sous-domaine blog :**
   - Configure un sous-domaine pour un site différent (`blog.example.com`).
   - Ajoute la prise en charge de PHP avec PHP-FPM.
   - Définit une page d'erreur personnalisée pour les erreurs 500.

---

### **Exercice pratique :**
1. **Testez la configuration :**
   - Configurez les chemins locaux (`/var/www/...`) avec des fichiers HTML ou PHP.
   - Ajoutez des certificats auto-signés pour le HTTPS.

2. **Utilisez des outils :**
   - Testez vos redirections et fonctionnalités avec des outils comme `curl` ou un navigateur.

3. **Analysez les journaux :**
   - Consultez les journaux d’accès et d’erreurs dans `/var/log/nginx/` pour voir le comportement des requêtes.
