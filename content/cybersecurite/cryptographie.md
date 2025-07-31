---
title: "Cryptographie"
description: "Principes fondamentaux de la cryptographie et applications en sécurité informatique"
category: "Cybersécurité"
tags: ["Cryptographie", "Chiffrement", "PKI", "Sécurité"]
level: "Avancé"
reading_time: "20 min"
last_updated: "1 août 2025"
author: "Mathéo Fauvel"
---

# Cryptographie

## Introduction

La cryptographie est l'art et la science de protéger l'information en utilisant des techniques mathématiques pour transformer les données en formats illisibles.

## Types de Chiffrement

### Chiffrement Symétrique

- **AES** (Advanced Encryption Standard)
- **ChaCha20**
- **3DES** (déprécié)

### Chiffrement Asymétrique

- **RSA**
- **Elliptic Curve Cryptography (ECC)**
- **Diffie-Hellman**

## Fonctions de Hachage

| Algorithme | Taille | Sécurité |
|------------|--------|----------|
| SHA-256 | 256 bits | Recommandé |
| SHA-3 | Variable | Recommandé |
| MD5 | 128 bits | Déprécié |

## Applications Pratiques

```bash
# Génération de clés SSH
ssh-keygen -t ed25519 -C "your_email@example.com"

# Chiffrement de fichier avec GPG
gpg --symmetric --cipher-algo AES256 file.txt

# Vérification d'intégrité
sha256sum file.txt > file.sha256
sha256sum -c file.sha256
```

> **Note:** Article en cours de rédaction. Contenu détaillé à venir. 