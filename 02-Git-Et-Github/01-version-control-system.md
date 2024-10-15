-----------------------------------------------
# 01 version control system
-----------------------------------------------

# **Système de Contrôle de Version (Version Control System)**

Un **système de contrôle de version** est un outil qui permet de suivre les modifications apportées aux fichiers d’un projet au fil du temps, afin que vous puissiez restaurer ou examiner une version spécifique ultérieurement. 

Cela permet aux développeurs de travailler ensemble efficacement sur des projets, en conservant un historique détaillé des modifications, des versions et des fonctionnalités ajoutées.

## **Pourquoi utiliser un système de contrôle de version ?**
- **Historique des changements** : Chaque modification du code est enregistrée, ce qui permet de revenir à un état antérieur.
- **Collaboration** : Plusieurs développeurs peuvent travailler simultanément sur le même projet, avec une gestion des versions pour fusionner leurs travaux.
- **Suivi des erreurs** : Si une erreur ou un bug apparaît, vous pouvez identifier précisément le changement qui l’a provoquée.
- **Sauvegarde** : Votre code est sauvegardé de manière sécurisée, souvent sur des serveurs distants, et peut être restauré à tout moment.

## **Types de Systèmes de Contrôle de Version**

1. **Système de Contrôle de Version Local (Local Version Control System)**  
2. **Système de Contrôle de Version Centralisé (Centralized Version Control System - CVCS)**  
3. **Système de Contrôle de Version Distribué (Distributed Version Control System - DVCS)**  

---

### **Système de Contrôle de Version Local (Local Version Control System)**

Dans un **système de contrôle de version local**, les modifications de fichiers sont suivies localement sur l’ordinateur d’un développeur. Ce type de versionnement est simple mais comporte des limites importantes en termes de collaboration.

Exemple :
- **RCS** (Revision Control System)

#### **Avantages** :
- Simplicité d’installation et de gestion.
- Fonctionne indépendamment d’une connexion réseau.

#### **Inconvénients** :
- Peu pratique pour la collaboration : les autres développeurs ne peuvent pas accéder aux fichiers versionnés.
- Risque de perte de données en cas de panne de l’ordinateur local.

---

### **Système de Contrôle de Version Centralisé (Centralized Version Control System - CVCS)**

Un **système de contrôle de version centralisé** (CVCS) repose sur un serveur centralisé où sont stockées toutes les versions des fichiers. Les développeurs récupèrent des copies des fichiers depuis le serveur pour y travailler, puis soumettent leurs modifications au même serveur.

Exemples :
- **Subversion (SVN)**
- **CVS (Concurrent Versions System)**

#### **Avantages** :
- Tous les fichiers et leur historique sont centralisés sur un serveur.
- Bonne gestion de la collaboration grâce à un accès contrôlé.

#### **Inconvénients** :
- Dépendance à un serveur central : si le serveur devient indisponible, les développeurs ne peuvent plus accéder au dépôt.
- Risque de surcharge du serveur central avec de nombreux utilisateurs actifs.

---

### **Système de Contrôle de Version Distribué (Distributed Version Control System - DVCS)**

Dans un **système de contrôle de version distribué** (DVCS), chaque développeur possède une copie complète du dépôt, y compris tout l’historique de révisions. Cela permet une plus grande flexibilité et une meilleure résilience, car chaque machine peut servir de sauvegarde.

Exemple :
- **Git** (un des outils de contrôle de version les plus populaires)

#### **Avantages** :
- Chaque développeur possède une copie complète de l’historique du projet, rendant le travail hors ligne possible.
- Réduction de la dépendance à un serveur central, car même si le serveur tombe en panne, les développeurs peuvent continuer à travailler.
- Fusion efficace des changements grâce à des algorithmes avancés comme ceux utilisés dans **Git**.

#### **Inconvénients** :
- La gestion des copies distribuées peut être plus complexe, surtout pour les débutants.
- Risque de confusion si de nombreux développeurs soumettent des modifications simultanément sans coordination.

---

## **Comparaison des systèmes de contrôle de version**

| Critère                               | Local VCS          | Centralisé VCS        | Distribué VCS         |
|---------------------------------------|--------------------|-----------------------|-----------------------|
| **Stockage des révisions**            | Local               | Serveur centralisé    | Distribué sur toutes les machines |
| **Collaboration**                     | Difficile           | Simple mais dépend du serveur | Très efficace, chaque développeur peut travailler en parallèle |
| **Travail hors ligne**                | Oui                 | Non                   | Oui                   |
| **Risque de perte de données**        | Élevé               | Dépend du serveur     | Faible (copies multiples) |
| **Complexité de gestion**             | Simple              | Modérée               | Plus complexe         |

---

## **Conclusion**

Le choix du système de contrôle de version dépend de la taille et de la nature du projet ainsi que des besoins de l’équipe. Pour des projets personnels ou de petite envergure, un **système local** peut suffire. Cependant, pour les projets nécessitant une collaboration entre plusieurs développeurs, un **système distribué** comme **Git** offre une flexibilité et une robustesse inégalées.

**Git** est aujourd’hui largement adopté dans l’industrie du logiciel grâce à sa capacité à gérer efficacement des projets de grande envergure avec plusieurs développeurs.

# Conclusion

Ce cours a couvert les types de systèmes de contrôle de version et leurs avantages respectifs. **Git**, en tant que système distribué, est souvent préféré pour sa flexibilité et sa robustesse.
