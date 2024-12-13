### ** Les Inputs et les Manipulations du DOM comme Vecteurs d'Attaques**

---

#### **Introduction**
Les inputs utilisateur et les manipulations du Document Object Model (DOM) constituent des aspects fondamentaux des applications web modernes. Cependant, mal gérés, ils deviennent des vecteurs d'attaques critiques. Comprendre comment ces attaques se produisent et les prévenir est essentiel pour sécuriser vos applications.

---

#### **1. Comprendre les Vecteurs d'Attaques**
1. **Inputs utilisateur :**
   - Les données fournies par les utilisateurs peuvent contenir des scripts malveillants, du code SQL ou d'autres contenus exploitables.
   - Exemple : Champs de formulaire, URL, cookies.

2. **Manipulations du DOM :**
   - Les modifications dynamiques du DOM par JavaScript, souvent basées sur des inputs utilisateur, peuvent introduire des vulnérabilités.
   - Exemple : Ajout de contenu HTML via `innerHTML` sans vérification.

---

#### **2. Principaux Types d'Attaques Liées aux Inputs et au DOM**
1. **Injection SQL :**
   - Exploitation des entrées utilisateur pour insérer du code SQL malveillant dans les requêtes de base de données.
   - Exemple : Champ de login permettant d'exécuter `DROP TABLE`.

2. **Cross-Site Scripting (XSS) :**
   - Injection de scripts malveillants dans des pages web pour voler des données ou contourner des politiques de sécurité.
   - Exemple : `<script>alert('XSS!')</script>` inséré dans un champ de commentaire.

3. **Cross-Site Request Forgery (CSRF) :**
   - Exploitation des sessions d'utilisateurs authentifiés pour exécuter des actions malveillantes.
   - Exemple : L’utilisateur clique sur un lien malveillant qui déclenche une action non désirée.

4. **DOM-Based XSS :**
   - Les scripts malveillants injectés manipulent directement le DOM côté client sans interaction avec le serveur.
   - Exemple : Modification d’un élément HTML avec du contenu injecté via JavaScript.

---

#### **3. Démonstration : Exemple d’Attaque XSS**
##### Code vulnérable :
```html
<!DOCTYPE html>
<html>
  <body>
    <input id="userInput" placeholder="Entrez votre nom" />
    <button onclick="greetUser()">Envoyer</button>
    <div id="output"></div>

    <script>
      function greetUser() {
        const input = document.getElementById("userInput").value;
        document.getElementById("output").innerHTML = "Bonjour, " + input;
      }
    </script>
  </body>
</html>
```

##### Exploitation :
Un attaquant peut entrer :  
`<script>alert('Vous avez été piraté!')</script>`  
Cela affichera une alerte car le contenu de l’input est directement inséré dans le DOM sans validation.

---

#### **4. Bonnes Pratiques de Sécurité**
1. **Validation côté client et côté serveur :**
   - Assurez-vous que les données saisies respectent des règles strictes.
   - Exemple : Utilisez des expressions régulières pour vérifier les formats autorisés.

2. **Echapper les données insérées dans le DOM :**
   - Utilisez des fonctions sécurisées pour manipuler le DOM :
     ```javascript
     const safeContent = document.createTextNode(input);
     document.getElementById("output").appendChild(safeContent);
     ```

3. **Désactiver l’exécution de scripts inutiles :**
   - Utilisez des attributs comme `Content-Security-Policy (CSP)` pour limiter l’exécution de scripts externes.

4. **Évitez `innerHTML` autant que possible :**
   - Préférez des méthodes sécurisées comme `textContent` ou `appendChild`.

5. **Sanitisation des entrées utilisateur :**
   - Nettoyez toutes les données avant de les traiter ou de les afficher.
   - Utilisez des bibliothèques comme **DOMPurify** pour nettoyer les inputs HTML.

6. **Utilisation de tokens pour prévenir les CSRF :**
   - Implémentez des jetons (tokens) dans les formulaires et les requêtes sensibles.

---

#### **5. Exemple de Code Sécurisé**
```html
<!DOCTYPE html>
<html>
  <body>
    <input id="userInput" placeholder="Entrez votre nom" />
    <button onclick="greetUser()">Envoyer</button>
    <div id="output"></div>

    <script>
      function greetUser() {
        const input = document.getElementById("userInput").value;
        const safeContent = document.createTextNode("Bonjour, " + input);
        const outputDiv = document.getElementById("output");

        outputDiv.innerHTML = ''; // Supprime tout contenu existant
        outputDiv.appendChild(safeContent); // Ajoute du contenu sécurisé
      }
    </script>
  </body>
</html>
```

---

#### **6. Étapes pour Sécuriser vos Applications**
1. **Effectuer des audits de sécurité réguliers.**
2. **Sensibiliser les équipes de développement aux vecteurs d'attaques courants.**
3. **Automatiser les tests de sécurité avec des outils comme OWASP ZAP ou Burp Suite.**
4. **Mettre à jour régulièrement les bibliothèques et frameworks utilisés.**

---

#### **Conclusion**
Les inputs utilisateur et les manipulations du DOM sont essentiels aux applications modernes mais aussi des cibles privilégiées pour les attaquants. En appliquant des pratiques de développement sécurisé, vous réduisez les risques tout en offrant une meilleure expérience utilisateur.

--- 

**Exercice :** Analysez un formulaire web de votre choix. Identifiez les potentielles failles de sécurité et proposez des améliorations en vous basant sur les bonnes pratiques vues en cours.
