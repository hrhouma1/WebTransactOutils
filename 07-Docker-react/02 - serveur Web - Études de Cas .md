### Serveur Web - Études de Cas 

Dans ce cours, nous allons explorer **les principes fondamentaux et avancés** pour servir des sites web statiques et des Single Page Applications (SPA) à la fois localement et sur Internet. Nous allons également approfondir les outils utilisés (comme Docker et Nginx) et détailler toutes les étapes nécessaires pour chaque scénario.

---

## **Introduction : Serveurs Web et Sites Web**

### Qu'est-ce qu'un site statique ?
Un site statique est un ensemble de fichiers HTML, CSS et JavaScript stockés sur un serveur. Chaque fichier est envoyé tel quel au navigateur, sans traitement dynamique.

### Qu'est-ce qu'une SPA (Single Page Application) ?
Une SPA est une application web qui charge une seule page HTML, puis met à jour son contenu dynamiquement grâce à JavaScript, souvent en utilisant des frameworks comme **React**, **Vue.js**, ou **Angular**.

### Pourquoi utiliser Docker ?
Docker est une solution de **virtualisation légère** qui permet de créer des environnements reproductibles et isolés. Avec Docker, on peut :
- Déployer facilement des sites web sur n'importe quel système.
- Utiliser des images prêtes à l'emploi comme celles de **Nginx**.
- Simplifier le processus de déploiement avec des fichiers de configuration (Dockerfiles).

---

## **1. Servir un Site Statique Localement avec Docker**

Un site statique local est souvent utilisé pour le développement ou les tests avant le déploiement en ligne.

### Étape 1 : Préparer le site
Structure classique d'un site :
```plaintext
/my-static-site
├── index.html    (Page principale)
├── styles.css    (Feuilles de style)
└── script.js     (Scripts JavaScript)
```

### Étape 2 : Créer un fichier Dockerfile
Le **Dockerfile** est un fichier texte contenant les instructions pour créer une image Docker. Voici un exemple :
```dockerfile
# Utilisation de l'image Nginx
FROM nginx:latest

# Copier les fichiers locaux dans le répertoire utilisé par Nginx
COPY . /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80

# Lancer Nginx en mode non-bloquant
CMD ["nginx", "-g", "daemon off;"]
```

#### Détails :
1. **FROM nginx:latest**  
   - Utilise l'image officielle de **Nginx** comme base.
   - Cette image contient un serveur Nginx configuré pour servir des fichiers HTML.

2. **COPY . /usr/share/nginx/html**  
   - Copie tous les fichiers du répertoire courant (dossier contenant `Dockerfile`) dans le répertoire `/usr/share/nginx/html` utilisé par Nginx.

3. **EXPOSE 80**  
   - Indique que l'application écoute sur le port **80** (le port par défaut pour HTTP).

4. **CMD ["nginx", "-g", "daemon off;"]**  
   - Lance Nginx en mode "foreground" (non-bloquant), ce qui est nécessaire pour Docker.

---

### Étape 3 : Construire et Lancer le Conteneur

1. **Construire l'image Docker** :
   ```bash
   docker build -t my-static-site .
   ```
   - `-t my-static-site` : Attribue un nom à l'image Docker.
   - Le point (`.`) indique que le fichier Dockerfile est dans le répertoire courant.

2. **Lancer le conteneur** :
   ```bash
   docker run -d -p 8080:80 my-static-site
   ```
   - `-d` : Lance le conteneur en arrière-plan (mode détaché).
   - `-p 8080:80` : Mappe le port 8080 de la machine hôte au port 80 du conteneur.

3. **Tester le site** :
   - Accédez à `http://localhost:8080` pour voir votre site.

---

## **2. Servir une SPA Localement avec Docker**

Les SPAs nécessitent des configurations spécifiques, car elles utilisent du **routage côté client**. Cela signifie que les URL sont gérées par le navigateur et non par le serveur.

### Étape 1 : Construire la SPA
- Par exemple, avec **React** :
  ```bash
  npm run build
  ```
  - Le dossier `build/` contiendra les fichiers HTML, CSS, et JavaScript générés.

### Étape 2 : Créer un Dockerfile pour la SPA
Voici un exemple de Dockerfile :
```dockerfile
# Utilisation de l'image Nginx
FROM nginx:latest

# Copier les fichiers générés par "npm run build"
COPY build/ /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80

# Lancer Nginx
CMD ["nginx", "-g", "daemon off;"]
```

### Étape 3 : Construire et Lancer le Conteneur
Les commandes sont similaires à celles utilisées pour le site statique :
```bash
docker build -t my-spa .
docker run -d -p 8080:80 my-spa
```

---

### **Problème spécifique des SPAs**
Les routes de la SPA (par ex., `/about`, `/contact`) ne correspondent pas toujours à des fichiers physiques. Cela peut entraîner des erreurs 404 si la configuration Nginx n’est pas adaptée.

### Configurer le routage dans Nginx
Ajoutez une directive `try_files` dans la configuration Nginx :
```nginx
server {
  listen 80;
  server_name localhost;

  root /usr/share/nginx/html;
  index index.html;

  location / {
    try_files $uri /index.html;
  }
}
```
- **try_files $uri /index.html** : Redirige toutes les requêtes vers `index.html`, permettant au routage de fonctionner correctement.

---

## **3. Servir un Site Statique sur Internet**

### Prérequis
1. **Un serveur public** :
   - Par exemple, une machine virtuelle sur AWS, Azure, ou Google Cloud.
2. **Docker installé sur le serveur**.

### Étape 1 : Préparer le serveur
1. Installer Docker :
   ```bash
   sudo apt update
   sudo apt install docker.io
   ```
2. Ouvrir le port **80** dans le pare-feu.

### Étape 2 : Déployer le site
1. Copier le Dockerfile et les fichiers du site sur le serveur.
2. Construire et exécuter le conteneur :
   ```bash
   docker build -t my-static-site .
   docker run -d -p 80:80 my-static-site
   ```

### Étape 3 : Configurer un Domaine et HTTPS
1. Utiliser un DNS pour pointer un domaine vers l'adresse IP du serveur.
2. Installer **Traefik** ou **Certbot** pour générer un certificat SSL.

---

## **4. Servir une SPA sur Internet**

### Étape 1 : Préparer la SPA
1. Construire l'application comme dans la section locale.
2. Ajouter une configuration Nginx pour le routage des SPA.

### Étape 2 : Déployer sur le serveur
1. Copier les fichiers sur le serveur.
2. Construire et exécuter l'image Docker.

### Étape 3 : Configurer le Reverse Proxy et HTTPS
- Utilisez **Traefik** ou **Nginx** comme reverse proxy pour gérer les domaines et le SSL.

---

## **Résumé des Étapes Clés**

| Type de Site         | Environnement  | Outil Principal | Configuration Importante                      |
|-----------------------|----------------|-----------------|----------------------------------------------|
| Site statique         | Local          | Nginx, Docker   | Aucune (simple copie des fichiers).          |
| SPA                  | Local          | Nginx, Docker   | Routage client avec `try_files`.             |
| Site statique         | Internet       | Nginx, Traefik  | Reverse proxy et HTTPS avec Let's Encrypt.   |
| SPA                  | Internet       | Nginx, Traefik  | Routage, reverse proxy, et HTTPS.            |

---

## **Conclusion**
Ce cours a détaillé chaque étape pour servir des sites statiques et des SPAs localement et sur Internet. En utilisant Docker et des outils modernes comme Nginx, il est possible de déployer des applications robustes, sécurisées et scalables.
