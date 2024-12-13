# **Cours : NGINX - Sécurisation du Trafic avec HTTPS**

Ce cours explore l'utilisation de **NGINX** pour sécuriser le trafic via **HTTPS**. Nous couvrirons les concepts fondamentaux de HTTPS, l’implémentation avec NGINX, et les configurations avancées pour optimiser la sécurité.

---

## **1. Introduction : Pourquoi HTTPS ?**

### **Définition**
HTTPS (HyperText Transfer Protocol Secure) est une version sécurisée de HTTP qui utilise le protocole **SSL/TLS** pour chiffrer les communications entre un client (navigateur) et un serveur web.

### **Avantages**
- **Confidentialité** : Les données échangées sont chiffrées.
- **Authenticité** : Vérifie que le serveur est légitime grâce à un certificat.
- **Intégrité** : Empêche la modification des données pendant leur transmission.
- **SEO et performance** : Google favorise les sites HTTPS dans son référencement.

---

## **2. Utiliser HTTPS avec NGINX**

### Étape 1 : Installer Certbot (Let's Encrypt)
Certbot est un outil gratuit permettant d’obtenir des certificats SSL/TLS de **Let's Encrypt**.

1. **Installer Certbot** :
   Sur un serveur Ubuntu :
   ```bash
   sudo apt update
   sudo apt install certbot python3-certbot-nginx
   ```

2. **Générer un certificat SSL** :
   Certbot configure automatiquement NGINX avec HTTPS :
   ```bash
   sudo certbot --nginx
   ```
   - Suivez les instructions pour spécifier votre domaine.
   - Le certificat est automatiquement installé dans la configuration NGINX.

3. **Renouvellement automatique** :
   Let's Encrypt émet des certificats valables 90 jours. Pour les renouveler automatiquement :
   ```bash
   sudo certbot renew --dry-run
   ```

---

### Étape 2 : Configurer HTTPS Manuellement

Si vous avez un certificat SSL/TLS (par exemple, acheté ou généré avec OpenSSL), suivez ces étapes.

1. **Préparer les fichiers nécessaires** :
   - Clé privée : `server.key`
   - Certificat : `server.crt`
   - Optionnel : Chaîne de certificats intermédiaires (`chain.pem`).

2. **Modifier la configuration NGINX** :
   Exemple de configuration pour activer HTTPS :
   ```nginx
   server {
       listen 443 ssl;
       server_name example.com;

       ssl_certificate /etc/nginx/ssl/server.crt;
       ssl_certificate_key /etc/nginx/ssl/server.key;

       ssl_protocols TLSv1.2 TLSv1.3;
       ssl_ciphers HIGH:!aNULL:!MD5;

       location / {
           root /var/www/html;
           index index.html;
       }
   }
   ```

3. **Rediriger le trafic HTTP vers HTTPS** :
   Ajoutez un serveur HTTP avec une redirection :
   ```nginx
   server {
       listen 80;
       server_name example.com;

       return 301 https://$host$request_uri;
   }
   ```

4. **Tester la configuration** :
   Testez la configuration avant de redémarrer NGINX :
   ```bash
   sudo nginx -t
   sudo systemctl reload nginx
   ```

---

## **3. Handshake et Chaîne de Certificats**

### **Le Handshake TLS**
Le **handshake TLS** est une séquence d'échanges entre le client et le serveur pour établir une connexion sécurisée.

1. **Étapes clés** :
   - **Hello Client/Server** :
     - Le client envoie une liste de **chiffres pris en charge**.
     - Le serveur choisit le chiffre et envoie son **certificat**.
   - **Vérification** :
     - Le client vérifie le certificat à l’aide des autorités de certification (CA).
   - **Clé symétrique** :
     - Une clé de session est échangée en toute sécurité pour chiffrer les données.

2. **Chaîne de certificats** :
   - Le certificat du serveur est signé par une **autorité de certification (CA)**.
   - Si la CA est intermédiaire, elle doit fournir une chaîne complète jusqu’à une CA racine reconnue.

   Exemple d'une chaîne de certificats :
   ```
   [Certificat du serveur]
          ↓ signé par
   [CA intermédiaire]
          ↓ signé par
   [CA racine]
   ```

---

## **4. Configuration Avancée de HTTPS**

### **Protocole TLS**
1. **Activer les versions récentes uniquement** :
   - Bloquez les versions anciennes de TLS (TLSv1.0 et TLSv1.1) :
     ```nginx
     ssl_protocols TLSv1.2 TLSv1.3;
     ```

2. **Configurer les chiffrements sécurisés** :
   - Utilisez des suites de chiffrement robustes :
     ```nginx
     ssl_ciphers HIGH:!aNULL:!MD5;
     ```

3. **Activer la reprise de session** :
   - Cela améliore les performances en évitant un nouveau handshake complet :
     ```nginx
     ssl_session_cache shared:SSL:10m;
     ssl_session_timeout 10m;
     ```

4. **Utiliser HSTS (HTTP Strict Transport Security)** :
   - HSTS oblige les navigateurs à utiliser HTTPS :
     ```nginx
     add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
     ```

---

### **Optimisation des Performances**

1. **Compression des données** :
   - Activez **gzip** pour réduire la taille des réponses HTTP :
     ```nginx
     gzip on;
     gzip_types text/plain text/css application/json application/javascript;
     gzip_min_length 1000;
     ```

2. **Optimiser le cache** :
   - Permettez aux navigateurs de mettre en cache les fichiers statiques :
     ```nginx
     location /static/ {
         expires 30d;
         add_header Cache-Control "public";
     }
     ```

---

### **Sécurité Renforcée**

1. **Désactiver les protocoles obsolètes** :
   - Bloquez SSLv2, SSLv3 et les suites de chiffrement faibles :
     ```nginx
     ssl_protocols TLSv1.2 TLSv1.3;
     ssl_prefer_server_ciphers on;
     ```

2. **Certificat ÉV (Extended Validation)** :
   - Utilisez des certificats EV pour renforcer la confiance (optionnel mais recommandé).

3. **Limiter les informations exposées** :
   - Désactivez les informations sensibles envoyées par NGINX :
     ```nginx
     server_tokens off;
     ```

---

### **Automatisation et Surveillance**

1. **Renouvellement automatique** :
   - Si vous utilisez Let's Encrypt, configurez une tâche cron pour renouveler les certificats :
     ```bash
     0 3 * * * certbot renew --quiet
     ```

2. **Surveiller les certificats** :
   - Utilisez des outils comme **SSL Labs** pour analyser la configuration HTTPS de votre site :
     - [SSL Labs Test](https://www.ssllabs.com/ssltest/)

3. **Configurer un journal HTTPS** :
   - Activez les journaux pour surveiller les erreurs SSL/TLS :
     ```nginx
     error_log /var/log/nginx/https_errors.log;
     ```

---

## **Exemple Complet de Configuration NGINX avec HTTPS**

Voici une configuration consolidée pour un site HTTPS sécurisé :
```nginx
server {
    listen 443 ssl;
    server_name example.com www.example.com;

    # Certificat SSL
    ssl_certificate /etc/nginx/ssl/server.crt;
    ssl_certificate_key /etc/nginx/ssl/server.key;

    # Protocoles TLS et chiffrements
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;

    # HSTS
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;

    # Compression gzip
    gzip on;
    gzip_types text/plain text/css application/json application/javascript;

    # Cache pour les fichiers statiques
    location /static/ {
        expires 30d;
        add_header Cache-Control "public";
    }

    # Root et index
    root /var/www/example;
    index index.html;

    # Journal des erreurs HTTPS
    error_log /var/log/nginx/https_errors.log;
}

server {
    listen 80;
    server_name example.com www.example.com;

    # Redirection vers HTTPS
    return 301 https://$host$request_uri;
}
```

---

## **Conclusion**

En suivant ce cours, vous êtes désormais capable de :
1. **Activer HTTPS avec NGINX**, que ce soit via Certbot ou une configuration manuelle.
2. Comprendre le **handshake TLS** et la chaîne de certificats pour une connexion sécurisée.
3. Appliquer des **configurations avancées** pour maximiser la sécurité et les performances.

Avec ces pratiques, votre serveur sera sécurisé, performant et conforme aux standards modernes.
