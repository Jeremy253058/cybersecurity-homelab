# 🌐 Packet Tracer — Infrastructure réseau & cybersécurité

Projet Cisco Packet Tracer construit en parallèle du homelab Windows/AD/Blue Team.

## Objectifs

- Concevoir une architecture réseau multi-VLAN.
- Mettre en œuvre le routage inter-VLAN.
- Segmenter les zones avec des ACL.
- Sécuriser la couche 2.
- Sécuriser l'administration avec SSHv2.
- Mettre en œuvre OSPF.
- Mettre en place NAT/PAT et un WAN simulé.
- Réaliser des scénarios Red Team / Blue Team.
- Conserver des preuves avant/après.
- Documenter les limites de Packet Tracer.

## Architecture

~~~text
                         INTERNET SIMULÉ
                              |
                       ISP-ROUTER
                       203.0.113.1/30
                              |
                       203.0.113.2/30
                           R1-EDGE
                              |
                       10.255.255.0/30
                              |
                           SW-CORE
                         /         \
                    trunk           L3
                      /              \
               SW-ACCESS1           R1-EDGE
              /  /  |  \  \
          ADMIN USERS USERS GUEST ...
~~~

VLANs :
- 10 ADMIN
- 20 USERS
- 30 SERVERS
- 40 VOIP
- 50 GUEST
- 60 MANAGEMENT
- 70 DMZ

## État final

### Infrastructure
- [x] VLAN 10/20/30/40/50/60/70
- [x] Trunks 802.1Q
- [x] Routage inter-VLAN
- [x] Lien L3 SW-CORE ↔ R1-EDGE
- [x] WAN R1-EDGE ↔ ISP-ROUTER
- [x] OSPF voisinage FULL
- [x] NAT/PAT
- [x] LAN → WAN simulé

### Sécurité
- [x] ACL Guest
- [x] ACL DMZ
- [x] Port Security
- [x] DHCP Snooping configuré
- [x] DAI actif
- [x] Rapid-PVST+
- [x] BPDU Guard
- [x] SSHv2
- [x] ACL VTY de management

### Tests
- [x] Guest → Servers bloqué
- [x] DMZ → Servers bloqué
- [x] Port Security : 6 violations observées
- [x] PC-ADMIN → SSH Core
- [x] PC-GUEST → SSH Core refusé
- [x] OSPF FULL
- [x] NAT/PAT fonctionnel
- [ ] DHCP Snooping validé par compteur dans Packet Tracer
- [ ] DAI validé par une vraie violation ARP dans Packet Tracer

## Limites constatées

DHCP Snooping était configuré sur les VLAN 10/20/50 avec le lien Core en Trusted, mais Packet Tracer indiquait que les VLAN n'étaient pas opérationnels.

DAI était actif avec les validations source MAC, destination MAC et IP, mais le scénario ARP spoofing réalisé n'a généré aucune violation.

Ces éléments sont donc documentés comme configurés mais non démontrés expérimentalement dans ce simulateur.

## Documentation

- [Architecture et adressage](architecture-addressing.md)
- [Configuration et sécurité](configuration-security.md)
- [Routage, OSPF et NAT/PAT](routing-wan.md)
- [Scénarios Red Team / Blue Team](red-blue-tests.md)

## Sécurité des secrets

Les vrais mots de passe du lab ne sont pas stockés dans ce dépôt public. Les exemples de configuration utilisent des placeholders.

## Contexte

Projet réalisé dans le cadre du parcours Master/Mastère Cybersécurité, en complément du homelab Windows/Active Directory/Blue Team.
