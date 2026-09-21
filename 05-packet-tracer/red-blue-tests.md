# Scénarios Red Team / Blue Team

## 1. Guest → Servers

Avant l'ACL, PC-GUEST pouvait joindre 10.10.30.10.

Après ACL-GUEST :

~~~text
PC-GUEST → 10.10.50.1  = OK
PC-GUEST → 10.10.30.10 = 100 % de perte
~~~

Contrôle validé : segmentation Guest → Servers.

## 2. DMZ → Servers

Avant ACL-DMZ, Server-WEB-DMZ pouvait joindre 10.10.30.10.

Après ACL-DMZ :

~~~text
Server-WEB-DMZ → 10.10.30.10
100 % de perte
Destination host unreachable
~~~

Contrôle validé : isolation de la DMZ.

## 3. Port Security

Fa0/2 était limité à une MAC avec apprentissage Sticky et violation Restrict.

PC-USER1 a été remplacé temporairement par PC-ATTACKER.

Après génération de trafic :

~~~text
Security Violation Count : 6
Port Status              : Secure-up
Violation Mode           : Restrict
~~~

Contrôle validé : équipement non autorisé détecté et restreint.

## 4. DHCP Rogue

Un DHCP-ROGUE a été placé sur Fa0/5 du VLAN 20 avec un pool 10.10.20.100+.

La connectivité IP PC-USER2 → DHCP-ROGUE a été validée.

Cependant :

~~~text
DHCP snooping is configured on following VLANs:
10,20,50

DHCP snooping is operational on following VLANs:
none
~~~

Conclusion : configuration réalisée mais blocage DHCP Rogue non retenu comme preuve expérimentale dans Packet Tracer.

## 5. ARP spoofing / DAI

DAI était Active sur les VLAN 10/20/50 avec validation src-mac, dst-mac et ip.

La tentative réalisée n'a produit aucune violation :

~~~text
Dropped               : 0
Source MAC Failures   : 0
Dest MAC Failures     : 0
IP Validation Failures: 0
~~~

Conclusion : DAI configuré et actif, mais attaque non démontrée par un compteur dans Packet Tracer.

## 6. SSH depuis ADMIN

Depuis PC-ADMIN :

~~~text
ssh -l admin-cyber 10.10.60.1
~~~

Connexion réussie vers SW-CORE.

## 7. SSH depuis GUEST

Depuis PC-GUEST :

~~~text
ssh -l admin-cyber 10.10.60.1
~~~

Résultat :

~~~text
Connection timed out; remote host not responding
~~~

L'ACL VTY autorise uniquement le réseau 10.10.10.0/24.

Contrôle validé : l'administration réseau n'est pas accessible depuis Guest.

## 8. Reconnaissance ARP

Sur PC-GUEST :

~~~text
arp -a
~~~

La table ARP montrait la passerelle du VLAN Guest. Les hôtes des autres VLAN n'étaient pas directement présents dans le domaine L2 Guest.

## 9. Validation réseau

- OSPF : voisinage FULL.
- NAT/PAT : translation 10.10.10.10 → 203.0.113.2 observée.
- PC-ADMIN → 203.0.113.1 : 4/4 réponses.
- Guest → Servers : bloqué.
- DMZ → Servers : bloqué.
- ADMIN → SSH Core : autorisé.
- GUEST → SSH Core : refusé.

## Synthèse

| Scénario | Défense | Résultat |
|---|---|---|
| Guest → Servers | ACL-GUEST | ✅ Bloqué |
| DMZ → Servers | ACL-DMZ | ✅ Bloqué |
| Équipement inconnu | Port Security | ✅ 6 violations |
| DHCP Rogue | DHCP Snooping | ⚠️ Non validé dans PT |
| ARP spoofing | DAI | ⚠️ Aucune violation générée |
| SSH Guest | ACL VTY | ✅ Refusé |
| SSH Admin | SSHv2 | ✅ Autorisé |
| OSPF | OSPF | ✅ FULL |
| LAN → WAN | NAT/PAT | ✅ 4/4 |

## Conclusion

Le lab démontre une architecture réseau segmentée avec des contrôles de sécurité validés expérimentalement. Les limites propres au simulateur sont explicitement distinguées des contrôles réellement démontrés.
