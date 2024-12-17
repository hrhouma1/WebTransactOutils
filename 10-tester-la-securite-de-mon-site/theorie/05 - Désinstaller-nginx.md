# Désinstaller nginx sur **Ubuntu 22.04**

Pour désinstaller **Nginx** sur **Ubuntu 22.04**, suivez ces étapes :

---

# **1. Arrêter le service Nginx**
Avant de désinstaller Nginx, arrêtez son service.  
```bash
sudo systemctl stop nginx
```

---

# **2. Désactiver Nginx au démarrage**
Désactivez Nginx pour qu’il ne démarre plus automatiquement.  
```bash
sudo systemctl disable nginx
```

---

# **3. Désinstaller Nginx**
Pour supprimer Nginx, exécutez cette commande :  
```bash
sudo apt remove --purge nginx nginx-common -y
```
- **`--purge`** permet de supprimer les fichiers de configuration en plus du programme.

---

# **4. Supprimer les fichiers restants**
Vérifiez s’il reste des fichiers de configuration dans `/etc/nginx` et supprimez-les si nécessaire.  
```bash
sudo rm -rf /etc/nginx
```

---

# **5. Nettoyer les dépendances inutilisées**
Supprimez les paquets et dépendances inutiles liés à Nginx.  
```bash
sudo apt autoremove -y
sudo apt autoclean
```

---

# **6. Vérifier la suppression**
Assurez-vous que Nginx est bien désinstallé.  
```bash
nginx -v
```

- Si Nginx est désinstallé correctement, la commande retournera une erreur indiquant que **nginx** n’est pas trouvé.
- Nginx est maintenant désinstallé de votre serveur Ubuntu 22.04. 🚀
