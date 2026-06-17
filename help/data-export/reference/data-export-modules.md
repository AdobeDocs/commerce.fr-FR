---
title: Modules d'export de données SaaS
description: Découvrez les packages de modules Magento inclus dans et  [!DNL SaaS Data Export]  leurs rôles dans la collecte de données, la transformation et l’envoi aux services SaaS d’Adobe.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 0%

---


# Modules d&#39;export de données SaaS

[!DNL SaaS Data Export] se compose de deux groupes de modules : le premier pour la collecte et l’indexation des données, et le second pour le transport et l’envoi HTTP.

Ces modules gèrent la détection des modifications d’entités, l’indexation des flux, l’extraction de données et la définition de schémas.
Le tableau suivant fournit uniquement des modules au niveau de la structure ; la liste complète des modules disponibles dépend des packages installés.

| Module | Objectif | Classes de clés |
| --- | --- |--- |
| `DataExporter` | Structure de base : indexeur, table de flux, hachage, reprise, verrouillage | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | DSL de requête XML pour la collecte de données | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | Transport HTTP partagé, reprise, interface de ligne de commande (`saas:resync`), orchestration de resynchronisation | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

Pour découvrir comment ces modules fonctionnent ensemble pendant la synchronisation, consultez [Pipeline d’exportation de données SaaS](../sync-overview.md).

>[!MORELIKETHIS]
>
>- [Fonctionnement de la synchronisation](../sync-overview.md)
>- [Schéma de la table des flux](feed-table-reference.md)
>- [Gérer l&#39;extension d&#39;export de données SaaS](../manage-extension.md)
