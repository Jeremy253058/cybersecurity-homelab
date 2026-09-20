# Prochaines étapes

## Blue Team / centralisation

1. Configurer `WIN11-CLIENT` comme source Windows Event Forwarding (WEF)
2. Créer une souscription WEF sur `SRV25`
3. Vérifier la réception des événements sur SRV25
4. Centraliser les journaux Security
5. Centraliser les événements Sysmon
6. Créer des règles/scénarios de détection
7. Réaliser un scénario complet de réponse à incident
8. Documenter les investigations dans GitHub

## Red / Purple Team

9. Ajouter Kali Linux lorsque les ressources le permettront
10. Réaliser des tests AD contrôlés
11. Construire des scénarios attaque/défense
12. Mapper les techniques observées avec MITRE ATT&CK
13. Corréler les événements d'attaque avec les logs Windows/Sysmon

## Note sur le SIEM

Une tentative d'installation de Wazuh All-in-One a été réalisée. Elle n'a pas abouti dans l'environnement matériel actuel et la VM a été supprimée. Le projet utilise donc pour le moment WEF/WEC et les outils natifs Windows afin de poursuivre le travail de centralisation et de détection sans alourdir l'infrastructure.
