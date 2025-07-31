---
title: "Active Directory"
description: "Administration et gestion d'Active Directory - concepts, configuration et bonnes pratiques"
category: "Administration Système"
tags: ["Active Directory", "Windows", "LDAP", "Authentification"]
level: "Avancé"
reading_time: "10 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
---

# Active Directory

## Introduction

Active Directory (AD) est le service de répertoire de Microsoft, essentiel pour la gestion centralisée des identités et des accès en entreprise.

## Concepts Fondamentaux

### Structure Hiérarchique

- **Forêt** : Niveau le plus élevé
- **Domaine** : Unité administrative
- **Unités d'Organisation (OU)** : Conteneurs logiques
- **Objets** : Utilisateurs, groupes, ordinateurs

### Rôles FSMO

| Rôle | Scope | Description |
|------|-------|-------------|
| Schema Master | Forêt | Modifications du schéma |
| Domain Naming Master | Forêt | Ajout/suppression de domaines |
| PDC Emulator | Domaine | Émulateur contrôleur principal |
| RID Master | Domaine | Attribution des RID |
| Infrastructure Master | Domaine | Références inter-domaines |

## Administration PowerShell

```powershell
# Module Active Directory
Import-Module ActiveDirectory

# Gestion des utilisateurs
New-ADUser -Name "John Doe" -SamAccountName "jdoe"
Get-ADUser -Filter "Department -eq 'IT'"
Set-ADUser -Identity "jdoe" -Department "HR"

# Gestion des groupes
New-ADGroup -Name "Sales Team" -GroupScope Global
Add-ADGroupMember -Identity "Sales Team" -Members "jdoe"
```

## Réplication et Sites

```powershell
# Vérification de la réplication
repadmin /replsum
repadmin /showrepl

# Sites et liens
Get-ADReplicationSite
Get-ADReplicationSiteLink
```

> **Note:** Article en cours de rédaction. Plus de contenu sera ajouté prochainement. 