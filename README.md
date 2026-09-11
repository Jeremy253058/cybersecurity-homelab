# 🔐 Cybersecurity Homelab

Homelab personnel dédié à la pratique de la cybersécurité, de l'administration systèmes et réseaux et des environnements Active Directory.

L'objectif est de construire progressivement une infrastructure réaliste permettant de pratiquer des scénarios **Red Team, Blue Team et Purple Team**.

## 🏗️ Architecture actuelle

```text
                         INTERNET
                            │
                         NAT-Lab
                       10.0.2.0/24
                            │
                       10.0.2.4
                     ┌─────────────┐
                     │    SRV25    │
                     │ Windows     │
                     │ Server 2025 │
                     │ AD DS + DNS │
                     └──────┬──────┘
                            │
                      LAB-CYBER
                   192.168.100.0/24
                            │
                 ┌──────────┼──────────┐
                 │          │          │
             Windows      Kali      Other VMs
              Client      Linux
🖥️ Infrastructure
Élément	Configuration
Hyperviseur	Oracle VirtualBox
Serveur	Windows Server 2025
Nom du serveur	SRV25
Domaine	lab-cyber.local
NetBIOS	LAB-CYBER
AD DS	Activé
DNS	Activé
Réseau Internet	10.0.2.0/24
Réseau laboratoire	192.168.100.0/24
📁 Organisation
installation.md — Installation et configuration initiale de Windows Server
network.md — Configuration réseau du laboratoire
domain.md — Installation et configuration Active Directory
users-groups.md — Utilisateurs, groupes et OU
dns.md — Configuration et tests DNS
troubleshooting.md — Résolution des problèmes rencontrés
next-steps.md — Évolutions prévues du laboratoire
🔐 Active Directory

Le domaine de laboratoire est :

lab-cyber.local

Structure actuelle :

LAB-CYBER
│
├── Admins
├── Utilisateurs
├── Postes
├── Serveurs
└── Groupes

Utilisateurs et groupes de test :

Jean Dupont
admin-cyber
GG-Utilisateurs
🎯 Objectifs du Homelab
Phase 1 — Infrastructure
 Installation Windows Server 2025
 Configuration réseau
 Installation Active Directory
 Installation DNS
 Création du domaine
 Création des OU
 Création des utilisateurs et groupes
Phase 2 — Sécurisation
 Création des GPO de sécurité
 Durcissement Windows Server
 Gestion des comptes privilégiés
 Politiques de mots de passe
 Audit et journalisation
 Segmentation réseau
Phase 3 — Blue Team
 Centralisation des logs
 Détection d'activités suspectes
 SIEM
 Analyse des événements Windows
 Détection avec Sysmon
 Réponse à incident
Phase 4 — Red Team
 Intégration d'une machine Kali Linux
 Reconnaissance réseau
 Tests Active Directory
 Exploitation contrôlée
 Tests de privilèges
 Simulation d'attaque
Phase 5 — Purple Team
 Scénarios attaque/défense
 Mapping MITRE ATT&CK
 Détection des techniques utilisées
 Amélioration des règles de détection
🧰 Technologies
Windows Server
Active Directory
DNS
VirtualBox
Linux
Kali Linux
PowerShell
Réseaux TCP/IP
GPO
SIEM
MITRE ATT&CK
📚 Objectif professionnel

Ce projet me permet de développer mes compétences pratiques en :

Administration systèmes
Administration réseaux
Active Directory
Sécurité des infrastructures
Windows Security
Détection et réponse aux incidents
Red Team / Blue Team
Cloud et cybersécurité

Projet réalisé dans le cadre de mon parcours en Master/Mastère Cybersécurité.

