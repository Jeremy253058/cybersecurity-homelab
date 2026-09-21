# Configuration réseau et sécurité

Les commandes ci-dessous reprennent les configurations réellement utilisées pendant le lab. Les secrets sont remplacés par des placeholders.

## VLANs sur SW-CORE

~~~cisco
configure terminal
vlan 10
 name ADMIN
vlan 20
 name USERS
vlan 30
 name SERVERS
vlan 40
 name VOIP
vlan 50
 name GUEST
vlan 60
 name MANAGEMENT
vlan 70
 name DMZ
~~~

## SVI

~~~cisco
interface vlan 10
 ip address 10.10.10.1 255.255.255.0
 no shutdown
interface vlan 20
 ip address 10.10.20.1 255.255.255.0
 no shutdown
interface vlan 30
 ip address 10.10.30.1 255.255.255.0
 no shutdown
interface vlan 40
 ip address 10.10.40.1 255.255.255.0
 no shutdown
interface vlan 50
 ip address 10.10.50.1 255.255.255.0
 no shutdown
interface vlan 60
 ip address 10.10.60.1 255.255.255.0
 no shutdown
interface vlan 70
 ip address 10.10.70.1 255.255.255.0
 no shutdown
~~~

## Trunk

~~~cisco
interface gigabitEthernet0/2
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30,40,50,60,70
~~~

SW-ACCESS1 Gi0/1 a été configuré comme trunk vers le Core avec les mêmes VLAN autorisés.

## ACL Guest

~~~cisco
ip access-list extended ACL-GUEST
 deny ip 10.10.50.0 0.0.0.255 10.10.10.0 0.0.0.255
 deny ip 10.10.50.0 0.0.0.255 10.10.20.0 0.0.0.255
 deny ip 10.10.50.0 0.0.0.255 10.10.30.0 0.0.0.255
 deny ip 10.10.50.0 0.0.0.255 10.10.40.0 0.0.0.255
 deny ip 10.10.50.0 0.0.0.255 10.10.60.0 0.0.0.255
 deny ip 10.10.50.0 0.0.0.255 10.10.70.0 0.0.0.255
 permit ip any any

interface vlan 50
 ip access-group ACL-GUEST in
~~~

## ACL DMZ

~~~cisco
ip access-list extended ACL-DMZ
 deny ip 10.10.70.0 0.0.0.255 10.10.10.0 0.0.0.255
 deny ip 10.10.70.0 0.0.0.255 10.10.20.0 0.0.0.255
 deny ip 10.10.70.0 0.0.0.255 10.10.30.0 0.0.0.255
 deny ip 10.10.70.0 0.0.0.255 10.10.40.0 0.0.0.255
 deny ip 10.10.70.0 0.0.0.255 10.10.50.0 0.0.0.255
 deny ip 10.10.70.0 0.0.0.255 10.10.60.0 0.0.0.255
 permit ip any any

interface vlan 70
 ip access-group ACL-DMZ in
~~~

## Port Security

Ports utilisateurs Fa0/1 à Fa0/4 :

~~~cisco
interface range fastEthernet0/1 - 4
 switchport port-security
 switchport port-security maximum 1
 switchport port-security mac-address sticky
 switchport port-security violation restrict
~~~

Résultat du test : 6 violations sur Fa0/2 avec le port resté Secure-up.

## DHCP Snooping

~~~cisco
ip dhcp snooping
ip dhcp snooping vlan 10,20,50

interface gigabitEthernet0/1
 ip dhcp snooping trust
~~~

Le Core est Trusted ; les ports utilisateurs restent Untrusted.

Limite : Packet Tracer indiquait que le DHCP Snooping n'était pas opérationnel sur les VLAN malgré la configuration.

## DAI

~~~cisco
ip arp inspection vlan 10,20,50

interface gigabitEthernet0/1
 ip arp inspection trust

ip arp inspection validate src-mac dst-mac ip
~~~

Les VLAN 10/20/50 étaient Active. Aucune violation n'a été générée par le scénario ARP réalisé.

## Rapid-PVST+

~~~cisco
spanning-tree mode rapid-pvst
spanning-tree vlan 10,20,30,40,50,60,70 root primary
~~~

La configuration observée sur le Core indiquait une priorité de 24576.

## SSHv2

~~~cisco
ip domain-name lab-cyber.local
username admin-cyber privilege 15 secret <SECRET>
enable secret <ENABLE_SECRET>
crypto key generate rsa
ip ssh version 2

line vty 0 15
 login local
 transport input ssh
~~~

SSHv2 a été vérifié avec show ip ssh. Une connexion réelle depuis PC-ADMIN vers 10.10.60.1 a réussi.

## Restriction de l'administration SSH

~~~cisco
ip access-list standard ACL-SSH-MGMT
 permit 10.10.10.0 0.0.0.255
 deny any

line vty 0 15
 access-class ACL-SSH-MGMT in
~~~

PC-ADMIN est autorisé ; PC-GUEST est refusé.

## Bonnes pratiques

Ne jamais copier les vrais secrets dans un dépôt public. Les valeurs utilisées dans le lab sont volontairement remplacées par des placeholders ici.
