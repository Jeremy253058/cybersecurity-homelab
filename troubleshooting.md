# Dépannage réseau — Adaptateur LAB-CYBER

## Problème

Après des modifications de la configuration VirtualBox, l'interface destinée à `LAB-CYBER` n'était plus correctement détectée par Windows.

## Diagnostic

Commandes utilisées :

```powershell
Get-NetAdapter
Get-PnpDevice -Class Net
Get-PnpDevice -Class Net |
    Format-Table Status,FriendlyName,Problem -AutoSize
```

Un ancien périphérique Intel PRO/1000 apparaissait comme périphérique fantôme (`CM_PROB_PHANTOM`).

VirtualBox confirmait que l'Adaptateur 2 était branché sur le réseau interne `lab-cyber`.

## Résolution

Une nouvelle interface réseau interne a été créée dans VirtualBox. Windows l'a ensuite détectée comme `Ethernet 2`.

Configuration finale :

```text
IP : 192.168.100.10/24
Passerelle : aucune
DNS : 192.168.100.10
```

## Retour d'expérience

Ce dépannage a permis de pratiquer le diagnostic réseau Windows, l'inspection Plug and Play, le diagnostic d'une carte virtuelle VirtualBox, l'IPv4 statique et la validation DNS.
