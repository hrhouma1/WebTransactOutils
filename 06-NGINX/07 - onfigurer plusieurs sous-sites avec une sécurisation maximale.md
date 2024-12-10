
## Configuration DNS

### Étape 1 : Configuration des domaines
Pour chaque domaine, ajoutez dans votre panel DNS :
```
Type    Nom    Valeur         TTL
A       @      [Votre_IP]     3600
A       www    [Votre_IP]     3600
```

## Structure des dossiers

### Étape 1 : Création des répertoires
```bash
# Création des dossiers pour chaque site
sudo mkdir -p /var/www/soccer.com/public_html
sudo mkdir -p /var/www/football.ca/public_html
sudo mkdir -p /var/www/spaghetti.fr/public_html

# Attribution des permissions
sudo chown -R $USER:$USER /var/www/soccer.com
sudo chown -R $USER:$USER /var/www/football.ca
sudo chown -R $USER:$USER /var/www/spaghetti.fr

# Permissions sécurisées
sudo chmod -R 755 /var/www
```

## Configuration Nginx

### Étape 1 : Configuration de soccer.com
```bash
sudo nano /etc/nginx/sites-available/soccer.com
```

```nginx
server {
    listen 80;
    listen [::]:80;
    server_name soccer.com www.soccer.com;
    root /var/www/soccer.com/public_html;

    # Logs personnalisés
    access_log /var/log/nginx/soccer.com.access.log;
    error_log /var/log/nginx/soccer.com.error.log;

    # Configuration de base
    index index.html index.htm;

    # Protection contre les attaques
    location ~ /\. {
        deny all;
    }

    # Configuration principale
    location / {
        try_files $uri $uri/ =404;
        add_header X-Frame-Options "SAMEORIGIN";
        add_header X-XSS-Protection "1; mode=block";
        add_header X-Content-Type-Options "nosniff";
        add_header Referrer-Policy "strict-origin-when-cross-origin";
        add_header Content-Security-Policy "default-src 'self' http: https: data: blob: 'unsafe-inline'";
    }

    # Configuration des fichiers statiques
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
    }
}
```

### Étape 2 : Configuration de football.ca et spaghetti.fr
```bash
# Répétez la même configuration pour chaque domaine en adaptant les noms
sudo nano /etc/nginx/sites-available/football.ca
sudo nano /etc/nginx/sites-available/spaghetti.fr
```

### Étape 3 : Activation des sites
```bash
# Création des liens symboliques
sudo ln -s /etc/nginx/sites-available/soccer.com /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/football.ca /etc/nginx/sites-enabled/
sudo ln -s /etc/nginx/sites-available/spaghetti.fr /etc/nginx/sites-enabled/

# Suppression de la configuration par défaut
sudo rm /etc/nginx/sites-enabled/default
```

## Sécurisation SSL

### Étape 1 : Installation des certificats
```bash
# Pour soccer.com
sudo certbot --nginx -d soccer.com -d www.soccer.com

# Pour football.ca
sudo certbot --nginx -d football.ca -d www.football.ca

# Pour spaghetti.fr
sudo certbot --nginx -d spaghetti.fr -d www.spaghetti.fr
```

### Étape 2 : Configuration SSL renforcée
Ajoutez dans chaque fichier de configuration :
```nginx
    # Configuration SSL avancée
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    ssl_ciphers ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
    ssl_stapling on;
    ssl_stapling_verify on;
    resolver 8.8.8.8 8.8.4.4 valid=300s;
    resolver_timeout 5s;
```

## Protection DDoS et Sécurité

### Étape 1 : Configuration anti-DDoS
```bash
sudo nano /etc/nginx/nginx.conf
```

Ajoutez dans le bloc http :
```nginx
    # Protection DDoS
    limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;
    limit_conn_zone $binary_remote_addr zone=addr:10m;

    # Protection supplémentaire
    client_body_buffer_size 1k;
    client_header_buffer_size 1k;
    client_max_body_size 1k;
    large_client_header_buffers 2 1k;
```

### Étape 2 : Configuration du pare-feu
```bash
# Configuration UFW
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh
sudo ufw allow 'Nginx Full'
sudo ufw enable
```

## Surveillance et Maintenance

### Étape 1 : Script de surveillance
```bash
sudo nano /root/monitor-sites.sh
```

```bash
#!/bin/bash
SITES=("soccer.com" "football.ca" "spaghetti.fr")
EMAIL="votre@email.com"

for SITE in "${SITES[@]}"
do
    if ! curl -s --head https://$SITE > /dev/null; then
        echo "Site $SITE est down!" | mail -s "Alerte Site Down" $EMAIL
    fi
done
```

### Étape 2 : Backup automatique
```bash
sudo nano /root/backup-sites.sh
```

```bash
#!/bin/bash
BACKUP_DIR="/root/backups"
DATE=$(date +%Y%m%d)
SITES=("soccer.com" "football.ca" "spaghetti.fr")

for SITE in "${SITES[@]}"
do
    tar -czf $BACKUP_DIR/$SITE-$DATE.tar.gz /var/www/$SITE
    tar -czf $BACKUP_DIR/nginx-conf-$SITE-$DATE.tar.gz /etc/nginx/sites-available/$SITE
done

find $BACKUP_DIR -type f -mtime +7 -delete
```

### Étape 3 : Configuration des tâches cron
```bash
sudo crontab -e
```

Ajoutez :
```
*/5 * * * * /root/monitor-sites.sh
0 3 * * * /root/backup-sites.sh
```

## Vérification finale
```bash
# Test de la configuration
sudo nginx -t

# Redémarrage de Nginx
sudo systemctl restart nginx

# Vérification des sites
curl -I https://soccer.com
curl -I https://football.ca
curl -I https://spaghetti.fr
```

Citations:
[1] https://stackoverflow.com/questions/17568981/nginx-two-subdomain-configuration/62782197
[2] https://www.youtube.com/watch?v=GCznXfbfMq0
[3] https://webdock.io/en/docs/how-guides/shared-hosting-multiple-websites/how-configure-nginx-to-serve-multiple-websites-single-vps
[4] https://hostadvice.com/blog/domains/nginx-subdomain/
