---
title: "PowerShell"
description: "Guide complet PowerShell - scripting, administration et automatisation"
category: "Administration Système"
tags: ["PowerShell", "Scripting", "Automatisation", "Windows"]
level: "Intermédiaire"
reading_time: "15 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
---

# PowerShell

## Introduction

PowerShell est un shell de commande et un langage de script développé par Microsoft, essentiel pour l'automatisation et l'administration Windows.

## Concepts de Base

### Cmdlets et Pipeline

```powershell
# Structure Verb-Noun
Get-Process
Set-Location
New-Item

# Pipeline
Get-Process | Where-Object {$_.CPU -gt 100} | Sort-Object CPU -Descending
```

### Variables et Types

```powershell
# Déclaration
$name = "John"
$age = 30
$services = Get-Service

# Types
[string]$text = "Hello"
[int]$number = 42
[datetime]$date = Get-Date
```

## Gestion des Fichiers

```powershell
# Navigation
Get-Location
Set-Location C:\Users
Get-ChildItem -Recurse -File *.txt

# Manipulation
Copy-Item source.txt destination.txt
Move-Item old.txt new.txt
Remove-Item *.tmp -Force
```

## Administration Système

### Services

```powershell
# Gestion des services
Get-Service -Name "Spooler"
Start-Service -Name "Spooler"
Stop-Service -Name "Spooler"
Restart-Service -Name "Spooler"

# Services multiples
Get-Service | Where-Object {$_.Status -eq "Stopped"} | Start-Service
```

### Registre

```powershell
# Navigation
Get-ChildItem HKLM:\Software
Get-ItemProperty HKLM:\Software\Microsoft\Windows\CurrentVersion

# Modification
Set-ItemProperty -Path "HKLM:\Software\MyApp" -Name "Version" -Value "2.0"
```

## Scripts et Fonctions

### Fonctions

```powershell
function Get-DiskSpace {
    param(
        [string]$ComputerName = $env:COMPUTERNAME
    )
    
    Get-WmiObject -Class Win32_LogicalDisk -ComputerName $ComputerName |
    Select-Object DeviceID, @{n="Size(GB)";e={[math]::Round($_.Size/1GB,2)}}, 
                           @{n="Free(GB)";e={[math]::Round($_.FreeSpace/1GB,2)}}
}
```

### Gestion d'Erreurs

```powershell
try {
    Get-Content "nonexistent.txt" -ErrorAction Stop
}
catch {
    Write-Error "Fichier introuvable: $($_.Exception.Message)"
}
finally {
    Write-Host "Nettoyage effectué"
}
```

## Modules Utiles

| Module | Description |
|--------|-------------|
| ActiveDirectory | Gestion AD |
| AzureAD | Administration Azure |
| Exchange | Gestion Exchange |
| Hyper-V | Virtualisation |
| Storage | Gestion stockage |

> **Note:** Article en cours de développement avec plus d'exemples à venir. 