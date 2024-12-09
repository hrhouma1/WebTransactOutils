### **Cours : NGINX - Sécurisation du Trafic (HTTPS)**

---

#### **Objectifs du cours**
- Comprendre l'importance de HTTPS dans la sécurisation des échanges web.
- Apprendre à configurer NGINX pour servir des sites via HTTPS.
- Explorer les concepts de **TLS handshake** et de **chaîne de certificats**.
- Mettre en place une configuration HTTPS avancée avec des bonnes pratiques de sécurité.

---

### **1. Introduction à HTTPS et son rôle dans la sécurité**

#### **Qu'est-ce que HTTPS ?**
- HTTPS (HyperText Transfer Protocol Secure) est une version sécurisée de HTTP.
- Basé sur **TLS** (Transport Layer Security), il offre :
  - **Confidentialité** : chiffrement des données échangées.
  - **Intégrité** : protection contre la modification des données.
  - **Authenticité** : assurance que le serveur est celui qu'il prétend être.

#### **Pourquoi utiliser HTTPS ?**
- Protéger les données sensibles (mots de passe, informations personnelles).
- Éviter les attaques de type MITM (Man-in-the-Middle).
- Améliorer le classement SEO des sites (Google favorise HTTPS).
- Inspirer confiance aux utilisateurs (icône de cadenas dans les navigateurs).

---

### **2. Mettre en place HTTPS avec NGINX**

#### **Étape 1 : Préparer les certificats SSL/TLS**
1. **Obtenir un certificat SSL/TLS** :
   - Option 1 : Certificat gratuit via **Let's Encrypt**.
   - Option 2 : Certificat payant d'une Autorité de Certification (CA) reconnue.
2. **Installer `certbot` pour Let's Encrypt** (si Let's Encrypt est choisi) :
   ```bash
   sudo apt update
   sudo apt install certbot python3-certbot-nginx
   ```

#### **Étape 2 : Configurer NGINX pour HTTPS**
1. Modifier le fichier de configuration du site :
   ```nginx
   server {
       listen 80;
       server_name example.com www.example.com;

       # Redirection HTTP vers HTTPS
       return 301 https://$host$request_uri;
   }

   server {
       listen 443 ssl;
       server_name example.com www.example.com;

       ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
       ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

       location / {
           root /var/www/html;
           index index.html index.htm;
       }
   }
   ```
2. Tester et recharger la configuration :
   ```bash
   sudo nginx -t
   sudo systemctl reload nginx
   ```

#### **Étape 3 : Automatiser le renouvellement des certificats**
- Avec Let's Encrypt :
  ```bash
  sudo certbot renew --dry-run
  ```

---

### **3. Comprendre le Handshake et la chaîne de certificats**

#### **TLS Handshake**
1. **Processus de négociation entre le client et le serveur** :
   - Établissement d'une connexion sécurisée.
   - Échange de clés cryptographiques.
   - Vérification du certificat du serveur par le client.

2. **Étapes clés du TLS Handshake** :
   - Le client envoie une liste de suites cryptographiques et de versions TLS acceptées.
   - Le serveur choisit une suite cryptographique et envoie son certificat.
   - Une clé de session est échangée via un algorithme (RSA ou Diffie-Hellman).
   - Les données chiffrées sont échangées à l'aide de cette clé.

#### **Chaîne de certificats**
- Composants :
  - **Certificat de serveur** : certifie l'identité du site.
  - **Certificat intermédiaire** : signé par une autorité reconnue.
  - **Certificat racine** : autorité de certification (CA) de confiance.

- Rôle : Établir un chemin de confiance entre le certificat du serveur et une CA de confiance.

---

### **4. Configuration HTTPS avancée**

#### **Renforcer la sécurité HTTPS**
1. **Configurer des suites cryptographiques robustes** :
   ```nginx
   ssl_protocols TLSv1.2 TLSv1.3;
   ssl_ciphers HIGH:!aNULL:!MD5;
   ssl_prefer_server_ciphers on;
   ```

2. **Utiliser HSTS (HTTP Strict Transport Security)** :
   ```nginx
   add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
   ```

3. **Activer OCSP Stapling** :
   ```nginx
   ssl_stapling on;
   ssl_stapling_verify on;
   resolver 8.8.8.8 8.8.4.4 valid=300s;
   resolver_timeout 5s;
   ```

4. **Désactiver les protocoles obsolètes** :
   - Désactiver SSLv3 et TLSv1.0.

5. **Limiter les attaques par force brute** :
   - Implémenter des outils comme fail2ban pour bloquer les connexions répétées.

---

### **5. Outils pour tester la sécurité HTTPS**

- **SSL Labs** : [Qualys SSL Labs](https://www.ssllabs.com/ssltest/) pour analyser la configuration.
- **Test rapide avec `curl`** :
  ```bash
  curl -I -k https://example.com
  ```

---

### **6. Étude de cas : Configuration sécurisée complète**
Exemple de configuration NGINX pour HTTPS :
```nginx
server {
    listen 443 ssl http2;
    server_name example.com www.example.com;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;

    add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;

    location / {
        root /var/www/html;
        index index.html;
    }
}
```

---

### **7. Conclusion**
- HTTPS est un standard indispensable pour sécuriser les sites web.
- Une bonne configuration HTTPS sur NGINX repose sur des certificats fiables, des protocoles modernes, et des en-têtes de sécurité.
- Vérifiez et testez régulièrement votre configuration pour rester à jour avec les meilleures pratiques de sécurité.

---

### **Exercices**
1. Configurez un site avec HTTPS sur un serveur NGINX en utilisant Let's Encrypt.
2. Testez la sécurité de votre configuration avec SSL Labs et améliorez votre score.
3. Ajoutez HSTS et OCSP Stapling pour renforcer votre configuration.

