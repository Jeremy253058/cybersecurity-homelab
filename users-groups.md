# Organisation Active Directory

## OU créées

```text
lab-cyber.local
├── Admins
├── Utilisateurs
├── Postes
├── Serveurs
└── Groupes
```

Les conteneurs Active Directory par défaut ont été conservés.

## Utilisateurs

### Jean Dupont

- Compte : `jdupont`
- OU : `Utilisateurs`
- Utilisateur standard

### Admin Cyber

- Compte : `admin-cyber`
- OU : `Admins`
- Membre du groupe privilégié `Admins du domaine`

## Groupe

```text
GG-Utilisateurs
```

Jean Dupont a été ajouté à ce groupe.

## Vérification

```powershell
Get-ADUser "admin-cyber" -Properties MemberOf |
    Select-Object -ExpandProperty MemberOf
```
