---
title: "Virtualisation VMware"
description: "Administration et gestion des environnements VMware vSphere"
category: "Infrastructure"
tags: ["VMware", "Virtualisation", "vSphere", "ESXi"]
level: "Intermédiaire"
reading_time: "15 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
---

# Virtualisation VMware

## Introduction

VMware vSphere est la plateforme de virtualisation leader pour les datacenters d'entreprise.

## Composants Principaux

- **ESXi** : Hyperviseur
- **vCenter Server** : Gestion centralisée
- **vMotion** : Migration à chaud
- **DRS** : Distribution des ressources
- **HA** : Haute disponibilité

## Installation ESXi

```bash
# Configuration réseau basique
esxcli network ip interface ipv4 set -i vmk0 -I 192.168.1.10 -N 255.255.255.0 -g 192.168.1.1 -t static
```

> **Note:** Contenu en développement. 