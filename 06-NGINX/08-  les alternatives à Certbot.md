
## Préparation initiale du serveur

### Étape 1 : Sécurisation initiale SSH
```bash
# Modifiez la configuration SSH
sudo nano /etc/ssh/sshd_config
```

Configuration SSH sécurisée :
```
Port 2222                         # Changez le port par défaut
PermitRootLogin no               
PasswordAuthentication no         
PubkeyAuthentication yes         
AllowUsers votre_utilisateur     
MaxAuthTries 3                   
LoginGraceTime 20                
ClientAliveInterval 300          
ClientAliveCountMax 2            
```

### Étape 2 : Configuration du pare-feu avancé
```bash
# Installation de fail2ban
sudo apt install fail2ban -y

# Configuration de fail2ban
sudo nano /etc/fail2ban/jail.local
```

```ini
[DEFAULT]
bantime = 3600
findtime = 600
maxretry = 3

[sshd]
enabled = true
port = 2222
filter = sshd
logpath = /var/log/auth.log
maxretry = 3

[nginx-http-auth]
enabled = true
filter = nginx-http-auth
port = http,https
logpath = /var/log/nginx/*error.log

[nginx-botsearch]
enabled = true
filter = nginx-botsearch
port = http,https
logpath = /var/log/nginx/*access.log
maxretry = 2
```

## Configuration des sites multiples

### Étape 1 : Configuration PHP-FPM (si nécessaire)
```bash
# Installation de PHP-FPM
sudo apt install php8.1-fpm php8.1-mysql php8.1-curl php8.1-gd php8.1-mbstring php8.1-xml -y

# Configuration PHP sécurisée
sudo nano /etc/php/8.1/fpm/php.ini
```

```ini
expose_php = Off
max_execution_time = 30
max_input_time = 30
memory_limit = 128M
post_max_size = 16M
upload_max_filesize = 16M
allow_url_fopen = Off
display_errors = Off
```

### Étape 2 : Configuration Nginx optimisée
```bash
sudo nano /etc/nginx/nginx.conf
```

```nginx
user www-data;
worker_processes auto;
pid /run/nginx.pid;

events {
    worker_connections 1024;
    multi_accept on;
    use epoll;
}

http {
    # Sécurité de base
    server_tokens off;
    more_clear_headers Server;
    more_clear_headers X-Powered-By;

    # Protection DDoS
    limit_req_zone $binary_remote_addr zone=one:10m rate=1r/s;
    limit_conn_zone $binary_remote_addr zone=addr:10m;

    # Buffer et timeouts
    client_body_buffer_size 10K;
    client_header_buffer_size 1k;
    client_max_body_size 8m;
    large_client_header_buffers 2 1k;
    client_body_timeout 12;
    client_header_timeout 12;
    keepalive_timeout 15;
    send_timeout 10;

    # Compression
    gzip on;
    gzip_vary on;
    gzip_min_length 1000;
    gzip_proxied expired no-cache no-store private auth;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
    gzip_disable "MSIE [1-6]\.";
}
```

### Étape 3 : Configuration des sites virtuels
Pour chaque site (exemple avec soccer.com) :
```nginx
server {
    listen 443 ssl http2;
    listen [::]:443 ssl http2;
    server_name soccer.com www.soccer.com;
    root /var/www/soccer.com/public_html;

    # SSL Configuration
    ssl_certificate /etc/letsencrypt/live/soccer.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/soccer.com/privkey.pem;
    ssl_trusted_certificate /etc/letsencrypt/live/soccer.com/chain.pem;
    
    # SSL Optimizations
    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
    ssl_prefer_server_ciphers off;

    # HSTS
    add_header Strict-Transport-Security "max-age=63072000" always;

    # Sécurité supplémentaire
    add_header X-Frame-Options "SAMEORIGIN" always;
    add_header X-XSS-Protection "1; mode=block" always;
    add_header X-Content-Type-Options "nosniff" always;
    add_header Referrer-Policy "no-referrer-when-downgrade" always;
    add_header Content-Security-Policy "default-src 'self' http: https: data: blob: 'unsafe-inline'" always;
    add_header Permissions-Policy "camera=(), microphone=(), geolocation=()";

    # Protection contre les injections
    location ~ [^/]\.php(/|$) {
        fastcgi_split_path_info ^(.+?\.php)(/.*)$;
        if (!-f $document_root$fastcgi_script_name) {
            return 404;
        }
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param HTTP_PROXY "";
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }

    # Protection des fichiers sensibles
    location ~ /\.(?!well-known) {
        deny all;
    }

    # Cache des fichiers statiques
    location ~* \.(jpg|jpeg|gif|png|css|js|ico|xml)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
    }
}
```

## Alternatives à Certbot pour SSL

### 1. acme.sh
```bash
# Installation
curl https://get.acme.sh | sh

# Génération de certificat
acme.sh --issue -d soccer.com -w /var/www/soccer.com/public_html
```

### 2. Caddy Server
```bash
# Installation
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
```

### 3. SSL Commercial
- Sectigo
- DigiCert
- GlobalSign

## Surveillance avancée

### Étape 1 : Installation de outils de monitoring
```bash
# Installation de Netdata
bash <(curl -Ss https://my-netdata.io/kickstart.sh)

# Installation de Monit
sudo apt install monit -y
```

### Étape 2 : Configuration de Monit
```bash
sudo nano /etc/monit/monitrc
```

```bash
set daemon 120
set mailserver smtp.gmail.com port 587
    username "votre@gmail.com"
    password "votre_mot_de_passe"
    using tlsv12

check system $HOST
    if loadavg (1min) > 4 then alert
    if memory usage > 85% then alert
    if cpu usage (user) > 70% then alert

check process nginx with pidfile /var/run/nginx.pid
    start program = "/etc/init.d/nginx start"
    stop program = "/etc/init.d/nginx stop"
    if failed host localhost port 80 protocol http then restart
    if 5 restarts within 5 cycles then timeout
```

## Script de maintenance automatique
```bash
sudo nano /root/maintenance.sh
```

```bash
#!/bin/bash

# Variables
SITES=("soccer.com" "football.ca" "spaghetti.fr")
BACKUP_DIR="/root/backups"
LOG_DIR="/var/log/maintenance"
DATE=$(date +%Y%m%d)

# Création des répertoires
mkdir -p $BACKUP_DIR $LOG_DIR

# Mise à jour système
apt update >> $LOG_DIR/update_$DATE.log 2>&1
apt upgrade -y >> $LOG_DIR/upgrade_$DATE.log 2>&1

# Nettoyage système
apt autoremove -y
apt clean

# Vérification des services
systemctl status nginx | grep active >> $LOG_DIR/status_$DATE.log
systemctl status php8.1-fpm | grep active >> $LOG_DIR/status_$DATE.log

# Backup des sites
for SITE in "${SITES[@]}"
do
    # Backup des fichiers
    tar -czf $BACKUP_DIR/$SITE-files-$DATE.tar.gz /var/www/$SITE
    
    # Backup de la configuration
    tar -czf $BACKUP_DIR/$SITE-config-$DATE.tar.gz /etc/nginx/sites-available/$SITE
    
    # Test SSL
    echo "Vérification SSL pour $SITE" >> $LOG_DIR/ssl_$DATE.log
    curl -vI https://$SITE 2>> $LOG_DIR/ssl_$DATE.log
done

# Nettoyage des vieux backups
find $BACKUP_DIR -type f -mtime +7 -delete
find $LOG_DIR -type f -mtime +30 -delete

# Vérification des logs d'erreur
grep -i error /var/log/nginx/*.log >> $LOG_DIR/errors_$DATE.log
```

## Conclusion

Pour une sécurité maximale, utilisez une combinaison de :

1. **SSL/TLS** :
   - Certbot (Let's Encrypt)
   - acme.sh
   - Caddy
   - Certificats commerciaux

2. **Protection DDoS** :
   - Fail2ban
   - UFW
   - Cloudflare
   - ModSecurity

3. **Monitoring** :
   - Netdata
   - Monit
   - Nagios
   - Zabbix

4. **Backup** :
   - Scripts personnalisés
   - Rsync
   - Rclone
   - Duplicity

5. **Maintenance** :
   - Cron jobs automatisés
   - Scripts de maintenance
   - Monitoring système
   - Alertes par email

N'oubliez pas de :
- Mettre à jour régulièrement tous les composants
- Vérifier les logs quotidiennement
- Tester les backups régulièrement
- Maintenir une documentation à jour
- Former les utilisateurs aux bonnes pratiques de sécurité
