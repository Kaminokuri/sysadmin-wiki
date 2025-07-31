---
title: "Cryptographie"
description: "Fondements et applications de la cryptographie moderne"
category: "Cybersécurité"
tags: ["Cryptographie", "Chiffrement", "PKI", "Certificates"]
level: "Avancé"
reading_time: "25 min"
last_updated: "31 juillet 2025"
author: "Mathéo Fauvel"
---

# 🔐 Cryptographie

## Introduction

La cryptographie est la science qui étudie les techniques permettant de sécuriser les communications et les données contre les accès non autorisés.

## 🔑 Types de Chiffrement

### Chiffrement Symétrique
- **AES** (Advanced Encryption Standard)
- **ChaCha20**
- **3DES** (obsolète)

```python
# Exemple AES en Python
from cryptography.fernet import Fernet

# Génération de clé
key = Fernet.generate_key()
cipher_suite = Fernet(key)

# Chiffrement
text = "Message secret"
encrypted_text = cipher_suite.encrypt(text.encode())
```

### Chiffrement Asymétrique
- **RSA**
- **ECC** (Elliptic Curve Cryptography)
- **Ed25519**

## 🔏 Fonctions de Hachage

### Algorithmes Recommandés
- **SHA-256/SHA-512**
- **BLAKE2**
- **Argon2** (pour mots de passe)

### Applications
- Intégrité des données
- Signatures numériques
- Proof of Work

## 📜 Infrastructure PKI

### Composants
1. **Autorité de Certification (CA)**
2. **Autorité d'Enregistrement (RA)**
3. **Certificats X.509**
4. **Listes de révocation (CRL)**

### Gestion des Certificats
```bash
# Génération clé privée RSA
openssl genrsa -out private.key 4096

# Génération CSR
openssl req -new -key private.key -out request.csr

# Auto-signature
openssl x509 -req -days 365 -in request.csr -signkey private.key -out certificate.crt
```

## 🔒 Protocoles Cryptographiques

### TLS/SSL
- **TLS 1.3** (recommandé)
- **Perfect Forward Secrecy**
- **Certificate Transparency**

### SSH
- **Ed25519** (clés)
- **ChaCha20-Poly1305** (chiffrement)

## 💾 Chiffrement des Données

### Au Repos
- **LUKS** (Linux)
- **BitLocker** (Windows)
- **FileVault** (macOS)

### En Transit
- **HTTPS/TLS**
- **VPN IPSec**
- **WireGuard**

## ⚡ Performance et Sécurité

### Recommandations
| Usage | Algorithme | Taille Clé |
|-------|------------|------------|
| Symétrique | AES | 256 bits |
| Asymétrique | RSA | 4096 bits |
| Asymétrique | ECC | P-384 |
| Hachage | SHA | 256+ bits |

## 🛡️ Attaques Cryptographiques

### Types d'Attaques
- **Brute Force**
- **Cryptanalyse différentielle**
- **Attaques par canaux auxiliaires**
- **Quantum computing**

### Contre-mesures
- Tailles de clés appropriées
- Rotation des clés
- Post-quantum cryptography

## 🔬 Cryptographie Post-Quantique

### Algorithmes Candidats
- **CRYSTALS-Kyber** (chiffrement)
- **CRYSTALS-Dilithium** (signatures)
- **FALCON**
- **SPHINCS+**

## 📚 Bonnes Pratiques

### Développement
1. **Ne jamais implémenter sa propre crypto**
2. **Utiliser des bibliothèques éprouvées**
3. **Gestion sécurisée des clés**
4. **Validation régulière**

### Audit et Compliance
- **FIPS 140-2**
- **Common Criteria**
- **ANSSI certifications**

## 🧪 Outils et Bibliothèques

### Recommandées
- **OpenSSL**
- **libsodium**
- **Bouncy Castle**
- **Cryptography (Python)**

### Audit
- **Qualys SSL Labs**
- **testssl.sh**
- **cryptsetup**

---

💡 **Important** : La cryptographie évolue constamment. Restez informé des dernières vulnérabilités et recommandations.