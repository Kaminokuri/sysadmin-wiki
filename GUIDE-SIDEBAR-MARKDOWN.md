# 📋 Guide : Sidebar en Markdown

## 🎯 Système Ultra-Simple

Maintenant, la **sidebar est entièrement gérée en Markdown** ! Plus besoin de JSON complexe.

## 📁 Structure des Fichiers

```
content/
├── navigation.md        # 🆕 Définit la sidebar
├── articles.json        # 🆕 Mapping ID → fichier
├── config.json          # ❌ Plus utilisé
└── [dossiers articles]
```

## ✍️ Comment Modifier la Sidebar

### 1. Éditer `content/navigation.md`

```markdown
# Navigation Wiki

## ⚙️ Administration Système

### [Windows Server](windows-server)
- [Installation & Configuration](windows-server-installation)
- [Rôles & Fonctionnalités](windows-server-roles)

### [Linux Administration](linux-admin)

### [PowerShell](powershell) `NEW`

## 🔒 Cybersécurité

### [Sécurité Réseau](securite-reseau)

### [Cryptographie](cryptographie)
```

### 2. Ajouter l'article dans `content/articles.json`

```json
{
  "articles": {
    "windows-server": "sysadmin/windows-server.md",
    "windows-server-installation": "sysadmin/windows-server/installation.md",
    "nouveau-article": "categorie/nouveau-article.md"
  }
}
```

## 📝 Syntaxe Markdown

### Catégories
```markdown
## 🔒 Nom de la Catégorie
```

### Articles Principaux
```markdown
### [Titre de l'Article](article-id)
```

### Sous-Articles
```markdown
### [Article Parent](parent-id)
- [Sous-Article 1](sous-article-1)
- [Sous-Article 2](sous-article-2)
```

### Badges
```markdown
### [PowerShell](powershell) `NEW`
### [Article](article-id) `UPDATED`
```

## 🎯 Exemple Complet

### Ajouter "Docker" sous Infrastructure

**1. Dans `navigation.md` :**
```markdown
## 🏗️ Infrastructure

### [Virtualisation VMware](virtualisation)

### [Docker](docker) `NEW`
- [Installation](docker-installation)
- [Conteneurs](docker-containers)
- [Compose](docker-compose)
```

**2. Dans `articles.json` :**
```json
{
  "articles": {
    "docker": "infrastructure/docker.md",
    "docker-installation": "infrastructure/docker/installation.md",
    "docker-containers": "infrastructure/docker/containers.md",
    "docker-compose": "infrastructure/docker/compose.md"
  }
}
```

**3. Créer les fichiers :**
```bash
mkdir content/infrastructure/docker
echo "# Docker" > content/infrastructure/docker.md
echo "# Installation Docker" > content/infrastructure/docker/installation.md
```

**4. Recharger la page → Terminé !**

## ✅ Avantages du Nouveau Système

| Avant (JSON) | Maintenant (Markdown) |
|-------------|----------------------|
| ❌ Syntaxe complexe | ✅ Markdown simple |
| ❌ Erreurs JSON fréquentes | ✅ Plus d'erreurs syntaxe |
| ❌ Difficile à lire | ✅ Lisible comme du texte |
| ❌ Imbrication compliquée | ✅ Structure claire |

## 🔧 Migration Automatique

L'ancien `config.json` n'est plus utilisé. Le système lit maintenant :
1. `navigation.md` → Structure de la sidebar
2. `articles.json` → Mapping ID vers fichiers

## 🎯 Bonnes Pratiques

### ✅ Recommandations

1. **IDs courts** : `docker`, `linux-admin`
2. **Hiérarchie claire** : catégorie → article → sous-article
3. **Badges utiles** : `NEW`, `UPDATED`
4. **Émojis catégories** : `⚙️`, `🔒`, `🏗️`, `📋`

### ❌ À Éviter

- IDs avec espaces : `windows server` ❌ → `windows-server` ✅
- Trop de niveaux : max 2 (article → sous-article)
- Oublier le mapping dans `articles.json`

## 🚀 Résultat

**Ajouter un article = 3 étapes :**
1. Ligne dans `navigation.md`
2. Ligne dans `articles.json`  
3. Créer le fichier `.md`

**C'est tout !** Le plus simple possible ! 🎉 