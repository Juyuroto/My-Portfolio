# Projet Infrastructure Portfolio

## Résumé du projet

Ce projet consiste à mettre en place une infrastructure réseau complète comprenant :

* un pare-feu **pfSense** avec WAN/LAN/DMZ,
* un switch **Cisco manageable** configuré avec VLANs,
* deux serveurs en **DMZ** (Portfolio + Backup),
* un PC Admin isolé dans le LAN,
* un site Portfolio hébergé localement et accessible via un nom de domaine.

Cette documentation décrit toute la configuration : réseau, sécurité, serveurs, firewall, VLAN, mise en ligne du site.

---

## Sommaire

- [Résumé du projet](#résumé-du-projet)  
- [Installation (Guide rapide)](#installation-guide-rapide)  
  - [1. Installer pfSense](#1-installer-pfsense)  
  - [2. Installer les serveurs (Ubuntu Server 22.04 recommandé)](#2-installer-les-serveurs-ubuntu-server-2204-recommandé)  
  - [3. Configurer switch Cisco](#3-configurer-switch-cisco)  
  - [4. Déployer le site Portfolio](#4-déployer-le-site-portfolio)  
- [Table des matières](#table-des-matières)  
- [Infrastructure Complete README](#infrastructure-complete-readme)  
  - [Infra](#infra)  
  - [Configuration Infra](#configuration-infra)  
    - [WAN (vers Box FAI)](#wan-vers-box-fai)  
    - [LAN (réseau interne + PC admin)](#lan-réseau-interne--pc-admin)  
    - [DMZ (Serveurs exposés)](#dmz-serveurs-exposés)  
- [Règles NAT & Firewall pfSense](#règles-nat--firewall-pfsense)  
  - [DMZ → Internet](#dmz-→-internet)  
  - [DMZ → LAN (INTERDIT)](#dmz-→-lan-interdit)  
  - [LAN → DMZ (PC Admin uniquement)](#lan-→-dmz-pc-admin-uniquement)  
  - [WAN → DMZ (Accès Internet au Portfolio)](#wan-→-dmz-accès-internet-au-portfolio)  
- [VLAN dans pfSense](#vlan-dans-pfsense)  
- [Switch Cisco (manageable)](#switch-cisco-manageable)  
- [Configuration des Serveurs (DMZ)](#configuration-des-serveurs-dmz)  
  - [Serveur Portfolio (Serveur 1)](#serveur-portfolio-serveur-1)  
  - [Serveur 2 (Backup / Assistance)](#serveur-2-backup--assistance)  
- [Synchronisation Serveur 1 → Serveur 2 (optionnel)](#synchronisation-serveur-1-→-serveur-2-optionnel)  
- [HAProxy (optionnel, sur pfSense)](#haproxy-optionnel-sur-pfsense)  
- [Installation du service web "Ubuntu" (Docker)](#installation-du-service-web-ubuntu-docker)  
- [Configuration réseau des serveurs (IP fixes)](#configuration-réseau-des-serveurs-ip-fixes)  
- [Sécurisation des serveurs](#sécurisation-des-serveurs)

## Pages

- [1. Configuration général](README_Config.md)
- [2. Configuration PC Admin](README_PC_Admin.md)
- [3. Configuration Switch](README_Switch.md)


## Archi code

```markdown
mon-projet/
├── docker/
│   ├── apache/
│   │   └── vhost.conf
│   └── php/
│       └── Dockerfile
│
├── public/
│   ├── index.php
│   ├── page2.php
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── app.js
│
├── src/
│   ├── Config/
│   │   └── Database.php
│   ├── Controllers/
│   │   ├── HomeController.php
│   │   └── Page2Controller.php
│   ├── Models/
│   │   └── User.php
│   └── Views/
│       ├── layouts/
│       │   └── main.php
│       ├── home.php
│       └── page2.php
│
├── vendor/
│
├── .env
├── .env.example
├── .gitignore
├── composer.json
├── docker-compose.yml
└── README.md
```