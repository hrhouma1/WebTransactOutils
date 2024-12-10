![image](https://github.com/user-attachments/assets/4423bbe3-8814-4685-9a9f-40bcf7223495)

- Ce rapport est directement lié aux en-têtes de sécurité dont nous avons parlé ! 
- Voici une explication pour t'aider à comprendre ce que signifie chaque point dans le rapport et comment le corriger :


Oui, ce rapport est directement lié aux **en-têtes de sécurité** dont nous avons parlé ! Voici une explication pour t'aider à comprendre ce que signifie chaque point dans le rapport et comment le corriger :

---

### **1. Strict-Transport-Security (HSTS)**
- **Problème détecté :** Cet en-tête manque sur ton site.
- **Qu’est-ce que c’est ?**  
  L’en-tête HTTP Strict-Transport-Security (HSTS) force les navigateurs à n'accéder à ton site que via HTTPS (connexion sécurisée). Cela empêche les attaques de type "downgrade" où un pirate essaie de rediriger un utilisateur vers une version non sécurisée de ton site.
- **Valeur recommandée :**  
  ```nginx
  add_header Strict-Transport-Security "max-age=31536000; includeSubDomains";
  ```
  - **`max-age=31536000` :** Garde la politique active pendant 1 an (31536000 secondes).
  - **`includeSubDomains` :** Applique aussi cette règle aux sous-domaines.

---

### **2. Content-Security-Policy (CSP)**
- **Problème détecté :** L'en-tête manque.
- **Qu’est-ce que c’est ?**  
  Cet en-tête empêche le chargement de scripts, images ou ressources malveillantes sur ton site. Il limite strictement ce que le navigateur est autorisé à charger.
- **Valeur recommandée (exemple basique) :**  
  ```nginx
  add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'";
  ```
  - **`default-src 'self'` :** Autorise seulement les ressources de ton propre site.
  - **`script-src 'self'` :** Charge uniquement les scripts locaux.
  - **`style-src 'self'` :** Charge uniquement les fichiers CSS locaux.

---

### **3. X-Frame-Options**
- **Problème détecté :** L'en-tête manque.
- **Qu’est-ce que c’est ?**  
  Cet en-tête empêche d'intégrer ton site dans des "frames" ou "iframes", ce qui peut éviter les attaques de type **clickjacking**.
- **Valeur recommandée :**  
  ```nginx
  add_header X-Frame-Options "SAMEORIGIN";
  ```

---

### **4. X-Content-Type-Options**
- **Problème détecté :** L'en-tête manque.
- **Qu’est-ce que c’est ?**  
  Empêche le navigateur de deviner le type des fichiers (par exemple, un fichier malveillant déguisé en image).
- **Valeur recommandée :**  
  ```nginx
  add_header X-Content-Type-Options "nosniff";
  ```

---

### **5. Referrer-Policy**
- **Problème détecté :** L'en-tête manque.
- **Qu’est-ce que c’est ?**  
  Contrôle la quantité d'informations que ton site partage lorsqu'un utilisateur clique sur un lien vers une autre page ou un autre site.
- **Valeur recommandée :**  
  ```nginx
  add_header Referrer-Policy "strict-origin-when-cross-origin";
  ```

---

### **6. Permissions-Policy**
- **Problème détecté :** L'en-tête manque.
- **Qu’est-ce que c’est ?**  
  Cet en-tête contrôle les fonctionnalités et les API accessibles sur ton site (comme la caméra, le micro, ou le GPS). Par exemple, tu peux limiter l’accès à ces fonctionnalités aux utilisateurs autorisés.
- **Valeur recommandée :**  
  ```nginx
  add_header Permissions-Policy "geolocation=(), microphone=(), camera=()";
  ```
  - **`geolocation=()` :** Désactive la géolocalisation.
  - **`microphone=()` :** Désactive l'accès au microphone.
  - **`camera=()` :** Désactive l'accès à la caméra.

---

### **Comment corriger cela ?**
1. **Ouvre le fichier de configuration Nginx de ton site :**
   ```bash
   sudo nano /etc/nginx/sites-available/ai-insighter.com
   ```

2. **Ajoute les en-têtes de sécurité dans le bloc `server {}` :**
   ```nginx
   server {
       listen 80;
       server_name ai-insighter.com www.ai-insighter.com;

       # En-têtes de sécurité
       add_header Strict-Transport-Security "max-age=31536000; includeSubDomains";
       add_header Content-Security-Policy "default-src 'self'; script-src 'self'; style-src 'self'";
       add_header X-Frame-Options "SAMEORIGIN";
       add_header X-Content-Type-Options "nosniff";
       add_header Referrer-Policy "strict-origin-when-cross-origin";
       add_header Permissions-Policy "geolocation=(), microphone=(), camera=()";

       root /var/www/ai-insighter.com;
       index index.html;
   }
   ```

3. **Redémarre le serveur Nginx pour appliquer les changements :**
   ```bash
   sudo systemctl restart nginx
   ```

---

### **Validation**
Après avoir ajouté ces en-têtes, utilise à nouveau l'outil de vérification ou la commande suivante pour confirmer qu'ils sont actifs :
```bash
curl -I https://www.ai-insighter.com
```

Tu devrais maintenant voir tous les en-têtes de sécurité appliqués et ton score de sécurité devrait s’améliorer considérablement ! 🎉
