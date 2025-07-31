---
title: "Installation & Configuration - Windows Server"
description: "Guide complet d'installation et de configuration initiale de Windows Server"
category: "Administration Système"
tags: ["Windows Server", "Installation", "Configuration", "Setup"]
level: "Débutant"
reading_time: "12 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
parent: "windows-server"
---

# Installation & Configuration - Windows Server

## Prérequis Système

### Configuration Minimale

| Composant | Spécification |
|-----------|---------------|
| Processeur | 1.4 GHz 64-bit |
| RAM | 2 GB (Server Core) / 4 GB (Desktop Experience) |
| Stockage | 32 GB minimum |
| Réseau | Carte réseau compatible |

### Configuration Recommandée

```text
• Processeur : 2+ GHz multi-core
• RAM : 8 GB ou plus
• Stockage : SSD 100 GB+
• Réseau : Gigabit Ethernet
```

## Installation Étape par Étape

### 1. Préparation du Media

```powershell
# Vérifier l'intégrité de l'ISO
Get-FileHash -Path "WindowsServer2022.iso" -Algorithm SHA256

# Créer une clé USB bootable avec Rufus ou PowerShell
$USBDrive = "E:"
Format-Volume -DriveLetter E -FileSystem NTFS -NewFileSystemLabel "WS2022"
```

### 2. Options d'Installation

#### Server Core (Recommandé)
- Interface en ligne de commande uniquement
- Empreinte réduite
- Plus sécurisé
- Gestion via PowerShell/Windows Admin Center

#### Desktop Experience
- Interface graphique complète
- Plus facile pour débuter
- Consomme plus de ressources

### 3. Configuration Post-Installation

```powershell
# Configurer le nom du serveur
Rename-Computer -NewName "SRV-DC01" -Restart

# Configuration réseau
New-NetIPAddress -InterfaceAlias "Ethernet" -IPAddress 192.168.1.10 -PrefixLength 24 -DefaultGateway 192.168.1.1
Set-DnsClientServerAddress -InterfaceAlias "Ethernet" -ServerAddresses 192.168.1.1, 8.8.8.8

# Activer le Bureau à distance
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -Name "fDenyTSConnections" -Value 0
Enable-NetFirewallRule -DisplayGroup "Remote Desktop"

# Configurer Windows Update
Install-Module PSWindowsUpdate -Force
Get-WindowsUpdate
Install-WindowsUpdate -AcceptAll -AutoReboot
```

## Sécurisation Initiale

### Configuration du Pare-feu

```powershell
# Activer le pare-feu sur tous les profils
Set-NetFirewallProfile -Profile Domain,Public,Private -Enabled True

# Règles essentielles
New-NetFirewallRule -DisplayName "Allow RDP" -Direction Inbound -Protocol TCP -LocalPort 3389 -Action Allow
New-NetFirewallRule -DisplayName "Allow WinRM" -Direction Inbound -Protocol TCP -LocalPort 5985,5986 -Action Allow
```

### Stratégies de Sécurité

```powershell
# Configurer la stratégie de mots de passe
secedit /export /cfg c:\temp\secpol.cfg
# Modifier le fichier puis l'importer
secedit /configure /db c:\temp\secedit.sdb /cfg c:\temp\secpol.cfg

# Désactiver les comptes non utilisés
Get-LocalUser | Where-Object {$_.Enabled -eq $true -and $_.Name -ne "Administrator"}
```

## Outils d'Administration

### Installation de Windows Admin Center

```powershell
# Télécharger et installer WAC
$url = "https://aka.ms/WACDownload"
$output = "C:\temp\WindowsAdminCenter.msi"
Invoke-WebRequest -Uri $url -OutFile $output

# Installation silencieuse
Start-Process msiexec.exe -Wait -ArgumentList "/i C:\temp\WindowsAdminCenter.msi /qn /L*v C:\temp\wac_install.log SME_PORT=443 SSL_CERTIFICATE_OPTION=generate"
```

### Configuration de PowerShell DSC

```powershell
# Installer le module DSC
Install-Module -Name PowerShellGet -Force
Install-Module -Name PSDscResources -Force

# Exemple de configuration DSC
Configuration BasicServerConfig {
    Import-DscResource -ModuleName PSDscResources
    
    Node "localhost" {
        WindowsFeature IIS {
            Ensure = "Present"
            Name = "IIS-WebServerRole"
        }
    }
}
```

## Bonnes Pratiques

> **Important :** Toujours effectuer une sauvegarde avant les modifications majeures.

### Checklist Post-Installation

- [ ] Configuration réseau validée
- [ ] Nom du serveur configuré
- [ ] Mises à jour installées
- [ ] Pare-feu configuré
- [ ] Comptes administrateur sécurisés
- [ ] Sauvegarde configurée
- [ ] Monitoring activé

## Ressources Complémentaires

- [Guide officiel Microsoft](https://docs.microsoft.com/windows-server/)
- [Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/)
- [PowerShell DSC](https://docs.microsoft.com/powershell/scripting/dsc/) 