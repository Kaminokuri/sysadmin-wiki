# 🔍 Guide de la Fonction Recherche

## 🎯 Recherche Côté Client - Compatible GitHub Pages

La fonction de recherche a été conçue pour être **100% compatible avec GitHub Pages** en fonctionnant entièrement côté client, sans besoin de serveur backend.

## ✨ Fonctionnalités

### 🚀 Recherche Intelligente
- **Recherche en temps réel** avec debounce (300ms)
- **Score de pertinence** pour classer les résultats
- **Recherche multi-critères** : titre, description, catégorie, tags, mots-clés
- **Highlight** des termes trouvés
- **Limite de 8 résultats** pour la performance

### ⌨️ Interface Utilisateur
- **Barre de recherche** intégrée dans la sidebar
- **Autocomplete** désactivée pour éviter les conflits
- **Raccourci clavier** : `Ctrl+K` ou `Cmd+K`
- **Navigation clavier** : 
  - `Entrée` pour sélectionner le premier résultat
  - `Échap` pour fermer les résultats
- **Responsive** pour mobile

## 📊 Comment Ça Marche

### 1. Index de Recherche

Chaque article est indexé avec :
```javascript
"article-id": {
    title: "Titre de l'Article",
    description: "Description complète",
    category: "Catégorie",
    tags: ["tag1", "tag2", "tag3"],
    keywords: "mots-clés supplémentaires pour la recherche"
}
```

### 2. Algorithme de Score

**Pondération des correspondances :**
- **Titre** : +10 points
- **Catégorie** : +8 points  
- **Tags** : +7 points
- **Mots-clés** : +6 points
- **Description** : +5 points
- **Mots individuels** : +2 points chacun

### 3. Processus de Recherche

1. **Saisie utilisateur** (minimum 2 caractères)
2. **Normalisation** (minuscules, trim)
3. **Calcul des scores** pour chaque article
4. **Tri par pertinence** décroissante
5. **Limitation** à 8 résultats
6. **Affichage** avec highlighting

## 🆕 Ajouter un Nouvel Article à l'Index

### 1. Créer l'Article Markdown

Créez votre fichier : `content/categorie/mon-article.md`

### 2. Ajouter au Mapping

Dans `index.html`, section `articlesMapping` :
```javascript
const articlesMapping = {
    // ... articles existants ...
    "mon-article": "content/categorie/mon-article.md",
};
```

### 3. Ajouter à l'Index de Recherche

Dans `index.html`, section `searchIndex` :
```javascript
const searchIndex = {
    // ... articles existants ...
    "mon-article": {
        title: "Titre de Mon Article",
        description: "Description détaillée pour la recherche",
        category: "Ma Catégorie",
        tags: ["tag1", "tag2", "tag3"],
        keywords: "mots-clés supplémentaires recherche optimisation seo"
    },
};
```

### 4. Ajouter à la Sidebar

```html
<div class="nav-item">
    <a href="#" onclick="loadMarkdownArticle('mon-article')" class="nav-link">
        <span>Mon Article</span>
        <span class="badge">NEW</span>
    </a>
</div>
```

## 🎨 Optimiser pour la Recherche

### Choisir des Mots-Clés Pertinents

```javascript
keywords: "docker conteneur containerization devops kubernetes orchestration deployment"
```

**Incluez :**
- **Synonymes** et **variantes**
- **Termes techniques** spécifiques
- **Acronymes** et **abréviations**
- **Technologies liées**
- **Cas d'usage** courants

### Exemples d'Optimisation

**❌ Trop basique :**
```javascript
keywords: "windows server"
```

**✅ Optimisé :**
```javascript
keywords: "windows server 2022 administration système entreprise configuration réseau sécurité active directory dns dhcp iis hyper-v failover cluster"
```

## 🔧 Personnalisation de la Recherche

### Modifier le Seuil Minimum

```javascript
// Dans performSearch()
if (query.length < 3) { // Au lieu de 2
    hideSearchResults();
    return;
}
```

### Ajuster les Scores

```javascript
// Dans performSearch(), section score
if (data.title.toLowerCase().includes(query)) score += 15; // Au lieu de 10
if (data.description.toLowerCase().includes(query)) score += 8; // Au lieu de 5
```

### Changer le Nombre de Résultats

```javascript
// Dans performSearch()
const limitedResults = results.slice(0, 12); // Au lieu de 8
```

### Modifier le Délai de Recherche

```javascript
// Dans initializeSearch()
searchTimeout = setTimeout(() => {
    performSearch(e.target.value);
}, 200); // Au lieu de 300ms
```

## 📱 Fonctionnalités Avancées

### Raccourcis Clavier

- **`Ctrl+K` / `Cmd+K`** : Focus sur la barre de recherche
- **`Entrée`** : Sélectionner le premier résultat
- **`Échap`** : Fermer les résultats et perdre le focus

### Recherche Multi-Mots

```
"windows server"     → Recherche des deux mots
"active directory"   → Recherche spécifique AD
"sécurité réseau"    → Combine sécurité ET réseau
```

### Recherche par Catégorie

```
"infrastructure"     → Tous les articles infrastructure
"cybersécurité"     → Tous les articles sécurité
"administration"    → Articles d'administration
```

## 🎯 Bonnes Pratiques

### Pour les Rédacteurs

1. **Titres descriptifs** : "Docker - Conteneurisation" plutôt que "Docker"
2. **Descriptions complètes** : Inclure le contexte et l'usage
3. **Tags pertinents** : 3-5 tags spécifiques
4. **Mots-clés exhaustifs** : Penser aux termes de recherche utilisateur

### Pour les Développeurs

1. **Index à jour** : Synchroniser avec les nouveaux articles
2. **Performance** : Limiter les résultats et optimiser les regex
3. **UX** : Debounce et feedback visuel
4. **Accessibilité** : Support clavier complet

## 🚀 Avantages de Cette Approche

### ✅ Compatibilité GitHub Pages
- **Aucun serveur** requis
- **Pas de base de données**
- **JavaScript pur** côté client
- **Déploiement simple**

### ✅ Performance
- **Index en mémoire** (chargement rapide)
- **Recherche instantanée** (pas de requête réseau)
- **Cache navigateur** optimisé
- **Debounce** pour éviter les calculs excessifs

### ✅ Expérience Utilisateur
- **Résultats en temps réel**
- **Highlighting** des termes
- **Navigation clavier**
- **Interface intuitive**

### ✅ SEO et Accessibilité
- **Contenu indexable** (articles en Markdown)
- **URLs propres** avec query params
- **Support screen readers**
- **Navigation au clavier**

## 🔍 Exemple d'Utilisation

### Recherche "powershell"
**Résultats attendus :**
1. **PowerShell** (Administration Système) - Score élevé (titre exact)
2. **Windows Server 2022** (Administration Système) - Score moyen (keywords)

### Recherche "sécurité"
**Résultats attendus :**
1. **Sécurité Réseau** (Cybersécurité) - Score élevé (titre)
2. **Windows Server 2022** (Administration Système) - Score moyen (keywords)
3. **Cryptographie** (Cybersécurité) - Score moyen (tags)
4. **Tests d'Intrusion** (Cybersécurité) - Score faible (description)

## 🎉 Résultat Final

Une fonction de recherche **moderne, rapide et intuitive** qui :
- ✅ Fonctionne sur **GitHub Pages**
- ✅ Recherche **intelligente** avec scoring
- ✅ Interface **responsive** et accessible
- ✅ **Zéro configuration** serveur
- ✅ **Performance optimale**

**La recherche parfaite pour un wiki statique !** 🚀