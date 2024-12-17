
# Partie 02 - **Questions de Développement : En-têtes HTTP de Sécurité**

---

### **Question 1 : Analyse et Correction d’une Configuration Défaillante**  
Un administrateur système a configuré les en-têtes HTTP pour sécuriser un site web. Voici la configuration actuelle dans Nginx :  

```nginx
server {
    listen 443 ssl;
    server_name example.com;

    ssl_certificate /etc/nginx/ssl/example.crt;
    ssl_certificate_key /etc/nginx/ssl/example.key;

    add_header X-Frame-Options "ALLOW-FROM https://another-site.com";
    add_header Content-Security-Policy "default-src *; script-src 'self'";
    add_header Strict-Transport-Security "max-age=600";
    add_header Referrer-Policy "unsafe-url";
    add_header X-Content-Type-Options "nosniff";
}
```

**Tâches :**
1. **Identifiez les erreurs ou mauvaises pratiques** dans cette configuration.  
2. **Proposez une version améliorée et sécurisée** du fichier de configuration Nginx avec des explications pour chaque modification.  

---

### **Question 2 : Scénario Pratique - Protection Contre XSS et Clickjacking**  
Un développeur web travaille sur un site de e-commerce permettant aux utilisateurs d’ajouter des commentaires sur les produits. Lors d’un test de sécurité, il a été constaté que le site est vulnérable aux attaques XSS (Cross-Site Scripting) et Clickjacking.  

**Tâches :**  
1. Expliquez **comment les en-têtes HTTP** peuvent être utilisés pour protéger le site contre ces attaques spécifiques.  
2. Rédigez les configurations nécessaires dans Nginx pour :  
   - Empêcher les attaques **XSS** à l’aide de Content-Security-Policy.  
   - Bloquer les attaques **Clickjacking** à l’aide de X-Frame-Options.  

---

### **Consignes :**  
- Répondez de manière structurée, en expliquant **chaque concept** et en justifiant vos choix.  
- Utilisez des exemples concrets et des configurations claires pour montrer votre compréhension.  

**Bonne rédaction !** 😊
