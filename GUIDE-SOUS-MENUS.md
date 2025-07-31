# 📋 Guide Simple : Ajouter des Sous-Menus

## 🎯 Comment Ajouter un Sous-Menu en 3 Étapes

### **Étape 1 : Créer le Dossier et les Fichiers**

```bash
# Créer un sous-dossier pour votre thème
mkdir content/categorie/nom-du-theme

# Exemple pour Linux
mkdir content/sysadmin/linux
```

### **Étape 2 : Créer les Articles**

Créez vos fichiers `.md` dans le sous-dossier :

```markdown
---
title: "Titre de l'Article"
description: "Description"
category: "Catégorie"
tags: ["tag1", "tag2"]
level: "Niveau"
reading_time: "X min"
last_updated: "Date"
author: "Votre Nom"
parent: "nom-du-parent"  # ← Important pour le breadcrumb
---

# Votre Contenu
```

### **Étape 3 : Modifier config.json**

Dans `content/config.json`, ajoutez les `subitems` à votre élément :

```json
{
  "id": "nom-parent",
  "title": "Titre Parent",
  "file": "categorie/fichier-principal.md",
  "badge": null,
  "subitems": [
    {
      "id": "sous-menu-1",
      "title": "Premier Sous-Menu",
      "file": "categorie/nom-du-theme/article1.md",
      "badge": null
    },
    {
      "id": "sous-menu-2",
      "title": "Deuxième Sous-Menu",
      "file": "categorie/nom-du-theme/article2.md",
      "badge": "NEW"
    }
  ]
}
```

## 📝 Exemple Complet : Linux Administration

### 1. Structure des Dossiers
```
content/
├── sysadmin/
│   ├── linux-admin.md          # Article principal
│   └── linux/                  # Sous-dossier
│       ├── installation.md
│       ├── commandes.md
│       └── securite.md
```

### 2. Configuration JSON
```json
{
  "id": "linux-admin",
  "title": "Linux Administration",
  "file": "sysadmin/linux-admin.md",
  "badge": null,
  "subitems": [
    {
      "id": "linux-installation",
      "title": "Installation & Configuration",
      "file": "sysadmin/linux/installation.md",
      "badge": null
    },
    {
      "id": "linux-commandes",
      "title": "Commandes Essentielles",
      "file": "sysadmin/linux/commandes.md",
      "badge": null
    },
    {
      "id": "linux-securite",
      "title": "Sécurisation",
      "file": "sysadmin/linux/securite.md",
      "badge": "NEW"
    }
  ]
}
```

## 🎨 Fonctionnalités des Sous-Menus

### ✅ Ce qui Fonctionne Automatiquement

- **Toggle Visuel** : Clic sur le parent ▶/▼
- **Navigation** : Clic direct vers sous-articles
- **Breadcrumb** : Navigation contextuelle
- **Badges** : Indicateurs sur sous-menus
- **Animation** : Déploiement fluide
- **URLs** : Liens directs vers sous-articles
- **Recherche Intelligente** : Trouve les articles dans les sous-menus automatiquement

> **Note :** La fonction de recherche d'articles a été améliorée pour supporter les sous-menus. Aucune configuration supplémentaire n'est nécessaire.

### 🎯 Exemples d'Utilisation

**Pour Windows Server :**
- Installation & Configuration
- Rôles & Fonctionnalités  
- Sécurisation
- Dépannage

**Pour Linux :**
- Distributions
- Administration
- Scripting
- Services

**Pour Cybersécurité :**
- Audit
- Pentest
- Forensics
- Response

## 🔧 Personnalisation Avancée

### Modifier l'Apparence

Dans `index.html`, section CSS des sous-menus :

```css
.submenu-item {
    padding: 0.5rem 1rem 0.5rem 2rem !important;
    font-size: 0.9rem;
    /* Modifiez ici pour changer l'apparence */
}
```

### Ajouter des Icônes

```json
{
  "id": "article-id",
  "title": "🔧 Mon Article",  // Icône dans le titre
  "file": "chemin/fichier.md",
  "badge": "NEW"
}
```

## 🚀 Bonnes Pratiques

### ✅ Recommandations

1. **Maximum 5-6 sous-menus** par parent
2. **Noms courts** pour les titres
3. **Structure logique** (du général au spécifique)
4. **Badges utiles** ("NEW", "UPDATED", etc.)
5. **Chemins cohérents** pour les fichiers

### ❌ À Éviter

- Sous-menus de sous-menus (max 2 niveaux)
- Titres trop longs
- Trop de badges
- Structure désorganisée

## 🔧 Dépannage

### Problème : "Erreur: Impossible de charger l'article demandé"

**Solutions :**

1. **Vérifier le fichier existe** :
   ```bash
   # Vérifier que le fichier .md existe
   ls content/categorie/sous-dossier/article.md
   ```

2. **Vérifier la configuration JSON** :
   ```json
   // S'assurer que l'ID et le chemin sont corrects
   {
     "id": "article-id",  // ← Doit correspondre à l'URL
     "file": "categorie/sous-dossier/article.md"  // ← Chemin exact
   }
   ```

3. **Vérifier la console navigateur** (F12) :
   - Logs de debug disponibles
   - Messages d'erreur détaillés

### Problème : Sous-menu ne se déploie pas

**Vérifier que :**
- L'élément parent a bien `"subitems": [...]`
- Les crochets et virgules JSON sont corrects
- Le cache navigateur est vidé (Ctrl+F5)

## 🎉 Résultat Final

Après configuration, vous aurez :

```
📁 Administration Système
  📄 Windows Server                    ▼
      └ Installation & Configuration
      └ Rôles & Fonctionnalités
  📄 Linux Administration             ▶
  📄 Active Directory                 ▶
  📄 PowerShell                       ▶
```

**C'est tout !** Votre sous-menu est maintenant fonctionnel et facilement extensible ! 🎯 