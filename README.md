# 🔐 Cybersecurity Homelab

Homelab personnel dédié à la pratique de la cybersécurité, de l'administration systèmes et réseaux, d'Active Directory, de la Blue Team, du Red Team/Pentest et de la sécurité réseau Cisco.

## 🏗️ Architecture principale

Le projet est organisé autour de plusieurs environnements complémentaires :

1. **Homelab Windows / Active Directory / Blue Team**
   - Windows Server 2025 / SRV25
   - Active Directory / DNS
   - Windows 11 / WIN11-CLIENT
   - GPO / audit / Sysmon
   - WEF / WEC

2. **Lab réseau Cisco Packet Tracer**
   - architecture multi-VLAN
   - routage inter-VLAN
   - ACL
   - sécurité Layer 2
   - SSHv2
   - OSPF
   - NAT/PAT
   - scénarios Red Team / Blue Team

3. **Lab Pentest / Red Team**
   - reconnaissance
   - scanning
   - énumération
   - sécurité Windows / Active Directory
   - sécurité web sur cibles de formation
   - exploitation contrôlée
   - analyse des traces côté Blue Team
   - scénarios Purple Team

## 📚 Documentation

### Homelab Windows / Blue Team

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

### Cisco Packet Tracer

- [Vue d'ensemble du projet](05-packet-tracer/README.md)
- [Architecture et plan d'adressage](05-packet-tracer/architecture-addressing.md)
- [Configuration et sécurité](05-packet-tracer/configuration-security.md)
- [Routage, OSPF et NAT/PAT](05-packet-tracer/routing-wan.md)
- [Scénarios Red Team / Blue Team](05-packet-tracer/red-blue-tests.md)

### Pentest / Red Team

- [Lab Pentest](10-pentest/README.md)

## 🖥️ Infrastructure Windows

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

## 🌐 Infrastructure Packet Tracer

| Élément | Rôle |
|---|---|
| SW-CORE | cœur réseau, routage inter-VLAN, ACL, OSPF, management |
| SW-ACCESS1 | accès utilisateurs et sécurité Layer 2 |
| R1-EDGE | routage frontière, OSPF, NAT/PAT |
| ISP-ROUTER | Internet simulé |
| VLANs | 10 ADMIN / 20 USERS / 30 SERVERS / 40 VOIP / 50 GUEST / 60 MANAGEMENT / 70 DMZ |

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
- configuration WEC sur SRV25 ;
- préparation de WEF pour la centralisation des journaux ;
- segmentation réseau Cisco ;
- ACL Guest et DMZ ;
- Port Security ;
- DHCP Snooping ;
- Dynamic ARP Inspection ;
- Rapid-PVST+ ;
- SSHv2 et restriction de l'administration ;
- OSPF ;
- NAT/PAT.

## 🔴🔵 Red / Blue Team

Scénarios Packet Tracer documentés :

- Guest → Servers bloqué par ACL ;
- DMZ → Servers bloqué par ACL ;
- équipement non autorisé détecté par Port Security ;
- tentative DHCP Rogue ;
- tentative ARP spoofing / DAI ;
- administration SSH autorisée depuis ADMIN et refusée depuis GUEST ;
- validation OSPF ;
- validation NAT/PAT.

Les résultats distinguent explicitement les contrôles réellement validés de ceux qui ont seulement été configurés mais non démontrés dans Packet Tracer.

## 🔴 Pentest / Red Team

Le module [10-pentest](10-pentest/README.md) couvre progressivement :

- reconnaissance ;
- scanning réseau ;
- énumération ;
- sécurité web sur environnements de formation ;
- Windows / Active Directory ;
- Linux ;
- exploitation contrôlée ;
- post-exploitation contrôlée ;
- analyse des traces ;
- rapports de pentest ;
- mapping MITRE ATT&CK ;
- scénarios Purple Team.

Tous les exercices d'exploitation sont limités aux systèmes du homelab ou aux plateformes explicitement prévues pour l'entraînement.

## 🎯 Progression

### Infrastructure Windows
- [x] Windows Server 2025
- [x] Réseau VirtualBox
- [x] Active Directory
- [x] DNS
- [x] OU, utilisateurs et groupes
- [x] Client Windows 11 joint au domaine

### Sécurisation Windows
- [x] GPO de sécurité
- [x] Politique de mots de passe
- [x] Politique de verrouillage
- [x] Audit Windows
- [x] Journalisation PowerShell
- [x] Sysmon

### Blue Team / centralisation
- [x] Event ID 1
- [x] Event ID 4728
- [x] Event ID 4740
- [x] Corrélation d'événements
- [x] Configuration WEC sur SRV25
- [ ] Configuration WEF complète sur WIN11-CLIENT
- [ ] Centralisation complète des événements
- [ ] Règles de détection avancées
- [ ] Réponse à incident complète

### Cisco / réseau sécurisé
- [x] VLAN 10/20/30/40/50/60/70
- [x] Trunks 802.1Q
- [x] Routage inter-VLAN
- [x] ACL Guest
- [x] ACL DMZ
- [x] Port Security
- [x] DHCP Snooping configuré
- [x] DAI actif
- [x] Rapid-PVST+
- [x] SSHv2
- [x] OSPF
- [x] NAT/PAT
- [x] Scénarios Red Team / Blue Team
- [ ] Validation DHCP Snooping dans un environnement permettant son fonctionnement complet
- [ ] Validation DAI avec une véritable trame ARP spoofing

### Pentest / Red Team
- [x] Structure du module Pentest
- [ ] Reconnaissance
- [ ] Network Scanning
- [ ] Énumération
- [ ] Web Security
- [ ] Windows / Active Directory
- [ ] Linux
- [ ] Exploitation contrôlée
- [ ] Post-exploitation contrôlée
- [ ] Purple Team

## 🧰 Technologies

Windows Server · Windows 11 · Active Directory · DNS · VirtualBox · PowerShell · Sysmon · WEF/WEC · Cisco Packet Tracer · VLAN · ACL · SSH · OSPF · NAT/PAT · TCP/IP · Linux/Kali · Nmap · SIEM · MITRE ATT&CK

## 📚 Objectif professionnel

Ce projet développe des compétences pratiques en administration systèmes et réseaux, Active Directory, Windows Security, durcissement, segmentation réseau, sécurité des équipements, centralisation et analyse de logs, détection et réponse aux incidents, pentest et approches Blue/Red/Purple Team.

Projet réalisé dans le cadre du parcours Master/Mastère Cybersécurité.
