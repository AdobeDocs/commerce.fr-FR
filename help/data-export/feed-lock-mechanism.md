---
title: Mécanisme de verrouillage de flux pour l'exportation de données SaaS
description: Découvrez comment utilise  [!DNL SaaS Data Export]  verrous de flux pour éviter les opérations de synchronisation en conflit et protéger l’intégrité des données lors de mises à jour simultanées des flux.
role: Admin, Developer
feature: Services
source-git-commit: cfa1002653bf66afd3f6b8484b33076adcd1b7d4
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Mécanisme de verrouillage de flux pour exportation de données SaaS

L’extension [!DNL SaaS Data Export] utilise un mécanisme de verrouillage des flux pour empêcher les conditions de concurrence lorsque plusieurs processus tentent de synchroniser le même flux simultanément. Cela peut se produire, par exemple, lorsqu’une resynchronisation déclenchée par cron chevauche un appel d’interface de ligne de commande `saas:resync` manuel.

## Fonctionnement du verrouillage de flux

Chaque opération de synchronisation de flux, qu’elle soit déclenchée par une tâche cron ou un appel d’interface de ligne de commande `saas:resync` manuel, suit la même séquence :

1. Le processus tente d&#39;acquérir le verrou d&#39;alimentation. La tentative de verrouillage est non bloquante et renvoie immédiatement si le verrouillage est déjà conservé par un autre processus.
1. Si le verrou n’est **pas disponible**, l’opération [ est ignorée et consignée].

   Aucune donnée n’est perdue. La prochaine exécution cron détecte les modifications en attente une fois le processus en cours terminé.
1. Si le verrou est **acquis**, le processus enregistre son nom et son PID à des fins de diagnostic, puis exécute la synchronisation.
1. Une fois la synchronisation terminée ou ayant échoué, le verrouillage est désactivé sans condition afin que la tâche cron suivante planifiée puisse se poursuivre normalement.

Une seule opération de synchronisation peut contenir le verrouillage du flux à la fois, qu’il ait été démarré par cron ou l’interface de ligne de commande. Le verrouillage d’alimentation est implémenté via le `LockManagerInterface` de [!DNL Adobe Commerce]. Le serveur principal par défaut est MySQL, qui utilise les fonctions `GET_LOCK` et `RELEASE_LOCK`. Pour configurer un autre fournisseur de verrous, voir [Configurer le fournisseur de verrous](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}.

## Messages du journal attendus

Le message suivant dans `commerce-data-export.log` est normal et n’indique pas de problème :

```json
{"feed":"products","operation":"partial sync","status":"operation skipped - process locked by \"full sync(1234)\"", ...}
```

Ce message s’affiche lorsqu’une synchronisation partielle déclenchée par cron tente de s’exécuter alors qu’une réindexation complète ou une `saas:resync` est déjà en cours. L’opération ignorée n’est pas perdue. Une fois que le processus en cours d’exécution se termine et libère le verrouillage, l’exécution cron suivante reprend et synchronise toutes les modifications en attente.

>[!NOTE]
>
>Pour obtenir des informations générales sur le format des journaux et les types d’opérations enregistrés dans `commerce-data-export.log`, voir [Vérification des journaux et dépannage](troubleshooting-logging.md).

## Plus d’aide sur cette rubrique

- [Synchroniser les données avec l&#39;export de données SaaS](data-synchronization.md)
- [Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce](data-export-cli-commands.md)
- [Configuration du fournisseur de verrous](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
