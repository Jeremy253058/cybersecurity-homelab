# DNS Active Directory

SRV25 utilise son propre service DNS AD.

Serveur DNS de l'interface LAB-CYBER :

```text
192.168.100.10
```

## Tests

```powershell
nslookup SRV25.lab-cyber.local 192.168.100.10
nslookup lab-cyber.local
nslookup -type=SRV _ldap._tcp.dc._msdcs.lab-cyber.local
dcdiag /test:dns
```

La résolution de `SRV25.lab-cyber.local` et `lab-cyber.local` fonctionne. `dcdiag /test:dns` a confirmé le fonctionnement du test DNS, avec quelques avertissements liés à la configuration multi-cartes qui seront traités ultérieurement.
