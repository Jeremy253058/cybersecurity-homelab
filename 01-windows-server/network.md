# Configuration réseau de SRV25

## Interface Internet

- VirtualBox : `Nat-Lab`
- Réseau : `10.0.2.0/24`
- IP : `10.0.2.4`
- Passerelle : `10.0.2.1`

## Interface LAB-CYBER

- VirtualBox : `lab-cyber`
- Réseau : `192.168.100.0/24`
- IP : `192.168.100.10`
- Masque : `255.255.255.0`
- Passerelle : aucune
- DNS : `192.168.100.10`

## Vérifications

```powershell
Get-NetAdapter
Get-NetIPConfiguration
Get-DnsClientServerAddress -AddressFamily IPv4
ping 8.8.8.8
```
