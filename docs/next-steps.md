# Prochaines étapes

## Blue Team / centralisation

1. Finaliser la source Windows Event Forwarding (WEF) sur `WIN11-CLIENT`
2. Finaliser la souscription WEF sur `SRV25`
3. Vérifier la réception des événements sur SRV25
4. Centraliser les journaux Security
5. Centraliser les événements Sysmon
6. Créer des règles/scénarios de détection
7. Réaliser un scénario complet de réponse à incident
8. Documenter les investigations dans GitHub
9. Mapper les techniques observées avec MITRE ATT&CK

## Cisco Packet Tracer — réalisé

Le projet réseau a été construit et documenté dans :

`05-packet-tracer/`

Il comprend notamment :

- architecture multi-VLAN ;
- routage inter-VLAN ;
- ACL Guest et DMZ ;
- Port Security ;
- DHCP Snooping ;
- DAI ;
- Rapid-PVST+ ;
- SSHv2 ;
- restriction SSH par réseau source ;
- OSPF ;
- NAT/PAT ;
- WAN simulé ;
- scénarios Red Team / Blue Team.

### Validations importantes

- Guest → Servers : bloqué ;
- DMZ → Servers : bloqué ;
- Port Security : 6 violations observées sur Fa0/2 ;
- PC-ADMIN → SW-CORE en SSH : réussi ;
- PC-GUEST → SW-CORE en SSH : refusé ;
- OSPF : voisinage FULL ;
- NAT/PAT : translation observée ;
- PC-ADMIN → ISP simulé : 4/4.

### Limites Packet Tracer

DHCP Snooping a été configuré mais le simulateur indiquait qu'il n'était pas opérationnel sur les VLAN concernés.

DAI était actif et configuré avec les validations MAC/IP, mais la méthode de simulation utilisée n'a pas produit de violation.

Ces points restent donc des pistes de validation dans un environnement plus réaliste plutôt que des contrôles déclarés comme démontrés.

## 🔴 Pentest / Red Team

Le nouveau module est documenté dans :

`10-pentest/README.md`

Progression prévue :

1. Reconnaissance du périmètre autorisé
2. Network Scanning
3. Énumération des services
4. Analyse de vulnérabilités
5. Web Security sur cibles de formation
6. Windows / Active Directory
7. Linux
8. Exploitation contrôlée
9. Post-exploitation contrôlée
10. Analyse des traces côté Blue Team
11. Mapping MITRE ATT&CK
12. Rapport de pentest
13. Scénarios Purple Team

La VM Kali sera ajoutée lorsque les ressources du poste le permettront. Les premiers exercices peuvent être préparés sans ajouter immédiatement une nouvelle VM.

## 🔴🔵 Purple Team

Après les premiers exercices Pentest :

- lancer un scénario Red Team contrôlé ;
- observer les traces générées ;
- corréler avec Windows Event Logs et Sysmon ;
- identifier les techniques MITRE ATT&CK ;
- créer ou améliorer les règles de détection ;
- rejouer le scénario pour vérifier la détection.

## Note sur le SIEM

Une tentative d'installation de Wazuh All-in-One a été réalisée. Elle n'a pas abouti dans l'environnement matériel actuel et la VM a été supprimée. Le projet utilise donc pour le moment WEF/WEC et les outils natifs Windows afin de poursuivre le travail de centralisation et de détection sans alourdir l'infrastructure.
