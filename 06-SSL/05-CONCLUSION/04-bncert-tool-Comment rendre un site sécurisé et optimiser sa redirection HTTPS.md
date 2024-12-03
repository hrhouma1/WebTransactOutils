# Partie 01

Pour installer un certificat SSL sur votre instance Bitnami WordPress hébergée sur Amazon Lightsail, suivez ces étapes :

---

# 1. Connectez-vous à votre instance
1. Ouvrez un terminal ou une invite de commande.
2. Connectez-vous à votre instance avec SSH :
   ```bash
   ssh -i /chemin/vers/votre-cle.pem bitnami@44.224.150.113
   ```

---

# 2. Lancez le script Bitnami HTTPS Configuration
1. Une fois connecté, exécutez le script intégré pour configurer HTTPS avec Let's Encrypt :
   ```bash
   sudo /opt/bitnami/bncert-tool
   ```

2. Suivez les instructions à l'écran :
   - Entrez le ou les noms de domaine associés à votre site (par exemple, `example.com` et `www.example.com`).
   - Acceptez les redirections HTTP vers HTTPS si demandé.
   - Confirmez la configuration pour générer et installer le certificat.

---

# 3. Testez la configuration
- Une fois terminé, visitez votre site en utilisant `https://` pour vérifier que le certificat SSL est actif.

---

# 4. (Facultatif) Renouvellement automatique
Les certificats Let's Encrypt expirent tous les 90 jours. Le script `bncert-tool` configure automatiquement le renouvellement via un cron job. Pour vérifier cela :
   ```bash
   sudo crontab -l
   ```

Si nécessaire, vous pouvez ajouter un job cron manuel pour renouveler les certificats :
   ```bash
   0 0 * * * sudo /opt/bitnami/letsencrypt/lego --tls --email="votre-email@example.com" --domains="example.com" --domains="www.example.com" renew && sudo /opt/bitnami/ctlscript.sh restart
   ```



# Partie 02 - Redémarrer Apache après l'installation du certificat SSL

1. **Relancez le script `bncert-tool` :**
   ```bash
   sudo /opt/bitnami/bncert-tool
   ```
   - Suivez les étapes pour configurer votre certificat.

2. **Redémarrez Apache (et les autres services Bitnami) avec la commande suivante :**
   ```bash
   sudo /opt/bitnami/ctlscript.sh restart apache
   ```
   Cette commande garantit que le serveur Apache utilise correctement le nouveau certificat.

---

### Étapes supplémentaires si Apache ne redémarre pas correctement :
- Si vous voyez une erreur lors du redémarrage d'Apache, vérifiez la syntaxe des fichiers de configuration :
   ```bash
   sudo /opt/bitnami/apache2/bin/apachectl -t
   ```
   Cela vous permettra d’identifier les erreurs potentielles dans la configuration.

- Consultez les logs pour diagnostiquer le problème :
   ```bash
   sudo tail -n 20 /opt/bitnami/apache2/logs/error_log
   ```

---

### Vérification finale :
- Accédez à votre site via `https://` pour confirmer que SSL est correctement configuré.
- Vous pouvez également tester votre site avec [SSL Labs](https://www.ssllabs.com/ssltest/) pour vérifier la validité du certificat et la configuration SSL.

