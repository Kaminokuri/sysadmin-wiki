---
title: "Virtualisation VMware"
description: "Guide complet sur la virtualisation avec VMware vSphere"
category: "Infrastructure"
tags: ["VMware", "vSphere", "ESXi", "vCenter"]
level: "Intermédiaire"
reading_time: "30 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# ☁️ Virtualisation VMware

## Vue d'ensemble

VMware vSphere est la plateforme de virtualisation leader du marché, permettant de créer et gérer des infrastructures virtualisées robustes et évolutives.

## 🏗️ Architecture vSphere

### Composants Principaux
- **ESXi** : Hyperviseur bare-metal
- **vCenter Server** : Plateforme de gestion centralisée
- **vSphere Client** : Interface web de gestion
- **VMFS** : Système de fichiers cluster

### Schéma Architecture
```
vCenter Server
     │
  ┌────┼────┐
  │         │
ESXi-1    ESXi-2
  │         │
 Shared   Storage
```

## 💿 Installation ESXi

### Prérequis Matériel
- **CPU** : 64-bit x86 avec support virtualisation
- **RAM** : 8 GB minimum (recommandé 16+ GB)
- **Stockage** : 32 GB minimum
- **Réseau** : 1 Gbps minimum

### Étapes Installation
1. **Boot depuis ISO ESXi**
2. **Configuration réseau**
3. **Création mot de passe root**
4. **Installation sur disque**
5. **Redémarrage**

### Configuration Post-Installation
```bash
# Activation SSH
vim-cmd hostsvc/enable_ssh
vim-cmd hostsvc/start_ssh

# Configuration NTP
esxcli system ntp set --server="pool.ntp.org"
esxcli system ntp set --enabled=true

# Configuration firewall
esxcli network firewall ruleset set --ruleset-id=sshServer --enabled=true
```

## 🏢 vCenter Server

### Méthodes de Déploiement
1. **vCenter Server Appliance (VCSA)** - Recommandé
2. **vCenter Server pour Windows** - Déprécié

### Déploiement VCSA
```bash
# Montage ISO VCSA
# Lancement du déployeur
./vcsa-deploy install --accept-eula --no-ssl-certificate-verification vcsa_config.json
```

### Configuration vCenter
- **SSO Domain** : vsphere.local
- **Datacenter** : Création structure logique
- **Cluster** : Groupement hôtes ESXi
- **Réseau** : Configuration port groups

## 📁 Gestion du Stockage

### Types de Datastores
- **VMFS** : VMware File System
- **NFS** : Network File System
- **vSAN** : Software-Defined Storage
- **vVols** : Virtual Volumes

### Configuration iSCSI
```bash
# Activation logiciel iSCSI
esxcli iscsi software set --enabled=true

# Ajout target iSCSI
vmkiscsi-tool -D -a 192.168.1.100:3260 vmhba33

# Découverte targets
esxcli iscsi adapter discovery sendtarget add -A vmhba33 -a 192.168.1.100
```

## 🌐 Réseau vSphere

### Composants Réseau
- **vSwitch Standard** : Switch virtuel basique
- **vSphere Distributed Switch** : Switch entreprise
- **Port Groups** : Segmentation réseau
- **VMkernel** : Trâfic gestion ESXi

### Configuration vSwitch
```bash
# Création vSwitch
esxcli network vswitch standard add --vswitch-name=vSwitch1

# Ajout uplink
esxcli network vswitch standard uplink add --uplink-name=vmnic1 --vswitch-name=vSwitch1

# Création port group
esxcli network vswitch standard portgroup add --portgroup-name="VM Network" --vswitch-name=vSwitch1
```

## 🔄 Haute Disponibilité

### vSphere HA
- **Restart automatique** des VMs
- **Admission Control** : Réservation ressources
- **VM Monitoring** : Redémarrage en cas de freeze

### Configuration HA
1. **Activer HA sur cluster**
2. **Définir Admission Control Policy**
3. **Configurer VM restart priority**
4. **Paramétrer isolation response**

### vSphere DRS
- **Load balancing** automatique
- **Resource pools** : Allocation ressources
- **Affinity rules** : Placement VMs

## 📊 Monitoring et Performance

### Métriques Clés
- **CPU Ready** : < 5%
- **Memory Ballooning** : Minimal
- **Storage Latency** : < 20ms
- **Network Dropped Packets** : 0%

### Outils Monitoring
```bash
# esxtop - Monitoring temps réel
esxtop

# VM stats
vmware-toolbox-cmd stat session

# Storage performance
esxcli storage core device stats get
```

### vRealize Operations
- **Predictive Analytics**
- **Capacity Planning**
- **Troubleshooting**
- **Compliance**

## 💾 Backup et Recovery

### Stratégies Backup
1. **VM-level backup** : Veeam, Commvault
2. **Array-based snapshots** : SAN/NAS
3. **Application-consistent** : VSS integration

### vSphere Snapshots
```bash
# Création snapshot
vim-cmd vmsvc/snapshot.create [vmid] "snapshot_name" "description" 0 0

# Liste snapshots
vim-cmd vmsvc/snapshot.get [vmid]

# Suppression snapshot
vim-cmd vmsvc/snapshot.remove [vmid] [snapshotId]
```

## 🔒 Sécurité

### Bonnes Pratiques
- **vCenter SSO** : Intégration Active Directory
- **Rôles et permissions** : Principe moindre privilège
- **Certificats SSL** : Remplacement certificats par défaut
- **Lockdown Mode** : Restriction accès ESXi

### Audit et Compliance
```bash
# Activation logging
vim-cmd hostsvc/advopt/update Syslog.global.logLevel string "info"

# Configuration syslog
esxcli system syslog config set --loghost="192.168.1.100:514"
```

## ☁️ Migration vers Cloud

### VMware Cloud on AWS
- **Extension datacenter** vers AWS
- **Migration workloads** sans modification
- **Disaster Recovery** as a Service

### vMotion Cross-Cloud
- **Storage vMotion** vers cloud
- **vSphere Replication** pour DR
- **HCX** pour migrations à grande échelle

## 📈 Troubleshooting

### Problèmes Courants
1. **VM ne démarre pas** : Vérifier ressources, locks
2. **Performance dégradée** : Analyser CPU ready, memory
3. **Connectivité réseau** : Vérifier vSwitch, VLANs
4. **Stockage inaccessible** : Vérifier paths, LUNs

### Outils Diagnostic
- **vSphere Client** : Tâches et événements
- **Log files** : /var/log/vmware/
- **vm-support** : Collecte logs support
- **RVTools** : Inventaire et audit

---

💡 **Conseil** : Planifiez toujours vos mises à jour vSphere et testez en laboratoire avant production.