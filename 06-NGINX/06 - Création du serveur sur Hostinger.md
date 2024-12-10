## Création du serveur sur Hostinger

# Étape 1 : Achat et Configuration
1. Allez sur hostinger.fr
2. Cliquez sur "VPS Hosting"
3. Choisissez un plan (recommandé minimum) :
   * 2GB RAM
   * 1 vCPU
   * 20GB SSD
4. Dans le processus d'installation :
   * OS : Sélectionnez **Ubuntu 22.04 LTS**
   * Région : Choisissez la plus proche de vous
   * Mot de passe : Créez un mot de passe fort

# Étape 2 : Configuration DNS
1. Dans le panel Hostinger :
   * Menu → Domaines
   * Sélectionnez hrehouma.com
   * DNS Zone
2. Ajoutez ces enregistrements :
```
Type    Nom    Valeur              TTL
A       @      [Votre_IP_VPS]      3600
A       www    [Votre_IP_VPS]      3600
```

## Connexion au serveur

### Étape 1 : Installation de PuTTY (Windows)
1. Téléchargez PuTTY depuis le site officiel
2. Installez-le
3. Ouvrez PuTTY
4. Entrez :
   * Host Name : votre_ip_vps
   * Port : 22
   * Connection type : SSH

### Étape 2 : Première connexion
```bash
# Pour Windows avec PuTTY :
# Entrez les informations fournies par Hostinger
Username: root
Password: votre_mot_de_passe

# Pour Mac/Linux :
ssh root@votre_ip_vps
```

# Étape 3 : Création d'un utilisateur sécurisé
```bash
# Créez un nouvel utilisateur
adduser votre_nom_utilisateur
# Exemple : adduser admin

# Suivez les instructions :
# - Mot de passe (2 fois)
# - Nom complet (Entrée pour passer)
# - Room number (Entrée)
# - Work phone (Entrée)
# - Home phone (Entrée)
# - Other (Entrée)

# Ajoutez l'utilisateur au groupe sudo
usermod -aG sudo votre_nom_utilisateur

# Connectez-vous avec le nouvel utilisateur
su - votre_nom_utilisateur
```

## Préparation du serveur

### Étape 1 : Mise à jour complète
```bash
# Mettez à jour la liste des paquets
sudo apt update

# Mettez à jour tous les paquets
sudo apt upgrade -y

# Installez les outils essentiels
sudo apt install -y curl wget git unzip ufw nano
```

### Étape 2 : Configuration du pare-feu
```bash
# Activez le pare-feu pour SSH
sudo ufw allow OpenSSH

# Vérifiez le statut
sudo ufw status

# Activez le pare-feu
sudo ufw enable

# Tapez 'y' pour confirmer
```

## Installation de Nginx

### Étape 1 : Installation
```bash
# Installez Nginx
sudo apt install nginx -y

# Vérifiez que Nginx est installé
nginx -v

# Démarrez Nginx
sudo systemctl start nginx

# Activez Nginx au démarrage
sudo systemctl enable nginx

# Vérifiez le statut
sudo systemctl status nginx
```

### Étape 2 : Configuration du pare-feu pour Nginx
```bash
# Autorisez le trafic HTTP (port 80)
sudo ufw allow 'Nginx HTTP'

# Autorisez le trafic HTTPS (port 443)
sudo ufw allow 'Nginx HTTPS'

# Vérifiez les règles
sudo ufw status
```

## Configuration du site web

### Étape 1 : Création de la structure
```bash
# Créez le dossier pour votre site
sudo mkdir -p /var/www/hrehouma.com/public_html

# Définissez les permissions
sudo chown -R $USER:$USER /var/www/hrehouma.com
sudo chmod -R 755 /var/www/hrehouma.com

# Créez une page de test
sudo nano /var/www/hrehouma.com/public_html/index.html
```

Copiez ce code HTML de test :
```html
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bienvenue sur hrehouma.com</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px auto;
            max-width: 800px;
            padding: 20px;
            text-align: center;
        }
    </style>
</head>
<body>
    <h1>Bienvenue sur hrehouma.com</h1>
    <p>Cette page confirme que Nginx fonctionne correctement.</p>
    <p>Date d'installation : <?php echo date('Y-m-d H:i:s'); ?></p>
</body>
</html>
```

### Étape 2 : Configuration Nginx
```bash
# Créez le fichier de configuration
sudo nano /etc/nginx/sites-available/hrehouma.com
```

Copiez cette configuration :
```nginx
server {
    listen 80;
    listen [::]:80;
    server_name hrehouma.com www.hrehouma.com;
    root /var/www/hrehouma.com/public_html;

    index index.html index.htm index.php;

    # Logs personnalisés
    access_log /var/log/nginx/hrehouma.com.access.log;
    error_log /var/log/nginx/hrehouma.com.error.log;

    location / {
        try_files $uri $uri/ =404;
    }

    # Configuration des fichiers statiques
    location ~* \.(jpg|jpeg|png|gif|ico|css|js)$ {
        expires 30d;
        add_header Cache-Control "public, no-transform";
    }

    # Sécurité de base
    location ~ /\. {
        deny all;
    }

    # Compression Gzip
    gzip on;
    gzip_vary on;
    gzip_min_length 1000;
    gzip_proxied expired no-cache no-store private auth;
    gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;
}
```

### Étape 3 : Activation du site
```bash
# Créez le lien symbolique
sudo ln -s /etc/nginx/sites-available/hrehouma.com /etc/nginx/sites-enabled/

# Supprimez la configuration par défaut
sudo rm /etc/nginx/sites-enabled/default

# Vérifiez la configuration
sudo nginx -t

# Si tout est OK, redémarrez Nginx
sudo systemctl restart nginx
```

## Installation SSL avec Let's Encrypt

### Étape 1 : Installation de Certbot
```bash
# Installez Certbot et le plugin Nginx
sudo apt install certbot python3-certbot-nginx -y
```

### Étape 2 : Obtention du certificat
```bash
# Obtenez et installez le certificat
sudo certbot --nginx -d hrehouma.com -d www.hrehouma.com

# Suivez les instructions :
# 1. Entrez votre email
# 2. Acceptez les conditions (A)
# 3. Choisissez si vous voulez partager votre email (N)
# 4. Choisissez la redirection HTTPS (2)
```

### Étape 3 : Vérification du renouvellement
```bash
# Testez le renouvellement automatique
sudo certbot renew --dry-run
```

## Sécurité supplémentaire

### Étape 1 : Configuration des en-têtes de sécurité
```bash
sudo nano /etc/nginx/sites-available/hrehouma.com
```

Ajoutez ces lignes dans le bloc server :
```nginx
    # En-têtes de sécurité
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Content-Type-Options "nosniff";
    add_header Referrer-Policy "strict-origin-when-cross-origin";
    add_header Content-Security-Policy "default-src 'self' http: https: data: blob: 'unsafe-inline'";
```

### Étape 2 : Configuration des backups
```bash
# Créez un script de backup
sudo nano /root/backup-nginx.sh
```

Copiez ce script :
```bash
#!/bin/bash
BACKUP_DIR="/root/backup"
DATE=$(date +%Y%m%d)
SITE_NAME="hrehouma.com"

# Créez le répertoire de backup s'il n'existe pas
mkdir -p $BACKUP_DIR

# Sauvegarde des fichiers de configuration
tar -czf $BACKUP_DIR/nginx-config-$DATE.tar.gz /etc/nginx/

# Sauvegarde des fichiers du site
tar -czf $BACKUP_DIR/www-$SITE_NAME-$DATE.tar.gz /var/www/$SITE_NAME/

# Suppression des backups de plus de 7 jours
find $BACKUP_DIR -type f -mtime +7 -delete
```

```bash
# Rendez le script exécutable
sudo chmod +x /root/backup-nginx.sh

# Ajoutez une tâche cron
sudo crontab -e
```

Ajoutez cette ligne :
```
0 3 * * * /root/backup-nginx.sh
```

## Vérification finale

### Étape 1 : Tests
```bash
# Vérifiez la configuration Nginx
sudo nginx -t

# Redémarrez Nginx
sudo systemctl restart nginx

# Vérifiez le statut
sudo systemctl status nginx

# Testez l'accès HTTP
curl -I http://hrehouma.com

# Testez l'accès HTTPS
curl -I https://hrehouma.com
```

### Étape 2 : Surveillance des logs
```bash
# Surveillez les logs d'erreur
sudo tail -f /var/log/nginx/hrehouma.com.error.log

# Surveillez les logs d'accès
sudo tail -f /var/log/nginx/hrehouma.com.access.log
```

Votre site est maintenant complètement configuré et sécurisé. Vérifiez régulièrement :
- Les mises à jour système : `sudo apt update && sudo apt upgrade`
- Les logs pour détecter les problèmes
- Le renouvellement SSL (automatique mais vérifiez)
- Les sauvegardes
