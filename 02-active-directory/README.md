# Active Directory — Homelab Windows

> Projet pratique d'administration et de sécurisation d'un environnement Windows Server / Active Directory, réalisé dans un laboratoire virtualisé.

## Objectifs

- Déployer un domaine Active Directory pour centraliser les identités.
- Configurer le DNS nécessaire à la résolution du domaine et aux services AD.
- Organiser les comptes et les ordinateurs avec des unités d'organisation (OU).
- Distinguer les comptes standards des comptes privilégiés.
- Documenter les contrôles de configuration et les prochaines étapes de sécurisation.

## Environnement

| Élément | Valeur documentée |
|---|---|
| Hyperviseur | Oracle VirtualBox |
| Serveur | Windows Server 2025 — `SRV25` |
| Domaine | `lab-cyber.local` |
| Nom NetBIOS | `LAB-CYBER` |
| Services | AD DS, DNS, catalogue global |
| Adresse DNS documentée | `192.168.100.10` |
| Réseau du laboratoire | `192.168.100.0/24` |
| Client | Windows 11 — `WIN11-CLIENT` |

## Architecture logique

```text
        Laboratoire VirtualBox
                 |
       Réseau privé du lab
          192.168.100.0/24
                 |
       +--------------------+
       | SRV25              |
       | Windows Server 2025|
       | AD DS + DNS        |
       | 192.168.100.10     |
       +--------------------+
           |            |
     Authentification   Résolution DNS
           |            |
       +--------------------+
       | WIN11-CLIENT       |
       | Windows 11         |
       | Membre du domaine* |
       +--------------------+
```

\* Le dépôt indique que le client a été joint au domaine. Ajoute une capture de vérification pour en fournir la preuve visuelle.

## Réalisations documentées

### 1. Domaine et contrôleur de domaine

- Domaine : `lab-cyber.local`
- Contrôleur de domaine : `SRV25.lab-cyber.local`
- Rôles documentés : AD DS, DNS et catalogue global.

Commandes de vérification utilisées :

```powershell
Get-ADDomain
Get-ADDomainController
Get-Service DNS
```

Ces commandes permettent respectivement d'inspecter les informations du domaine, les contrôleurs de domaine et l'état du service DNS. Elles servent de vérifications techniques ; leur présence dans la documentation ne remplace pas une capture de résultat.

### 2. DNS Active Directory

Le serveur utilise le DNS du laboratoire. Les vérifications documentées portent sur la résolution du serveur, du domaine et des enregistrements SRV LDAP :

```powershell
nslookup SRV25.lab-cyber.local 192.168.100.10
nslookup lab-cyber.local
nslookup -type=SRV _ldap._tcp.dc._msdcs.lab-cyber.local
dcdiag /test:dns
```

**Point de vigilance :** la documentation du lab signale des avertissements liés à une configuration multi-interface réseau. Ils doivent être analysés et documentés avant de présenter le DNS comme entièrement validé dans toutes les conditions.

### 3. Unités d'organisation, utilisateurs et groupes

Les OU documentées sont :

- `Admins`
- `Utilisateurs`
- `Postes`
- `Serveurs`
- `Groupes`

Le lab comprend notamment un utilisateur standard (`jdupont`) et un compte d'administration (`admin-cyber`). Le dépôt indique que ce dernier appartient à un groupe privilégié et que `jdupont` a été ajouté à `GG-Utilisateurs`.

Commande de contrôle de l'appartenance aux groupes :

```powershell
Get-ADUser "admin-cyber" -Properties MemberOf |
    Select-Object -ExpandProperty MemberOf
```

**Bonne pratique à expliquer :** limiter l'utilisation des comptes privilégiés aux tâches d'administration et éviter d'utiliser un compte Domain Admin pour les activités quotidiennes. Le compte `admin-cyber` est décrit ici selon la configuration documentée du laboratoire, pas comme une recommandation de conception en production.

## Sécurité et suites du projet

Le dépôt global documente également des travaux liés aux GPO, à l'audit Windows, à la journalisation PowerShell, à Sysmon et à la collecte d'événements WEF/WEC. La centralisation complète entre le client et le collecteur reste indiquée comme une étape à terminer.

Pour garder un état fiable, distingue dans tes prochaines mises à jour :
- **Configuré** : la configuration a été appliquée.
- **Testé** : un contrôle a été exécuté.
- **Validé** : le résultat attendu a été observé et une preuve est conservée.
- **À faire** : la vérification ou l'implémentation n'est pas terminée.

## Captures à ajouter

Ajoute uniquement des captures réellement prises dans ton lab, en masquant toute information personnelle ou sensible :

1. Vue d'ensemble du Gestionnaire de serveur montrant AD DS et DNS.
2. Console Utilisateurs et ordinateurs Active Directory avec les OU.
3. Propriétés du domaine ou résultat de `Get-ADDomain`.
4. Résultat de la requête DNS SRV.
5. Vérification que le poste client est membre du domaine.
6. Si disponible, résultat d'une stratégie de groupe appliquée au client.

Tu peux placer les images dans un dossier `screenshots/` sous `02-active-directory/`, puis les intégrer ici avec des chemins relatifs.

## Documentation détaillée

- [Configuration du domaine](domain.md)
- [Configuration DNS](dns.md)
- [Utilisateurs, groupes et OU](users-groups.md)

## Compétences mises en pratique

- Administration Windows Server
- Notions de domaine Active Directory et contrôleur de domaine
- DNS et résolution des enregistrements nécessaires à AD
- Gestion des utilisateurs, groupes et OU
- Vérification de configuration avec PowerShell
- Documentation technique et suivi des points restant à valider

---

**Périmètre :** laboratoire pédagogique isolé. Les paramètres et résultats présentés correspondent à la documentation du lab ; ils ne constituent pas une certification de sécurité ni une recommandation de déploiement en production.
