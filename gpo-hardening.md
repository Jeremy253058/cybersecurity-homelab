# GPO et durcissement Windows

## Objectif
Mettre en place des contrôles de sécurité sur les postes Windows du domaine `lab-cyber.local`.

## Contrôles configurés
- verrouillage de compte après plusieurs échecs ;
- durée de verrouillage : 15 minutes ;
- fenêtre d'observation : 15 minutes ;
- journalisation PowerShell ;
- transcription PowerShell ;
- journalisation des modules PowerShell.

## Politique de mots de passe
- longueur minimale : 12 caractères ;
- complexité : activée ;
- historique : 24 mots de passe ;
- âge maximal : 90 jours ;
- âge minimal : 1 jour ;
- chiffrement réversible : désactivé.

## Pare-feu
Une règle ICMP personnalisée a été testée, mais son application par GPO n'a pas été confirmée. Elle n'est donc pas considérée comme une configuration validée du lab.
