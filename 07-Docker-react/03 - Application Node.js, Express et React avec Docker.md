# Étude de Cas : Application Node.js, Express et React avec Docker

## 1. Structure du Projet

```bash
mkdir mon-projet-fullstack
cd mon-projet-fullstack

# Créer les dossiers
mkdir backend frontend
```

## 2. Backend (Node.js + Express)

**Étape 1 : Initialisation du backend**
```bash
cd backend
npm init -y
npm install express
```

**Étape 2 : Créer le serveur Express (server.js)**
```javascript
const express = require('express');
const app = express();
const port = 4000;

app.use(express.json());

app.get('/api/test', (req, res) => {
    res.json({ message: 'Le serveur fonctionne!' });
});

app.listen(port, () => {
    console.log(`Serveur démarré sur le port ${port}`);
});
```

**Étape 3 : Dockerfile pour le backend**
```dockerfile
FROM ubuntu:22.04

# Installation de Node.js
RUN apt-get update && \
    apt-get install -y nodejs npm && \
    apt-get clean

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 4000

CMD ["node", "server.js"]
```

## 3. Frontend (React)

**Étape 1 : Création de l'application React**
```bash
cd ../frontend
npx create-react-app .
```

**Étape 2 : Modifier App.js**
```javascript
import { useState, useEffect } from 'react';

function App() {
  const [message, setMessage] = useState('');

  useEffect(() => {
    fetch('http://localhost:4000/api/test')
      .then(res => res.json())
      .then(data => setMessage(data.message));
  }, []);

  return (
    <div>
      <h1>Mon Application</h1>
      <p>{message}</p>
    </div>
  );
}

export default App;
```

**Étape 3 : Dockerfile pour le frontend**
```dockerfile
FROM ubuntu:22.04

# Installation de Node.js
RUN apt-get update && \
    apt-get install -y nodejs npm && \
    apt-get clean

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["npm", "start"]
```

## 4. Docker Compose

**Créer docker-compose.yml à la racine du projet**
```yaml
version: '3'
services:
  backend:
    build: ./backend
    ports:
      - "4000:4000"
    volumes:
      - ./backend:/app
    environment:
      - NODE_ENV=development

  frontend:
    build: ./frontend
    ports:
      - "3000:3000"
    volumes:
      - ./frontend:/app
    depends_on:
      - backend
```

## 5. Lancement de l'Application

```bash
# Construction des images
docker-compose build

# Démarrage des conteneurs
docker-compose up

# Pour arrêter les conteneurs
docker-compose down
```

## 6. Commandes Utiles

**Gestion des conteneurs**
```bash
# Voir les logs
docker-compose logs

# Redémarrer un service
docker-compose restart backend

# Voir l'état des services
docker-compose ps
```

## 7. Tests

1. Accéder au frontend : http://localhost:3000
2. Tester l'API : http://localhost:4000/api/test

## 8. Bonnes Pratiques

- Créer un fichier .dockerignore :
```
node_modules
npm-debug.log
build
.git
.env
```

- Utiliser des variables d'environnement :
```bash
# Dans le backend
PORT=4000
NODE_ENV=development

# Dans le frontend
REACT_APP_API_URL=http://localhost:4000
```

Cette étude de cas fournit une base solide pour démarrer un projet fullstack avec Docker. Elle peut être étendue selon les besoins spécifiques du projet.

