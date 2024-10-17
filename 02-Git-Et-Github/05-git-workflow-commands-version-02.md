# 05 git workflow commands


## **Commandes de Workflow Git**

Ce guide va vous apprendre à gérer votre projet PHP avec Git, étape par étape, en vous expliquant chaque action avant de l'exécuter. Nous allons aussi vous montrer comment faire des modifications dans un fichier, et comment les gérer avec Git.

### **Dépôt Local** : `Git`

### **Dépôt Distant** : `GitHub` ([https://github.com](https://github.com))

---

## **Étapes du workflow Git**

### **Étape 1 : Cloner le projet existant depuis GitHub**

D'abord, nous allons récupérer le projet **site-php-1** depuis GitHub. Ouvrez votre terminal (ou Git Bash si vous êtes sous Windows), et exécutez cette commande pour cloner le projet :

```bash
git clone https://github.com/hrhouma1/site-php-1.git
```

Cette commande télécharge le projet dans votre machine. Ensuite, entrez dans le dossier cloné en tapant :

```bash
cd site-php-1
```

### **Étape 2 : Initialiser Git dans le projet**

Si vous démarrez un tout nouveau projet, vous devez initialiser Git dans le dossier du projet. Tapez cette commande pour créer un dépôt Git local :

```bash
git init
```

### **Étape 3 : Vérifier l'état du dépôt local**

Ensuite, nous allons vérifier l'état actuel de notre dépôt Git pour voir s'il y a des fichiers modifiés ou non suivis. Utilisez cette commande :

```bash
git status
```

Cela vous montrera quels fichiers ont été modifiés ou ajoutés.

### **Étape 4 : Ajouter des fichiers à la zone de staging**

Avant de pouvoir enregistrer des modifications, vous devez les "stager" (préparer pour le commit). Pour ajouter tous les fichiers modifiés ou nouveaux à la zone de staging, tapez :

```bash
git add .
```

### **Étape 5 : Commiter les fichiers dans le dépôt local**

Maintenant que les fichiers sont ajoutés à la zone de staging, nous allons créer un commit pour sauvegarder ces modifications dans l'historique Git. N'oubliez pas d'écrire un message explicatif pour chaque commit :

```bash
git commit -m "Premier commit avec le projet PHP CRUD"
```

### **Étape 6 : Configurer le dépôt distant**

Si vous avez créé un dépôt GitHub, nous devons le lier à notre projet local. Copiez l'URL HTTPS de votre dépôt GitHub, puis exécutez ces commandes pour lier votre projet local au dépôt distant et définir la branche principale :

```bash
git remote add origin https://github.com/hrhouma1/site-php-1.git
git branch -M main
```

### **Étape 7 : Pousser les changements vers le dépôt distant**

Maintenant que tout est configuré, nous allons envoyer les commits locaux vers GitHub avec la commande suivante :

```bash
git push -u origin main
```

### **Étape 8 : Travailler avec d'autres branches**

Pour ne pas impacter directement la branche principale, il est bon de créer une nouvelle branche pour chaque fonctionnalité. Par exemple, pour travailler sur une nouvelle fonctionnalité :

```bash
git checkout -b feature/new-functionality
```

Ensuite, modifiez les fichiers, ajoutez-les à la zone de staging et commitez-les :

```bash
git add .
git commit -m "Ajout d'une nouvelle fonctionnalité"
```

### **Étape 9 : Fusionner une branche dans `main`**

Lorsque votre nouvelle fonctionnalité est prête et testée, vous pouvez la fusionner dans la branche principale :

```bash
git checkout main
git merge feature/new-functionality
git push origin main
```

### **Étape 10 : Utiliser `git pull` pour récupérer les changements**

Si vous travaillez avec d'autres développeurs, vous devrez souvent récupérer leurs modifications depuis le dépôt distant. Tapez cette commande pour télécharger et intégrer les modifications :

```bash
git pull origin main
```

---

## **Commandes supplémentaires après les modifications**

### **Étape 11 : Modifier un fichier (ex: `app.js`)**

Maintenant, on va modifier un fichier pour voir comment Git gère les changements.

1. Ouvrez le fichier `app.js` dans votre éditeur de texte préféré (par exemple VSCode, Sublime Text, etc.).
2. Cherchez la ligne suivante dans le fichier `app.js` :
   
   ```javascript
   $('#addnew').click(function(){
   ```

3. Modifiez cette ligne pour y ajouter un petit message de console qui sera affiché lorsque le bouton sera cliqué. Par exemple, remplacez-la par :

   ```javascript
   $('#addnew').click(function(){
       console.log("Le bouton 'Add New' a été cliqué !");
   ```

4. Enregistrez le fichier.

Maintenant que vous avez modifié le fichier, revenez à votre terminal et tapez :

```bash
git status
```

Vous verrez que `app.js` est marqué comme modifié.

### **Étape 12 : Réinitialiser un fichier modifié (`app.js`)**

Imaginons que vous vouliez annuler la modification que vous venez de faire sur `app.js`. Pour revenir à la dernière version du fichier enregistrée dans Git, tapez cette commande :

```bash
git checkout -- app.js
```

Cela annulera toutes les modifications locales non committées sur ce fichier et le ramènera à son état dans le dernier commit.

### **Étape 13 : Réinitialiser toutes les modifications non committées sur tous les fichiers**

Si vous avez modifié plusieurs fichiers (comme `index.php`, `connection.php`, et `app.js`), mais que vous souhaitez annuler toutes les modifications locales non committées, vous pouvez réinitialiser tous les fichiers à leur dernier état committé avec cette commande :

```bash
git reset --hard
```

### **Étape 14 : Renommer une branche**

Si vous devez renommer la branche actuelle, vous pouvez le faire avec la commande suivante. Par exemple, pour renommer `main` en `production` :

```bash
git branch -m production
```

### **Étape 15 : Supprimer une branche locale**

Si une branche locale n'est plus nécessaire, vous pouvez la supprimer avec cette commande :

```bash
git branch -d feature/new-functionality
```

### **Étape 16 : Supprimer une branche distante**

Pour supprimer une branche sur GitHub, utilisez cette commande :

```bash
git push origin --delete feature/new-functionality
```

### **Étape 17 : Voir l'historique des commits avec un graphique**

Pour afficher un historique visuel des commits avec les branches et les fusions, tapez cette commande :

```bash
git log --graph --oneline --all
```

### **Étape 18 : Revenir à un commit spécifique**

Si vous souhaitez revenir à un commit précédent sans affecter les autres commits, utilisez cette commande avec l'ID du commit :

```bash
git checkout abc1234
```

---

## **Résumé des commandes**

### **Gestion des fichiers**
- Ajouter tous les fichiers à la zone de staging : `git add .`
- Commiter les changements : `git commit -m "message"`
- Réinitialiser un fichier spécifique (ex: `app.js`) : `git checkout -- app.js`
- Réinitialiser tous les fichiers non committés : `git reset --hard`

### **Gestion des branches**
- Créer une nouvelle branche : `git checkout -b feature/new-functionality`
- Fusionner une branche : `git merge feature/new-functionality`
- Renommer une branche : `git branch -m production`
- Supprimer une branche locale : `git branch -d feature/new-functionality`
- Supprimer une branche distante : `git push origin --delete feature/new-functionality`

### **Visualisation et historique**
- Voir l'historique des commits en graphique : `git log --graph --oneline --all`
- Revenir à un commit spécifique : `git checkout abc1234`

---




### **Étape 19 : Modifier les informations de connexion dans `connection.php` et les committer**

#### **1. Ouvrir le fichier `connection.php`**

D'abord, ouvrez le fichier `connection.php` dans votre éditeur de texte (VSCode, Sublime Text, etc.).

Dans ce fichier, vous allez voir quelque chose comme ceci :

```php
<?php

Class Connection{
 
	private $server = "mysql:host=localhost;dbname=mydatabase";
	private $username = "root";
	private $password = "root";
	private $options  = array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,);
	protected $conn;
 	
	public function open(){
 		try{
 			$this->conn = new PDO($this->server, $this->username, $this->password, $this->options);
 			return $this->conn;
 		}
 		catch (PDOException $e){
 			echo "There is some problem in connection: " . $e->getMessage();
 		}
    }
 
	public function close(){
   		$this->conn = null;
 	}
}
?>
```

#### **2. Modifier les informations de connexion**

Modifiez les informations de connexion pour qu'elles correspondent à votre propre environnement de base de données :

- **$server** : Si vous travaillez en local, laissez `localhost`. Sinon, indiquez l'adresse IP ou le nom de domaine du serveur de base de données.
- **$dbname** : Remplacez `"mydatabase"` par le nom exact de votre base de données (ex : `studentDB`).
- **$username** : Remplacez `"root"` par votre nom d'utilisateur de base de données.
- **$password** : Modifiez `"root"` avec votre mot de passe de base de données.

**Exemple après modification :**

```php
<?php

Class Connection{
 
	private $server = "mysql:host=localhost;dbname=studentDB";
	private $username = "admin";
	private $password = "admin123";
	private $options  = array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,);
	protected $conn;
 	
	public function open(){
 		try{
 			$this->conn = new PDO($this->server, $this->username, $this->password, $this->options);
 			return $this->conn;
 		}
 		catch (PDOException $e){
 			echo "There is some problem in connection: " . $e->getMessage();
 		}
    }
 
	public function close(){
   		$this->conn = null;
 	}
}
?>
```

#### **3. Enregistrer les modifications**

Après avoir modifié les informations de connexion, enregistrez le fichier `connection.php`.

---

### **Étape 20 : Créer une nouvelle branche Git pour ces modifications**

Nous allons créer une nouvelle branche pour ces modifications avant de les pousser vers GitHub. Cela vous permet de travailler sur vos changements sans affecter la branche principale.

1. Ouvrez votre terminal et tapez la commande suivante pour créer une nouvelle branche :

```bash
git checkout -b update-connection-settings
```

Cette commande crée et bascule vers une nouvelle branche appelée `update-connection-settings`.

---

### **Étape 21 : Ajouter et committer les modifications**

Après avoir modifié le fichier `connection.php`, vous devez l'ajouter à la zone de staging avant de créer un commit.

1. Ajoutez le fichier modifié à la zone de staging :

```bash
git add connection.php
```

2. Maintenant, créez un commit avec un message expliquant ce que vous avez fait :

```bash
git commit -m "Modification des informations de connexion dans connection.php"
```

---

### **Étape 22 : Pousser la nouvelle branche vers GitHub**

Après avoir committé les modifications, il est temps de pousser la nouvelle branche vers GitHub pour que tout soit synchronisé.

1. Poussez la branche `update-connection-settings` vers GitHub avec cette commande :

```bash
git push -u origin update-connection-settings
```

Cette commande enverra votre nouvelle branche et vos modifications sur GitHub.

---

### **Étape 23 : Ouvrir une pull request sur GitHub**

Maintenant que la branche est sur GitHub, vous pouvez créer une pull request pour fusionner vos changements dans la branche principale (`main`).

1. Rendez-vous sur [GitHub](https://github.com) et allez sur votre dépôt.
2. Vous verrez une option vous proposant de créer une **pull request**. Cliquez dessus.
3. Ajoutez un titre et une description, puis cliquez sur **Create Pull Request**.
4. Vous pouvez ensuite fusionner cette branche dans `main` une fois que vous avez vérifié les modifications.

---

### **Étape 24 : Résumé des commandes utilisées**

Voici un résumé des commandes que vous avez utilisées dans cette section :

1. **Créer une nouvelle branche** :
   ```bash
   git checkout -b update-connection-settings
   ```

2. **Ajouter le fichier modifié à la zone de staging** :
   ```bash
   git add connection.php
   ```

3. **Créer un commit avec un message** :
   ```bash
   git commit -m "Modification des informations de connexion dans connection.php"
   ```

4. **Pousser la branche vers GitHub** :
   ```bash
   git push -u origin update-connection-settings
   ```

---

En suivant ces étapes, vous aurez appris à modifier un fichier dans un projet Git, à créer une nouvelle branche, et à pousser les changements vers GitHub. Vous pourrez ensuite créer une pull request pour fusionner vos modifications dans la branche principale.
