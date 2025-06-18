---
title: Gestion des ressources
description: Utilisez les Visuels de produit avec AEM Assets pour gérer les ressources multimédias de votre storefront.
feature: CMS, Media
source-git-commit: 0e7bdfab3efff7f994c63215f4ac31ed00562628
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---


# Gestion des ressources multimédias Commerce à l’aide de visuels de produit

<!--In ACAP-844, this topic was linked to from the Commerce Admin products images and videos when the Assets integration is enabled. If the URL to the topic changes, be sure to add a redirect.-->

Vous pouvez gérer les types de médias suivants à l’aide des Visuels de produit optimisés par AEM Assets :

* Images du produit
* Images de contenu
* Vidéos sur les produits
* Images de catégorie

## Images du produit

Lorsque l’intégration des visuels de produit est activée, la gestion des images est centralisée au sein du système de gestion des ressources numériques (DAM). Adobe Commerce fonctionne ensuite comme un canal d’engagement essentiel, en s’assurant que seules des images de haute qualité approuvées sont utilisées sur les storefronts. Cette configuration améliore la cohérence de la marque, réduit les efforts manuels et rationalise les mises à jour de contenu, éliminant ainsi la nécessité pour les commerçants de charger ou de gérer manuellement des images dans Adobe Commerce.

### Affichage des images des produits dans Adobe Commerce

Les images des produits sont automatiquement extraites d’AEM Assets en fonction de règles de correspondance préconfigurées :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Sélectionnez un produit.

1. Ouvrez la section **Images et vidéos**.

   ![ Image du produit ](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > Un message indique que l’intégration est activée, ce qui en fait une section **lecture seule** car la gestion des images est centralisée dans la gestion des ressources numériques (DAM).

### Gestion des images de produits dans AEM Assets

Pour gérer les images liées au produit, toutes les modifications doivent être apportées directement dans **AEM Assets**. Ce processus est entièrement automatisé, ce qui garantit que toutes les modifications sont synchronisées avec Adobe Commerce sans nécessiter d’intervention manuelle.

### Contrats SLA de synchronisation

Consultez [SLA de synchronisation](get-started/setup-synchronization.md#synchronization-sla) pour plus d’informations sur cette rubrique.

## Images de contenu

Adobe Commerce fournit Page Builder en tant que **système de gestion de contenu (CMS)** pour les commerçants qui n’utilisent pas l’ensemble d’outils Adobe Experience Manager (AEM). Pour améliorer la création de contenu, notre intégration utilise le [sélecteur de ressources AEM](synchronize/asset-selector-integration.md), ce qui permet aux marketeurs d’accéder et d’incorporer facilement des images directement à partir du **DAM**. Cela permet de s’assurer que seules des images approuvées et de haute qualité sont utilisées dans la création de contenu, éliminant ainsi le besoin de stockage redondant dans Adobe Commerce.

### Utilisation du sélecteur de ressources AEM dans Page Builder

Pour utiliser le sélecteur de ressources **AEM** pour incorporer des images :

1. Accédez à n’importe quelle section de l’**administration Adobe Commerce** qui prend en charge les `content enrichment` à l’aide de **Page Builder**.

1. Ouvrez [Page Builder](https://developer.adobe.com/commerce/frontend-core/page-builder/){target=_blank}.

   Un nouveau type de média appelé **Ressource AEM** sera disponible.

1. Effectuez un glisser-déposer du type de média Ressource AEM dans un bloc de contenu.

1. Lorsque vous y êtes invité, indiquez les informations d’identification pour accéder à la gestion des ressources numériques.

1. Sélectionnez une image dans la gestion des ressources numériques et insérez-la directement dans le contenu.

L’association à l’image sélectionnée sera stockée dans Adobe Commerce en tant qu’URL directe pointant vers **Dynamic Media**, en veillant à ce que :

* Les fichiers image n’ont pas besoin d’être stockés dans Adobe Commerce.

* Les spécialistes marketing travaillent exclusivement avec des ressources approuvées de la gestion des ressources numériques.

* Le contenu reste cohérent et à jour sur tous les points de contact des clients.

## Vidéos sur les produits

Adobe Commerce sert de canal d’engagement essentiel pour les ressources numériques. Une fois la visualisation du produit activée, la gestion vidéo est centralisée dans la **gestion des ressources numériques**, ce qui garantit la cohérence, la conformité et une diffusion optimisée sur les storefronts de commerce.

### Gestion des vidéos de produit

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Sélectionnez un produit.

1. Ouvrez la section **Images et vidéos**.

   ![ Image du produit ](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > Un message indique que l’intégration est activée, ce qui rend cette section **en lecture seule**, car les vidéos sont contrôlées dans AEM Assets.

### Associer des vidéos dans AEM Assets

1. Dans AEM Assets, accédez à la vidéo que vous souhaitez associer à un produit.

1. Liez la vidéo à un ou plusieurs produits dans Adobe Commerce.

1. L’intégration synchronise automatiquement l’association, affichant le lecteur vidéo Dynamic Media directement sur le storefront. Les commerçants n’ont ainsi plus à gérer les configurations de lecture vidéo.

### Prise en charge vidéo API-First uniquement

Actuellement, l’intégration prend en charge les vidéos via l’API, ce qui permet aux partenaires de récupérer les vidéos par programmation.

>[!WARNING]
>
> Les vidéos ne sont pas encore intégrées par défaut aux solutions de storefront Adobe Commerce existantes.

Cette intégration permet aux commerçants de gérer facilement les vidéos de produits de manière évolutive et optimisée, en exploitant AEM Assets et Dynamic Media pour une diffusion transparente.

### Contrats SLA de synchronisation

Consultez [SLA de synchronisation](get-started/setup-synchronization.md#synchronization-sla) pour plus d’informations sur cette rubrique.

## Images de catégorie

Adobe Commerce permet aux commerçants d’associer des images à des catégories de produits, contribuant ainsi à créer un storefront visuellement attrayant. L’intégration tire parti du sélecteur de ressources AEM, ce qui permet aux marketeurs de sélectionner facilement des visuels de produit directement depuis le **système de gestion des ressources numériques (DAM)**. Cela permet de s’assurer que seules les images approuvées sont utilisées et élimine la nécessité de les stocker dans Adobe Commerce, en maintenant la cohérence et l’efficacité sur tous les canaux d’engagement.

### Utilisation du sélecteur de ressources AEM pour les images de catégorie

Après avoir configuré le sélecteur de ressources [AEM](synchronize/asset-selector-integration.md), vous pouvez l’utiliser pour ajouter des ressources dans le contenu des catégories de votre catalogue.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Catalog]** > **[!UICONTROL Categories]**.

1. Sélectionnez une catégorie à mettre à jour.

1. Développez le ![sélecteur d’extension](../assets/icon-display-expand.png) dans la section **[!UICONTROL Content]**.

1. Dans la section **[!UICONTROL Content]**, recherchez le champ *Image* associé à la catégorie.

   ![Contenu de la catégorie](assets/category-asset.png){width="600" zoomable="yes"}

1. Cliquez sur **[!UICONTROL Select from Assets]** pour modifier l’image de la catégorie.

   ![Contenu de la catégorie](assets/asset-view.png){width="600" zoomable="yes"}

1. Sélectionnez une image dans le sélecteur de ressources AEM.

   ![Contenu de la catégorie](assets/select-image.png){width="600" zoomable="yes"}

1. Cliquez sur **[!UICONTROL Save]** et continuez.

   Pour plus d’informations sur la création d’une catégorie, voir [Compléter le contenu de la catégorie](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/create/category-create#step-3-complete-the-category-content) dans le **Guide de gestion des catalogues Commerce**.

## Mise à jour d’une ressource

Une fois que vous avez mis à jour et approuvé une ressource dans AEM Assets, les mises à jour sont automatiquement envoyées à Adobe Commerce à l’aide de la fonctionnalité de correspondance automatisée des Visuels de produit . Ce processus est déclenché lors de l’approbation des ressources. Pour vous assurer que toutes les modifications finales et les mises à jour des métadonnées sont incluses, veillez à retraiter la ressource avant de l’approuver.

Pour plus d’informations, consultez la documentation d’AEM Assets ci-après.

* [ Retraitement des ressources numériques ](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/manage/reprocessing)

* [Approuver une ressource](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/approve-assets)
