# 🔐 Cybersecurity Homelab

Homelab personnel dédié à la pratique de la cybersécurité, de l'administration systèmes et réseaux, d'Active Directory et de la Blue Team.

## 🏗️ Architecture

```text
Internet
   │
Nat-Lab 10.0.2.0/24
   │
SRV25 — Windows Server 2025
10.0.2.4 / 192.168.100.10
   │
LAB-CYBER 192.168.100.0/24
   │
WIN11-CLIENT — 192.168.100.20
   │
   └── Sysmon → événements Windows
                 │
                 ▼
          WEF / WEC (SRV25)
```

## 🖥️ Infrastructure

| Élément | Configuration |
|---|---|
| Hyperviseur | Oracle VirtualBox |
| Serveur | Windows Server 2025 / SRV25 |
| Domaine | `lab-cyber.local` |
| NetBIOS | `LAB-CYBER` |
| AD DS | Activé |
| DNS | Activé |
| Réseau lab | `192.168.100.0/24` |
| Client | Windows 11 / WIN11-CLIENT |
| Collecte d'événements | Windows Event Collector sur SRV25 |

## 📚 Documentation

- [Active Directory](domain.md)
- [Utilisateurs, groupes et OU](users-groups.md)
- [GPO et durcissement](gpo-hardening.md)
- [Audit Windows / AD](audit.md)
- [Sysmon](sysmon.md)
- [WEF / WEC](wef-wec.md)
- [Exercices Blue Team](blue-team.md)
- [Réseau](network.md)
- [Dépannage](troubleshooting.md)
- [Prochaines étapes](next-steps.md)

## 🔐 Active Directory

Structure :

```text
LAB-CYBER
├── Admins
├── Utilisateurs
├── Postes
├── Serveurs
└── Groupes
```

Comptes/groupes de lab :
- `jdupont`
- `admin-cyber`
- `GG-Utilisateurs`
- `test-attacker`

## 🛡️ Blue Team

Travaux réalisés :

- GPO de sécurité et politique de mots de passe ;
- verrouillage de compte ;
- audit des comptes et groupes ;
- journalisation PowerShell ;
- déploiement de Sysmon ;
- analyse Sysmon Event ID 1 ;
- analyse Security Event ID 4728 ;
- analyse Security Event ID 4740 ;
- corrélation temporelle d'événements ;
- configuration de Windows Event Collector (WEC) sur SRV25 ;
- préparation de Windows Event Forwarding (WEF) pour la centralisation des journaux.

### Événements étudiés

| Event ID | Source | Signification |
|---|---|---|
| 1 | Sysmon | Création de processus |
| 4728 | Security | Ajout d'un membre à un groupe global de sécurité |
| 4740 | Security | Verrouillage d'un compte |

## 📡 Centralisation des événements

Le serveur `SRV25` a été configuré comme **Windows Event Collector (WEC)** avec :

```powershell
winrm quickconfig
wecutil quick-config
```

Le service Windows Event Collector est opérationnel.

**Prochaine étape :** configurer `WIN11-CLIENT` comme source WEF et créer une souscription pour centraliser les événements de sécurité et Sysmon sur SRV25.

## 🎯 Progression

### Infrastructure
- [x] Windows Server 2025
- [x] Réseau VirtualBox
- [x] Active Directory
- [x] DNS
- [x] OU, utilisateurs et groupes
- [x] Client Windows 11 joint au domaine

### Sécurisation
- [x] GPO de sécurité
- [x] Politique de mots de passe
- [x] Politique de verrouillage
- [x] Audit Windows
- [x] Journalisation PowerShell

### Blue Team
- [x] Sysmon
- [x] Event ID 1
- [x] Event ID 4728
- [x] Event ID 4740
- [x] Corrélation d'événements
- [x] Configuration WEC sur SRV25
- [ ] Configuration WEF sur WIN11-CLIENT
- [ ] Souscription WEF et centralisation des événements
- [ ] Règles de détection avancées
- [ ] Réponse à incident complète

### Red / Purple Team
- [ ] Kali Linux
- [ ] Tests AD contrôlés
- [ ] Scénarios attaque/défense
- [ ] Mapping MITRE ATT&CK

## 🧰 Technologies

Windows Server · Windows 11 · Active Directory · DNS · VirtualBox · PowerShell · GPO · Sysmon · WEF/WEC · TCP/IP · Linux/Kali · SIEM · MITRE ATT&CK

## 📚 Objectif professionnel

Ce projet développe des compétences pratiques en administration systèmes et réseaux, Active Directory, Windows Security, durcissement, centralisation et analyse de logs, détection et réponse aux incidents, et Blue/Red/Purple Team.

Projet réalisé dans le cadre du parcours Master/Mastère Cybersécurité.
