### **Cours : Les En-têtes HTTP de Sécurité**

---

#### **Introduction : Pourquoi les en-têtes de sécurité sont-ils essentiels ?**
Les en-têtes HTTP de sécurité sont des directives envoyées par le serveur au navigateur pour dicter comment traiter les requêtes. Ces en-têtes permettent de renforcer la sécurité des sites web contre des attaques courantes telles que :

- **Cross-Site Scripting (XSS)** : Injection de scripts malveillants.
- **Clickjacking** : Piégeage d’utilisateurs via des frames invisibles.
- **Downgrade attacks** : Forcer un utilisateur à utiliser HTTP au lieu de HTTPS.
- **MIME sniffing** : Deviner le type de contenu malveillant.

Leur absence ou une mauvaise configuration expose les utilisateurs à des risques majeurs. En tant qu’administrateur ou développeur, il est indispensable de comprendre et de configurer correctement ces en-têtes.

---

### **1. Strict-Transport-Security (HSTS)**

**Objectif** : 
Forcer le navigateur à utiliser uniquement le protocole HTTPS, même si l’utilisateur ou un lien tente de charger le site en HTTP.

**Scénario de vulnérabilité sans HSTS** :  
Un attaquant effectue une attaque de type "downgrade" où il force la connexion d’un utilisateur en HTTP (non sécurisé). L’absence d’HSTS permet au pirate de voir ou manipuler les données transmises.

**Configuration recommandée** :  
```nginx
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload";
```

**Explication des paramètres** :
- **`max-age`** : Durée (en secondes) pendant laquelle le navigateur doit forcer HTTPS (1 an = 31 536 000 s).
- **`includeSubDomains`** : Applique cette règle à tous les sous-domaines.
- **`preload`** : Permet au domaine d’être ajouté à la liste HSTS Preload des navigateurs (voir annexe 01).

**Bonnes pratiques** :  
- Activez HSTS uniquement après avoir configuré correctement HTTPS sur votre site.  
- Testez sur un environnement de staging avant de l’appliquer sur le site principal.

---

### **2. Content-Security-Policy (CSP)**

**Objectif** :  
Limiter les sources autorisées pour charger des scripts, styles, images, et d’autres ressources afin de prévenir les attaques de type XSS.

**Scénario de vulnérabilité sans CSP** :  
Un attaquant injecte un script malveillant dans une page (via un commentaire ou un champ de formulaire). Sans CSP, ce script sera exécuté par le navigateur.

**Configuration recommandée** :  
```nginx
add_header Content-Security-Policy "default-src 'self'; script-src 'self' https://apis.google.com; style-src 'self'; img-src 'self';";
```

**Explication des directives** :
- **`default-src`** : Définit la source par défaut pour toutes les ressources.
- **`script-src`** : Autorise les scripts uniquement depuis les sources spécifiées (ici le site lui-même et l'API de Google).
- **`style-src`** : Définit les styles CSS autorisés.
- **`img-src`** : Contrôle l’origine des images.

**Bonnes pratiques** :
- Utilisez l’outil [CSP Evaluator](https://csp-evaluator.withgoogle.com/) pour analyser vos politiques.
- Commencez avec un mode de rapport (`report-only`) pour détecter les violations sans bloquer immédiatement.

---

### **3. X-Frame-Options**

**Objectif** :  
Empêcher l’intégration de votre site dans une iframe non autorisée afin de prévenir les attaques de type clickjacking.

**Scénario de vulnérabilité sans X-Frame-Options** :  
Un pirate affiche votre site dans une iframe invisible et incite les utilisateurs à cliquer sur des boutons ou liens à leur insu.

**Configuration recommandée** :  
```nginx
add_header X-Frame-Options "SAMEORIGIN";
```

**Explication des valeurs** :
- **`SAMEORIGIN`** : Autorise uniquement les frames provenant du même domaine.
- **`DENY`** : Interdit complètement les frames.
- **`ALLOW-FROM https://trusted-site.com`** : Autorise uniquement les frames provenant d’un domaine spécifique (option rarement prise en charge par les navigateurs modernes).

**Bonnes pratiques** :  
- Préférez `SAMEORIGIN` pour autoriser les intégrations internes nécessaires.  
- Pour les applications critiques (ex. banques), utilisez `DENY`.

---

### **4. X-Content-Type-Options**

**Objectif** :  
Empêcher le navigateur de deviner le type MIME des fichiers (MIME sniffing), ce qui pourrait permettre l’exécution de fichiers malveillants.

**Scénario de vulnérabilité sans X-Content-Type-Options** :  
Un fichier `.txt` téléchargé est interprété par le navigateur comme un fichier `.exe`, permettant à l’attaquant d'exécuter du code.

**Configuration recommandée** :  
```nginx
add_header X-Content-Type-Options "nosniff";
```

**Explication des paramètres** :
- **`nosniff`** : Bloque tout type MIME incorrect, assurant que le fichier sera interprété uniquement selon son type déclaré.

**Bonnes pratiques** :
- Activez `nosniff` pour tous les types de fichiers, particulièrement les scripts et styles.
- Combinez-le avec CSP pour une protection optimale.

---

### **5. Referrer-Policy**

**Objectif** :  
Contrôler les informations envoyées dans le header "Referer" lorsqu’un utilisateur clique sur un lien vers une autre page ou un autre site.

**Scénario de vulnérabilité sans Referrer-Policy** :  
Un lien externe peut collecter des informations sensibles de l’URL de votre site, comme des jetons d'authentification ou des IDs utilisateur.

**Configuration recommandée** :  
```nginx
add_header Referrer-Policy "strict-origin-when-cross-origin";
```

**Explication des valeurs** :
- **`no-referrer`** : Ne transmet aucune information.
- **`strict-origin`** : Transmet uniquement l’origine (exemple : `https://mon-site.com`).
- **`strict-origin-when-cross-origin`** : Partage l’origine uniquement pour des liens sécurisés (HTTPS).

**Bonnes pratiques** :
- Utilisez une politique stricte par défaut (`strict-origin-when-cross-origin`).
- Évitez `unsafe-url`, car elle partage des informations détaillées avec le site cible.

---

### **6. Permissions-Policy** (anciennement Feature-Policy)

**Objectif** :  
Restreindre l’accès à certaines fonctionnalités sensibles du navigateur comme la caméra, le micro, ou la géolocalisation.

**Scénario de vulnérabilité sans Permissions-Policy** :  
Un site malveillant utilise des API non restreintes pour activer la caméra ou accéder à votre position sans votre consentement.

**Configuration recommandée** :  
```nginx
add_header Permissions-Policy "geolocation=(), microphone=(), camera=()";
```

**Explication des directives** :
- **`geolocation=()`** : Désactive complètement l'accès à la géolocalisation.
- **`microphone=()`** : Interdit l'accès au microphone.
- **`camera=()`** : Désactive la caméra.

**Bonnes pratiques** :
- Restreignez toutes les fonctionnalités sensibles sauf si elles sont explicitement nécessaires.
- Sur les applications nécessitant ces permissions (ex. visioconférence), limitez l’accès à des pages spécifiques.

---

### **7. Mise en œuvre pratique**

1. **Configurer les en-têtes dans Nginx** :  
   Ouvrez le fichier de configuration de votre site :
   ```bash
   sudo nano /etc/nginx/sites-available/mon-site
   ```

   Ajoutez les en-têtes :
   ```nginx
   server {
       add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload";
       add_header Content-Security-Policy "default-src 'self'; script-src 'self' https://apis.google.com";
       add_header X-Frame-Options "SAMEORIGIN";
       add_header X-Content-Type-Options "nosniff";
       add_header Referrer-Policy "strict-origin-when-cross-origin";
       add_header Permissions-Policy "geolocation=(), microphone=(), camera=()";
   }
   ```

2. **Tester les en-têtes** :
   Utilisez la commande suivante pour vérifier leur présence :
   ```bash
   curl -I https://mon-site.com
   ```

3. **Analyser avec des outils en ligne** :
   - [SecurityHeaders](https://securityheaders.com)
   - [Mozilla Observatory](https://observatory.mozilla.org)

---

### **Conclusion : Pourquoi ces en-têtes sont-ils critiques ?**

- **Renforcer la confiance** : Un site sécurisé inspire la confiance des utilisateurs.
- **Réduire les risques légaux** : Protéger les données des utilisateurs est une exigence légale dans de nombreux pays (ex. RGPD).
- **Se prémunir contre les attaques** : Chaque en-tête cible une classe spécifique d’attaques.
- **Améliorer le SEO** : Les moteurs de recherche privilégient les sites sécurisés.

En appliquant correctement ces en-têtes, vous passez d’un site vulnérable à un site résilient, prêt à répondre aux menaces modernes.


# Annexe 01

### **HSTS Preload : Ajout d'un Domaine à la Liste HSTS Preload des Navigateurs**

#### **1. Qu'est-ce que HSTS (HTTP Strict Transport Security) ?**
HSTS est un mécanisme de sécurité web qui force les navigateurs à utiliser **exclusivement HTTPS** pour se connecter à un domaine, empêchant ainsi les connexions HTTP non sécurisées. Cela protège contre des attaques comme le **man-in-the-middle (MITM)** et le **downgrade attack** où un attaquant force une connexion HTTP non sécurisée.

---

#### **2. Qu'est-ce que la Liste HSTS Preload ?**
La liste **HSTS Preload** est une base de données maintenue par les navigateurs (comme Chrome, Firefox, Edge, Safari, etc.) qui contient les domaines configurés pour **toujours** utiliser HTTPS, même lors de la première connexion d'un utilisateur.

- **Problème sans Preload :**
  Lors de la première visite d'un utilisateur sur un domaine, si celui-ci accède via HTTP, il est vulnérable à une attaque MITM avant que HSTS ne soit appliqué. 
- **Solution avec Preload :**
  En ajoutant un domaine à la liste HSTS Preload, le navigateur sait **dès le départ** que seules les connexions HTTPS sont autorisées, éliminant toute possibilité de connexion HTTP initiale.

---

#### **3. Conditions pour Activer HSTS Preload**
Pour qu'un domaine soit ajouté à la liste HSTS Preload, il doit respecter certaines exigences strictes définies par les navigateurs. Voici ces exigences :

1. **HSTS doit être activé sur le domaine principal** (et ses sous-domaines) :
   - Exemple de configuration dans **NGINX** :
     ```nginx
     add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;
     ```
   - **Détails des directives :**
     - `max-age=31536000` : Définit la durée (en secondes) pendant laquelle HSTS est actif (1 an ici).
     - `includeSubDomains` : Applique la politique HSTS à tous les sous-domaines du domaine principal.
     - `preload` : Indique que le domaine doit être ajouté à la liste HSTS Preload.

2. **Le domaine principal et tous ses sous-domaines doivent être accessibles via HTTPS uniquement.**
   - Aucune connexion HTTP ne doit être possible.

3. **Certificat SSL/TLS valide et bien configuré :**
   - Le domaine doit utiliser un certificat valide, émis par une autorité de certification reconnue.

4. **Redirection automatique de HTTP vers HTTPS :**
   - Toute requête HTTP doit être redirigée vers HTTPS :
     ```nginx
     server {
         listen 80;
         server_name example.com;
         return 301 https://example.com$request_uri;
     }
     ```

5. **Le domaine ne doit pas contenir de sous-domaines non sécurisés :**
   - Par exemple, `sub.example.com` doit aussi être configuré pour HTTPS et HSTS si `includeSubDomains` est utilisé.

---

#### **4. Comment Ajouter un Domaine à la Liste HSTS Preload ?**

1. **Configurer le serveur avec HSTS Preload :**
   - Ajoutez la directive `preload` à la politique HSTS comme montré précédemment.

2. **Tester la configuration :**
   - Utilisez l'outil de vérification officiel pour s'assurer que votre domaine respecte les exigences :  
     [https://hstspreload.org](https://hstspreload.org)

3. **Soumettre le domaine :**
   - Si tout est correct, soumettez votre domaine via le formulaire sur [hstspreload.org](https://hstspreload.org).

4. **Processus de validation :**
   - Les mainteneurs de la liste vérifient que votre domaine respecte les critères avant de l’ajouter.

5. **Propagation aux navigateurs :**
   - Une fois ajouté, votre domaine apparaîtra dans la liste HSTS Preload incluse dans les navigateurs. Cela peut prendre quelques semaines.

---

#### **5. Points Importants à Considérer**

1. **Engagement à long terme :**
   - Une fois qu’un domaine est ajouté à la liste HSTS Preload, il est très difficile de l’en retirer. Cela signifie que toutes les connexions doivent rester en HTTPS pour toujours.

2. **Risques potentiels :**
   - Si le domaine ou un sous-domaine devient inaccessible via HTTPS (par exemple, certificat expiré), cela entraînera des erreurs critiques pour les utilisateurs.

3. **Meilleures pratiques :**
   - Toujours renouveler les certificats SSL/TLS à temps.
   - Vérifier régulièrement que tous les sous-domaines sont conformes à la politique HTTPS.

---

#### **6. Avantages d'utiliser la Liste HSTS Preload**
1. **Sécurité renforcée :**
   - Élimine totalement le risque d’une connexion HTTP initiale non sécurisée.
2. **Confiance des utilisateurs :**
   - Les utilisateurs sont assurés que leurs données sont protégées.
3. **Conformité :**
   - Répond aux exigences des normes modernes de sécurité web.

---

#### **Exemple Complet : Configuration NGINX pour HSTS Preload**

Voici une configuration complète pour un domaine avec HSTS Preload dans NGINX :

```nginx
server {
    listen 443 ssl;
    server_name example.com www.example.com;

    ssl_certificate /etc/nginx/ssl/example.com.crt;
    ssl_certificate_key /etc/nginx/ssl/example.com.key;

    # Activer HSTS avec Preload
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains; preload" always;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}

server {
    listen 80;
    server_name example.com www.example.com;

    # Redirection HTTP vers HTTPS
    return 301 https://$host$request_uri;
}
```

---

#### **7. Résumé**
- **HSTS Preload** garantit que les navigateurs exigent une connexion HTTPS dès le premier contact avec un domaine.
- Il est particulièrement utile pour éliminer les risques associés à la connexion initiale en HTTP.
- Une configuration correcte de HSTS avec `preload` est essentielle avant de soumettre le domaine.

Ce mécanisme est devenu un standard dans la sécurisation des sites web modernes.
