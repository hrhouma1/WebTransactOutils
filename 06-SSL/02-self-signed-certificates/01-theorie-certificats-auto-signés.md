### Cours sur les certificats auto-signés

#### Introduction aux certificats auto-signés

Les **certificats auto-signés** sont utilisés pour sécuriser les communications, en particulier dans les environnements de test et de développement. Contrairement aux certificats émis par une autorité de certification (CA), ils sont créés et signés par le propriétaire, ce qui signifie qu'ils ne sont pas reconnus comme fiables par les navigateurs ou autres systèmes de validation de confiance par défaut.

Dans ce cours, nous allons examiner les aspects suivants :
- Comment générer un certificat auto-signé ?
- Les algorithmes utilisés pour la création des clés et des certificats.
- Les performances et la sécurité des certificats en fonction de la longueur des clés.
- Comparaison des protocoles SSL/TLS, et impact sur les performances et la sécurité.

#### Génération d’un certificat auto-signé

##### 1. Création de la clé privée
La première étape consiste à générer une clé privée RSA ou ECDSA, les algorithmes les plus couramment utilisés pour les clés SSL/TLS.

```bash
openssl genpkey -algorithm RSA -out key.pem
```

##### 2. Génération d’un certificat auto-signé
Une fois la clé privée générée, un certificat auto-signé est créé :

```bash
openssl req -new -x509 -key key.pem -out cert.pem -days 365
```

#### Algorithmes utilisés pour les certificats

##### **RSA (Rivest-Shamir-Adleman)**

L'algorithme RSA est l'un des plus anciens et des plus utilisés pour le chiffrement à clé publique. Il repose sur la difficulté de factorisation des grands nombres premiers. La taille des clés RSA varie généralement de **1024 à 4096 bits**, bien que 2048 bits soit la norme.

- **Avantages** : Bonne compatibilité, sécurité éprouvée.
- **Inconvénients** : Lenteur pour les opérations de chiffrement et de déchiffrement comparée aux autres algorithmes modernes.

##### **ECDSA (Elliptic Curve Digital Signature Algorithm)**

L'algorithme ECDSA est basé sur les courbes elliptiques. Il offre une sécurité équivalente à RSA avec des clés beaucoup plus courtes, ce qui améliore les performances.

- **Avantages** : Sécurité forte avec des clés plus petites, plus rapide pour la signature.
- **Inconvénients** : Moins de compatibilité avec les anciens systèmes que RSA.

##### **Comparaison entre RSA et ECDSA**

| **Algorithme** | **Taille de la clé (bits)** | **Performance** | **Sécurité** |
|----------------|-----------------------------|-----------------|--------------|
| RSA            | 2048                        | Modéré          | Fort         |
| RSA            | 4096                        | Lent            | Très fort    |
| ECDSA          | 256                         | Très rapide     | Fort         |
| ECDSA          | 521                         | Rapide          | Très fort    |

#### Impact de la longueur des clés sur les performances et la sécurité

- **Sécurité** : Plus la clé est longue, plus le chiffrement est difficile à casser. Cependant, après un certain point, l'augmentation de la taille de la clé n'apporte qu'un faible gain de sécurité supplémentaire.
- **Performances** : L'augmentation de la taille des clés RSA entraîne une baisse des performances, en particulier pour les opérations de signature et de déchiffrement. Les clés plus longues nécessitent plus de ressources et de temps pour être traitées.

##### Exemple d'impact de la taille de la clé RSA sur les performances :

| **Taille de la clé** | **Temps de génération** | **Temps de chiffrement** | **Temps de déchiffrement** |
|----------------------|-------------------------|--------------------------|----------------------------|
| 1024 bits            | Très rapide             | Rapide                   | Rapide                     |
| 2048 bits            | Modéré                  | Modéré                   | Modéré                     |
| 4096 bits            | Lent                    | Très lent                | Très lent                  |

#### Protocoles SSL/TLS et certificats auto-signés

Les certificats SSL/TLS sont utilisés dans les protocoles SSL et TLS pour sécuriser les communications réseau. **TLS (Transport Layer Security)** est une version améliorée et plus sécurisée de SSL (Secure Sockets Layer). Voici les principales différences entre SSL et TLS :

| **Protocole** | **Version** | **Sécurité** | **Compatibilité** | **Performances** |
|---------------|-------------|--------------|-------------------|------------------|
| SSL           | 3.0         | Obsolète     | Très large        | Faible           |
| TLS           | 1.0         | Faible       | Large             | Modéré           |
| TLS           | 1.2         | Très forte   | Large             | Bonne            |
| TLS           | 1.3         | Optimisée    | Plus récente      | Très bonne       |

#### Comparaison entre les algorithmes, performances et sécurité

| **Algorithme** | **Taille de la clé** | **Sécurité**     | **Performance**  | **Utilisation typique** |
|----------------|----------------------|------------------|------------------|-------------------------|
| RSA            | 2048 bits            | Sécurité forte   | Modéré           | Web, Serveurs HTTPS      |
| RSA            | 4096 bits            | Très haute       | Lent             | Communications critiques |
| ECDSA          | 256 bits             | Sécurité forte   | Très rapide      | Appareils mobiles        |
| ECDSA          | 521 bits             | Très haute       | Rapide           | VPN, IoT                 |

#### Conclusion

- **RSA** : Adapté pour la compatibilité avec la plupart des systèmes. Cependant, ses performances se dégradent avec l'augmentation de la taille de la clé.
- **ECDSA** : Plus rapide avec une sécurité équivalente, surtout pour des clés plus petites. Il est idéal pour des environnements où la vitesse est cruciale, comme les appareils mobiles ou les systèmes embarqués.

**Protocole** : Il est préférable d'utiliser TLS 1.2 ou 1.3 pour garantir une sécurité maximale et de meilleures performances par rapport aux anciennes versions de SSL.

L'impact de l'augmentation de la taille des clés sur la sécurité est significatif, mais cela se fait au détriment des performances. Il faut donc trouver un équilibre entre sécurité et efficacité en fonction de vos besoins spécifiques.

#### Tableau comparatif des algorithmes et protocoles

| **Algorithme** | **Protocole** | **Taille de la clé** | **Sécurité**     | **Performance**  |
|----------------|---------------|----------------------|------------------|------------------|
| RSA            | SSL 3.0       | 2048 bits            | Modéré           | Modéré           |
| RSA            | TLS 1.2       | 4096 bits            | Très forte       | Lent             |
| ECDSA          | TLS 1.3       | 256 bits             | Très forte       | Très rapide      |
| ECDSA          | TLS 1.2       | 521 bits             | Très forte       | Rapide           |

En résumé, l'augmentation du nombre de bits améliore la sécurité mais peut ralentir les performances. Les algorithmes modernes comme ECDSA offrent une alternative plus rapide pour des niveaux de sécurité équivalents.
