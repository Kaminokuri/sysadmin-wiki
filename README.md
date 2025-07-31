# Wiki Cybersécurité & Administration Systèmes

Ce wiki utilise maintenant un système de gestion de contenu basé sur Markdown, permettant une modification facile du contenu sans toucher au CSS ou au HTML principal.

## 🚀 Structure du Projet

```
sysadmin-wiki/
├── index.html              # Interface principale (CSS + JS)
├── content/                # Dossier contenant tous les contenus
│   ├── config.json        # Configuration de la navigation
│   ├── sysadmin/          # Articles d'administration système
│   ├── cybersecurite/     # Articles de cybersécurité
│   ├── infrastructure/    # Articles d'infrastructure
│   └── gestion-projet/    # Articles de gestion de projet
└── README.md              # Ce fichier
```

## ✍️ Comment Ajouter un Nouvel Article

### 1. Créer le fichier Markdown

Créez un nouveau fichier `.md` dans le bon dossier de catégorie :

```bash
# Exemple pour un article sur Docker
content/infrastructure/docker.md
```

### 2. Ajouter les métadonnées (Front Matter)

Chaque article doit commencer par des métadonnées YAML :

```yaml
---
title: "Titre de l'article"
description: "Description courte de l'article"
category: "Nom de la catégorie"
tags: ["tag1", "tag2", "tag3"]
level: "Débutant|Intermédiaire|Avancé"
reading_time: "X min"
last_updated: "Date de mise à jour"
author: "Nom de l'auteur"
---
```

### 3. Écrire le contenu en Markdown

```markdown
# Titre Principal

## Section 1

Votre contenu ici...

### Sous-section

```bash
# Exemple de code
sudo apt update
```

> **Note:** Les alertes sont créées avec des blockquotes.

| Colonne 1 | Colonne 2 |
|-----------|-----------|
| Donnée 1  | Donnée 2  |
```

### 4. Ajouter l'article à la navigation

Modifiez le fichier `content/config.json` pour ajouter votre article :

```json
{
  "navigation": {
    "Infrastructure": {
      "icon": "🏗️",
      "items": [
        {
          "id": "docker",
          "title": "Docker",
          "file": "infrastructure/docker.md",
          "badge": "NEW"
        }
      ]
    }
  }
}
```

## 🎨 Fonctionnalités Markdown Supportées

### Alertes
```markdown
> **Note:** Message d'information
> **Attention:** Message d'avertissement
```

### Blocs de Code
```markdown
```bash
sudo systemctl restart nginx
```
```

### Tableaux
```markdown
| Colonne 1 | Colonne 2 |
|-----------|-----------|
| Donnée    | Autre     |
```

### Liens et Images
```markdown
[Lien externe](https://example.com)
![Image](url-de-l-image.jpg)
```

## 🔧 Configuration Avancée

### Modifier la Navigation

Éditez `content/config.json` pour :
- Ajouter/supprimer des catégories
- Changer les icônes des sections
- Réorganiser l'ordre des articles
- Ajouter des badges ("NEW", "UPDATED", etc.)

### Personnaliser les Métadonnées

Les champs supportés dans le front matter :
- `title` : Titre affiché
- `description` : Description pour le SEO
- `category` : Catégorie de l'article
- `tags` : Tags pour la recherche
- `level` : Niveau de difficulté
- `reading_time` : Temps de lecture estimé
- `last_updated` : Date de dernière modification
- `author` : Auteur de l'article

## 📱 Fonctionnalités

- ✅ **Responsive Design** : Interface adaptée mobile/desktop
- ✅ **Recherche en Temps Réel** : Recherche dans le contenu
- ✅ **Navigation Dynamique** : Génération automatique du menu
- ✅ **Coloration Syntaxique** : Support de nombreux langages
- ✅ **Copie de Code** : Bouton de copie sur tous les blocs
- ✅ **URLs Persistantes** : Liens directs vers les articles
- ✅ **Breadcrumb Automatique** : Navigation contextuelle

## 🚀 Utilisation

1. **Développement Local** : Ouvrez `index.html` dans votre navigateur
2. **Serveur Web** : Déployez tous les fichiers sur votre serveur
3. **Modification** : Éditez les fichiers `.md` et rechargez la page

## 📝 Exemple Complet

Voici un exemple d'article complet :

```markdown
---
title: "Configuration SSH Sécurisée"
description: "Guide complet pour sécuriser un serveur SSH"
category: "Cybersécurité"
tags: ["SSH", "Sécurité", "Linux"]
level: "Intermédiaire"
reading_time: "10 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
---

# Configuration SSH Sécurisée

## Introduction

SSH est un protocole essentiel pour l'administration système...

## Configuration de Base

```bash
# Éditer le fichier de configuration
sudo nano /etc/ssh/sshd_config
```

> **Attention:** Toujours garder une session active lors de modifications SSH.

## Bonnes Pratiques

- Désactiver l'authentification par mot de passe
- Utiliser des clés SSH
- Changer le port par défaut

| Paramètre | Valeur Recommandée |
|-----------|-------------------|
| Port | 2222 |
| PasswordAuthentication | no |
| PermitRootLogin | no |
```

Cette structure permet une maintenance facile du contenu tout en conservant une interface professionnelle et moderne ! 