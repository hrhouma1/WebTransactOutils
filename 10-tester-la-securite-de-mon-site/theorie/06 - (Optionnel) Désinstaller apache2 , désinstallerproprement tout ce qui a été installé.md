
# **Guide de Désinstallation Complète : Suppression d'Apache, MySQL, PHP, phpMyAdmin et Git sur un Serveur Ubuntu 22.04**

Pour **désinstaller proprement tout ce qui a été installé** sur votre serveur Ubuntu, suivez ces étapes dans l'ordre :

---

## 01 - **Désinstallation de Git, PHP, Apache et MySQL**

### **1. Arrêter les services :**
```bash
sudo systemctl stop apache2
sudo systemctl stop mysql
```

### **2. Désinstaller les paquets :**

Supprimer Apache, MySQL, PHP et leurs dépendances associées :
```bash
sudo apt remove --purge apache2 mysql-server mysql-client php libapache2-mod-php php-mysql phpmyadmin php-mbstring php-zip php-gd php-json php-curl -y
sudo apt autoremove -y
sudo apt autoclean
```

### **3. Vérifier que les services ne sont plus actifs :**
```bash
sudo systemctl status apache2
sudo systemctl status mysql
```

---

## 02 - **Suppression des fichiers de configuration et des bases de données**

### **1. Supprimer les fichiers de configuration Apache, MySQL et PHP :**
```bash
sudo rm -rf /etc/apache2
sudo rm -rf /etc/mysql
sudo rm -rf /etc/php
sudo rm -rf /usr/share/phpmyadmin
```

### **2. Supprimer les répertoires du projet web :**
```bash
sudo rm -rf /var/www/html/demo
sudo rm -rf /var/www/html/info.php
```

### **3. Supprimer les bases de données MySQL :**
- Connectez-vous à MySQL pour vérifier et supprimer la base de données :
```bash
sudo mysql -u root -p
DROP DATABASE demobdd;
DROP USER 'demoutilisateur'@'localhost';
FLUSH PRIVILEGES;
exit;
```

---

## 03 - **Nettoyage des dépôts Git et autres résidus**

### **1. Supprimer Git :**
```bash
sudo apt remove --purge git -y
sudo apt autoremove -y
```

### **2. Supprimer les répertoires et fichiers Git clonés :**
```bash
sudo rm -rf /var/www/html/demo
```

---

## 04 - **Vérification et nettoyage final**

### **1. Vérifier que tous les services sont désactivés :**
```bash
sudo systemctl status apache2
sudo systemctl status mysql
```

### **2. Nettoyer les journaux Apache et MySQL :**
```bash
sudo rm -rf /var/log/apache2/*
sudo rm -rf /var/log/mysql/*
```

### **3. Relancer le nettoyage automatique des paquets inutilisés :**
```bash
sudo apt autoremove -y
sudo apt autoclean
```

---

## 05 - **Redémarrage du serveur**
Redémarrez votre serveur pour appliquer toutes les modifications :
```bash
sudo reboot
```

---

## Vérification finale :
- **Apache** : Tapez `http://<IP_SERVEUR>` dans votre navigateur. Vous devriez voir une erreur de connexion.
- **PHPMyAdmin** : Tapez `http://<IP_SERVEUR>/phpmyadmin`. Vous ne devriez pas avoir accès.
- **MySQL** : Vérifiez que MySQL n'est pas en cours d'exécution :
  ```bash
  sudo systemctl status mysql
  ```

À ce stade, tout ce qui a été installé (Apache, MySQL, PHP, phpMyAdmin, Git) a été désinstallé, y compris les configurations et fichiers associés.
