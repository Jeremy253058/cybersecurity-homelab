# Réseau du laboratoire

## VirtualBox
- réseau interne : `lab-cyber`
- réseau NAT : `Nat-Lab`

## Plan d'adressage
| Équipement | Réseau | Adresse |
|---|---|---|
| SRV25 | LAB-CYBER | 192.168.100.10/24 |
| WIN11-CLIENT | LAB-CYBER | 192.168.100.20/24 |
| SRV25 | Nat-Lab | 10.0.2.4/24 |

La connectivité TCP entre WIN11-CLIENT et SRV25 a été vérifiée sur le port LDAP 389.
