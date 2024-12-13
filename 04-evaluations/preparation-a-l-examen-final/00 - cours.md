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
- **`preload`** : Permet au domaine d’être ajouté à la liste HSTS Preload des navigateurs.

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
