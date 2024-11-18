### Introduction à SSL/TLS et Certbot

Le protocole **SSL (Secure Sockets Layer)** et son successeur **TLS (Transport Layer Security)** assurent une communication sécurisée sur Internet. Ils permettent de chiffrer les échanges entre un client (navigateur) et un serveur, protégeant ainsi la confidentialité et l'intégrité des données.

---

### **Les bases de SSL/TLS**
1. **Objectifs principaux** :
   - **Chiffrement** : Garantir que les données échangées restent privées.
   - **Authentification** : Assurer que le serveur est bien celui qu'il prétend être.
   - **Intégrité des données** : Garantir que les données n'ont pas été altérées en transit.

2. **Comment fonctionne SSL/TLS** :
   - Utilisation de **certificats numériques** pour authentifier les parties.
   - Établissement d'une **connexion sécurisée** via une négociation appelée **handshake TLS**.
   - Les données sont ensuite chiffrées avec des clés symétriques pour des performances optimales.

---

### **Certificats numériques**
Un certificat numérique est un document électronique utilisé pour prouver l'identité d'une entité (un site web, une entreprise, etc.).

1. **Certificat auto-signé** :
   - Créé par l'entité elle-même sans intervention d'une autorité tierce.
   - Utilisé principalement à des fins de test ou pour des environnements internes.
   - Inconvénient : Les navigateurs le marquent comme non fiable.

2. **Certificat signé par une Autorité de Certification (CA)** :
   - Délivré par une **CA (Certificate Authority)**, comme Let's Encrypt, DigiCert, ou GlobalSign.
   - Reconnus comme fiables par les navigateurs.
   - Fournit une authentification et une reconnaissance par les systèmes externes.

3. **Certificats SSL/TLS** :
   - **DV (Domain Validation)** : Valide uniquement la propriété du domaine.
   - **OV (Organization Validation)** : Vérifie également l'existence de l'organisation.
   - **EV (Extended Validation)** : Vérification approfondie, souvent utilisée pour les entreprises.

---

### **Certbot**
Certbot est un outil gratuit et open source développé par l'EFF pour automatiser la génération et le renouvellement de certificats SSL/TLS auprès de **Let's Encrypt**.

1. **Installation et configuration de Certbot** :
   - Installez Certbot via votre gestionnaire de paquets (apt, yum, etc.).
   - Utilisez la commande suivante pour obtenir et configurer un certificat :
     ```bash
     sudo certbot --apache
     # ou
     sudo certbot --nginx
     ```
   - Certbot configure automatiquement votre serveur web pour qu'il utilise HTTPS.

2. **Renouvellement automatique** :
   - Let's Encrypt délivre des certificats valides pendant 90 jours.
   - Certbot ajoute une tâche cron pour les renouveler automatiquement.

---

### **Outils équivalents à Certbot**
1. **Acme.sh** : Client ACME léger écrit en bash.
2. **Dehydrated** : Script ACME simple et minimaliste.
3. **lego** : Client ACME en Go, compatible avec plusieurs serveurs DNS.
4. **Caddy** : Serveur web avec SSL/TLS intégré (certificats Let's Encrypt automatiques).

---

### **Comparatif des solutions SSL/TLS**

| **Caractéristique**            | **Certbot**       | **Acme.sh**     | **Caddy**        | **Certificat auto-signé** |
|---------------------------------|-------------------|-----------------|------------------|---------------------------|
| **Gratuité**                   | ✅                | ✅              | ✅               | ✅                        |
| **Configuration automatique**  | ✅ (Apache/Nginx) | ❌              | ✅ (serveur web) | ❌                        |
| **Autorité de certification**  | Let's Encrypt     | Let's Encrypt   | Let's Encrypt    | Non                       |
| **Renouvellement automatique** | ✅                | ✅              | ✅               | ❌                        |
| **Utilisation en production**  | ✅                | ✅              | ✅               | ❌ (non recommandé)       |

---

### Exemple d'un certificat auto-signé

Pour créer un certificat auto-signé sous Linux :
```bash
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout selfsigned.key -out selfsigned.crt
```

### Comparaison : Certificat auto-signé vs Certificat signé par CA

| **Critère**                  | **Certificat Auto-signé** | **Certificat signé par CA** |
|------------------------------|---------------------------|-----------------------------|
| **Fiabilité**                | Faible                   | Élevée                     |
| **Reconnaissance des navigateurs** | ❌                      | ✅                          |
| **Coût**                     | Gratuit                  | Gratuit (Let's Encrypt) ou payant |
| **Complexité de configuration** | Faible                  | Moyenne                    |
| **Utilisation recommandée**  | Tests/Environnements internes | Production                  |

---

### Conclusion
- Pour des environnements de production, utilisez un certificat signé par une **CA** comme Let's Encrypt via Certbot.
- Les certificats auto-signés sont utiles uniquement pour des tests ou pour des réseaux internes non accessibles publiquement.

