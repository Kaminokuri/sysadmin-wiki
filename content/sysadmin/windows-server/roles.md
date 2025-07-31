---
title: "Rôles & Fonctionnalités - Windows Server"
description: "Guide des rôles et fonctionnalités Windows Server - installation et configuration"
category: "Administration Système"
tags: ["Windows Server", "Rôles", "Fonctionnalités", "Services"]
level: "Intermédiaire"
reading_time: "15 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
parent: "windows-server"
---

# Rôles & Fonctionnalités - Windows Server

## Vue d'Ensemble des Rôles

### Rôles Principaux

| Rôle | Description | Usage Typique |
|------|-------------|---------------|
| **Active Directory DS** | Services de domaine | Authentification centralisée |
| **DNS Server** | Résolution de noms | Infrastructure réseau |
| **DHCP Server** | Attribution IP automatique | Gestion des adresses |
| **File Services** | Partage de fichiers | Stockage centralisé |
| **Web Server (IIS)** | Serveur web | Applications web |
| **Hyper-V** | Virtualisation | Consolidation serveurs |

## Installation des Rôles

### Via PowerShell (Recommandé)

```powershell
# Lister tous les rôles disponibles
Get-WindowsFeature | Where-Object {$_.FeatureType -eq "Role"}

# Installer Active Directory Domain Services
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools

# Installer DNS Server
Install-WindowsFeature -Name DNS -IncludeManagementTools

# Installer DHCP Server
Install-WindowsFeature -Name DHCP -IncludeManagementTools

# Installer File Services
Install-WindowsFeature -Name FileAndStorage-Services -IncludeManagementTools

# Installation multiple
Install-WindowsFeature -Name AD-Domain-Services,DNS,DHCP -IncludeManagementTools -Restart
```

### Via Server Manager (GUI)

1. Ouvrir **Server Manager**
2. Cliquer **Manage** → **Add Roles and Features**
3. Suivre l'assistant d'installation
4. Sélectionner les rôles souhaités
5. Confirmer et redémarrer si nécessaire

## Configuration des Rôles Majeurs

### Active Directory Domain Services

#### Promotion en Contrôleur de Domaine

```powershell
# Installer le rôle AD DS
Install-WindowsFeature -Name AD-Domain-Services -IncludeManagementTools

# Promouvoir en contrôleur de domaine (nouvelle forêt)
Import-Module ADDSDeployment
Install-ADDSForest `
    -DomainName "contoso.local" `
    -DomainNetbiosName "CONTOSO" `
    -ForestMode "WinThreshold" `
    -DomainMode "WinThreshold" `
    -InstallDns:$true `
    -SafeModeAdministratorPassword (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force) `
    -Force:$true
```

#### Configuration Post-Installation

```powershell
# Créer une OU
New-ADOrganizationalUnit -Name "Users" -Path "DC=contoso,DC=local"
New-ADOrganizationalUnit -Name "Computers" -Path "DC=contoso,DC=local"

# Créer un utilisateur
New-ADUser -Name "John Doe" -SamAccountName "jdoe" -UserPrincipalName "jdoe@contoso.local" -Path "OU=Users,DC=contoso,DC=local" -Enabled $true -AccountPassword (ConvertTo-SecureString "UserP@ssw0rd!" -AsPlainText -Force)

# Créer un groupe
New-ADGroup -Name "IT Support" -GroupScope Global -GroupCategory Security -Path "OU=Users,DC=contoso,DC=local"
```

### DNS Server

```powershell
# Créer une zone DNS primaire
Add-DnsServerPrimaryZone -Name "contoso.local" -ZoneFile "contoso.local.dns"

# Ajouter des enregistrements
Add-DnsServerResourceRecordA -ZoneName "contoso.local" -Name "web" -IPv4Address "192.168.1.100"
Add-DnsServerResourceRecordCName -ZoneName "contoso.local" -Name "www" -HostNameAlias "web.contoso.local"

# Configurer les redirecteurs
Set-DnsServerForwarder -IPAddress 8.8.8.8, 8.8.4.4
```

### DHCP Server

```powershell
# Configurer l'étendue DHCP
Add-DhcpServerv4Scope -Name "LAN Scope" -StartRange 192.168.1.100 -EndRange 192.168.1.200 -SubnetMask 255.255.255.0

# Configurer les options DHCP
Set-DhcpServerv4OptionValue -OptionId 3 -Value 192.168.1.1 -ScopeId 192.168.1.0  # Gateway
Set-DhcpServerv4OptionValue -OptionId 6 -Value 192.168.1.10 -ScopeId 192.168.1.0  # DNS

# Autoriser le serveur DHCP dans AD
Add-DhcpServerInDC -DnsName "srv-dhcp.contoso.local" -IPAddress 192.168.1.10
```

## Gestion des Fonctionnalités

### Fonctionnalités Utiles

```powershell
# Windows PowerShell ISE
Install-WindowsFeature -Name PowerShell-ISE

# Outils d'administration à distance
Install-WindowsFeature -Name RSAT-Feature-Tools

# Failover Clustering
Install-WindowsFeature -Name Failover-Clustering -IncludeManagementTools

# Network Load Balancing
Install-WindowsFeature -Name NLB
```

### Surveillance des Rôles

```powershell
# Vérifier l'état des services
Get-Service | Where-Object {$_.Status -eq "Running" -and $_.Name -like "*DNS*"}
Get-Service | Where-Object {$_.Status -eq "Running" -and $_.Name -like "*DHCP*"}

# Vérifier les journaux d'événements
Get-EventLog -LogName System -Source "Service Control Manager" -Newest 10
Get-EventLog -LogName "Directory Service" -Newest 10

# Surveillance des performances
Get-Counter "\DNS\Total Query Received/sec"
Get-Counter "\DHCP Server\Packets Received/sec"
```

## Bonnes Pratiques

### Sécurité des Rôles

> **Attention :** Ne jamais installer tous les rôles sur un seul serveur en production.

#### Principe de Moindre Privilège

```powershell
# Créer des comptes de service dédiés
New-ADUser -Name "SVC_DHCP" -SamAccountName "svc_dhcp" -Enabled $true -PasswordNeverExpires $true

# Assigner des droits spécifiques
Add-ADGroupMember -Identity "DHCP Users" -Members "svc_dhcp"
```

#### Ségrégation des Rôles

- **Contrôleur de Domaine** : AD DS + DNS uniquement
- **Serveur Fichiers** : File Services + DFS
- **Serveur Web** : IIS + App Services
- **Serveur DHCP** : DHCP + IPAM

### Monitoring et Maintenance

```powershell
# Script de vérification quotidienne
$Roles = Get-WindowsFeature | Where-Object {$_.InstallState -eq "Installed" -and $_.FeatureType -eq "Role"}
foreach ($Role in $Roles) {
    Write-Host "Rôle actif: $($Role.DisplayName)" -ForegroundColor Green
}

# Vérifier l'espace disque
Get-PSDrive -PSProvider FileSystem | Select-Object Name, @{n="Used(GB)";e={[math]::Round($_.Used/1GB,2)}}, @{n="Free(GB)";e={[math]::Round($_.Free/1GB,2)}}
```

## Dépannage Courant

### Problèmes d'Installation

```powershell
# Vérifier les prérequis
Get-WindowsFeature -Name NET-Framework-45-Features
Get-WindowsFeature -Name WAS-Process-Model

# Forcer la réinstallation
Uninstall-WindowsFeature -Name DHCP
Install-WindowsFeature -Name DHCP -IncludeManagementTools -Restart
```

### Logs de Diagnostic

```powershell
# Activer les logs détaillés
wevtutil sl "Microsoft-Windows-DNS-Server/Debug" /e:true
wevtutil sl "Microsoft-Windows-Dhcp-Server/Debug" /e:true

# Consulter les événements critiques
Get-WinEvent -FilterHashtable @{LogName="System"; Level=1,2,3} -MaxEvents 50
```

## Ressources Complémentaires

- [Planification des rôles serveur](https://docs.microsoft.com/windows-server/get-started/server-role-upgradeability-table)
- [Meilleures pratiques AD DS](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/)
- [Guide DHCP Server](https://docs.microsoft.com/windows-server/networking/technologies/dhcp/) 