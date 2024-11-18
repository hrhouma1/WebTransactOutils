# Comprendre la Création et l'Utilisation de Certificats Auto-Signés avec OpenSSL : Étapes et Workflow Détaillés

### Workflow simplifié avec une Autorité de Certification (CA)

#### Rôle de chaque entité :
1. **CA (Autorité de Certification)** : C'est elle qui signe les certificats pour garantir l'identité des serveurs et des clients. Son rôle est de délivrer des certificats de manière vérifiée.
2. **Serveur** : Il génère une clé privée et demande un certificat à la CA pour prouver son identité aux clients.
3. **Client** : Comme le serveur, il génère une clé privée et demande à la CA un certificat pour prouver son identité au serveur (cela peut être optionnel selon les besoins).

### Étapes détaillées du processus

1. **Génération de la clé privée de la CA** (`ca-key.pem`):
   - La CA génère d'abord sa propre clé privée. Cette clé est utilisée pour signer les certificats des autres entités (serveur, client).
   - Commande :
     ```bash
     openssl genrsa -out ca-key.pem 2048
     ```

2. **Création du certificat auto-signé de la CA** (`ca-cert.pem`):
   - La CA génère ensuite son certificat auto-signé. Ce certificat est utilisé pour prouver que la CA est fiable. C'est ce certificat que les autres entités (serveur, client) utiliseront pour vérifier que leurs certificats sont authentiques.
   - Commande :
     ```bash
     openssl req -new -x509 -key ca-key.pem -out ca-cert.pem -days 365
     ```

#### Serveur

3. **Génération de la clé privée du serveur** (`server-key.pem`):
   - Le serveur génère sa propre clé privée. Cette clé reste confidentielle et sert à chiffrer et déchiffrer les communications.
   - Commande :
     ```bash
     openssl genrsa -out server-key.pem 2048
     ```

4. **Création de la requête de signature de certificat (CSR) pour le serveur** (`server-req.pem`):
   - Le serveur génère une requête de signature de certificat (CSR), qui contient sa clé publique et des informations sur son identité. Cette requête est envoyée à la CA pour être signée.
   - Commande :
     ```bash
     openssl req -new -key server-key.pem -out server-req.pem
     ```

5. **Signature du certificat du serveur par la CA** (`server-cert.pem`):
   - La CA prend la requête de signature du serveur (CSR) et signe un certificat pour le serveur, confirmant ainsi son identité.
   - Commande :
     ```bash
     openssl x509 -req -in server-req.pem -CA ca-cert.pem -CAkey ca-key.pem -out server-cert.pem -days 365 -set_serial 01
     ```

#### Client (Optionnel selon les besoins)

6. **Génération de la clé privée du client** (`client-key.pem`):
   - Le client génère également sa propre clé privée.
   - Commande :
     ```bash
     openssl genrsa -out client-key.pem 2048
     ```

7. **Création de la requête de signature de certificat (CSR) pour le client** (`client-req.pem`):
   - Comme pour le serveur, le client génère une CSR et l’envoie à la CA pour être signée.
   - Commande :
     ```bash
     openssl req -new -key client-key.pem -out client-req.pem
     ```

8. **Signature du certificat du client par la CA** (`client-cert.pem`):
   - La CA signe également la requête du client et lui délivre un certificat.
   - Commande :
     ```bash
     openssl x509 -req -in client-req.pem -CA ca-cert.pem -CAkey ca-key.pem -out client-cert.pem -days 365 -set_serial 02
     ```

#### Communication sécurisée

9. **Établissement d'une connexion sécurisée** :
   - Une fois que le serveur et le client ont leurs certificats (signés par la CA), ils peuvent établir une communication sécurisée.
   - Le client utilise le certificat du serveur pour vérifier son identité et chiffrer les communications. Si le client utilise aussi un certificat, le serveur peut également vérifier son identité, ce qu'on appelle l'authentification mutuelle (mutual TLS).

### Pour Résumer

- **Client** et **serveur** génèrent chacun une clé privée et demandent un certificat (CSR) à l'autorité de certification (CA).
- **La CA** signe ces certificats pour valider l'identité du serveur et du client.
- **Le certificat du serveur** prouve son identité au client. Le client vérifie ce certificat en utilisant le certificat de la CA.
- Si le client dispose également d’un certificat, le serveur peut vérifier l'identité du client.

### Schéma simplifié

```plaintext
                         +---------------------------+
                         |    Autorité de            |
                         |  Certification (CA)       |
                         |                           |
                         |  ca-key.pem (Clé privée)  |
                         |  ca-cert.pem (Certificat) |
                         +---------------------------+
                                  | (Signe les CSR)
                                  v
              +-----------------------------------------+
              | Serveur                                 |
              |                                         |
              |  server-key.pem (Clé privée)            |
              |  server-req.pem (CSR)                   |
              |  server-cert.pem (Certificat signé)     |
              +-----------------------------------------+
                         ^
                         |  (Signe les CSR)
                         |
              +-----------------------------------------+
              | Client                                  |
              |                                         |
              |  client-key.pem (Clé privée)            |
              |  client-req.pem (CSR)                   |
              |  client-cert.pem (Certificat signé)     |
              +-----------------------------------------+
```

### Conclusion

- **Client et serveur demandent leurs certificats à la CA.**
- **La CA valide les certificats en les signant.**
- **Le serveur et le client peuvent ensuite s'authentifier mutuellement grâce à leurs certificats signés.**

