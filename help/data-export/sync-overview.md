---
title: Synchroniser les données avec l'export de données SaaS
description: Découvrez comment le collecte et synchronise  [!DNL SaaS Data Export]  données entre les instances Adobe Commerce et les services Commerce connectés.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: d3cdead0-685a-4489-9250-4bb709942f66id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 879
ht-degree: 0%

---

# Synchroniser les données avec l&#39;export de données SaaS

Lorsque vous installez un service [!DNL Adobe Commerce] qui nécessite l’exportation de données, tel que Catalog Service, Live Search ou Product Recommendations, une collection de modules d’exportation de données SaaS est installée pour gérer le processus de collecte de données et de synchronisation.

L’exportation des données SaaS déplace régulièrement les données de produit d’une instance Adobe Commerce vers la plateforme Commerce Services afin de maintenir les données à jour. Par exemple, Recommandations de produits nécessite des informations de catalogue actuelles pour renvoyer avec précision des recommandations aux noms, prix et disponibilité corrects. Pour plus d&#39;informations sur la surveillance du processus de synchronisation, voir [Afficher et gérer le processus de synchronisation](data-sync-manage.md).

Le diagramme suivant illustre le flux d’exportation des données SaaS.

![Collecte de données d&#39;export SaaS et flux de synchronisation pour Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

Lorsque les données du catalogue changent dans [!DNL Adobe Commerce], la synchronisation passe par ces étapes.

1. **Détection des modifications d&#39;entité** - Le système Mview de Magento détecte les modifications de ligne dans les tables de base de données auxquelles vous êtes abonné (par exemple, `catalog_product_entity`) et écrit les entrées dans une table de journal des modifications.
1. **Indexation des flux** - L’indexeur des flux lit le journal des modifications, charge les données d’entité à partir des tables source et assemble les éléments de flux.
1. **Collecte et transformation des données** - Les fournisseurs enregistrés dans le schéma de flux [`et_schema.xml`](extensibility-and-customizations.md#feed-schema-overview) collecter des données de champ.
1. **Déduplication de hachage** - Un hachage de contenu est calculé pour chaque élément de flux. Les éléments dont le hachage n’a pas changé depuis la dernière exportation sont ignorés, de sorte que seules les données modifiées sont transmises.
1. **Envoi HTTP** - Les éléments de flux sont envoyés par lots HTTP POST authentifiés au service d’ingestion de flux SaaS d’Adobe.
1. **Statut persistant** - Le statut de la réponse de l’API est réécrit dans le [tableau de flux](reference/feed-table-reference.md) pour chaque élément.
1. **Reprise en échec** - Les éléments dont l’exportation a échoué sont automatiquement repris par une tâche cron planifiée.

>[!NOTE]
>
>Pour les déploiements [!DNL Adobe Commerce Optimizer Connector], [!DNL SaaS Data Export] gère la détection des modifications d’entité et l’assemblage d’alimentation. Le connecteur mappe ensuite les flux au format [!DNL Catalog Data Ingestion API] et les envoie vers [!DNL Adobe Commerce Optimizer]. Voir [Pipeline de synchronisation du connecteur](../aco-connector/connector-sync-pipeline.md) pour le contrôle de l’étendue, l’envoi et la gestion des erreurs.

>[!NOTE]
>
>Pour garantir une planification fluide et éviter toute perturbation du fonctionnement du site, Adobe recommande d’estimer le volume de données et l’heure de synchronisation avant de démarrer la synchronisation des flux de données. Cette estimation est importante lors de la planification de synchronisations initiales ou de mises à jour de catalogue à grande échelle, telles que des modifications de prix en masse. Pour plus d’informations, voir [ Estimation du volume de données et de la durée de transmission pour la synchronisation des données](estimate-data-volume-sync-time.md)

## Modes de synchronisation

L’exportation des données SaaS comporte deux modes de traitement des flux d’entités :

- **Mode d’exportation immédiat** : dans ce mode, les données sont collectées et envoyées immédiatement au service Commerce en une seule itération. Ce mode accélère la diffusion des mises à jour d’entités au service Commerce et réduit la taille de stockage des tables de flux.

- **Mode d’exportation hérité** : dans ce mode, les données sont collectées dans un seul processus. Ensuite, une tâche cron envoie les données collectées aux services commerciaux connectés. Dans les entrées du journal d’exportation de données, les flux qui utilisent le mode hérité sont étiquetés `(legacy)`.

## Types de synchronisation

L&#39;exportation de données SaaS prend en charge trois types de synchronisation : synchronisation complète, synchronisation partielle et synchronisation des éléments ayant échoué à une nouvelle tentative.

### Synchronisation complète

Après la connexion d’une instance Adobe Commerce au service Commerce, effectuez une synchronisation complète pour envoyer des données de flux d’entités d’Adobe Commerce au service connecté.

>[!NOTE]
>
>La synchronisation complète est principalement destinée à la phase d’intégration. Évitez de l’utiliser régulièrement pour éviter la surcharge de la base de données. Après la synchronisation initiale, les modifications en cours sont automatiquement synchronisées à l’aide d’une synchronisation partielle.

### Synchronisation partielle {#partial-sync}

Avec une synchronisation partielle, l’exportation de données SaaS envoie automatiquement des mises à jour depuis l’application Commerce, telles que des modifications de nom de produit ou de prix, aux services commerciaux connectés.
Pour que la synchronisation partielle fonctionne, l’application Commerce nécessite la configuration suivante :

- [La planification des tâches est activée via les tâches cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)
- Tous les indexeurs d&#39;export de données SaaS sont configurés en mode `Update by Schedule`.

### Réessayer la synchronisation des éléments ayant échoué {#retry-failed-items-sync}

La synchronisation des éléments en échec de la reprise utilise un processus distinct pour renvoyer les éléments qui n’ont pas pu être synchronisés en raison d’erreurs lors du processus de synchronisation, par exemple une erreur d’application, une interruption de réseau ou une erreur de service SaaS. Les tâches cron `*_resend_failed_items` du groupe `resync_failed_feeds_data_exporter` le gèrent automatiquement toutes les 5 minutes.

## Traitements cron planifiés

Les groupes cron suivants automatisent le pipeline selon un planning fixe.

| Groupe cron | Tâche cron | Objectif | Planning |
|---|---|---|---|
| `index` | `indexer_update_all_views` | Traite les logs de modification Mview et déclenche des mises à jour partielles des flux | Toutes les 1 minute |
| `index` | `indexer_reindex_all_invalid` | Effectue une resynchronisation complète pour les index de flux marqués comme « Réindexation requise » | Toutes les 1 minute |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | Détecte les éléments de flux ayant échoué et les soumet à nouveau. | Toutes les 5 minutes |
| `commerce_data_export` | `saas_data_exporter` | Envoie des données pour les flux en mode hérité (commandes, portées) | Toutes les 5 minutes |
| `commerce_data_export` | `cleanup_deleted_feed_items` | Nettoie les éléments de flux supprimés synchronisés après la période de conservation (7 jours) | Tous les jours à 2:00 h |

## Envoi de flux et gestion des erreurs HTTP {#feed-submission-and-http-error-handling}

Les éléments de flux sont envoyés en tant que lots JSON compressés GZIP authentifiés via HTTP POST. Le tableau suivant montre comment les codes de réponse HTTP sont associés au statut d’exportation et au comportement de reprise.

| Code de statut | Réessayer ? | Signification |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------|
| 200 | Non | Accepted successfully |
| 400 | Non | Données incorrectes ou échec de validation - nécessite une enquête manuelle. `var/log/saas-export-errors.log` pour plus de détails. |
| 429 | Oui | Accès à la limite de débit : réduisez les `thread_count` dans [paramètres de traitement des exportations](customize-export-processing.md). |
| 5xx | Oui | Erreur côté SaaS : reprise automatique |
| 2 | Oui | La reprise de l&#39;élément est planifiée |

Outre les échecs au niveau du HTTP, les erreurs au niveau de l’application, telles que les échecs de traitement local ou les perturbations du réseau, sont également planifiées pour une reprise automatique par les tâches cron `*_resend_failed_items`.

Surveillez le statut par flux à partir de la page [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) de l’administration Commerce.

>[!MORELIKETHIS]
>
> - [Gérer la synchronisation](data-sync-manage.md) — Vérifier le statut de synchronisation et resynchroniser manuellement les flux.
> - [Schéma de la table de flux](reference/feed-table-reference.md) — Examinez le statut au niveau de l’élément et les détails des erreurs.
> - [Améliorer les performances d’exportation des données](customize-export-processing.md) — Ajuster la taille du lot et le nombre de threads.
