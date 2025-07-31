# 🚀 Guide du Système Hybride - Le Meilleur des Deux Mondes

## 🎯 Concept : Sidebar Statique + Contenu Markdown

Notre système hybride combine :
- **Sidebar statique** intégrée dans `index.html` (compatible GitHub Pages)
- **Contenu dynamique** en fichiers Markdown (facilité d'édition)

## 📁 Structure du Projet

```
sysadmin-wiki/
├── index.html                 # Sidebar statique + JavaScript
├── content/
│   ├── sysadmin/
│   │   ├── windows-server.md
│   │   ├── linux-admin.md
│   │   ├── active-directory.md
│   │   ├── powershell.md
│   │   └── windows-server/
│   │       ├── installation.md
│   │       └── roles.md
│   ├── cybersecurite/
│   │   ├── securite-reseau.md
│   │   ├── cryptographie.md
│   │   ├── pentest.md
│   │   └── siem.md
│   ├── infrastructure/
│   │   ├── virtualisation.md
│   │   ├── reseau.md
│   │   ├── stockage.md
│   │   └── cloud.md
│   └── gestion-projet/
│       ├── methodologies.md
│       ├── outils.md
│       └── itil.md
```

## 📝 Ajouter/Modifier du Contenu

### ✅ Avantages du Système Hybride

- **✏️ Édition facile** : Contenu en Markdown
- **🌐 Compatible GitHub Pages** : Sidebar statique
- **⚡ Performance** : Sidebar instantanée
- **🔄 Navigation dynamique** : Contenu rechargé à la demande

## 📖 Créer un Nouvel Article

### 1. Créer le Fichier Markdown

Créez votre fichier dans le bon dossier, par exemple `content/sysadmin/docker.md` :

```markdown
---
title: "Docker - Conteneurisation"
description: "Guide complet pour Docker et la conteneurisation"
category: "Administration Système"
tags: ["Docker", "Containers", "DevOps"]
level: "Intermédiaire"
reading_time: "20 min"
last_updated: "1 février 2025"
author: "Mathéo Fauvel"
---

# Docker - Conteneurisation

> **Note:** Guide complet pour maîtriser Docker et la conteneurisation.

## Introduction

Docker révolutionne le déploiement d'applications en utilisant la conteneurisation...

## Installation

### Sur Ubuntu
\`\`\`bash
sudo apt update
sudo apt install docker.io
sudo systemctl start docker
sudo systemctl enable docker
\`\`\`

### Sur Windows
\`\`\`powershell
# Via Chocolatey
choco install docker-desktop
\`\`\`

> **Attention:** Redémarrage requis après installation sur Windows.

## Commandes Essentielles

| Commande | Description |
|----------|-------------|
| `docker run` | Exécuter un conteneur |
| `docker build` | Construire une image |
| `docker ps` | Lister les conteneurs |

## Dockerfile Exemple

\`\`\`dockerfile
FROM node:16-alpine
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
\`\`\`

## Ressources

- [Documentation officielle Docker](https://docs.docker.com)
- [Docker Hub](https://hub.docker.com)
```

### 2. Ajouter à la Sidebar

Dans `index.html`, ajoutez votre article dans la bonne section :

```html
<!-- Dans la section Administration Système -->
<div class="nav-item">
    <a href="#" onclick="loadMarkdownArticle('docker')" class="nav-link">
        <span>Docker</span>
        <span class="badge">NEW</span>
    </a>
</div>
```

### 3. Déclarer le Mapping

Dans `index.html`, ajoutez votre article au mapping JavaScript :

```javascript
const articlesMapping = {
    // ... articles existants ...
    "docker": "content/sysadmin/docker.md",
    // ... autres articles ...
};
```

## 📋 Ajouter des Sous-Menus

### 1. Structure Markdown

Créez vos sous-articles :
- `content/sysadmin/docker/basics.md`
- `content/sysadmin/docker/compose.md`
- `content/sysadmin/docker/swarm.md`

### 2. Sidebar avec Sous-Menu

```html
<div class="nav-item has-submenu">
    <a href="#" onclick="loadMarkdownArticle('docker')" class="nav-link">
        <span>Docker</span>
        <span class="nav-toggle">▼</span>
    </a>
    <div class="submenu">
        <a href="#" onclick="loadMarkdownArticle('docker-basics')" class="submenu-item">
            <span>Concepts de Base</span>
        </a>
        <a href="#" onclick="loadMarkdownArticle('docker-compose')" class="submenu-item">
            <span>Docker Compose</span>
        </a>
        <a href="#" onclick="loadMarkdownArticle('docker-swarm')" class="submenu-item">
            <span>Docker Swarm</span>
            <span class="badge">BETA</span>
        </a>
    </div>
</div>
```

### 3. Mapping des Sous-Articles

```javascript
const articlesMapping = {
    // ... autres articles ...
    "docker": "content/sysadmin/docker.md",
    "docker-basics": "content/sysadmin/docker/basics.md",
    "docker-compose": "content/sysadmin/docker/compose.md",
    "docker-swarm": "content/sysadmin/docker/swarm.md",
    // ... autres articles ...
};
```

## 🎨 Ajouter une Nouvelle Section

### 1. Ajouter dans la Sidebar

```html
<!-- Nouvelle section après les sections existantes -->
<div class="nav-section">
    <h3 class="nav-header">🔬 Laboratoire</h3>
    <div class="nav-item">
        <a href="#" onclick="loadMarkdownArticle('homelab')" class="nav-link">
            <span>HomeLab Setup</span>
        </a>
    </div>
    <div class="nav-item">
        <a href="#" onclick="loadMarkdownArticle('testing')" class="nav-link">
            <span>Environnement de Test</span>
            <span class="badge">NEW</span>
        </a>
    </div>
</div>
```

### 2. Créer les Articles

- `content/laboratoire/homelab.md`
- `content/laboratoire/testing.md`

### 3. Ajouter au Mapping

```javascript
const articlesMapping = {
    // ... autres articles ...
    "homelab": "content/laboratoire/homelab.md",
    "testing": "content/laboratoire/testing.md",
    // ... autres articles ...
};
```

## 🎯 Fonctionnalités Markdown Supportées

### Métadonnées (Front Matter)
```yaml
---
title: "Titre de l'Article"
description: "Description SEO"
category: "Catégorie"
tags: ["tag1", "tag2"]
level: "Débutant|Intermédiaire|Avancé"
reading_time: "15 min"
last_updated: "Date"
author: "Auteur"
---
```

### Blockquotes avec Types
```markdown
> **Note:** Information importante

> **Attention:** Point critique à retenir

> **Conseil:** Bonne pratique recommandée
```

### Code avec Coloration
```markdown
\`\`\`powershell
Get-Service | Where-Object {$_.Status -eq "Running"}
\`\`\`

\`\`\`bash
sudo systemctl status nginx
\`\`\`

\`\`\`dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
\`\`\`
```

### Tableaux
```markdown
| Colonne 1 | Colonne 2 | Colonne 3 |
|-----------|-----------|-----------|
| Donnée 1  | Donnée 2  | Donnée 3  |
```

## 🔧 Workflow de Développement

### 1. Développement Local
```bash
# 1. Créer/modifier fichier Markdown
# 2. Ajouter à la sidebar (si nouveau)
# 3. Ajouter au mapping (si nouveau)
# 4. Tester sur http://localhost:8000
```

### 2. Test et Validation
- ✅ Article se charge correctement
- ✅ Navigation fonctionne
- ✅ Coloration syntaxique active
- ✅ Métadonnées affichées
- ✅ Version mobile OK

### 3. Déploiement
```bash
git add .
git commit -m "Ajout article Docker"
git push origin main
```

## 🌐 Compatibilité GitHub Pages

### ✅ Ce qui Fonctionne
- **Sidebar statique** (intégrée dans HTML)
- **Navigation** (JavaScript simple)
- **Chargement Markdown** (fetch API)
- **Coloration syntaxique** (Prism.js CDN)

### ⚠️ Limitations GitHub Pages
- **Pas de backend** (seulement du statique)
- **CORS** : fichiers doivent être sur le même domaine
- **HTTPS requis** pour fetch dans certains cas

## 📈 Avantages vs Système Purement Statique

### 🚀 Avantages
- **Édition facile** : Markdown au lieu de HTML
- **Séparation des préoccupations** : Structure vs Contenu
- **Réutilisabilité** : Articles réutilisables
- **Maintenance** : Un seul endroit pour chaque article
- **Collaboration** : Plusieurs personnes peuvent éditer

### 🎯 Performance
- **Première visite** : Sidebar instantanée
- **Navigation** : Seul le contenu change
- **Cache navigateur** : Articles mis en cache
- **SEO** : URLs propres avec query params

## 🔍 Exemple Complet : Ajouter Kubernetes

### 1. Créer l'Article Principal
`content/infrastructure/kubernetes.md` :

```markdown
---
title: "Kubernetes - Orchestration de Conteneurs"
description: "Guide complet pour Kubernetes et l'orchestration"
category: "Infrastructure"
tags: ["Kubernetes", "Containers", "Orchestration"]
level: "Avancé"
reading_time: "30 min"
last_updated: "1 février 2025"
author: "Mathéo Fauvel"
---

# Kubernetes - Orchestration de Conteneurs

Guide complet pour maîtriser Kubernetes...
```

### 2. Créer les Sous-Articles
- `content/infrastructure/kubernetes/pods.md`
- `content/infrastructure/kubernetes/services.md`
- `content/infrastructure/kubernetes/deployments.md`

### 3. Ajouter à la Sidebar
```html
<!-- Dans la section Infrastructure -->
<div class="nav-item has-submenu">
    <a href="#" onclick="loadMarkdownArticle('kubernetes')" class="nav-link">
        <span>Kubernetes</span>
        <span class="nav-toggle">▼</span>
    </a>
    <div class="submenu">
        <a href="#" onclick="loadMarkdownArticle('k8s-pods')" class="submenu-item">
            <span>Pods & Conteneurs</span>
        </a>
        <a href="#" onclick="loadMarkdownArticle('k8s-services')" class="submenu-item">
            <span>Services</span>
        </a>
        <a href="#" onclick="loadMarkdownArticle('k8s-deployments')" class="submenu-item">
            <span>Déploiements</span>
        </a>
    </div>
</div>
```

### 4. Ajouter au Mapping
```javascript
const articlesMapping = {
    // ... autres articles ...
    "kubernetes": "content/infrastructure/kubernetes.md",
    "k8s-pods": "content/infrastructure/kubernetes/pods.md",
    "k8s-services": "content/infrastructure/kubernetes/services.md",
    "k8s-deployments": "content/infrastructure/kubernetes/deployments.md",
    // ... autres articles ...
};
```

## 🎉 Résultat Final

Vous obtenez :
- **Sidebar statique** qui fonctionne sur GitHub Pages
- **Contenu en Markdown** facile à éditer
- **Navigation fluide** entre les articles
- **Performance optimale** 
- **Expérience utilisateur** moderne

**C'est le meilleur des deux mondes ! 🚀**