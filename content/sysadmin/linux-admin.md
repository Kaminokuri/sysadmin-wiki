---
title: "Linux Administration"
description: "Guide d'administration système Linux - commandes essentielles et bonnes pratiques"
category: "Administration Système"
tags: ["Linux", "Administration", "Bash", "Sysadmin"]
level: "Intermédiaire"
reading_time: "8 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
---

# Linux Administration

## Introduction

L'administration Linux est une compétence fondamentale pour tout administrateur système. Ce guide couvre les commandes essentielles et les bonnes pratiques.

## Commandes de Base

### Gestion des Fichiers

```bash
# Navigation
ls -la          # Lister avec détails
cd /path/to/dir # Changer de répertoire
pwd             # Afficher le répertoire courant

# Manipulation
cp source dest  # Copier
mv source dest  # Déplacer/renommer
rm -rf directory # Supprimer récursivement
```

### Gestion des Processus

```bash
# Surveillance
ps aux          # Liste des processus
top             # Moniteur temps réel
htop            # Version améliorée

# Contrôle
kill PID        # Arrêter un processus
killall name    # Arrêter par nom
nohup command & # Lancer en arrière-plan
```

## Gestion des Utilisateurs

| Commande | Description |
|----------|-------------|
| `useradd` | Ajouter un utilisateur |
| `usermod` | Modifier un utilisateur |
| `userdel` | Supprimer un utilisateur |
| `passwd` | Changer le mot de passe |

## Services et Systemd

```bash
# Gestion des services
systemctl status service
systemctl start service
systemctl stop service
systemctl enable service
systemctl disable service

# Logs
journalctl -u service
journalctl -f
```

> **Note:** Article en cours de rédaction. Plus de contenu sera ajouté prochainement. 