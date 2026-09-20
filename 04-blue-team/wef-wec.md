# Windows Event Forwarding / Windows Event Collector

## Objectif

Centraliser les journaux Windows du poste `WIN11-CLIENT` sur le serveur `SRV25` afin de construire une base de supervision et de détection Blue Team sans ajouter de serveur SIEM lourd.

## Architecture

```text
WIN11-CLIENT
192.168.100.20
    │
    │ Windows Event Forwarding (WEF)
    ▼
SRV25
192.168.100.10
Windows Event Collector (WEC)
    │
    ▼
Journaux centralisés
```

## Configuration réalisée sur SRV25

WinRM était déjà actif :

```powershell
winrm quickconfig
```

Résultat : WinRM était déjà configuré pour la gestion à distance.

Le rôle de collecteur d'événements a ensuite été configuré :

```powershell
wecutil quick-config
```

Résultat :

> Le service Collecteur d'événements Windows a été configuré.

## État actuel

- [x] WinRM actif sur SRV25
- [x] Windows Event Collector configuré sur SRV25
- [ ] Configurer WIN11-CLIENT comme source WEF
- [ ] Créer la souscription d'événements
- [ ] Vérifier la réception des événements sur SRV25
- [ ] Centraliser les événements Security
- [ ] Centraliser les événements Sysmon
- [ ] Créer des scénarios de détection

## Objectif Blue Team

Une fois la centralisation opérationnelle, les événements pourront être analysés depuis SRV25 pour rechercher notamment :

- créations de processus ;
- authentifications ;
- verrouillages de comptes ;
- modifications de groupes ;
- événements PowerShell ;
- événements Sysmon.

La centralisation permettra ensuite de construire des scénarios d'investigation et de réponse à incident à partir des événements déjà étudiés dans le lab.

## Choix d'architecture

Une tentative d'installation d'un SIEM Wazuh All-in-One a été réalisée, mais l'installation n'a pas abouti dans l'environnement matériel actuel. La VM Wazuh a donc été supprimée afin de préserver les ressources de l'hôte.

Le lab continue avec les mécanismes natifs Windows WEF/WEC, adaptés aux ressources disponibles, tout en conservant les objectifs de centralisation, détection et investigation.
