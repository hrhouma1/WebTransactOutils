## **Cours : Utilisation de NGINX comme serveur Web**

### **Introduction**
NGINX est un serveur web performant utilisé pour servir des sites web statiques, agir comme reverse proxy, équilibrer la charge, et gérer des redirections ou réécritures d'URI. Ce cours explore les concepts clés pour configurer NGINX efficacement en mettant l'accent sur les directives et fonctionnalités essentielles.

---

### **1. La sélection de serveurs**
NGINX utilise des blocs de configuration appelés **server blocks** pour définir comment les requêtes HTTP sont traitées. Chaque bloc peut être sélectionné en fonction de domaines, adresses IP ou ports.

**Exemple :**
```nginx
server {
    listen 80;
    server_name example.com www.example.com;

    location / {
        root /var/www/example;
        index index.html;
    }
}
```

- **listen** : Définit le port d'écoute (ex : `80` pour HTTP, `443` pour HTTPS).
- **server_name** : Spécifie les noms de domaine associés à ce bloc.

---

### **2. Configuration des emplacements avec `location`**
La directive `location` permet de définir comment traiter les requêtes en fonction de leur URI. Elle utilise des blocs pour matcher des chemins spécifiques.

**Types de correspondance :**
1. **Exacte (`=`)** : Correspondance exacte de l'URI.
2. **Commence par (`^~`)** : Priorité aux emplacements avec ce préfixe.
3. **Expression régulière (`~` ou `~*`)** :
   - `~` : Sensible à la casse.
   - `~*` : Insensible à la casse.
4. **Par défaut** : Si aucune autre correspondance ne s'applique.

**Exemple :**
```nginx
server {
    location = /exact {
        return 200 "Exact match\n";
    }

    location ^~ /static/ {
        root /var/www/static/;
    }

    location ~* \.(jpg|jpeg|png|gif)$ {
        root /var/www/images/;
    }

    location / {
        root /var/www/html/;
    }
}
```

---

### **3. La directive `root`**
La directive `root` spécifie le répertoire où se trouvent les fichiers à servir pour une requête donnée.

**Exemple :**
```nginx
location / {
    root /var/www/site;
}
```
Si un utilisateur demande `/about.html`, le fichier sera cherché dans `/var/www/site/about.html`.

---

### **4. La directive `index`**
`index` définit les fichiers par défaut à charger lorsqu’une requête cible un répertoire.

**Exemple :**
```nginx
location / {
    root /var/www/site;
    index index.html index.htm;
}
```
- Si `/` est demandé, NGINX cherche `index.html`, puis `index.htm`.

---

### **5. La directive `try_files`**
`try_files` est utilisée pour vérifier plusieurs chemins possibles pour un fichier ou une URI et rediriger en conséquence.

**Exemple :**
```nginx
location / {
    root /var/www/site;
    try_files $uri $uri/ /index.html;
}
```
- `$uri` : Vérifie si l’URI demandé existe comme fichier.
- `$uri/` : Vérifie si l’URI correspond à un répertoire.
- `/index.html` : Redirige vers une page par défaut si les deux précédents échouent.

---

### **6. Les variables**
NGINX fournit des variables intégrées pour accéder à des informations sur les requêtes.

**Exemples courants :**
- `$host` : Nom de domaine ou adresse IP demandée.
- `$uri` : URI de la requête.
- `$args` : Arguments de requête (GET).
- `$request_method` : Méthode HTTP (GET, POST, etc.).

**Exemple :**
```nginx
location /info {
    return 200 "Host: $host, URI: $uri, Method: $request_method\n";
}
```

---

### **7. Retourner des codes et rediriger**
La directive `return` permet de retourner un code HTTP ou rediriger une requête.

**Exemple :**
```nginx
location /old {
    return 301 /new;
}

location /new {
    return 200 "Welcome to the new location\n";
}
```
- **301** : Redirection permanente.
- **302** : Redirection temporaire.

---

### **8. Les réécritures d'URI**
La directive `rewrite` modifie les URI à l’aide d’expressions régulières.

**Exemple :**
```nginx
location / {
    rewrite ^/old-path/(.*)$ /new-path/$1 permanent;
}
```
- Redirige `/old-path/abc` vers `/new-path/abc`.

---

### **9. Les réécritures de réponses HTTP**
NGINX peut modifier les réponses HTTP en interceptant et réécrivant les en-têtes.

**Exemple :**
```nginx
proxy_set_header X-Modified "true";
proxy_pass http://backend;
```
Cela ajoute un en-tête personnalisé `X-Modified` à toutes les réponses du proxy.

---

### **10. La directive `error_page`**
`error_page` configure la gestion des pages d’erreur personnalisées.

**Exemple :**
```nginx
error_page 404 /404.html;

location = /404.html {
    root /var/www/errors;
}
```
Lorsqu’une page n’est pas trouvée (404), NGINX sert `/var/www/errors/404.html`.

---

### **Conclusion**
NGINX offre une flexibilité incroyable grâce à ses directives. Avec des fonctionnalités comme `try_files`, `rewrite`, et `error_page`, vous pouvez personnaliser le comportement du serveur pour répondre à des besoins spécifiques.

**Exercice :**
1. Créez une configuration NGINX avec :
   - Un site statique avec un fichier index.
   - Une redirection d’une ancienne URI vers une nouvelle.
   - Une page d’erreur 404 personnalisée.
2. Testez votre configuration avec différentes requêtes.
