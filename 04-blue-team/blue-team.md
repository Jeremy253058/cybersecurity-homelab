# Exercices Blue Team

## 1. Analyse d'un processus avec Sysmon
Event ID 1 utilisé pour analyser une création de processus.

Questions :
- Quel processus a été créé ?
- Qui l'a lancé ?
- Avec quels privilèges ?
- Quel est son chemin ?
- Quel est son contexte ?

Exemple : `WmiPrvSE.exe` lancé par `svchost.exe`.

## 2. Modification d'un groupe AD
Simulation contrôlée :
```
Administrateur → Test Attacker → GG-Utilisateurs
```

Événement : **4728**.

L'analyse a permis d'identifier l'acteur, le compte ajouté, le groupe et le domaine.

Point important : la présence du domaine ne suffit pas à déterminer qu'une activité est légitime. Il faut vérifier si la modification était attendue.

## 3. Verrouillage de compte
Simulation contrôlée : plusieurs authentifications avec un mauvais mot de passe jusqu'au seuil de verrouillage.

Événement : **4740**.

Résultat :
- compte : `test-attacker`
- machine appelante : `WIN11-CLIENT`
- serveur : `SRV25`
- heure : 19/09/2026 22:36:34

## 4. Corrélation
- 15/09/2026 23:54:25 — Event 4728 ;
- 19/09/2026 22:36:34 — Event 4740.

Conclusion : le 15 septembre, `Test Attacker` a été ajouté à `GG-Utilisateurs` par `Administrateur`. Quatre jours plus tard, le compte a été verrouillé depuis `WIN11-CLIENT`.

La chronologie seule ne permet pas d'affirmer que les deux événements sont directement liés.
