# Déploiement Active Directory

## Domaine

```text
lab-cyber.local
```

Nom NetBIOS :

```text
LAB-CYBER
```

Contrôleur de domaine :

```text
SRV25.lab-cyber.local
```

## Rôles

- Active Directory Domain Services
- DNS
- Catalogue global

## Niveau fonctionnel

- Forêt : Windows Server 2025
- Domaine : Windows Server 2025

## Vérifications

```powershell
Get-ADDomain
Get-ADDomainController
Get-Service DNS
```
