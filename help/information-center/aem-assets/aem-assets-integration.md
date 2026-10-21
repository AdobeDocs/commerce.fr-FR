---
title: Intégration d’AEM Assets pour Commerce
description: Découvrez comment intégrer AEM Assets à Adobe Commerce, Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer afin de gérer les images et les médias de produit de manière centralisée.
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%
---

# Intégration d’AEM Assets pour Commerce

L’intégration d’AEM Assets active les fonctionnalités de visualisation des produits dans Adobe Commerce afin que vous puissiez gérer les images, les vidéos et d’autres médias des produits de manière centralisée dans AEM Assets. Il s’agit d’un module complémentaire facultatif qui fonctionne avec n’importe quelle option d’architecture Commerce, et non avec une plateforme Commerce distincte.

## Chemins d’intégration par architecture

Il existe deux chemins d’intégration. Le chemin d’accès dépend de votre architecture Commerce.

| Architecture de Commerce | Chemin d’intégration d’AEM Assets | En savoir plus |
| --- | --- | --- |
| [!DNL Adobe Commerce] sur le cloud ou sur site | Intégration [!DNL AEM Assets] pour Commerce. Utilise le package d’intégration Commerce pour synchroniser et gérer les images du produit, les vidéos et d’autres médias entre [!DNL Adobe Commerce] et [!DNL AEM Assets]. | [Intégration AEM Assets pour Commerce](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | [!DNL Product Visuals] optimisé par [!DNL AEM Assets] | [configuration de l’intégration &#x200B;](/help/aem-assets-integration/overview.md#next-steps) |
| [!DNL Adobe Commerce Optimizer] autonome | [!DNL Product Visuals] optimisé par [!DNL AEM Assets]. Les données de catalogue et de prix de base arrivent via l’API [Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/). | [Visuels de produit avec AEM Assets](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce] avec le [!DNL Adobe Commerce Optimizer Connector] | [!DNL Product Visuals] optimisé par [!DNL AEM Assets]. Les données de catalogue et de prix sont synchronisées à partir de [!DNL Adobe Commerce] par le connecteur. | [Intégrations &#x200B;](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals] est le chemin d’intégration d’Adobe Commerce as a Cloud Service et de Adobe Commerce Optimizer. Il synchronise les images de produit gérées par AEM avec la couche Catalogue Commerce et les diffuse dans les expériences storefront via les API storefront.

## Avant de choisir

- Les exigences de configuration et de licence diffèrent entre le chemin d’accès Commerce sur le cloud ou sur site et le chemin d’accès Commerce as a Cloud Service ou Adobe Optimizer [!DNL Product Visuals]. Examinez d’abord les exigences spécifiques au déploiement.
- [!DNL AEM Assets] gère les ressources numériques. Il ne remplace pas le système de catalogue, de tarification, de panier, de passage en caisse ou de commande de Commerce.
- Les ressources de produit sont mises en correspondance avec les produits Commerce à l’aide du SKU ou d’autres métadonnées correspondantes documentées.
- Si les équipes de marketing et de merchandising ont besoin de workflows centralisés pour les ressources et les images de produit, choisissez le chemin qui correspond à votre architecture Commerce.

## Informations connexes

- [Documentation Adobe Experience Manager Assets](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/assets/overview)
- [Aperçu de l’architecture](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
