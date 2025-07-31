# 📚 Guide Complet d'Utilisation du Wiki SysAdmin

> **Wiki 100% Markdown** - Tout est modifiable via des fichiers `.md` pour une simplicité maximale

---

## 🎯 Vue d'Ensemble

Ce wiki est conçu pour être **ultra-simple** à utiliser. Tout le contenu et la navigation sont gérés via des fichiers Markdown, sans avoir besoin de modifier du HTML ou du JavaScript.

### ✨ Fonctionnalités Principales
- **100% Markdown** : Tout le contenu est en `.md`
- **Navigation automatique** : La sidebar se génère automatiquement
- **Sous-menus dynamiques** : Système de navigation hiérarchique
- **Recherche intégrée** : Recherche client-side instantanée
- **Compatible GitHub Pages** : Fonctionne parfaitement en ligne
- **Responsive** : S'adapte à tous les écrans

---

## 📁 Structure des Fichiers

```
sysadmin-wiki/
├── index.html                    # Page principale (ne pas modifier)
├── content/
│   ├── navigation.md             # 🎛️ CONTRÔLE DE LA NAVIGATION
│   ├── sysadmin/                 # Administration Système
│   │   ├── windows-server.md
│   │   ├── linux-admin.md
│   │   ├── active-directory.md
│   │   ├── powershell.md
│   │   └── windows-server/       # Sous-menus
│   │       ├── installation.md
│   │       └── roles.md
│   ├── cybersecurite/           # Cybersécurité
│   │   ├── securite-reseau.md
│   │   ├── cryptographie.md
│   │   ├── pentest.md
│   │   └── siem.md
│   ├── infrastructure/           # Infrastructure
│   │   ├── virtualisation.md
│   │   ├── reseau.md
│   │   ├── stockage.md
│   │   ├── cloud.md
│   │   └── cloud/               # Sous-menus
│   │       ├── aws.md
│   │       ├── azure.md
│   │       └── gcp.md
│   ├── gestion-projet/          # Gestion de Projet
│   │   ├── methodologies.md
│   │   ├── outils.md
│   │   └── itil.md
│   └── devops/                  # DevOps
│       ├── docker.md
│       ├── ci-cd.md
│       ├── kubernetes.md
│       ├── docker/              # Sous-menus
│       │   ├── installation.md
│       │   └── compose.md
│       └── kubernetes/          # Sous-menus
│           ├── pods.md
│           └── deployments.md
└── GUIDE-UTILISATION-COMPLET.md # Ce guide
```

---

## 🎛️ Contrôle de la Navigation

### Fichier Principal : `content/navigation.md`

Ce fichier contrôle **entièrement** la sidebar. Voici comment il fonctionne :

```markdown
# 🗂️ Configuration de la Navigation

## ⚙️ Administration Système
<!-- order: 1, icon: ⚙️ -->

### Windows Server
<!-- file: sysadmin/windows-server.md, badge: HOT -->
- [Installation & Configuration](sysadmin/windows-server/installation.md)
- [Rôles & Fonctionnalités](sysadmin/windows-server/roles.md)

### [Linux Administration](sysadmin/linux-admin.md)
### [Active Directory](sysadmin/active-directory.md)
### [PowerShell](sysadmin/powershell.md)
<!-- badge: NEW -->
```

### 📝 Syntaxe de Navigation

#### Sections Principales
```markdown
## 🔒 Cybersécurité
<!-- order: 2, icon: 🔒 -->
```
- `##` = Section principale
- `<!-- order: X -->` = Ordre d'affichage
- `<!-- icon: 🎯 -->` = Icône de la section

#### Articles Simples
```markdown
### [Titre de l'Article](chemin/vers/fichier.md)
<!-- badge: NEW -->
```
- `###` = Article principal
- `[Titre](fichier.md)` = Lien vers le fichier
- `<!-- badge: HOT/NEW -->` = Badge optionnel

#### Articles avec Sous-menus
```markdown
### Docker
<!-- file: devops/docker.md, badge: NEW -->
- [Installation Docker](devops/docker/installation.md)
- [Docker Compose](devops/docker/compose.md)
```
- `### Titre` = Article parent
- `<!-- file: chemin.md -->` = Fichier de l'article parent
- `- [Sous-titre](chemin.md)` = Sous-articles

---

## 📝 Création et Modification d'Articles

### 1. Structure d'un Article Markdown

```markdown
---
title: "Titre de l'Article"
description: "Description courte de l'article"
category: "Administration Système"
tags: ["Windows Server", "Administration", "PowerShell"]
level: "Intermédiaire"
reading_time: "15 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# Titre Principal

## Introduction

Contenu de l'article...

## Section 1

### Sous-section 1.1

Contenu avec **gras**, *italique*, et `code`.

```powershell
# Exemple de code PowerShell
Get-Service | Where-Object {$_.Status -eq "Running"}
```

## Section 2

- Liste à puces
- Point 2
- Point 3

1. Liste numérotée
2. Point 2
3. Point 3

> **Note importante** : Cette information est cruciale.

### Tableaux

| Colonne 1 | Colonne 2 | Colonne 3 |
|-----------|-----------|-----------|
| Donnée 1  | Donnée 2  | Donnée 3  |
| Donnée 4  | Donnée 5  | Donnée 6  |

## Conclusion

Résumé et prochaines étapes...
```

### 2. Métadonnées (Front Matter)

Les métadonnées en haut du fichier contrôlent :
- **title** : Titre affiché dans la navigation
- **description** : Description pour la recherche
- **category** : Catégorie principale
- **tags** : Mots-clés pour la recherche
- **level** : Niveau de difficulté
- **reading_time** : Temps de lecture estimé
- **last_updated** : Date de dernière mise à jour
- **author** : Auteur de l'article

---

## ➕ Comment Ajouter du Contenu

### Ajouter un Article Simple

1. **Créer le fichier** : `content/section/nom-article.md`
2. **Ajouter le contenu** avec les métadonnées
3. **Ajouter à la navigation** dans `content/navigation.md`

**Exemple** :
```markdown
# Créer : content/sysadmin/backup-strategies.md

---
title: "Stratégies de Sauvegarde"
description: "Guide complet des stratégies de sauvegarde Windows"
category: "Administration Système"
tags: ["Backup", "Windows", "Sécurité"]
level: "Avancé"
reading_time: "20 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# Stratégies de Sauvegarde

Contenu de l'article...
```

**Ajouter à la navigation** :
```markdown
### [Stratégies de Sauvegarde](sysadmin/backup-strategies.md)
<!-- badge: HOT -->
```

### Ajouter une Section

1. **Créer le dossier** : `content/nouvelle-section/`
2. **Ajouter des articles** dans ce dossier
3. **Ajouter la section** dans `content/navigation.md`

**Exemple** :
```markdown
## 🆕 Nouvelle Section
<!-- order: 6, icon: 🆕 -->

### [Premier Article](nouvelle-section/premier-article.md)
### [Deuxième Article](nouvelle-section/deuxieme-article.md)
```

### Ajouter des Sous-menus

1. **Créer le dossier** : `content/section/sous-section/`
2. **Créer les fichiers** dans ce dossier
3. **Modifier la navigation** :

```markdown
### Article Principal
<!-- file: section/article-principal.md, badge: NEW -->
- [Sous-article 1](section/sous-section/sous-article1.md)
- [Sous-article 2](section/sous-section/sous-article2.md)
```

---

## 🔍 Fonctionnalité de Recherche

### Comment ça marche
- **Indexation automatique** : Tous les articles sont indexés
- **Recherche instantanée** : Résultats en temps réel
- **Recherche dans** : Titres, descriptions, tags, contenu

### Utilisation
1. Cliquer sur la barre de recherche (en haut à droite)
2. Taper des mots-clés
3. Les résultats s'affichent instantanément
4. Cliquer sur un résultat pour ouvrir l'article

### Améliorer la Recherche
Pour que vos articles soient bien trouvés :
- **Tags pertinents** : Ajouter des mots-clés dans les tags
- **Description claire** : Décrire précisément le contenu
- **Titre explicite** : Utiliser des titres descriptifs

---

## 🎨 Personnalisation

### Icônes Disponibles
```
🎯 ⚙️ 🔒 🏗️ 📋 🚀 🔧 📊 🌐 💻 📱 🔄 🎨 📝 🔍 🆕 🔥
```

### Badges Disponibles
- `HOT` : Article populaire/important
- `NEW` : Article récent

### Ordre des Sections
Utiliser `<!-- order: X -->` pour contrôler l'ordre :
- `order: 1` = Premier
- `order: 2` = Deuxième
- etc.

---

## 🚀 Déploiement

### Test Local
```bash
# Démarrer un serveur local
python -m http.server 8000
# Puis ouvrir http://localhost:8000
```

### GitHub Pages
1. **Pousser** les modifications sur GitHub
2. **Activer GitHub Pages** dans les paramètres du repo
3. **Sélectionner** la branche `main`
4. **Attendre** quelques minutes pour le déploiement

### Structure pour GitHub Pages
```
Repository/
├── index.html          # Page principale
├── content/            # Tous les fichiers Markdown
└── README.md          # Description du projet
```

---

## 🔧 Dépannage

### Problèmes Courants

#### 1. Article ne s'affiche pas
- **Vérifier** : Le fichier existe dans le bon dossier
- **Vérifier** : Le lien dans `navigation.md` est correct
- **Vérifier** : Les métadonnées sont bien formatées

#### 2. Sous-menu ne fonctionne pas
- **Vérifier** : La syntaxe dans `navigation.md` est correcte
- **Vérifier** : Les fichiers des sous-articles existent
- **Vérifier** : Le fichier parent est bien défini avec `<!-- file: -->`

#### 3. Recherche ne trouve rien
- **Vérifier** : Les métadonnées sont complètes
- **Vérifier** : Les tags sont pertinents
- **Vérifier** : La description est claire

#### 4. Erreur JavaScript
- **Actualiser** la page (Ctrl+F5)
- **Vérifier** la console du navigateur
- **Vérifier** que tous les fichiers sont bien créés

### Logs de Debug
Ouvrir la console du navigateur (F12) pour voir :
- ✅ Articles découverts
- ✅ Navigation générée
- ✅ Index de recherche créé
- ❌ Erreurs éventuelles

---

## 📋 Checklist de Création d'Article

- [ ] Créer le fichier `.md` dans le bon dossier
- [ ] Ajouter les métadonnées complètes
- [ ] Rédiger le contenu avec une structure claire
- [ ] Ajouter le lien dans `content/navigation.md`
- [ ] Tester l'affichage localement
- [ ] Vérifier que la recherche fonctionne
- [ ] Pousser sur GitHub

---

## 🎯 Bonnes Pratiques

### Rédaction
- **Titres clairs** : Utiliser des titres descriptifs
- **Structure logique** : Hiérarchie des sections
- **Code commenté** : Expliquer les commandes
- **Exemples concrets** : Donner des cas d'usage réels

### Organisation
- **Dossiers cohérents** : Respecter la structure existante
- **Noms de fichiers** : Utiliser des noms explicites
- **Tags pertinents** : Faciliter la recherche
- **Mise à jour régulière** : Maintenir les articles

### Navigation
- **Ordre logique** : Organiser les sections logiquement
- **Icônes cohérentes** : Utiliser des icônes appropriées
- **Badges utiles** : Marquer les articles importants
- **Sous-menus équilibrés** : Éviter les menus trop profonds

---

## 📞 Support

### En cas de problème :
1. **Vérifier** ce guide
2. **Consulter** la console du navigateur
3. **Tester** localement avant de pousser
4. **Vérifier** la syntaxe Markdown

### Ressources utiles :
- **Markdown** : [Guide de syntaxe](https://www.markdownguide.org/)
- **GitHub Pages** : [Documentation officielle](https://pages.github.com/)
- **JavaScript** : [Console de debug](https://developer.mozilla.org/fr/docs/Web/API/Console)

---

## 🎉 Conclusion

Ce wiki est conçu pour être **ultra-simple** à utiliser. Tout se fait via des fichiers Markdown, sans avoir besoin de connaissances techniques avancées.

**Rappel des points clés** :
- ✅ Tout en Markdown
- ✅ Navigation automatique
- ✅ Recherche intégrée
- ✅ Sous-menus dynamiques
- ✅ Compatible GitHub Pages
- ✅ Responsive design

**Pour commencer** : Modifiez `content/navigation.md` et créez vos premiers articles !

---

*Dernière mise à jour : 31 juillet 2025* 