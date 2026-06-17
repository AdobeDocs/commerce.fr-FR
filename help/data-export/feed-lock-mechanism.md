---
title: Mécanisme de verrouillage de flux pour l'exportation de données SaaS
description: Découvrez comment utilise  [!DNL SaaS Data Export]  verrous de flux pour éviter les opérations de synchronisation en conflit et protéger l’intégrité des données lors de mises à jour simultanées des flux.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 355
ht-degree: 0%

---


# Mécanisme de verrouillage de flux pour exportation de données SaaS

L’extension [!DNL SaaS Data Export] utilise un mécanisme de verrouillage des flux pour empêcher les conditions de concurrence lorsque plusieurs processus tentent de synchroniser le même flux simultanément. Cela peut se produire, par exemple, lorsqu’une resynchronisation déclenchée par cron chevauche un appel d’interface de ligne de commande `saas:resync` manuel.

## Fonctionnement du verrouillage de flux

Chaque opération de synchronisation de flux, qu’elle soit déclenchée par une tâche cron ou un appel d’interface de ligne de commande `saas:resync` manuel, suit la même séquence :

1. Le processus tente d&#39;acquérir le verrou d&#39;alimentation. La tentative de verrouillage est non bloquante et renvoie immédiatement si le verrouillage est déjà conservé par un autre processus.
1. Si le verrou n’est **pas disponible**, l’opération est ignorée et consignée.

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
>Pour obtenir des informations générales sur le format des journaux et les types d’opérations enregistrés dans `commerce-data-export.log`, voir [Vérification des journaux et dépannage](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Synchroniser les données avec l’exportation de données SaaS](sync-overview.md)
> - [Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce](data-export-cli-commands.md)
> - [Pipeline de synchronisation du connecteur](../aco-connector/connector-sync-pipeline.md)
> - [Configurer le fournisseur de verrouillage](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/lock-provider){target="_blank"}
