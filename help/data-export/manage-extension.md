---
title: '[!DNL Manage the Data Export extension]'
description: Découvrez comment mettre à niveau l’extension et supprimer ou désactiver  [!DNL Data Export]  services d’exportation de données qui ne sont pas requis.
role: Admin, Developer
exl-id: 94702995-d272-47b9-9560-198eee3250a6
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Gérer l&#39;extension d&#39;export de données SaaS

L’extension [!DNL data export] pour les services SaaS est un ensemble de modules qui permettent la collecte de données et la synchronisation entre Adobe Commerce et les services Commerce connectés.

Des modules spécifiques sont inclus dans les métapaquets pour les extensions Adobe Commerce Services, tels que
comme [Live Search](/help/live-search/overview.md), [Product Recommendations](/help/product-recommendations/overview.md) et [Catalog Service](/help/catalog-service/overview.md). Si vous utilisez ces services, aucune installation distincte n’est nécessaire pour activer l’extension Data Export.

## Suppression ou désactivation des fonctionnalités d’exportation des données de Commerce

Si vous n’avez pas besoin de l’un des modules d’exportation de données de commerce installés, utilisez la commande de l’interface de ligne de commande `magento:module:disable` pour le désactiver.

Par exemple, il existe une [API Categories](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) qui utilise en interne les données de flux des autorisations relatives aux catégories. Si vous n’utilisez pas cette API, vous pouvez désactiver l’exportation des données pour le flux d’autorisations des catégories.

```shell script
bin/magento module:disable Magento_CategoryPermissionDataExporter Magento_SaaSCategoryPermissions
```

### Mise à jour d’un module vers une version spécifique

Vous pouvez mettre à jour n’importe quel module d’exportation de données Commerce installé à l’aide du compositeur. Par exemple, vous pouvez mettre à jour un module vers une version spécifiée et également mettre à jour les dépendances requises.

1. Connectez-vous au serveur d’applications Commerce.

1. Sur la ligne de commande, mettez à jour le module à l’aide du compositeur :

   ```bash
   composer require magento/module-saas-price:103.3.1 --with-all-dependencies
   ```

Si l’instance Commerce est déployée sur une infrastructure cloud, mettez à jour l’extension à partir du répertoire de votre projet cloud. Voir [Mettre à niveau une extension](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension) dans le _Guide d’Adobe Commerce sur les infrastructures cloud_.
