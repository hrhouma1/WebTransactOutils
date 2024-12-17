# Évaluation formative de la Sécurité des Sites Web des Collèges et Universités

Pour les sites webs des 50 institutions listées, nous allons vérifier les éléments suivants pour quelques sites (choisissez 3):

1. **Protection de /wp-admin :** Vérifier si la page de connexion à l'administration WordPress est protégée.
2. **Utilisateurs WordPress :** Utiliser la commande curl pour lister les utilisateurs disponibles via l'API REST.

#### Tableau de Vérification

| Site Web                                      | /wp-admin Protégé | Utilisateurs WordPress (via curl)          |
|-----------------------------------------------|-------------------|--------------------------------------------|
| https://www.crosemont.qc.ca/                  | Oui/Non           | Utilisateur(s)                             |
| https://www.bdeb.qc.ca/                       | Oui/Non           | Utilisateur(s)                             |
| https://www.collegecanada.com/                | Oui/Non           | Utilisateur(s)                             |
| https://institutelite.ca/                     | Oui/Non           | Utilisateur(s)                             |
| https://www.lasallecollege.com/               | Oui/Non           | Utilisateur(s)                             |
| https://www.johnabbott.qc.ca/                 | Oui/Non           | Utilisateur(s)                             |
| https://www.dawsoncollege.qc.ca/              | Oui/Non           | Utilisateur(s)                             |
| https://www.vaniercollege.qc.ca/              | Oui/Non           | Utilisateur(s)                             |
| https://www.claurendeau.qc.ca/                | Oui/Non           | Utilisateur(s)                             |
| https://www.cmaisonneuve.qc.ca/               | Oui/Non           | Utilisateur(s)                             |
| https://www.collegeahuntsic.qc.ca/            | Oui/Non           | Utilisateur(s)                             |
| https://www.cegepsl.qc.ca/                    | Oui/Non           | Utilisateur(s)                             |
| https://www.cvm.qc.ca/                        | Oui/Non           | Utilisateur(s)                             |
| https://www.marianopolis.edu/                 | Oui/Non           | Utilisateur(s)                             |
| https://www.cimf.qc.ca/                       | Oui/Non           | Utilisateur(s)                             |
| https://www.etsmtl.ca/                        | Oui/Non           | Utilisateur(s)                             |
| https://www.cegepgarneau.ca/                  | Oui/Non           | Utilisateur(s)                             |
| https://www.cegeplimoilou.ca/                 | Oui/Non           | Utilisateur(s)                             |
| https://uqam.ca/                              | Oui/Non           | Utilisateur(s)                             |
| https://umontreal.ca/                         | Oui/Non           | Utilisateur(s)                             |
| https://enit.rnu.tn/                          | Oui/Non           | Utilisateur(s)                             |
| https://www.cegeptr.qc.ca/                    | Oui/Non           | Utilisateur(s)                             |
| https://www.cegepshawinigan.ca/               | Oui/Non           | Utilisateur(s)                             |
| https://www.clafleche.qc.ca/                  | Oui/Non           | Utilisateur(s)                             |
| https://www.ellis.qc.ca/                      | Oui/Non           | Utilisateur(s)                             |
| https://www.conservatoire.gouv.qc.ca/         | Oui/Non           | Utilisateur(s)                             |
| https://www.cegepst.qc.ca/                    | Oui/Non           | Utilisateur(s)                             |
| https://www.cegepsth.qc.ca/                   | Oui/Non           | Utilisateur(s)                             |
| https://www.cegepvalleyfield.ca/              | Oui/Non           | Utilisateur(s)                             |
| https://www.cegepmontpetit.ca/                | Oui/Non           | Utilisateur(s)                             |
| https://www.cstjean.qc.ca/                    | Oui/Non           | Utilisateur(s)                             |
| https://www.champlainonline.com/              | Oui/Non           | Utilisateur(s)                             |
| https://www.academie-ent.com/                 | Oui/Non           | Utilisateur(s)                             |
| https://www.airrichelieu.com/                 | Oui/Non           | Utilisateur(s)                             |
| https://www.april-fortier.com/                | Oui/Non           | Utilisateur(s)                             |
| https://www.cdicollege.ca/                    | Oui/Non           | Utilisateur(s)                             |
| https://www.collegeimmobilier.com/            | Oui/Non           | Utilisateur(s)                             |
| https://cargair.com/                          | Oui/Non           | Utilisateur(s)                             |
| https://www.centreequestredechambly.com/      | Oui/Non           | Utilisateur(s)                             |
| https://sainthubertflyingcollege.com/         | Oui/Non           | Utilisateur(s)                             |
| https://collegemilestone.ca/                  | Oui/Non           | Utilisateur(s)                             |
| https://helicraft.ca/                         | Oui/Non           | Utilisateur(s)                             |
| https://www.teccart.qc.ca/                    | Oui/Non           | Utilisateur(s)                             |
| https://www.itaq.ca/                          | Oui/Non           | Utilisateur(s)                             |
| https://www.collegemv.qc.ca/                  | Oui/Non           | Utilisateur(s)                             |
| https://www.cgodin.qc.ca/                     | Oui/Non           | Utilisateur(s)                             |
| https://www.grasset.qc.ca/                    | Oui/Non           | Utilisateur(s)                             |
| https://www.brebeuf.qc.ca/                    | Oui/Non           | Utilisateur(s)                             |
| https://www.collegedecarie.ca/                | Oui/Non           | Utilisateur(s)                             |
| https://www.osullivan.edu/                    | Oui/Non           | Utilisateur(s)                             |
| https://collegeuniversel.ca/                  | Oui/Non           | Utilisateur(s)                             |

# Étapes pour la Vérification

1. **Protection de /wp-admin :**
   - Tenter d'accéder à `https://[site]/wp-admin`.
   - Vérifier si une page de connexion sécurisée apparaît ou si l'accès est libre.

2. **Liste des Utilisateurs :**
   - Utiliser la commande curl pour lister les utilisateurs via l'API REST :
     ```bash
     curl -s https://[site]/wp-json/wp/v2/users
     ```
   - Noter les utilisateurs retournés.

# Importance de la Sécurité

La vérification de ces éléments est cruciale pour garantir la sécurité des sites WordPress. Les administrateurs de sites doivent :

- Protéger l'accès à l'administration (`/wp-admin`).
- Empêcher les accès non autorisés aux informations des utilisateurs via l'API REST.
- Mettre en œuvre des mesures de sécurité supplémentaires comme l'authentification à deux facteurs (2FA) et la limitation des tentatives de connexion.

Ces pratiques permettent de réduire les risques de compromission et d'assurer la sécurité des données.

# Annexe 1 - Étapes pour la Vérification de Sécurité sous Windows

Sous Windows, vous pouvez utiliser des outils et des commandes pour vérifier la sécurité des sites web listés. Voici un guide étape par étape pour accomplir cette tâche :

#### Outils Nécessaires
1. **Navigateur Web** pour tester l'accès à `/wp-admin`.
2. **curl** pour vérifier les utilisateurs via l'API REST de WordPress.
3. **PowerShell** pour automatiser certaines tâches.

#### Étapes à Suivre

1. **Tester l'accès à `/wp-admin` :**

   Vous pouvez utiliser votre navigateur web pour vérifier manuellement si la page de connexion est protégée.

   - Ouvrez un navigateur web (comme Chrome, Firefox, Edge).
   - Tapez `https://[site]/wp-admin` dans la barre d'adresse.
   - Vérifiez si une page de connexion s'affiche ou si l'accès est libre.

2. **Utiliser curl pour vérifier les utilisateurs WordPress :**

   Sous Windows, vous pouvez utiliser **PowerShell** pour exécuter des commandes curl.

   - Ouvrez **PowerShell**.
   - Utilisez la commande suivante pour vérifier les utilisateurs :
     ```powershell
     curl -s https://[site]/wp-json/wp/v2/users
     ```

   Voici un exemple de script PowerShell pour vérifier plusieurs sites automatiquement :

   ```powershell
   $sites = @(
       "https://www.crosemont.qc.ca/",
       "https://www.bdeb.qc.ca/",
       "https://www.collegecanada.com/",
       "https://institutelite.ca/",
       "https://www.lasallecollege.com/",
       "https://www.johnabbott.qc.ca/",
       "https://www.dawsoncollege.qc.ca/",
       "https://www.vaniercollege.qc.ca/",
       "https://www.claurendeau.qc.ca/",
       "https://www.cmaisonneuve.qc.ca/",
       "https://www.collegeahuntsic.qc.ca/",
       "https://www.cegepsl.qc.ca/",
       "https://www.cvm.qc.ca/",
       "https://www.marianopolis.edu/",
       "https://www.cimf.qc.ca/",
       "https://www.etsmtl.ca/",
       "https://www.cegepgarneau.ca/",
       "https://www.cegeplimoilou.ca/",
       "https://uqam.ca/",
       "https://umontreal.ca/",
       "https://enit.rnu.tn/",
       "https://www.cegeptr.qc.ca/",
       "https://www.cegepshawinigan.ca/",
       "https://www.clafleche.qc.ca/",
       "https://www.ellis.qc.ca/",
       "https://www.conservatoire.gouv.qc.ca/",
       "https://www.cegepst.qc.ca/",
       "https://www.cegepsth.qc.ca/",
       "https://www.cegepvalleyfield.ca/",
       "https://www.cegepmontpetit.ca/",
       "https://www.cstjean.qc.ca/",
       "https://www.champlainonline.com/",
       "https://www.academie-ent.com/",
       "https://www.airrichelieu.com/",
       "https://www.april-fortier.com/",
       "https://www.cdicollege.ca/",
       "https://www.collegeimmobilier.com/",
       "https://cargair.com/",
       "https://www.centreequestredechambly.com/",
       "https://sainthubertflyingcollege.com/",
       "https://collegemilestone.ca/",
       "https://helicraft.ca/",
       "https://www.teccart.qc.ca/",
       "https://www.itaq.ca/",
       "https://www.collegemv.qc.ca/",
       "https://www.cgodin.qc.ca/",
       "https://www.grasset.qc.ca/",
       "https://www.brebeuf.qc.ca/",
       "https://www.collegedecarie.ca/",
       "https://www.osullivan.edu/",
       "https://collegeuniversel.ca/",
       "https://inkcrown.com/"
          
   )

   $results = @()

   foreach ($site in $sites) {
       $wpAdminStatus = try {
           $response = Invoke-WebRequest -Uri "$site/wp-admin" -UseBasicParsing
           if ($response.StatusCode -eq 200) {
               "Accessible"
           } else {
               "Protected"
           }
       } catch {
           "Protected"
       }

       $users = try {
           $userResponse = Invoke-RestMethod -Uri "$site/wp-json/wp/v2/users" -UseBasicParsing
           $userResponse | ForEach-Object { $_.name } -join ", "
       } catch {
           "Non accessible"
       }

       $results += [pscustomobject]@{
           Site       = $site
           AdminStatus = $wpAdminStatus
           Users      = $users
       }
   }

   $results | Format-Table -AutoSize
   ```

   Ce script PowerShell parcourt chaque site, vérifie l'accès à `/wp-admin`, et récupère les utilisateurs via l'API REST de WordPress. Les résultats sont affichés dans un tableau.

### Importance de la Sécurité

La sécurité des sites WordPress est essentielle pour protéger les données sensibles et éviter les compromissions. Les étapes de vérification et les outils décrits ici sont des moyens pratiques pour s'assurer que les sites web des institutions éducatives sont bien sécurisés.

**Mesures de Sécurité Recommandées :**
- **Utilisation de .htaccess :** Pour restreindre l'accès à `/wp-admin`.
  ```apache
  <Files wp-login.php>
      Order Deny,Allow
      Deny from all
      Allow from [YOUR IP ADDRESS]
  </Files>
  ```
  Remplacez `[YOUR IP ADDRESS]` par votre adresse IP pour sécuriser l'accès.

- **Authentification à Deux Facteurs (2FA) :** Implémenter 2FA pour ajouter une couche de sécurité supplémentaire.

- **Mises à jour Régulières :** Toujours maintenir WordPress, les thèmes et les plugins à jour pour corriger les vulnérabilités.

En suivant ces pratiques, les administrateurs peuvent renforcer la sécurité de leurs sites WordPress et protéger les données des utilisateurs.

# Exemple 1
```ssh
curl -s https://inkcrown.com/wp-json/wp/v2/users
```
# Exemple 2

```ssh
# Définir les URLs des sites pour les utilisateurs
$sites = @("https://collegeuniversel.ca/wp-json/wp/v2/users", "https://inkcrown.com/wp-json/wp/v2/users")

# Boucler sur chaque site pour récupérer les données des utilisateurs
foreach ($site in $sites) {
    try {
        # Tenter de récupérer les données utilisateur
        $users = Invoke-RestMethod -Uri $site -UseBasicParsing
        # Vérifier si des utilisateurs sont trouvés
        if ($users.count -gt 0) {
            Write-Host "Utilisateurs du site $site :"
            foreach ($user in $users) {
                Write-Host $user.name
            }
        } else {
            Write-Host "Aucun utilisateur trouvé pour $site."
        }
    } catch {
        Write-Host "Échec de récupération des utilisateurs pour $site : $_"
    }
}
```

# Exemple 3
```ssh
# Définir les URLs des sites pour les utilisateurs
$sites = @(
    "https://www.crosemont.qc.ca/wp-json/wp/v2/users",
    "https://www.bdeb.qc.ca/wp-json/wp/v2/users",
    "https://www.collegecanada.com/wp-json/wp/v2/users",
    "https://institutelite.ca/wp-json/wp/v2/users",
    "https://www.lasallecollege.com/wp-json/wp/v2/users",
    "https://www.johnabbott.qc.ca/wp-json/wp/v2/users",
    "https://www.dawsoncollege.qc.ca/wp-json/wp/v2/users",
    "https://www.vaniercollege.qc.ca/wp-json/wp/v2/users",
    "https://www.claurendeau.qc.ca/wp-json/wp/v2/users",
    "https://www.cmaisonneuve.qc.ca/wp-json/wp/v2/users",
    "https://www.collegeahuntsic.qc.ca/wp-json/wp/v2/users",
    "https://www.cegepsl.qc.ca/wp-json/wp/v2/users",
    "https://www.cvm.qc.ca/wp-json/wp/v2/users",
    "https://www.marianopolis.edu/wp-json/wp/v2/users",
    "https://www.cimf.qc.ca/wp-json/wp/v2/users",
    "https://www.etsmtl.ca/wp-json/wp/v2/users",
    "https://www.cegepgarneau.ca/wp-json/wp/v2/users",
    "https://www.cegeplimoilou.ca/wp-json/wp/v2/users",
    "https://uqam.ca/wp-json/wp/v2/users",
    "https://umontreal.ca/wp-json/wp/v2/users",
    "https://enit.rnu.tn/wp-json/wp/v2/users",
    "https://www.cegeptr.qc.ca/wp-json/wp/v2/users",
    "https://www.cegepshawinigan.ca/wp-json/wp/v2/users",
    "https://www.clafleche.qc.ca/wp-json/wp/v2/users",
    "https://www.ellis.qc.ca/wp-json/wp/v2/users",
    "https://www.conservatoire.gouv.qc.ca/wp-json/wp/v2/users",
    "https://www.cegepst.qc.ca/wp-json/wp/v2/users",
    "https://www.cegepsth.qc.ca/wp-json/wp/v2/users",
    "https://www.cegepvalleyfield.ca/wp-json/wp/v2/users",
    "https://www.cegepmontpetit.ca/wp-json/wp/v2/users",
    "https://www.cstjean.qc.ca/wp-json/wp/v2/users",
    "https://www.champlainonline.com/wp-json/wp/v2/users",
    "https://www.academie-ent.com/wp-json/wp/v2/users",
    "https://www.airrichelieu.com/wp-json/wp/v2/users",
    "https://www.april-fortier.com/wp-json/wp/v2/users",
    "https://www.cdicollege.ca/wp-json/wp/v2/users",
    "https://www.collegeimmobilier.com/wp-json/wp/v2/users",
    "https://cargair.com/wp-json/wp/v2/users",
    "https://www.centreequestredechambly.com/wp-json/wp/v2/users",
    "https://sainthubertflyingcollege.com/wp-json/wp/v2/users",
    "https://collegemilestone.ca/wp-json/wp/v2/users",
    "https://helicraft.ca/wp-json/wp/v2/users",
    "https://www.teccart.qc.ca/wp-json/wp/v2/users",
    "https://www.itaq.ca/wp-json/wp/v2/users",
    "https://www.collegemv.qc.ca/wp-json/wp/v2/users",
    "https://www.cgodin.qc.ca/wp-json/wp/v2/users",
    "https://www.grasset.qc.ca/wp-json/wp/v2/users",
    "https://www.brebeuf.qc.ca/wp-json/wp/v2/users",
    "https://www.collegedecarie.ca/wp-json/wp/v2/users",
    "https://www.osullivan.edu/wp-json/wp/v2/users",
    "https://collegeuniversel.ca/wp-json/wp/v2/users",
    "https://inkcrown.com/wp-json/wp/v2/users"
)

# Boucler sur chaque site pour récupérer les données des utilisateurs
foreach ($site in $sites) {
    try {
        # Tenter de récupérer les données utilisateur
        $users = Invoke-RestMethod -Uri $site -UseBasicParsing
        # Vérifier si des utilisateurs sont trouvés
        if ($users.count -gt 0) {
            Write-Host "Utilisateurs du site $site :"
            foreach ($user in $users) {
                Write-Host $user.name
            }
        } else {
            Write-Host "Aucun utilisateur trouvé pour $site."
        }
    } catch {
        Write-Host "Échec de récupération des utilisateurs pour $site : $_"
    }
}
```


# Exemple 4

```ssh
# Définir les URLs des sites pour les utilisateurs
$sites = @(
       "https://www.crosemont.qc.ca/",
       "https://www.bdeb.qc.ca/",
       "https://www.collegecanada.com/",
       "https://institutelite.ca/",
       "https://www.lasallecollege.com/",
       "https://www.johnabbott.qc.ca/",
       "https://www.dawsoncollege.qc.ca/",
       "https://www.vaniercollege.qc.ca/",
       "https://www.claurendeau.qc.ca/",
       "https://www.cmaisonneuve.qc.ca/",
       "https://www.collegeahuntsic.qc.ca/",
       "https://www.cegepsl.qc.ca/",
       "https://www.cvm.qc.ca/",
       "https://www.marianopolis.edu/",
       "https://www.cimf.qc.ca/",
       "https://www.etsmtl.ca/",
       "https://www.cegepgarneau.ca/",
       "https://www.cegeplimoilou.ca/",
       "https://uqam.ca/",
       "https://umontreal.ca/",
       "https://enit.rnu.tn/",
       "https://www.cegeptr.qc.ca/",
       "https://www.cegepshawinigan.ca/",
       "https://www.clafleche.qc.ca/",
       "https://www.ellis.qc.ca/",
       "https://www.conservatoire.gouv.qc.ca/",
       "https://www.cegepst.qc.ca/",
       "https://www.cegepsth.qc.ca/",
       "https://www.cegepvalleyfield.ca/",
       "https://www.cegepmontpetit.ca/",
       "https://www.cstjean.qc.ca/",
       "https://www.champlainonline.com/",
       "https://www.academie-ent.com/",
       "https://www.airrichelieu.com/",
       "https://www.april-fortier.com/",
       "https://www.cdicollege.ca/",
       "https://www.collegeimmobilier.com/",
       "https://cargair.com/",
       "https://www.centreequestredechambly.com/",
       "https://sainthubertflyingcollege.com/",
       "https://collegemilestone.ca/",
       "https://helicraft.ca/",
       "https://www.teccart.qc.ca/",
       "https://www.itaq.ca/",
       "https://www.collegemv.qc.ca/",
       "https://www.cgodin.qc.ca/",
       "https://www.grasset.qc.ca/",
       "https://www.brebeuf.qc.ca/",
       "https://www.collegedecarie.ca/",
       "https://www.osullivan.edu/",
       "https://collegeuniversel.ca/",
       "https://inkcrown.com/"
)

# Initialiser le rapport HTML
$htmlReport = @"
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <title>Rapport des utilisateurs WordPress</title>
    <style>
        body { font-family: Arial, sans-serif; }
        table { width: 100%; border-collapse: collapse; }
        th, td { border: 1px solid #dddddd; padding: 8px; text-align: left; }
        th { background-color: #f2f2f2; }
    </style>
</head>
<body>
    <h1>Rapport des utilisateurs WordPress</h1>
    <table>
        <tr>
            <th>Site</th>
            <th>Statut</th>
            <th>Utilisateurs</th>
        </tr>
"@

# Boucler sur chaque site
foreach ($site in $sites) {
    $usersList = ""
    $status = "Accessible"
    try {
        $users = Invoke-RestMethod -Uri "$site/wp-json/wp/v2/users" -UseBasicParsing
        if ($users.count -gt 0) {
            foreach ($user in $users) {
                $usersList += $user.name + "<br>"
            }
        } else {
            $usersList = "Aucun utilisateur trouvé"
        }
    } catch {
        $status = "Non accessible (Erreur: $($_.Exception.Message))"
    }

    # Ajouter les résultats au rapport HTML
    $htmlReport += @"
        <tr>
            <td>$site</td>
            <td>$status</td>
            <td>$usersList</td>
        </tr>
"@
}

# Terminer le rapport HTML
$htmlReport += @"
    </table>
</body>
</html>
"@

# Enregistrer le rapport HTML dans un fichier
Set-Content -Path "rapport_utilisateurs.html" -Value $htmlReport

# Ouvrir le rapport dans le navigateur par défaut
Start-Process "rapport_utilisateurs.html"

```
