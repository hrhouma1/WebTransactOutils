# Sur le serveur Ubuntu 

# Informations utilisées:
- user : demoutilisateur
- password : Mdp@Ass3zSécuris3

![image](https://github.com/user-attachments/assets/f00d238c-5e7f-4286-a5b7-dd3c9461ca29)

---------
# 01 - Préparation du serveur distant et installation des prérequis
---------

**Installation de Git**
```bash
apt update
apt install git
```

**Installation des prérequis sur le serveur Ubuntu**


```bash

sudo apt update
sudo apt install php libapache2-mod-php php-mysql
sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl (password : Mdp@Ass3zSécuris3)
sudo systemctl start apache2
sudo systemctl start mysql
php -v
cd /var/www/html
touch info.php
nano info.php
<?php
phpinfo();
cat info.php
http://IP/info.php
http://IP/phpmyadmin.php

```



---------
# 02 - Création du répertoire sur le serveur et clonage du dépôt
---------

```bash
sudo mkdir /var/www/html/demo
sudo chmod -R 755 /var/www/html/demo
sudo chown -R www-data:www-data /var/www/html/demo
```


**Clonage du dépôt**
```bash
cd /var/www/html
git clone https://github.com/hrhouma1/sitev.git demo
cd /var/www/html/demo
unzip site.zip

```

**Configuration des permissions**
```bash
chmod -R 755 /var/www/html/demo
chown -R www-data:www-data /var/www/html/demo
```

---------
# 03 - Configuration de la base de données
---------

1. Création de la base de donnée
   
```bash
sudo mysql
CREATE DATABASE demobdd;
USE demobdd;
exit;
```

2. Vérifiez maintenant la présence du fichier sql:
   
```bash
cd /var/www/html/demo
ls -l demobdd.sql
```

3. Vérifiez les permissions :
   
```bash
sudo chmod -R 755 /var/www/html/demo
sudo chown -R www-data:www-data /var/www/html/demo
```


4. Créez d'abord l'utilisateur séparément :
   
```bash
mysql
CREATE USER 'demoutilisateur'@'localhost' IDENTIFIED BY 'Mdp@Ass3zSécuris3';
GRANT ALL PRIVILEGES ON demobdd.* TO 'demoutilisateur'@'localhost';
FLUSH PRIVILEGES;
exit;
```

5. Modifiez le fichier demobdd.sql :
```bash
cd /var/www/html/demo
sed -i '/GRANT ALL PRIVILEGES/d' demobdd.sql
sed -i '/FLUSH PRIVILEGES/d' demobdd.sql
```

6. Importez maintenant la base :
```bash
mysql demobdd < demobdd.sql
```

---------
# 04 - Vérification
---------

1. Testez votre site :
```
http://adresse_ip_serveur/demo
```


**En cas de problème**
- Vérifiez les logs Apache : `sudo tail -f /var/log/apache2/error.log`
- Redémarrez Apache : `sudo systemctl restart apache2`
- Vérifiez que MySQL tourne : `sudo systemctl status mysql`


2. Testez l'accès au site :
```
http://46.202.178.98/demo
http://46.202.178.98/phpmyadmin/
http://46.202.178.98/demo/admin/
http://46.202.178.98/demo/article.php?id=1
```

```
https://latestworlds.com/demo
https://latestworlds.com/phpmyadmin/
http://latestworlds.com/demo/admin/
http://latestworlds.com/demo/article.php?id=1
```

3. En cas de problème, vérifiez les logs :
```bash
tail -f /var/log/apache2/error.log
```

