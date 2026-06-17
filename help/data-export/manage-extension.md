---
title: '[!DNL Manage the Data Export extension]'
description: Découvrez comment mettre à niveau l’extension et supprimer ou désactiver  [!DNL Data Export]  services d’exportation de données qui ne sont pas requis.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
TQID: https://experienceleague.adobe.com/ghrA-YFR7hurQgEnjS8PdxR7Zcx-ayLTuyBfhbCC-KI
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: d3cdead0-685a-4489-9250-4bb709942f66
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# Gérer l&#39;extension d&#39;export de données SaaS

L’extension [[!DNL data export] extension](https://github.com/magento/commerce-data-export) pour les services SaaS est un ensemble de modules qui permettent la collecte de données et la synchronisation entre Adobe Commerce et les services Commerce connectés.

Des modules spécifiques sont inclus dans les métapaquets pour les extensions Adobe Commerce Services, tels que
comme [Live Search](/help/live-search/overview.md), [Product Recommendations](/help/product-recommendations/overview.md), [Catalog Service](/help/catalog-service/overview.md) et le [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md). Si vous utilisez ces services, aucune installation distincte n’est nécessaire pour activer l’extension Data Export.

## Suppression ou désactivation des fonctionnalités d’exportation des données de Commerce

Si vous n’avez pas besoin de l’un des modules d’exportation de données de commerce installés, utilisez la commande de l’interface de ligne de commande `magento:module:disable` pour le désactiver.

Par exemple, il existe une [API Categories](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) qui utilise en interne les données de flux des autorisations relatives aux catégories. Si vous n’utilisez pas cette API, vous pouvez désactiver l’exportation des données pour le flux d’autorisations des catégories.

```shell
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Mise à jour d’un module vers une version spécifique

Vous pouvez mettre à jour n’importe quel module d’exportation de données Commerce installé à l’aide du compositeur. Consultez les [notes de mise à jour](release-notes.md) pour déterminer si un correctif dont vous avez besoin est disponible, puis effectuez une mise à niveau vers cette version spécifique et toutes les dépendances requises.

>[!NOTE]
>
>Si vous effectuez une mise à jour vers la dernière version de [Live Search](/help/live-search/overview.md), [Catalog Service](/help/catalog-service/overview.md), [Product Recommendations](/help/product-recommendations/overview.md) ou la [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md), vous obtenez également la dernière version de l’extension d’exportation des données. Le métapaquet d’exportation de données est une dépendance des packages du compositeur pour ces services.

1. Connectez-vous au serveur d’applications Commerce.

1. Sur la ligne de commande, mettez à jour le module à l’aide du compositeur :

   ```bash
   composer require magento/module-data-exporter:103.0.4 --with-all-dependencies
   ```

Si l’instance Commerce est déployée sur une infrastructure cloud, mettez à jour l’extension à partir du répertoire de votre projet cloud. Voir [Mettre à niveau une extension](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) dans le _Guide d’Adobe Commerce sur les infrastructures cloud_.

>[!MORELIKETHIS]
>
> - [Notes de mise à jour](release-notes.md)
> - [Modules d’export de données SaaS](reference/data-export-modules.md)
> - [Présentation du guide](overview.md)
