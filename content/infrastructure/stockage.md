---
title: "Solutions de Stockage"
description: "Systèmes de stockage d'entreprise : SAN, NAS, et stockage défini par logiciel"
category: "Infrastructure"
tags: ["Storage", "SAN", "NAS", "iSCSI", "Fibre Channel"]
level: "Avancé"
reading_time: "28 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# 💾 Solutions de Stockage

## Vue d'ensemble

Les solutions de stockage d'entreprise constituent l'épine dorsale de l'infrastructure IT, garantissant la disponibilité, les performances et la protection des données critiques.

## 🗄️ Types de Stockage

### Direct Attached Storage (DAS)
- **Connexion directe** au serveur
- **Haute performance** locale
- **Faible coût** d'entrée
- **Évolutivité limitée**

### Network Attached Storage (NAS)
- **Partage de fichiers** en réseau
- **Protocoles** : NFS, CIFS/SMB
- **Facilité de gestion**
- **Backup centralisé**

### Storage Area Network (SAN)
- **Réseau dédié** au stockage
- **Haute disponibilité**
- **Performance élevée**
- **Évolutivité maximale**

## 🔌 Protocoles de Stockage

### Fibre Channel
```bash
# Configuration zoning Cisco MDS
zone name SERVER1_STORAGE1 vsan 1
  member pwwn 10:00:00:00:c9:84:3b:2c
  member pwwn 50:05:07:68:01:23:45:67

zoneset name PRODUCTION vsan 1
  member SERVER1_STORAGE1
  
zoneset activate name PRODUCTION vsan 1
```

### iSCSI Configuration
```bash
# Linux initiator setup
echo "InitiatorName=iqn.2020-01.com.company:server01" > /etc/iscsi/initiatorname.iscsi

# Discovery targets
iscsiadm -m discovery -t sendtargets -p 192.168.1.100

# Login to target
iscsiadm -m node --targetname iqn.2020-01.com.storage:lun1 --login
```

### NVMe over Fabrics
```bash
# NVMe-oF target configuration
modprobe nvmet
modprobe nvmet-rdma

# Create subsystem
mkdir /sys/kernel/config/nvmet/subsystems/nvme-subsys1
cd /sys/kernel/config/nvmet/subsystems/nvme-subsys1
echo 1 > attr_allow_any_host
```

## 🏢 Solutions Entreprise

### Dell EMC PowerMax
- **NVMe end-to-end**
- **Machine Learning** optimization
- **Inline compression**
- **Multi-cloud ready**

### NetApp ONTAP
```bash
# ONTAP CLI examples
cluster setup
vserver create -vserver svm1 -rootvolume root -aggregate aggr1
volume create -vserver svm1 -volume vol1 -aggregate aggr1 -size 100GB
```

### HPE 3PAR/Primera
- **Thin provisioning**
- **Autonomous management**
- **Always-on encryption**
- **Peer persistence**

## ☁️ Software-Defined Storage

### VMware vSAN
```bash
# vSAN cluster setup
esxcli vsan cluster join -u [cluster_uuid]
esxcli vsan storage add -s mpx.vmhba1:C0:T0:L0 -d mpx.vmhba1:C0:T1:L0

# vSAN health check
esxcli vsan health cluster get
```

### Red Hat Ceph
```yaml
# Ceph cluster configuration
[global]
fsid = 12345678-1234-1234-1234-123456789012
mon initial members = mon1, mon2, mon3
mon host = 192.168.1.10, 192.168.1.11, 192.168.1.12
auth cluster required = cephx
auth service required = cephx
```

### Microsoft Storage Spaces Direct
```powershell
# S2D setup
Enable-ClusterStorageSpacesDirect
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -Size 1TB
```

## 🔄 Réplication et Backup

### Technologies de Réplication
- **Synchrone** : Zero RPO
- **Asynchrone** : Low WAN impact
- **Semi-synchrone** : Compromise
- **Snapshot-based** : Point-in-time

### Configuration NetApp SnapMirror
```bash
# Create snapshot policy
snapshot policy create -policy daily -enabled true -schedule1 daily -count1 7

# Initialize SnapMirror
snapmirror initialize -destination-path svm2:vol1_mirror
snapmirror show
```

### Veeam Backup
```powershell
# Veeam PowerShell
Add-VBRViBackupRepository -Name "Repository1" -Folder "C:\Backup" -MaxConcurrentJobs 4
New-VBRViBackupJob -Name "Daily Backup" -BackupRepository $repo -Entity $vm
```

## 📊 Performance et Monitoring

### Métriques Clés
- **IOPS** : Input/Output Operations Per Second
- **Throughput** : MB/s sustained
- **Latency** : Response time (ms)
- **Queue Depth** : Pending I/O requests

### Outils de Monitoring
```bash
# Linux storage monitoring
iostat -x 1
iotop -o
lsblk
smartctl -a /dev/sda

# Windows storage monitoring
Get-Counter "\PhysicalDisk(*)\Disk Transfers/sec"
Get-StorageJob
Get-PhysicalDisk | Get-StorageReliabilityCounter
```

### Performance Tuning
```bash
# Linux I/O scheduler
echo noop > /sys/block/sda/queue/scheduler

# Queue depth optimization
echo 32 > /sys/block/sda/queue/nr_requests

# Read-ahead tuning
blockdev --setra 4096 /dev/sda
```

## 🛡️ Protection des Données

### RAID Levels
| RAID | Minimum Disks | Usable Space | Fault Tolerance |
|------|---------------|--------------|----------------|
| 0 | 2 | 100% | None |
| 1 | 2 | 50% | 1 disk |
| 5 | 3 | (n-1)/n | 1 disk |
| 6 | 4 | (n-2)/n | 2 disks |
| 10 | 4 | 50% | 1 disk per mirror |

### Erasure Coding
```bash
# Ceph erasure coding pool
ceph osd pool create ecpool 128 erasure
ceph osd erasure-code-profile set myprofile k=4 m=2
ceph osd pool set ecpool erasure-code-profile myprofile
```

### Encryption
```bash
# LUKS encryption
cryptsetup luksFormat /dev/sdb
cryptsetup luksOpen /dev/sdb encrypted_volume
mkfs.ext4 /dev/mapper/encrypted_volume
```

## 🔧 Troubleshooting

### Diagnostics Communs
```bash
# Check disk health
smartctl -H /dev/sda
badblocks -v /dev/sda

# Network storage troubleshooting
showmount -e nfs_server
rpcinfo -p nfs_server

# iSCSI diagnostics
iscsiadm -m session -P 3
multipathd show paths
```

### Performance Issues
1. **High latency** : Check storage queue depth
2. **Low throughput** : Verify network bandwidth
3. **Hot spots** : Analyze data placement
4. **Capacity issues** : Monitor thin provisioning

## 💰 Capacity Planning

### Growth Prediction
```python
# Simple capacity model
import numpy as np
from sklearn.linear_model import LinearRegression

# Historical data (months, GB used)
months = np.array([1, 2, 3, 4, 5, 6]).reshape(-1, 1)
usage = np.array([100, 120, 145, 170, 200, 230])

model = LinearRegression()
model.fit(months, usage)

# Predict next 6 months
future_months = np.array([7, 8, 9, 10, 11, 12]).reshape(-1, 1)
predictions = model.predict(future_months)
```

### TCO Calculation
- **Hardware costs** : Initial + maintenance
- **Software licensing** : OS + management
- **Operational costs** : Power + cooling + space
- **Staff costs** : Administration + training

## 🌐 Cloud Storage Integration

### AWS Storage Gateway
```json
{
  "StorageGatewayArn": "arn:aws:storagegateway:us-east-1:123456789012:gateway/sgw-12A3456B",
  "GatewayType": "FILE_S3",
  "FileShares": [
    {
      "FileShareArn": "arn:aws:storagegateway:us-east-1:123456789012:share/share-12A3456B",
      "S3BucketName": "my-bucket"
    }
  ]
}
```

### Azure StorSimple
- **Hybrid cloud storage**
- **Automated tiering**
- **Snapshot backup**
- **Disaster recovery**

## 🔮 Tendances Futures

### Technologies Émergentes
- **Storage Class Memory** (SCM)
- **Computational Storage**
- **DNA Storage** (recherche)
- **Quantum Storage** (théorique)

### NVMe Adoption
- **NVMe SSDs** : Standard performance
- **NVMe-oF** : Network fabric
- **NVMe/TCP** : Lower cost option
- **NVMe Key-Value** : Optimized access

---

💡 **Best Practice** : Dimensionnez votre stockage pour les pics de charge et planifiez la croissance sur 3-5 ans.