------------------
------------------
------------------
# **Cours SSL/TLS - partie 01**
------------------
------------------
------------------


Ce paragraphe est conçu pour introduire les concepts de base de SSL/TLS, expliquer pourquoi ces technologies sont nécessaires, et exposer les solutions existantes avec des exemples pratiques.

---

# **1. Introduction : Qu’est-ce que SSL/TLS ?**
- **SSL (Secure Sockets Layer)** et **TLS (Transport Layer Security)** sont des protocoles qui sécurisent les communications sur Internet.
- Ils assurent :
  - **Confidentialité** : Les données échangées sont cryptées, donc illisibles par des tiers.
  - **Authenticité** : On s’assure que le site web est bien celui qu’il prétend être.
  - **Intégrité des données** : Les données ne peuvent pas être modifiées en transit.

---

# **2. Pourquoi avons-nous besoin de SSL/TLS ?**

- **Problème sans SSL/TLS** :
  - Les communications non sécurisées (HTTP) peuvent être interceptées, modifiées ou volées par des attaquants.
  - Exemple : Sur un réseau Wi-Fi public, quelqu’un peut voler vos identifiants.

- **Solution avec SSL/TLS** :
  - Les données sont **chiffrées** (cryptées), donc même si elles sont interceptées, elles restent illisibles.
  - Les certificats garantissent que vous communiquez avec le bon serveur.

---

# **3. Concepts de base**

## **3.1 Les notions clés**
- **HTTPS** : Une version sécurisée de HTTP qui utilise SSL/TLS pour chiffrer les communications.
- **Certificat numérique** : Document électronique qui prouve l'identité d'un site web.
- **CA (Certificate Authority)** : Une autorité de certification qui émet des certificats reconnus par les navigateurs.
- **Handshake TLS** : Processus qui établit une connexion sécurisée entre un client (navigateur) et un serveur.

---

## **3.2 Les étapes d’une communication SSL/TLS**

1. **Demande de connexion** :
   - Le navigateur (client) se connecte au serveur et demande un certificat.
2. **Vérification du certificat** :
   - Le navigateur vérifie que le certificat est valide et émis par une CA reconnue.
3. **Échange de clés** :
   - Une clé de session est générée pour chiffrer les données.
4. **Communication sécurisée** :
   - Les données sont échangées de manière chiffrée.

---

# **4. Types de certificats SSL/TLS**

1. **Certificat auto-signé** :
   - Créé par le serveur lui-même sans vérification externe.
   - Avantages : Gratuit et rapide à mettre en place.
   - Inconvénients : Non reconnu par les navigateurs, donc pas recommandé pour un site web public.

2. **Certificat signé par une CA** :
   - Émis par une autorité de certification reconnue.
   - Requis pour les sites web publics.
   - Types :
     - **DV (Domain Validation)** : Vérifie seulement la propriété du domaine.
     - **OV (Organization Validation)** : Vérifie également l’identité de l’organisation.
     - **EV (Extended Validation)** : Offre la validation la plus stricte (barre verte dans les navigateurs, bien que ce soit moins courant aujourd’hui).

---

# **5. Pourquoi utiliser un certificat ?**
- **Authentifier le site web** : Le certificat prouve que le site est légitime.
- **Protéger les utilisateurs** : Les données sensibles (mots de passe, informations bancaires) sont chiffrées.
- **Améliorer le SEO** : Google favorise les sites utilisant HTTPS.
- **Éviter les alertes** : Les navigateurs modernes marquent les sites sans HTTPS comme "non sécurisés".

---

# **6. Introduction à Certbot et Let's Encrypt**

1. **Certbot** :
   - Outil open-source pour obtenir et gérer des certificats SSL/TLS gratuits de Let's Encrypt.
   - Automatisation de la configuration et du renouvellement.

2. **Let's Encrypt** :
   - Une CA gratuite et automatisée.
   - Fournit des certificats reconnus par tous les navigateurs modernes.

---

# **7. Solutions équivalentes à Certbot**

| **Solution**        | **Avantages**                                  | **Inconvénients**                           |
|---------------------|-----------------------------------------------|--------------------------------------------|
| **Certbot**         | Gratuit, automatisé, facile à utiliser        | Support limité à certaines plateformes      |
| **Acme.sh**         | Léger, flexible                               | Plus complexe à configurer                 |
| **Caddy**           | Serveur web avec certificats intégrés         | Moins utilisé pour de grandes installations |
| **Outils payants**  | Support technique, fonctionnalités avancées   | Coûts élevés                               |

---

# **8. Comparatif entre les certificats auto-signés et signés par CA**

| **Critère**                  | **Certificat Auto-signé** | **Certificat signé par CA** |
|------------------------------|---------------------------|-----------------------------|
| **Fiabilité**                | Non reconnu              | Reconnu par les navigateurs |
| **Coût**                     | Gratuit                  | Gratuit (Let's Encrypt) ou payant |
| **Utilisation recommandée**  | Tests ou interne         | Sites publics               |

---

# **9. Mise en pratique : Installation de Certbot**

1. **Installation** (par exemple sur Ubuntu) :
   ```bash
   sudo apt update
   sudo apt install certbot python3-certbot-nginx
   ```

2. **Obtention d’un certificat** :
   ```bash
   sudo certbot --nginx
   ```

3. **Renouvellement automatique** :
   - Ajout automatique d’une tâche cron par Certbot.
   - Tester avec :
     ```bash
     sudo certbot renew --dry-run
     ```

---

# **10. Problèmes courants et solutions**

| **Problème**                        | **Solution**                                             |
|-------------------------------------|---------------------------------------------------------|
| "Certificat non valide"             | Vérifier l’expiration ou la configuration du domaine.   |
| "Certificat auto-signé non fiable" | Utiliser un certificat Let's Encrypt ou commercial.    |
| Erreur de renouvellement automatique | Vérifier les autorisations ou la configuration DNS.     |

---

# **Résumé**
- SSL/TLS est essentiel pour sécuriser les communications sur Internet.
- Certbot et Let's Encrypt sont des solutions simples et gratuites pour mettre en place HTTPS.
- Choisissez le bon type de certificat selon vos besoins (DV, OV, EV).

