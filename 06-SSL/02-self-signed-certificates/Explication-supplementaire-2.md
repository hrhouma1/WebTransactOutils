# Processus et relations entre chaque élément (CA, serveur, client) et leurs interactions.

### Schéma en ASCII du Workflow des certificats

```plaintext
                    +---------------------------+
                    | Autorité de Certification  |
                    |       (CA)                 |
                    |--------------------------- |
                    |  Clé privée : ca-key.pem    |
                    |  Certificat : ca-cert.pem   |
                    +----------------------------+
                               |
              (Signé par la CA)|        
                               v
                    +---------------------------+
                    |         Serveur            |
                    |----------------------------|
                    |  Clé privée : server-key.pem|
                    |  Certificat : server-cert.pem|
                    +----------------------------+
                               ^
                               |
              (Signé par la CA)|
                               v
                    +---------------------------+
                    |         Client             |
                    |----------------------------|
                    |  Clé privée : client-key.pem|
                    |  Certificat : client-cert.pem|
                    +----------------------------+
```

### Workflow expliqué étape par étape

#### **Étape 1 : Création de l'Autorité de Certification (CA)**

1. **Générer une clé privée pour la CA :**
   - Cette clé privée sera utilisée pour signer les certificats du serveur et du client.
   
   ```bash
   openssl genrsa 2048 > ca-key.pem
   ```

2. **Créer le certificat auto-signé de la CA :**
   - Ce certificat est auto-signé, car la CA est la seule à valider les autres entités (serveur et client). Il sera utilisé pour vérifier les certificats des autres.
   
   ```bash
   openssl req -new -x509 -key ca-key.pem -out ca-cert.pem -days 365
   ```

#### **Étape 2 : Création du certificat du Serveur**

1. **Générer une clé privée pour le serveur :**
   - Le serveur génère sa propre clé privée, qui sera utilisée pour chiffrer ses communications.
   
   ```bash
   openssl genrsa 2048 > server-key.pem
   ```

2. **Générer une requête de signature de certificat (CSR) pour le serveur :**
   - Le serveur demande à la CA de signer son certificat. C'est ce qu'on appelle une requête de signature (CSR).
   
   ```bash
   openssl req -new -key server-key.pem -out server-req.pem
   ```

3. **Signer la requête du serveur avec la CA pour générer le certificat :**
   - La CA signe la requête du serveur, et cela génère le certificat du serveur.
   
   ```bash
   openssl x509 -req -in server-req.pem -CA ca-cert.pem -CAkey ca-key.pem -out server-cert.pem -days 365 -set_serial 01
   ```

#### **Étape 3 : Création du certificat du Client**

1. **Générer une clé privée pour le client :**
   - Comme pour le serveur, le client génère sa propre clé privée pour sécuriser ses communications.
   
   ```bash
   openssl genrsa 2048 > client-key.pem
   ```

2. **Générer une requête de signature de certificat (CSR) pour le client :**
   - Le client, comme le serveur, fait une demande à la CA pour que son certificat soit signé.
   
   ```bash
   openssl req -new -key client-key.pem -out client-req.pem
   ```

3. **Signer la requête du client avec la CA pour générer le certificat :**
   - La CA signe la requête du client, ce qui génère le certificat du client.
   
   ```bash
   openssl x509 -req -in client-req.pem -CA ca-cert.pem -CAkey ca-key.pem -out client-cert.pem -days 365 -set_serial 02
   ```

#### **Étape 4 : Vérification des certificats**

1. **Vérification du certificat du serveur :**
   - On vérifie que le certificat du serveur a bien été signé par la CA.
   
   ```bash
   openssl verify -CAfile ca-cert.pem server-cert.pem
   ```

2. **Vérification du certificat du client :**
   - De la même manière, on vérifie que le certificat du client est valide.
   
   ```bash
   openssl verify -CAfile ca-cert.pem client-cert.pem
   ```

### Résumé des fichiers générés

- **Clés privées** :
  - `ca-key.pem` : clé privée de l'autorité de certification (CA).
  - `server-key.pem` : clé privée du serveur.
  - `client-key.pem` : clé privée du client.

- **Certificats** :
  - `ca-cert.pem` : certificat auto-signé de l'autorité de certification (CA).
  - `server-cert.pem` : certificat signé pour le serveur.
  - `client-cert.pem` : certificat signé pour le client.

### Conclusion

Chaque entité (serveur et client) dispose d'une clé privée et d'un certificat signé par la CA. Lors des échanges, le serveur et le client peuvent s'authentifier mutuellement en vérifiant que leurs certificats ont été signés par la même CA. Les clés privées ne sont jamais partagées et restent secrètes pour chaque entité.

