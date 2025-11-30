# ⚡ Temps De Réaction Test

## 👤 Auteur

    Aissaoui Abderrahmen


## 📋 Description du projet

Application web interactive permettant de tester et mesurer votre temps de réaction visuel. Le joueur doit cliquer (ou appuyer sur la barre d'espace) le plus rapidement possible lorsqu'une boîte rouge devient verte. Le projet enregistre le meilleur score et classe les performances selon différents niveaux (Débutant, Intermédiaire, Avancé, Professionnel, Élite).

---

## 🛠️ Technologies utilisées

- **HTML5** : Structure de la page
- **CSS3** : Stylisation et design responsive
  - Flexbox pour la mise en page
  - Media queries pour la responsivité mobile
- **JavaScript** : Logique du jeu et interactivité
  - Event listeners (click, keydown)
  - LocalStorage API pour la persistance des données
  - Gestion avancée des événements (bubbling, propagation)
  - fonctions asynchrones (Timers)

---

## ✨ Fonctionnalités principales

### 🎮 Modes de jeu
- **Mode Souris** : Interaction par clic de souris
- **Mode Clavier** : Interaction par appui sur la barre d'espace
- Sauvegarde du mode choisi entre les sessions

### 📊 Système de scoring
- Enregistrement du meilleur temps personnel dans le localStorage
- Classification par niveaux :
  - 🐢 Débutant : 400+ ms
  - 🎯 Intermédiaire : 300-399 ms
  - 🚀 Avancé : 200-299 ms
  - 🏆 Professionnel : 150-199 ms
  - 👑 Élite : 0-149 ms

### 🎯 Détection de triche
- Système anti-triche : détecte si l'utilisateur clique avant que l'écran ne devienne vert
- Message d'erreur "TROP TÔT !" avec possibilité de réessayer

### 📱 Design responsive
- Interface adaptée aux écrans desktop et mobile
- Boutons et textes optimisés pour différentes tailles d'écran
- Utilisation d'unités relatives (`em`) au lieu de pixels fixes pour une meilleure scalabilité
- Media queries pour adaptation mobile (< 768px)

---

## 🔗 Lien vers le projet

**GitHub Pages** : https://abderrahmenaissaoui.github.io/Abderrahmen_Aissaoui_Reaction_rapide/

**Repository GitHub** : https://github.com/abderrahmenaissaoui/Abderrahmen_Aissaoui_Reaction_rapide

---

## 🚀 Nouveautés explorées

### Ce que j'ai appris durant ce projet :

1. **Event Bubbling et Propagation**
   - Compréhension approfondie du mécanisme de propagation(Bubbling) des événements dans le DOM grace à un problème rencontré lors du travail.

2. **LocalStorage API**
   - Sauvegarde persistante des données (score et mode d'entrée)
   - Méthodes : `getItem()`, `setItem()`
   - Conversion entre types de données avec `parseInt()` car local storage store toujours en chaine de caractères

3. **Gestion avancée des événements**
   - `addEventListener()` et `removeEventListener()`
   - `e.preventDefault()` pour bloquer les comportements par défaut

4. **Timers JavaScript**
   - `setTimeout()` pour créer des délais
   - `clearTimeout()` pour annuler des timers
   - `Date.now()` pour mesurer le temps avec précision


## 🔧 Difficultés rencontrées

### 1. **Propagation d'événement inattendue** 🐛

**Problème :** Lorsque l'utilisateur cliquait sur le bouton "start", le système détectait immédiatement un clic "trop tôt", même si l'écran n'était pas encore rouge.

**Cause technique :**
```
Timeline du bug :
0ms   : Clic sur <button id="start">
0.1ms : startTest() s'exécute
0.2ms : addEventListener("click", checkEarly) ajouté sur test-container (div qu'on va cliquer au jeu)
0.3ms : startTest() se termine
0.4ms : Le clic REMONTE (bubbling) vers <div>
0.5ms : checkEarly() détecte le clic → "TROP TÔT !" ❌
```

Le problème venait du **event bubbling** : le clic sur le bouton (qui est un enfant de `test-container`) remontait naturellement vers le parent après terminer startTest(), où `checkEarly()` venait d'être ajouté.

**Solution :** Ajout d'un délai de 50ms avec `setTimeout()` avant d'attacher l'événement `checkEarly`, permettant à la propagation du clic initial de se terminer :

```javascript
setTimeout(() => {
    testContainer.addEventListener("click", checkEarly);
}, 50);
```

---

### 2. **Différence entre `e.code` en JavaScript** ⌨️
**Problème:** Comment détecter l'utilisation d'espace.

**Solution :** La propriété `e.code` renvoie les codes avec majuscule : `"Space"`, `"Enter"`, `"KeyA"`, etc.

---

## 📚 Solutions et méthodologie

### Recherche et documentation
 J'ai utilisé le chatbot Claude pour comprendre de nouveau concepts

### Tests et itérations
2. Tests en inspects mode pour vérifier la responsivité

### Bonnes pratiques appliquées
- **Nettoyage des événements** : Utilisation systématique de `removeEventListener()` pour éviter les fuites mémoire
- **Commentaires détaillés** : Documentation du code pour faciliter la maintenance
- **Code organisé** : Séparation claire entre initialisation, logique du jeu, et gestion des événements

---

## 🎓 Compétences développées

- Manipulation avancée du DOM
- Gestion des événements JavaScript
- Design responsive
- Debugging et résolution de problèmes techniques