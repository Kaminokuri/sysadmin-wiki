---
title: "SIEM & SOC"
description: "Security Information and Event Management et Security Operations Center"
category: "Cybersécurité"
tags: ["SIEM", "SOC", "Monitoring", "Logs"]
level: "Avancé"
reading_time: "18 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
---

# SIEM & SOC

## Introduction

Les SIEM (Security Information and Event Management) et SOC (Security Operations Center) sont essentiels pour la surveillance et la réponse aux incidents de sécurité.

## Concepts SIEM

### Fonctionnalités Principales

- **Collecte de logs** centralisée
- **Corrélation d'événements**
- **Alertes en temps réel**
- **Tableaux de bord**
- **Reporting et conformité**

## Solutions Populaires

| Solution | Type | Description |
|----------|------|-------------|
| Splunk | Commercial | Plateforme complète |
| ELK Stack | Open Source | Elasticsearch, Logstash, Kibana |
| QRadar | Commercial | IBM SIEM |
| Security Onion | Open Source | Distribution NSM |

## Architecture SOC

```bash
# Exemple de collecte avec rsyslog
# Configuration serveur central
$ModLoad imudp
$UDPServerRun 514
$template RemoteLogs,"/var/log/remote/%HOSTNAME%/%PROGRAMNAME%.log"
*.* ?RemoteLogs
```

> **Note:** Article en cours de développement. 