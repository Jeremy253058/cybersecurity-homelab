# Audit Windows et Active Directory

## Objectif
Transformer les journaux Windows en sources de détection exploitables par la Blue Team.

## Audit vérifié
Les catégories suivantes ont été activées :
- Logon / Logoff ;
- Account Lockout ;
- Security Group Management ;
- User Account Management.

Vérification :
```powershell
auditpol /get /category:*
```

## Event ID 4728
Ajout d'un membre à un groupe global dont la sécurité est activée.

Scénario observé :
- acteur : `Administrateur`
- membre : `Test Attacker`
- groupe : `GG-Utilisateurs`
- domaine : `LAB-CYBER`

## Event ID 4740
Verrouillage d'un compte.

Scénario observé :
- compte : `test-attacker`
- ordinateur appelant : `WIN11-CLIENT`
- serveur : `SRV25`
- heure : 19/09/2026 22:36:34

## Méthode d'analyse
1. identifier l'action ;
2. identifier l'acteur ou le compte ;
3. identifier la machine ;
4. vérifier la chronologie ;
5. déterminer si l'activité était attendue ;
6. corréler avec d'autres événements avant de conclure.
