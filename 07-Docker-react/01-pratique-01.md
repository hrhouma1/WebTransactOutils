# Étude de cas: Serveur Web avec Docker


## 1. Installation des Prérequis

**Installation de Docker sur Ubuntu 22.04**

```bash
# Mettre à jour le système
sudo apt update

# Installer les paquets nécessaires
sudo apt install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    software-properties-common

# Ajouter la clé GPG officielle de Docker
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Ajouter le dépôt Docker
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Mettre à jour et installer Docker
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io

# Ajouter votre utilisateur au groupe docker
sudo usermod -aG docker $USER

# Redémarrer le service Docker
sudo systemctl restart docker
```

## 2. Site Statique Local avec Docker

**Étape 1 : Créer la structure du projet**
```bash
# Créer le dossier du projet
mkdir mon-site-statique
cd mon-site-statique

# Créer les fichiers de base
touch index.html
touch styles.css
touch Dockerfile
```

**Étape 2 : Créer le contenu HTML minimal**
```bash
# Éditer index.html
nano index.html
```

Contenu de index.html :
```html
<!DOCTYPE html>
<html>
<head>
    <title>Mon Site</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <h1>Bienvenue sur mon site</h1>
    <p>Ceci est un site statique servi avec Docker.</p>
</body>
</html>
```

**Étape 3 : Créer le Dockerfile**
```bash
# Éditer Dockerfile
nano Dockerfile
```

Contenu du Dockerfile :
```dockerfile
# Utiliser Ubuntu 22.04 comme image de base
FROM ubuntu:22.04

# Éviter les interactions pendant l'installation
ENV DEBIAN_FRONTEND=noninteractive

# Mettre à jour et installer nginx
RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copier les fichiers du site
COPY . /var/www/html/

# Exposer le port 80
EXPOSE 80

# Démarrer nginx
CMD ["nginx", "-g", "daemon off;"]
```

**Étape 4 : Construction et démarrage**
```bash
# Construire l'image Docker
docker build -t mon-site-statique .

# Vérifier que l'image est créée
docker images

# Lancer le conteneur
docker run -d -p 8080:80 --name mon-site mon-site-statique

# Vérifier que le conteneur fonctionne
docker ps
```

## 3. SPA Local avec Docker (Exemple avec React)

**Étape 1 : Créer une application React**
```bash
# Installer Node.js
sudo apt update
sudo apt install -y nodejs npm

# Créer une nouvelle application React
npx create-react-app ma-spa
cd ma-spa
```

**Étape 2 : Créer le Dockerfile pour la SPA**
```bash
# Créer le Dockerfile
nano Dockerfile
```

Contenu du Dockerfile :
```dockerfile
# Étape de build
FROM node:16 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Étape de production
FROM ubuntu:22.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y nginx && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copier les fichiers buildés
COPY --from=builder /app/build /var/www/html/

# Configuration Nginx pour SPA
RUN echo ' \
server { \
    listen 80; \
    location / { \
        root /var/www/html; \
        try_files $uri $uri/ /index.html; \
    } \
}' > /etc/nginx/sites-available/default

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

**Étape 3 : Construction et démarrage**
```bash
# Construire l'image
docker build -t ma-spa .

# Lancer le conteneur
docker run -d -p 3000:80 --name mon-app-spa ma-spa
```

## 4. Commandes Docker Utiles

**Gestion des conteneurs**
```bash
# Voir les conteneurs en cours d'exécution
docker ps

# Voir tous les conteneurs (même arrêtés)
docker ps -a

# Arrêter un conteneur
docker stop nom_conteneur

# Supprimer un conteneur
docker rm nom_conteneur

# Voir les logs d'un conteneur
docker logs nom_conteneur

# Entrer dans un conteneur
docker exec -it nom_conteneur bash
```

**Gestion des images**
```bash
# Voir toutes les images
docker images

# Supprimer une image
docker rmi nom_image

# Nettoyer les images non utilisées
docker image prune
```

## 5. Dépannage Courant

**Si le site n'est pas accessible**
```bash
# Vérifier que le conteneur tourne
docker ps

# Vérifier les logs
docker logs nom_conteneur

# Vérifier la configuration nginx dans le conteneur
docker exec -it nom_conteneur cat /etc/nginx/sites-available/default

# Redémarrer le conteneur
docker restart nom_conteneur
```

**Si le build échoue**
```bash
# Nettoyer Docker
docker system prune

# Reconstruire sans cache
docker build --no-cache -t mon-image .
```

