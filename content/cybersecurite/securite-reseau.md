---
title: "Sécurité Réseau"
description: "Principes fondamentaux et meilleures pratiques pour sécuriser l'infrastructure réseau"
category: "Cybersécurité"
tags: ["Réseau", "Sécurité", "Firewall", "VPN"]
level: "Intermédiaire"
reading_time: "12 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
---

# Sécurité Réseau

## Introduction

La sécurité réseau constitue la première ligne de défense de toute infrastructure informatique. Elle englobe l'ensemble des mesures techniques et organisationnelles visant à protéger les données et les ressources contre les accès non autorisés.

## Principes Fondamentaux

### Défense en Profondeur

La sécurité réseau repose sur une approche multicouche :

- **Périmètre** : Firewalls, IDS/IPS
- **Réseau interne** : Segmentation, VLANs
- **Endpoints** : Antivirus, EDR
- **Applications** : WAF, authentification

### Modèle Zero Trust

> **Note:** Le modèle Zero Trust part du principe qu'aucun utilisateur ou dispositif ne doit être automatiquement approuvé.

## Configuration Firewall

### Règles de Base

```bash
# Bloquer tout le trafic entrant par défaut
iptables -P INPUT DROP

# Autoriser le trafic sortant
iptables -P OUTPUT ACCEPT

# Autoriser SSH depuis un réseau spécifique
iptables -A INPUT -p tcp -s 192.168.1.0/24 --dport 22 -j ACCEPT

# Autoriser HTTP/HTTPS
iptables -A INPUT -p tcp --dport 80 -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -j ACCEPT
```

### Surveillance et Logs

```bash
# Activer le logging des connexions rejetées
iptables -A INPUT -j LOG --log-prefix "DROPPED: "

# Analyser les logs
tail -f /var/log/syslog | grep "DROPPED:"
```

## Segmentation Réseau

| Zone | Description | Accès |
|------|-------------|-------|
| DMZ | Serveurs publics | Internet → DMZ |
| LAN Utilisateurs | Postes de travail | Interne uniquement |
| LAN Serveurs | Infrastructure critique | Accès contrôlé |
| Gestion | Equipment réseau | Admin uniquement |

## VPN et Accès Distant

### Configuration OpenVPN

```bash
# Installation
sudo apt install openvpn easy-rsa

# Génération des certificats
cd /etc/openvpn/easy-rsa
./easyrsa init-pki
./easyrsa build-ca
./easyrsa gen-req server nopass
./easyrsa sign-req server server
```

> **Attention:** Toujours utiliser des certificats avec une durée de vie limitée.

## Monitoring et Détection

### Outils Essentiels

- **Suricata** : IDS/IPS open source
- **pfSense** : Firewall avec interface web
- **Security Onion** : Distribution pour SOC
- **Zeek** : Analyseur de trafic réseau

### Métriques Clés

```bash
# Surveillance des connexions
netstat -tuln | grep LISTEN

# Analyse du trafic
tcpdump -i eth0 -n -c 100

# Détection des scans de ports
nmap -sS -O target_ip
```

## Bonnes Pratiques

**Recommandations de sécurité :**

- Changer les mots de passe par défaut
- Mettre à jour régulièrement les firmwares
- Désactiver les services non utilisés
- Utiliser des VLANs pour segmenter
- Implémenter l'authentification 802.1X
- Surveiller le trafic en continu

## Gestion des Incidents

### Procédure de Réponse

1. **Détection** : Alertes automatisées
2. **Investigation** : Analyse des logs
3. **Confinement** : Isolation des systèmes
4. **Éradication** : Suppression des menaces
5. **Récupération** : Remise en service
6. **Leçons apprises** : Amélioration des processus

## Ressources Complémentaires

- [NIST Cybersecurity Framework](https://www.nist.gov/cyberframework)
- [SANS Network Security Monitoring](https://www.sans.org/white-papers/1359/)
- [Documentation pfSense](https://docs.netgate.com/pfsense/) 