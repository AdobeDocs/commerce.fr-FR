---
title: Storefronts
description: Découvrez les options du storefront Adobe Commerce, notamment le storefront Commerce optimisé par Edge Delivery Services et les implémentations découplées personnalisées.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%
---

# Storefronts

Le storefront est distinct du serveur principal Commerce et des couches d’API. Selon l’architecture sélectionnée, un storefront peut récupérer des données à partir des API Commerce Foundation, des API Storefront Services, des API [!DNL Adobe Commerce Optimizer] Merchandising Services ou de systèmes connectés via le maillage API, App Builder ou d’autres mécanismes d’intégration. Consultez [Options d’architecture](../architecture-options/overview.md) pour savoir comment chaque storefront se couple à un serveur principal Commerce.

## Commerce Storefront optimisé par Edge Delivery Services

Le storefront Commerce optimisé par [!DNL Edge Delivery Services] est une option de storefront destinée aux clients qui repose sur la norme Adobe Commerce, utilisant des composants de dépôt et des blocs de contenu. Il est compatible avec tous les [présentation de l’architecture](../architecture-options/overview.md), la connexion à Commerce Foundation, les services Storefront ou les services de marchandisage [!DNL Adobe Commerce Optimizer], selon le serveur principal. Consultez la [présentation du storefront ](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

## Services Storefront

[!DNL Storefront Services] sont des services orientés magasin utilisés avec [!DNL Adobe Commerce]. Les API de service offrent un accès optimisé aux fonctionnalités telles que :

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

Les deux [!DNL Adobe Commerce] sur le cloud ou sur site (lorsqu’ils sont configurés) et [!DNL Adobe Commerce as a Cloud Service] utiliser les services Storefront. Ils ne sont pas exclusifs à [!DNL Adobe Commerce as a Cloud Service] et ne doivent pas être utilisés comme libellé distinctif entre les deux options de plateforme [!DNL Adobe Commerce]. Reportez-vous au schéma [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## Storefronts découplés personnalisés

Au-delà de la vitrine Commerce optimisée par [!DNL Edge Delivery Services], les options de vitrine incluent la [!DNL Luma], la [!DNL PWA Studio] ou une vitrine découplée personnalisée, en fonction de la prise en charge de la plateforme et des exigences d’implémentation. Un storefront découplé personnalisé se connecte aux mêmes familles d’API que toute autre option de storefront (Commerce Foundation, Storefront Services ou Commerce Optimizer Merchandising Services), en fonction de l’option [architecture](../architecture-options/overview.md) sélectionnée.

## Intégration du panier et du passage en caisse

L’emplacement où les transactions de panier et de passage en caisse sont gérées dépend du serveur principal de Commerce, et non de la technologie storefront :

- Lorsqu’[!DNL Adobe Commerce] Commerce Foundation est le serveur principal, le storefront utilise les API Commerce Foundation pour les opérations de panier, de passage en caisse, de client et de commande, ainsi que pour les intégrations de paiement, de taxe, d’expédition et d’exécution configurées.
- Lorsqu’une plateforme commerciale tierce constitue le serveur principal (comme avec les [!DNL Adobe Commerce Optimizer] autonomes), le storefront se connecte au panier, au passage en caisse, au client, à la commande, au paiement, aux taxes, à l’expédition et aux services de réalisation de cette plateforme via un maillage API, App Builder ou une intégration directe.

## Conseils connexes

- [Aperçu de l’architecture](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
