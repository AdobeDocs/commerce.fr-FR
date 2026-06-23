---
title: Affichage et gestion du processus de synchronisation
description: Découvrez comment afficher et gérer le processus  [!DNL SaaS Data Export]  synchronisation à l’aide du tableau de bord de gestion des données et de la page Statut de la synchronisation des flux de données.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
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
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 98d604a71c2062a44070b207fc43b9d9b1c434fd
workflow-type: tm+mt
source-wordcount: 557
ht-degree: 0%

---

# Afficher et gérer le processus de synchronisation

La plupart des activités de synchronisation sont traitées automatiquement à l’aide d’une synchronisation complète, partielle ou par une nouvelle synchronisation des éléments ayant échoué. Voir [Types de synchronisation](sync-overview.md#synchronization-types) pour savoir quand chaque type s’exécute. [!DNL SaaS Data Export] fournit également des outils de surveillance, de gestion et de dépannage du processus. Vous pouvez afficher l’état de synchronisation et gérer le processus de synchronisation des données à l’aide des tableaux de bord de votre déploiement .

>[!BEGINTABS]

>[!TAB Tab]

Pour les déploiements d’Adobe Commerce on cloud, on-premise ou Adobe Commerce as a Cloud Service, affichez et gérez le processus de synchronisation à partir de ces ressources d’administration Commerce :

- **[Page Statut de synchronisation des flux de données](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** : vérifiez le statut d’exportation des flux pour les déploiements connectés à [!DNL Live Search], [!DNL Product Recommendations] ou [!DNL Catalog Service]. Ce tableau de bord affiche le statut d’exportation de chaque flux, y compris les erreurs rencontrées. Une vue détaillée affiche le statut d’exportation des flux pour chaque élément de flux.

- **[Tableau de bord de gestion des données](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)** : les utilisateurs administrateurs peuvent afficher et suivre les données exportées et synchronisées avec succès vers les services Commerce connectés. Ce tableau de bord affiche les données de produit synchronisées avec les services Commerce.

>[!NOTE]
>
>Le tableau de bord de gestion des données et la page État de la synchronisation des flux de données ne sont disponibles que si vous avez installé [!DNL Live Search], [!DNL Product Recommendations] ou [!DNL Catalog Service].

>[!TAB Adobe Commerce avec Commerce Optimizer]

Pour les déploiements sur le cloud ou on-premise de Commerce intégrés avec [!DNL Commerce Optimizer], visualisez et gérez le processus de synchronisation à l’aide des ressources suivantes :

- **[Page Statut de la synchronisation des flux de données](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status)** : surveiller le statut d’exportation des flux du connecteur depuis Commerce Admin. Cette page indique si les données de catalogue ont bien été exportées à partir de [!DNL Adobe Commerce], y compris les détails d’erreur par flux et par élément.

- **[Page de synchronisation des données](../optimizer/setup/data-sync.md)** : la page de synchronisation des données donne un aperçu de l&#39;état de synchronisation des données de produit provenant de votre source de catalogue en amont dans [!DNL Commerce Optimizer].

Pour plus d’informations sur l’utilisation de ces tableaux de bord pour vérifier que la synchronisation des données fonctionne et pour resynchroniser manuellement les données, voir [Gérer la synchronisation](../aco-connector/data-sync-manage.md) dans le guide du connecteur Adobe Commerce Optimizer __.

>[!ENDTABS]

## Vérifier que la synchronisation des données fonctionne {#verify-that-the-data-sync-is-working}


{{$include /help/_includes/data-export/verify-commerce-service-data-sync.md}}

## resynchroniser manuellement les données

Lorsque la synchronisation partielle et la reprise automatique ne résolvent pas les problèmes de synchronisation, vous pouvez resynchroniser manuellement les données à partir de l’Administration Commerce ou à l’aide des commandes de l’interface de ligne de commande Commerce. Les options disponibles dépendent de votre déploiement .

### Options de resynchronisation manuelle disponibles {#manual-resync-options-commerce}

Utilisez les options suivantes pour resynchroniser manuellement les données de flux.

| Tâche | Option | Remarques |
| --- | --- | --- |
| Resynchroniser les éléments de flux sélectionnés ayant échoué ou posant problème | **[!UICONTROL Data Feed Sync Status]page** | Surveillez et resynchronisez les éléments de flux sélectionnés depuis l’administration Commerce. Voir [Vérifier que la synchronisation des données fonctionne](#verify-that-the-data-sync-is-working). |
| Resynchronisation complète de tous les flux | **[!UICONTROL Data Management Dashboard]** | Effectuer une resynchronisation complète de tous les flux à partir de l’administrateur Commerce ; Adobe recommande cette opération principalement lorsque vous vous connectez pour la première fois à un service Commerce. Les éléments dont le hachage du contenu n’a pas changé depuis la dernière exportation sont ignorés. Voir [Vérifier que la synchronisation des données fonctionne](#verify-that-the-data-sync-is-working). |
| Resynchronisation ciblée de flux avec contrôle opérationnel | **Commerce CLI** | Utilisez la commande `saas:resync` pour les resynchronisations de flux ciblées. Voir [Synchronisation des flux à l’aide de l’interface de ligne de commande Commerce](data-export-cli-commands.md). |

>[!MORELIKETHIS]
>
> - [Fonctionnement de la synchronisation &#x200B;](sync-overview.md) — Découvrez les modes de synchronisation, la synchronisation complète, la synchronisation partielle et les éléments pour lesquels une nouvelle tentative a échoué.
> - [Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce](data-export-cli-commands.md) : utilisez la commande `saas:resync` pour les resynchronisations de flux ciblées.
> - [Consulter les journaux et résoudre les problèmes](troubleshooting/logging.md) — Diagnostiquer les erreurs d&#39;exportation de données et d&#39;exportation SaaS.
> - [Gérer la synchronisation sur  [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md) — Vérifier la synchronisation des données du catalogue et resynchroniser manuellement les flux du connecteur.
