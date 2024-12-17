
# **Quiz Final : HTTPS, SSL/TLS, Let's Encrypt et En-têtes HTTP de Sécurité**  

**Instructions :**  
- Chaque question possède **une seule réponse correcte**.  
- Lisez attentivement chaque réponse. Certaines peuvent sembler correctes, mais il y a **des pièges**.  



---

### **Question 1 : Objectif principal de HTTPS**  
**Quel est le principal avantage de l’utilisation de HTTPS ?**  
a) Améliorer la vitesse de chargement des pages web  
b) Chiffrer les échanges de données entre le navigateur et le serveur  
c) Bloquer les attaques XSS automatiquement  
d) Permettre l’utilisation d’un certificat SSL pour HTTP  

---

### **Question 2 : Durée de validité d’un certificat Let's Encrypt**  
**Quelle est la durée de validité d’un certificat Let's Encrypt ?**  
a) 30 jours  
b) 60 jours  
c) 90 jours  
d) 1 an  

---

### **Question 3 : HSTS (Strict-Transport-Security)**  
**Quel est le rôle principal de l’en-tête HSTS ?**  
a) Empêcher les attaques de type "downgrade" en forçant HTTPS  
b) Bloquer l’exécution des scripts inline malveillants  
c) Autoriser uniquement les frames provenant du même domaine  
d) Limiter les informations transmises via le header Referrer  

---

### **Question 4 : Content-Security-Policy (CSP)**  
**Comment CSP aide-t-il à prévenir les attaques XSS ?**  
a) En forçant l’utilisation de HTTPS pour tous les contenus  
b) En limitant les sources autorisées pour les scripts et ressources  
c) En empêchant les navigateurs de deviner le type MIME des fichiers  
d) En bloquant les frames externes non autorisées  

---

### **Question 5 : Commande Certbot**  
**Quelle commande permet de tester le renouvellement automatique des certificats Let's Encrypt ?**  
a) `certbot renew`  
b) `certbot renew --dry-run`  
c) `certbot --force-renew`  
d) `certbot test-renew`  

---

### **Question 6 : X-Frame-Options**  
**Quel en-tête HTTP empêche l’intégration d’un site dans une iframe non autorisée ?**  
a) X-Frame-Options  
b) Content-Security-Policy  
c) Referrer-Policy  
d) X-Content-Type-Options  

---

### **Question 7 : X-Content-Type-Options**  
**Quel problème l’en-tête X-Content-Type-Options résout-il ?**  
a) Les attaques XSS  
b) Les erreurs d’interprétation des types MIME par le navigateur  
c) Les attaques par force brute sur les mots de passe  
d) Les fuites d’informations via le Referrer  

---

### **Question 8 : Redirection HTTPS dans Nginx**  
**Quelle configuration permet de rediriger automatiquement le trafic HTTP vers HTTPS dans Nginx ?**  
a) `listen 443 ssl;`  
b) `return 301 https://$host$request_uri;`  
c) `force-ssl on;`  
d) `ssl_redirect true;`  

---

### **Question 9 : Let's Encrypt – Port utilisé**  
**Quel port doit être ouvert pour que Let's Encrypt fonctionne avec le protocole HTTP-01 ?**  
a) Port 22  
b) Port 80  
c) Port 443  
d) Port 8080  

---

### **Question 10 : Referrer-Policy**  
**Quel est l’objectif principal de l’en-tête Referrer-Policy ?**  
a) Bloquer les scripts inline malveillants  
b) Protéger la vie privée en limitant les informations envoyées sur les requêtes HTTP  
c) Forcer l’utilisation de HTTPS pour toutes les requêtes  
d) Limiter l’accès aux ressources sensibles du navigateur  



**Bonne chance !** 😊
