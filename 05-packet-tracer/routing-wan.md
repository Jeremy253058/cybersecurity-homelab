# Routage, OSPF et NAT/PAT

## Lien SW-CORE ↔ R1-EDGE

### SW-CORE

~~~cisco
interface gigabitEthernet0/1
 description L3-LINK-VERS-R1-EDGE
 no switchport
 ip address 10.255.255.2 255.255.255.252
 no shutdown
~~~

### R1-EDGE

~~~cisco
interface gigabitEthernet0/0
 description LINK-VERS-SW-CORE
 ip address 10.255.255.1 255.255.255.252
 no shutdown
~~~

Ping validé : 5/5.

## WAN simulé

### R1-EDGE

~~~cisco
interface gigabitEthernet0/1
 description WAN-VERS-ISP
 ip address 203.0.113.2 255.255.255.252
 no shutdown
~~~

### ISP-ROUTER

~~~cisco
interface gigabitEthernet0/0
 description WAN-VERS-R1-EDGE
 ip address 203.0.113.1 255.255.255.252
 no shutdown
~~~

Ping R1-EDGE → ISP : 5/5.

## OSPF

### SW-CORE

~~~cisco
router ospf 1
 router-id 1.1.1.1
 passive-interface default
 no passive-interface gigabitEthernet0/1
 network 10.10.0.0 0.0.255.255 area 0
 network 10.255.255.0 0.0.0.3 area 0
~~~

### R1-EDGE

~~~cisco
router ospf 1
 router-id 2.2.2.2
 network 10.255.255.0 0.0.0.3 area 0
 network 203.0.113.0 0.0.0.3 area 0
~~~

Voisinage observé des deux côtés :

~~~text
Neighbor State: FULL
~~~

Le Core a appris :

~~~text
O 203.0.113.0/30 via 10.255.255.1
~~~

## NAT/PAT

Sur R1-EDGE :

~~~cisco
interface gigabitEthernet0/0
 ip nat inside

interface gigabitEthernet0/1
 ip nat outside

access-list 1 permit 10.10.0.0 0.0.255.255

ip nat inside source list 1 interface gigabitEthernet0/1 overload
~~~

Une translation réelle a été observée :

~~~text
Inside local   : 10.10.10.10
Inside global  : 203.0.113.2
~~~

Une route de retour vers 10.10.0.0/16 a été configurée sur l'ISP via 203.0.113.2.

## Validation finale

Depuis PC-ADMIN :

~~~text
ping 203.0.113.1
~~~

Résultat :

~~~text
4 envoyés
4 reçus
0 % de perte
~~~

Le chemin LAN → SW-CORE → R1-EDGE → NAT/PAT → ISP simulé est fonctionnel.
