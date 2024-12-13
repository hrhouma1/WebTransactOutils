### **Guide Pratique pour Configurer les En-têtes de Sécurité**


### **1. Strict-Transport-Security (HSTS)**

#### **Objectif** :
Forcer le navigateur à utiliser HTTPS exclusivement pour toutes les requêtes, empêchant ainsi les connexions non sécurisées (HTTP).

#### **Configuration pour Nginx** :
Ajoutez cette directive dans votre bloc `server` :
```nginx
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
```

#### **Configuration pour Apache** :
Ajoutez cette ligne dans le fichier de configuration du site :
```apache
Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains; preload"
```

#### **Points importants** :
- **`max-age`** : Définit la durée pendant laquelle HSTS est actif (31 536 000 secondes = 1 an).
- **`includeSubDomains`** : Applique la politique HSTS à tous les sous-domaines.
- **`preload`** : Permet d'ajouter votre site à la liste HSTS Preload des navigateurs.

---

### **2. Content-Security-Policy (CSP)**

#### **Objectif** :
Limiter les sources autorisées pour charger des scripts, styles, images, etc., afin de prévenir les attaques XSS.

#### **Configuration pour Nginx** :
Ajoutez une politique de base :
```nginx
add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'; img-src 'self';";
```

#### **Configuration pour Apache** :
Ajoutez cette ligne dans la configuration du site :
```apache
Header set Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'; img-src 'self';"
```

#### **Exemple avancé** :
Si votre site utilise des scripts tiers comme des APIs :
```nginx
add_header Content-Security-Policy "default-src 'self'; script-src 'self' https://apis.google.com; style-src 'self'; img-src 'self'; connect-src 'self';";
```

#### **Points importants** :
- **`default-src`** : Définit la source par défaut pour toutes les ressources.
- **`script-src`** : Contrôle les scripts (JavaScript).
- **`style-src`** : Contrôle les feuilles de styles CSS.
- **`img-src`** : Définit les sources d'images.

---

### **3. X-Frame-Options**

#### **Objectif** :
Empêcher votre site d’être intégré dans des frames non autorisées, protégeant contre le clickjacking.

#### **Configuration pour Nginx** :
```nginx
add_header X-Frame-Options "SAMEORIGIN";
```

#### **Configuration pour Apache** :
```apache
Header set X-Frame-Options "SAMEORIGIN"
```

#### **Valeurs possibles** :
- **`SAMEORIGIN`** : Autorise les frames provenant du même domaine.
- **`DENY`** : Bloque complètement les frames.
- **`ALLOW-FROM`** : Autorise uniquement un domaine spécifique (obsolète et rarement supporté).

---

### **4. X-Content-Type-Options**

#### **Objectif** :
Empêcher le navigateur de deviner le type MIME des fichiers, évitant l’exécution de fichiers malveillants.

#### **Configuration pour Nginx** :
```nginx
add_header X-Content-Type-Options "nosniff";
```

#### **Configuration pour Apache** :
```apache
Header set X-Content-Type-Options "nosniff"
```

#### **Points importants** :
- La valeur **`nosniff`** est obligatoire pour activer cette protection.

---

### **5. Referrer-Policy**

#### **Objectif** :
Contrôler les informations envoyées via l’en-tête "Referer" lorsque l’utilisateur clique sur un lien externe.

#### **Configuration pour Nginx** :
```nginx
add_header Referrer-Policy "strict-origin-when-cross-origin";
```

#### **Configuration pour Apache** :
```apache
Header set Referrer-Policy "strict-origin-when-cross-origin"
```

#### **Valeurs recommandées** :
- **`no-referrer`** : Ne transmet aucune information.
- **`strict-origin`** : Transmet uniquement l’origine (https://example.com) pour des connexions sécurisées.
- **`strict-origin-when-cross-origin`** : Transmet l’origine pour les requêtes HTTPS seulement.

---

### **6. Permissions-Policy** (anciennement Feature-Policy)

#### **Objectif** :
Limiter l'accès aux fonctionnalités sensibles du navigateur, telles que la caméra, le microphone, ou la géolocalisation.

#### **Configuration pour Nginx** :
```nginx
add_header Permissions-Policy "geolocation=(), microphone=(), camera=()";
```

#### **Configuration pour Apache** :
```apache
Header set Permissions-Policy "geolocation=(), microphone=(), camera=()"
```

#### **Points importants** :
- **`geolocation=()`** : Désactive la géolocalisation.
- **`microphone=()`** : Bloque l’accès au micro.
- **`camera=()`** : Interdit l’utilisation de la caméra.

---

### **7. Cross-Origin Resource Sharing (CORS)**

#### **Objectif** :
Contrôler les requêtes provenant de domaines différents et limiter les sources autorisées.

#### **Configuration pour Nginx** :
```nginx
add_header Access-Control-Allow-Origin "https://trusted-site.com";
```

#### **Configuration pour Apache** :
```apache
Header set Access-Control-Allow-Origin "https://trusted-site.com"
```

#### **Points importants** :
- Spécifiez les domaines de confiance pour éviter les abus.
- Combinez avec une politique CSP pour une sécurité renforcée.

---

### **8. Exemple Complet pour Nginx**

Voici une configuration complète pour un serveur Nginx :
```nginx
server {
    listen 443 ssl;
    server_name example.com;

    # En-têtes de sécurité
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
    add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'; img-src 'self';";
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";
    add_header Referrer-Policy "strict-origin-when-cross-origin";
    add_header Permissions-Policy "geolocation=(), microphone=(), camera=()";

    # SSL Configuration
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers EECDH+AESGCM:EDH+AESGCM:AES256+EECDH:AES256+EDH;
    ssl_prefer_server_ciphers on;

    root /var/www/example.com;
    index index.html;
}
```

---

### **9. Exemple Complet pour Apache**

Voici une configuration complète pour un serveur Apache :
```apache
<VirtualHost *:443>
    ServerName example.com

    # En-têtes de sécurité
    Header always set Strict-Transport-Security "max-age=31536000; includeSubDomains; preload"
    Header set Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'; img-src 'self';"
    Header set X-Frame-Options "SAMEORIGIN"
    Header set X-Content-Type-Options "nosniff"
    Header set Referrer-Policy "strict-origin-when-cross-origin"
    Header set Permissions-Policy "geolocation=(), microphone=(), camera=()"

    # SSL Configuration
    SSLEngine on
    SSLProtocol all -SSLv2 -SSLv3
    SSLCipherSuite HIGH:!aNULL:!MD5

    DocumentRoot "/var/www/example.com"
</VirtualHost>
```

---

### **10. Testez Vos Configurations**

Après avoir configuré les en-têtes, utilisez ces outils pour vérifier leur efficacité :
1. [SecurityHeaders](https://securityheaders.com) : Analyse les en-têtes de sécurité.
2. [Mozilla Observatory](https://observatory.mozilla.org) : Vérifie les pratiques de sécurité globales.
3. [SSL Labs](https://www.ssllabs.com/ssltest/) : Teste les configurations SSL/TLS.

---

### **Conclusion**

En suivant ces guides pratiques, vous pouvez sécuriser votre site contre les attaques courantes et offrir une meilleure expérience utilisateur. Chaque en-tête remplit un rôle spécifique, et leur combinaison offre une protection robuste contre les cybermenaces modernes.
