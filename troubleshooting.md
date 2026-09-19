# Dépannage

## DNS multihoming
SRV25 publiait plusieurs adresses DNS. L'interface NAT a été empêchée d'enregistrer son adresse :
```powershell
Set-DnsClient -InterfaceAlias "Ethernet 3" -RegisterThisConnectionsAddress $false
ipconfig /registerdns
```

## Synchronisation horaire
```powershell
w32tm /resync
```
La source observée était `SRV25.lab-cyber.local`.

## Pare-feu ICMP
Le ping pouvait échouer alors que la connectivité TCP fonctionnait. Le ping n'a donc pas été utilisé seul pour conclure à une panne.

## Sysmon
Le service Sysmon fonctionnait et produisait des Event ID 1. Certains tests spécifiques n'ont pas produit le résultat filtré attendu.
