# **Cours : Notions de Sécurité Informatique et Chiffrement**

Ce cours présente les **principes fondamentaux de la sécurité informatique** et une introduction aux **concepts de chiffrement**, deux piliers essentiels pour protéger les systèmes et les données dans le monde numérique.

---

## **1. Sécurité Informatique : Notions Fondamentales**

### **1.1. Enjeux de la Sécurité Informatique**

La sécurité informatique vise à **protéger les systèmes, les réseaux et les données** contre les menaces et les vulnérabilités. Elle est devenue un enjeu critique dans un monde hyper-connecté.

#### **Enjeux principaux :**
1. **Protection des données personnelles :**  
   Les réglementations comme le RGPD imposent la protection des données sensibles.
   
2. **Continuité des activités :**  
   Les entreprises doivent protéger leurs systèmes pour éviter les interruptions.

3. **Conformité légale :**  
   Respecter les lois sur la protection des données et les cyberattaques.

4. **Réputation :**  
   Une violation de données peut nuire à la confiance des utilisateurs et à l'image de l'organisation.

5. **Propriété intellectuelle :**  
   Les organisations doivent protéger leurs secrets industriels contre l'espionnage.

---

### **1.2. Principaux Objectifs de la Sécurité**

Les objectifs fondamentaux de la sécurité informatique sont souvent résumés par le **triangle CIA** :

1. **Confidentialité** :  
   Empêcher l'accès non autorisé aux données sensibles.
   - Exemple : Chiffrement des fichiers pour protéger les informations bancaires.

2. **Intégrité** :  
   Garantir que les données ne sont pas altérées ou modifiées sans autorisation.
   - Exemple : Hachage des fichiers pour détecter les modifications.

3. **Disponibilité** :  
   Assurer que les systèmes et données restent accessibles en cas de besoin.
   - Exemple : Utiliser des systèmes redondants pour prévenir les pannes.

---

### **1.3. Menaces et Vulnérabilités**

#### **Menaces :**
1. **Cyberattaques** :
   - **Phishing** : Tromper les utilisateurs pour obtenir leurs informations.
   - **Malwares** : Logiciels malveillants comme les virus et ransomwares.
   - **Attaques DDoS** : Saturation des serveurs pour les rendre indisponibles.

2. **Erreurs humaines** :
   - Mauvais paramétrages, mots de passe faibles, ou partage d'informations sensibles.

3. **Espionnage** :
   - Piratage pour voler des secrets industriels ou gouvernementaux.

#### **Vulnérabilités :**
1. **Failles logicielles** :  
   Bugs ou faiblesses exploitables dans des logiciels ou systèmes.

2. **Mauvaises configurations** :  
   Ports ouverts inutiles, mots de passe par défaut.

3. **Absence de mises à jour** :  
   Des systèmes obsolètes sont vulnérables à des exploits connus.

---

### **1.4. Mesures de Protection**

Pour se défendre contre les menaces, plusieurs mesures peuvent être adoptées :

#### **1. Mesures techniques :**
- **Pare-feu** : Filtrer les connexions entrantes et sortantes.
- **Antivirus** : Détecter et supprimer les malwares.
- **Chiffrement** : Protéger les données pendant leur stockage et leur transmission.
- **Mises à jour** : Corriger les failles de sécurité des logiciels.

#### **2. Mesures organisationnelles :**
- **Sensibilisation** : Former les utilisateurs à reconnaître les menaces comme le phishing.
- **Politiques de sécurité** : Établir des règles claires pour l'utilisation des systèmes.

#### **3. Mesures physiques :**
- **Contrôle d'accès** : Sécuriser les locaux avec des badges ou des clés.
- **Surveillance vidéo** : Prévenir les intrusions physiques.

---

## **2. Notions de Chiffrement**

Le **chiffrement** est une technique utilisée pour transformer des données lisibles (**texte en clair**) en une version illisible (**texte chiffré**) afin de protéger leur confidentialité.

---

### **2.1. Fonctions du Chiffrement**

1. **Confidentialité** :
   Empêcher l’accès non autorisé aux données.

2. **Authenticité** :
   Vérifier l’identité de l’expéditeur des données.

3. **Intégrité** :
   S’assurer que les données n’ont pas été modifiées pendant la transmission.

4. **Non-répudiation** :
   Garantir que l’expéditeur ne peut nier avoir envoyé les données.

---

### **2.2. Algorithmes de Chiffrement**

Les algorithmes de chiffrement sont des formules mathématiques utilisées pour chiffrer et déchiffrer les données. Ils se divisent en deux catégories principales :

#### **1. Chiffrement Symétrique** :
- **Définition** : Utilise une seule clé pour chiffrer et déchiffrer les données.
- **Exemples d'algorithmes** :
  - **AES (Advanced Encryption Standard)** : Norme utilisée dans de nombreux systèmes.
  - **DES (Data Encryption Standard)** : Ancien standard, moins sécurisé.
  - **Blowfish** : Rapide et sécurisé.
- **Avantages** :
  - Rapide et efficace pour de grandes quantités de données.
- **Inconvénients** :
  - La clé doit être partagée entre les parties, ce qui pose un problème de distribution.

#### **2. Chiffrement Asymétrique** :
- **Définition** : Utilise deux clés distinctes : une clé publique pour le chiffrement et une clé privée pour le déchiffrement.
- **Exemples d'algorithmes** :
  - **RSA (Rivest-Shamir-Adleman)** : Couramment utilisé pour sécuriser les communications.
  - **ECC (Elliptic Curve Cryptography)** : Plus rapide et efficace que RSA pour certaines applications.
- **Avantages** :
  - Pas besoin de partager la clé privée.
  - Idéal pour les échanges sécurisés entre parties inconnues.
- **Inconvénients** :
  - Plus lent que le chiffrement symétrique.

---

### **2.3. Comparaison : Symétrique vs Asymétrique**

| **Aspect**         | **Symétrique**                  | **Asymétrique**                |
|---------------------|---------------------------------|---------------------------------|
| **Nombre de clés**  | Une seule clé partagée         | Une clé publique et une privée |
| **Vitesse**         | Très rapide                   | Plus lent                      |
| **Utilisation**     | Chiffrement des données volumineuses | Échange de clés, signatures   |

---

### **2.4. Applications Pratiques du Chiffrement**

1. **HTTPS** (HyperText Transfer Protocol Secure) :
   - Utilise le chiffrement asymétrique pour établir une connexion sécurisée, puis symétrique pour transmettre les données.

2. **VPN** (Virtual Private Network) :
   - Chiffre le trafic réseau pour garantir la confidentialité.

3. **Messageries sécurisées** :
   - Applications comme Signal utilisent des algorithmes asymétriques pour échanger des clés, puis symétriques pour le contenu.

4. **Stockage sécurisé** :
   - Les disques durs ou bases de données peuvent être chiffrés pour protéger les données en cas de vol physique.

---

## **Résumé**

| **Thème**                  | **Concepts Clés**                                                                           |
|----------------------------|--------------------------------------------------------------------------------------------|
| **Sécurité Informatique**  | Enjeux (confidentialité, continuité), objectifs (CIA), menaces (malwares, phishing), mesures (pare-feu, chiffrement). |
| **Chiffrement**            | Fonctionnalités (confidentialité, intégrité), algorithmes (AES, RSA), méthodes (symétrique, asymétrique). |

---

## **Conclusion**

- La sécurité informatique et le chiffrement sont au cœur de la protection des systèmes et des données.  
- Les bonnes pratiques combinant des mesures organisationnelles, techniques et des outils modernes permettent de réduire les risques liés aux menaces et vulnérabilités.
