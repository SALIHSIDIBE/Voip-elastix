# 📞 Implémentation d'une solution VoIP avec Elastix

> Rapport de fin d'études — Spécialité : Réseaux Informatiques & Télécommunications  
> Université de l'Unité Africaine (UUA) — Année académique 2023/2024  
> Auteurs : **KAMBOU Louis Arthur** & **SIDIBE Sâlih**

---

## 🎯 Objectif du projet

Mise en œuvre d'un réseau **VoIP sécurisé** en environnement virtuel, utilisant :
- **Elastix** comme serveur PBX (géré via interface graphique)
- **X-Lite** et **3CX Phone** comme softphones clients
- **ZoiPer** sur téléphones physiques pour les tests d'appels

---

## 🧰 Technologies & Outils utilisés

| Catégorie | Outils |
|---|---|
| Serveur PBX | Elastix (basé sur Asterisk) |
| Hyperviseur | VMware Workstation Pro |
| Softphones | X-Lite, 3CX Phone |
| App mobile | ZoiPer (Android/iOS) |
| Protocole | SIP (Session Initiation Protocol) |
| Réseau | LAN, adressage IP statique |

---

## 🏗️ Architecture déployée

```
[X-Lite / 3CX Phone]  ←──SIP──→  [Serveur Elastix PBX]  ←──SIP──→  [ZoiPer (mobile)]
       (Softphones PC)                  (IP: 192.168.43.254)              (Téléphones physiques)
```

Le serveur **Elastix** joue le rôle de **proxy SIP** : toutes les extensions sont enregistrées sur lui. Lorsqu'un client veut appeler un autre, il compose le numéro d'extension, le serveur vérifie les enregistrements et établit la connexion.

---

## 📋 Extensions créées

| Numéro (SIP Alias) | Nom utilisateur (Display Name) |
|---|---|
| 10 | Arthur |
| 20 | Sidibe |
| 30 | Kambou |
| 40 | Salih |
| 50 | Conférence |

---

## ⚙️ Étapes de réalisation

### 1. Installation d'Elastix sur VMware
- Création d'une machine virtuelle dédiée sous VMware Workstation Pro
- Boot depuis l'ISO Elastix
- Configuration : langue française, clavier `frpc`, fuseau horaire `Africa/Ouagadougou`
- Adresse IP statique configurée manuellement : `192.168.43.254`
- Définition du mot de passe administrateur

### 2. Configuration du serveur PBX
- Accès à l'interface web via `http://192.168.43.254`
- Création des 5 extensions SIP (numéros 10, 20, 30, 40, 50) avec Display Name, SIP Alias et Secret
- Configuration d'une salle de conférence (extension 50)

### 3. Installation et configuration des softphones
- **X-Lite** : configuration via *SIP Account Settings* → renseignement du Display Name, User Name (numéro), Password (secret) et Domain (IP du serveur)
- **3CX Phone** : configuration via *Account Settings* → extension, mot de passe, IP du PBX
- **ZoiPer** (mobile) : configuration du compte SIP avec proxy sortant `192.168.43.254`

### 4. Tests d'appels réalisés
- ✅ Appel X-Lite (Arthur/10) → 3CX Phone (Sidibe/20)
- ✅ Appel 3CX Phone (Sidibe/20) → X-Lite (Arthur/10)
- ✅ Appel entre deux téléphones physiques (ZoiPer)
- ✅ Appel softphone PC → téléphone physique
- ✅ Appel en conférence à 4 clients simultanément (extension 50)

---

## 📊 Comparaison des serveurs PBX étudiés

| Critère | Elastix | Asterisk | YATE |
|---|---|---|---|
| Gateway VoIP/PSTN | ✅ | ✅ | ✅ |
| Messagerie vocale | ✅ | ✅ | ✅ |
| Conférence | ✅ | ✅ | ✅ |
| Protocoles | H.323, SIP, MGCP | H.323, SIP, MGCP | H.323, SIP, MGCP |
| Administration | GUI | GUI | GUI |
| QoS | ✅ | ✅ | ❌ |

---

## 🔑 Concepts clés abordés

- **RTC vs VoIP** : passage du réseau téléphonique commuté vers la voix sur IP
- **Architecture VoIP** : routeur, passerelle (Gatekeeper), switch, PABX, terminaux
- **Protocole SIP** : négociation d'appel, enregistrement des extensions, établissement de session
- **PBX open source** : Asterisk, Elastix, YATE — comparaison fonctionnelle
- **Softphones** : 3CX, ZoiPer, Jitsi, X-Lite

---

## 📁 Structure du projet

```
voip-elastix/
│
├── README.md               # Ce fichier
├── rapport/
│   └── Projet_de_fin_etude.pdf   # Rapport complet (33 pages)
└── docs/
    ├── architecture_voip.png     # Schéma architecture
    └── extensions_list.png       # Captures des extensions créées
```

---

## 📚 Références

- [www.3cx.com](https://www.3cx.com)
- [www.elastixtech.com](https://www.elastixtech.com)
- [www.wikipedia.org](https://www.wikipedia.org)

---

## 👨‍💻 Auteurs

| Nom | LinkedIn |
|---|---|
| **SIDIBE Salih** | [linkedin.com/in/salih-sidibe](https://linkedin.com/in/salih-sidibe) |
| **KAMBOU Louis Arthur** | — |

---

> 📅 Projet réalisé dans le cadre du rapport de fin d'études — Licence Réseaux & Télécommunications — UUA Ouagadougou — 2023/2024
