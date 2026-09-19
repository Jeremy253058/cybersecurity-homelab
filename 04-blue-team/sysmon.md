# Sysmon

## Installation
Sysmon v15.22 a été installé sur `WIN11-CLIENT`.

Chemin :
```
C:\Sysmon\Sysmon64.exe
```

Service :
```
Sysmon64
```

## Configuration
La configuration XML utilisée couvre :
- ProcessCreate
- NetworkConnect
- ImageLoad
- FileCreate
- RegistryEvent

Hash : SHA256.

## Event ID 1 — Process Create
Méthode d'analyse :
- chemin du processus ;
- éditeur ;
- utilisateur ;
- niveau d'intégrité ;
- processus parent ;
- ligne de commande ;
- contexte.

Exemple observé :
```
Image: C:\Windows\System32\wbem\WmiPrvSE.exe
ParentImage: C:\Windows\System32\svchost.exe
User: AUTORITE NT\SERVICE LOCAL
IntegrityLevel: System
```

Réflexe utilisé :
**Processus → Parent → Utilisateur → Privilèges → Chemin → Contexte**

Un test spécifique de recherche de `cmd.exe` n'a pas produit le résultat filtré attendu ; d'autres Event ID 1 étaient bien présents.
