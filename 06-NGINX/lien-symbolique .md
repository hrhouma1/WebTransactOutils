# **Évaluation formative 01 : À quoi servent les dossiers `sites-available` et `sites-enabled` ?**

- **`sites-available`** :  
  Ce dossier contient tous les fichiers de configuration des sites web que le serveur Nginx peut potentiellement héberger. Chaque fichier représente un site ou une configuration particulière. Les fichiers ici ne sont pas activés par défaut.

- **`sites-enabled`** :  
  Ce dossier contient uniquement les fichiers de configuration activés et utilisés par Nginx. Les fichiers dans ce dossier sont souvent des **liens symboliques** vers les fichiers de configuration dans `sites-available`.

> **Pourquoi cette séparation ?**  
Cela permet de garder une distinction claire entre les configurations disponibles et celles effectivement actives, rendant la gestion des sites plus facile.

---

# **Évaluation formative 02 :**

1. **C'est quoi un lien symbolique ?**  
Un lien symbolique (ou symlink) est un type de fichier spécial qui pointe vers un autre fichier ou dossier. C'est comme un raccourci. Quand Nginx lit un fichier dans `sites-enabled`, il suit ce lien pour accéder au fichier réel dans `sites-available`.

   - Par exemple, la ligne `default -> /etc/nginx/sites-available/default` signifie que dans `sites-enabled`, le fichier `default` est un lien symbolique qui pointe vers `/etc/nginx/sites-available/default`.

---

2. **C'est quoi `default` ?**  
`default` est un fichier de configuration fourni par défaut avec Nginx. Il contient une configuration générique pour un site web ou un serveur web local. Typiquement, il est utilisé comme configuration de base ou comme exemple.

   - Ce fichier peut être modifié ou remplacé pour configurer un site web spécifique. Par défaut, il répond aux requêtes HTTP vers l'adresse IP du serveur (sans nom de domaine).

---

3. **Puis-je utiliser un autre nom comme `mondomaine.ca` à la place de `default` ?**  
Oui, vous pouvez utiliser un autre nom. Par exemple, vous pouvez créer un fichier de configuration appelé `mondomaine.ca` dans `sites-available`, y configurer votre site, et ensuite créer un lien symbolique dans `sites-enabled` :
   ```bash
   ln -s /etc/nginx/sites-available/mondomaine.ca /etc/nginx/sites-enabled/mondomaine.ca
   ```
   Assurez-vous de recharger Nginx après avoir fait ce changement :
   ```bash
   sudo systemctl reload nginx
   ```

---

4. **Expliquez cette ligne : `default -> /etc/nginx/sites-available/default`**  
Cette ligne indique que dans le dossier `sites-enabled`, le fichier `default` est un lien symbolique qui pointe vers le fichier réel `/etc/nginx/sites-available/default`.

- **Fonctionnement** :  
  Quand Nginx lit `sites-enabled/default`, il suit ce lien pour lire la configuration réelle dans `sites-available/default`.

- **Utilité** :  
  Cela permet d’activer ou de désactiver un site simplement en ajoutant ou supprimant le lien symbolique dans `sites-enabled`, sans toucher au fichier d’origine dans `sites-available`.

---

### **Résumé :**
- `sites-available` : contient toutes les configurations de sites.
- `sites-enabled` : contient les liens symboliques vers les configurations actives.
- Un lien symbolique est un raccourci vers un fichier ou dossier réel.
- `default` est une configuration de site générique par défaut, mais vous pouvez le remplacer par un fichier personnalisé comme `mondomaine.ca`.
