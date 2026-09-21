# Architecture et plan d'adressage

## Équipements

| Équipement | Rôle |
|---|---|
| SW-CORE | Cœur réseau, routage inter-VLAN, ACL, OSPF, management |
| SW-ACCESS1 | Accès utilisateurs, trunk, sécurité L2 |
| R1-EDGE | Routeur frontière, OSPF, NAT/PAT, WAN |
| ISP-ROUTER | Internet simulé |
| PC-ADMIN | Administration |
| PC-USER1 | Utilisateur |
| PC-USER2 | Utilisateur |
| PC-GUEST | Invité / Red Team |
| Server-AD-DNS | Serveur interne VLAN 30 |
| Server-WEB-DMZ | Serveur DMZ VLAN 70 |
| DHCP-ROGUE | Faux serveur DHCP du scénario de test |

## VLANs

| VLAN | Nom | Réseau | Passerelle |
|---:|---|---|---|
| 10 | ADMIN | 10.10.10.0/24 | 10.10.10.1 |
| 20 | USERS | 10.10.20.0/24 | 10.10.20.1 |
| 30 | SERVERS | 10.10.30.0/24 | 10.10.30.1 |
| 40 | VOIP | 10.10.40.0/24 | 10.10.40.1 |
| 50 | GUEST | 10.10.50.0/24 | 10.10.50.1 |
| 60 | MANAGEMENT | 10.10.60.0/24 | 10.10.60.1 |
| 70 | DMZ | 10.10.70.0/24 | 10.10.70.1 |

## Hôtes importants

| Hôte | Adresse / rôle |
|---|---|
| PC-ADMIN | 10.10.10.10 |
| Server-AD-DNS | 10.10.30.10 |
| DHCP-ROGUE | 10.10.20.200 |
| SW-CORE VLAN 60 | 10.10.60.1 |
| SW-CORE ↔ R1-EDGE | 10.255.255.2 / 10.255.255.1 |
| R1-EDGE ↔ ISP | 203.0.113.2 / 203.0.113.1 |

## Topologie logique

~~~text
                         ISP-ROUTER
                       203.0.113.1/30
                              |
                       203.0.113.2/30
                           R1-EDGE
                              |
                       10.255.255.0/30
                              |
                           SW-CORE
                              |
                       802.1Q trunk
                              |
                         SW-ACCESS1
                     /   /   |   \   \
                 ADMIN USERS USERS GUEST ...
~~~

## Liaisons

- SW-CORE Gi0/2 ↔ SW-ACCESS1 Gi0/1 : trunk 802.1Q.
- SW-CORE Gi0/1 ↔ R1-EDGE Gi0/0 : lien routé /30.
- R1-EDGE Gi0/1 ↔ ISP-ROUTER Gi0/0 : WAN /30.

## Management

Le VLAN 60 est dédié au management. Le SVI du Core utilise 10.10.60.1 et cette adresse a servi de cible SSH.

Les secrets d'authentification sont volontairement exclus du dépôt.
