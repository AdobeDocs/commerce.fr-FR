---
title: Options d’architecture d’implémentation
description: Comparez les architectures Adobe Commerce, y compris Commerce Foundation, Adobe Commerce as a Cloud Service, le connecteur Optimizer et l’optimiseur autonome.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:39:51.406Z'
TQID: 'https://experienceleague.adobe.com/tYkxRAfJWOY7C0OEqYxEb4onwvnnL9wEofEG2e6qnKA'
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
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%
---

# Options d’architecture d’implémentation

Les architectures d’implémentation d’Adobe Commerce combinent trois couches : un serveur principal de commerce ([!DNL Adobe Commerce] ou [!DNL Adobe Commerce Optimizer]), un storefront et un ensemble de services et d’intégrations connectés. Comparez les options suivantes pour identifier le système propriétaire du catalogue, de la tarification, du panier, de la commande, des commandes et des transactions client dans chaque architecture.

## Résumé des options d’architecture

Comparez les options par propriété de transaction et par expérience storefront.

### Plateforme et transactions Commerce

| Option | Système d&#39;enregistrement | Chemin de la transaction | Ajustement optimal |
| --- | --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]avec Commerce Foundation** | Adobe-managed Commerce Foundation | Managed Commerce Foundation et services Commerce connectés | Les clients qui souhaitent un Commerce SaaS (Software as a Service) géré par Adobe avec une propriété d’infrastructure réduite |
| **[!DNL Adobe Commerce]sur le cloud ou sur site avec le[!DNL Adobe Commerce Optimizer Connector]** | Commerce Foundation existant, pour les données et transactions Commerce | API Commerce Foundation existantes et services de transaction connectés | Les clients qui souhaitent ajouter des fonctionnalités de découverte et de marchandisage Optimizer à un déploiement [!DNL Adobe Commerce] existant |
| [!DNL Adobe Commerce Optimizer] autonome avec serveur principal de commerce externe **** | Plateforme commerciale existante ou tierce. Les données de catalogue et de prix sont ajoutées à Optimizer à partir d’une source externe | Le maillage API, App Builder ou les intégrations directes connectent le storefront à des services tiers de panier, de passage en caisse, client, de commande, de paiement, de taxe, d’expédition et d’exécution | Clients qui souhaitent bénéficier des fonctionnalités d’Optimizer tout en conservant une plateforme commerciale transactionnelle existante ou tierce |
| **[!DNL Adobe Commerce]sur le cloud ou sur site avec Commerce Foundation** | Commerce Foundation | API Commerce Foundation et intégrations configurées pour les paiements, les taxes, l’expédition, les stocks et l’exécution | Clients qui ont besoin de la plateforme [!DNL Adobe Commerce] complète avec contrôle du déploiement sur le cloud ou l’infrastructure locale |

### Expérience Storefront

Les storefronts se connectent aux API Commerce Foundation, aux services Storefront ([!DNL Catalog Service], [!DNL Live Search] et [!DNL Product Recommendations]) ou aux services de marchandisage [!DNL Adobe Commerce Optimizer].

| Option | Expérience Storefront | Chemin d’accès aux données du storefront |
| --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]avec Commerce Foundation** | Commerce Storefront optimisé par Edge Delivery Services ou une autre expérience découplée prise en charge | Services Storefront, et API Commerce Foundation pour les données de plateforme principales |
| **[!DNL Adobe Commerce]sur le cloud ou sur site avec le[!DNL Adobe Commerce Optimizer Connector]** | Edge Delivery Services ou storefront découplé personnalisé à l’aide d’expériences Optimizer | API GraphQL des services de marchandisage Commerce Optimizer pour les données de catalogue et de marchandisage gérées par Optimizer |
| [!DNL Adobe Commerce Optimizer] autonome avec serveur principal de commerce externe **** | Commerce Storefront optimisé par Edge Delivery Services ou un storefront découplé personnalisé | API GraphQL des services de marchandisage Commerce Optimizer pour les données de catalogue et de marchandisage |
| **[!DNL Adobe Commerce]sur le cloud ou sur site avec Commerce Foundation** | Edge Delivery Services, Luma, PWA ou storefront découplé personnalisé | API Commerce Foundation et services Storefront lors de leur configuration |

## Adobe Commerce as a Cloud Service

![Diagramme d’architecture d’Adobe Commerce as a Cloud Service avec Managed Commerce Foundation et les services Storefront alimentant un storefront Commerce](../assets/architecture/commerce-cloud-service-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Limite de clé** : Adobe gère la plateforme Commerce Foundation. L’architecture utilise les services Storefront, notamment [!DNL Catalog Service], [!DNL Live Search] et [!DNL Product Recommendations], pour les expériences de storefront. [!DNL Product Visuals] optimisé par AEM Assets est une intégration SaaS facultative. Voir [Intégration d’AEM Assets pour Commerce](../aem-assets/aem-assets-integration.md).

**Références:**

- [Vue d’ensemble des [!DNL Adobe Commerce as a Cloud Service]](/help/cloud-service/overview.md)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [Schéma GraphQL de Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Adobe Commerce avec Commerce Foundation

![Diagramme d’architecture d’Adobe Commerce sur le cloud ou sur site avec les services Storefront et les API Commerce Foundation alimentant un storefront Commerce](../assets/architecture/commerce-paas-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Limite de clé** : Commerce Foundation est propriétaire de la plateforme Commerce et des flux de transactions. [!DNL Catalog Service], [!DNL Live Search] et [!DNL Product Recommendations] offrent un accès storefront optimisé au catalogue, à la recherche et aux recommandations lors de leur configuration. L’intégration d’AEM Assets est facultative. Voir [Intégration d’AEM Assets pour Commerce](../aem-assets/aem-assets-integration.md).

**Références:**

- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [API COMMERCE GRAPHQL](https://developer.adobe.com/commerce/webapi/graphql/)
- [Schéma GraphQL de Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)


## Adobe Commerce avec le connecteur Optimizer

![Diagramme d’architecture du connecteur Adobe Commerce Optimizer synchronisant les données de catalogue et de prix d’Adobe Commerce vers Adobe Commerce Optimizer, alimentant une vitrine Commerce via les API de services de marchandisage](../assets/architecture/adobe-commerce-optimizer-architecture.drawio.png){width="600" zoomable="yes"}

**Limite de clé** : le connecteur synchronise les données de catalogue et de prix de [!DNL Adobe Commerce] à [!DNL Adobe Commerce Optimizer]. [!DNL Adobe Commerce] reste le système de transactions, tandis qu’Optimizer fournit des expériences de découverte et de marchandisage par le biais de ses API de services de marchandisage.

**Références:**

- [Intégrations Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md)
- [Services de marchandisage Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [API COMMERCE GRAPHQL](https://developer.adobe.com/commerce/webapi/graphql/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Commerce Optimizer autonome avec un serveur principal tiers

![Diagramme d’architecture des systèmes sources détenus par le client envoyant des données de catalogue et de prix par le biais de l’ingestion de données à un Adobe Commerce Optimizer autonome, alimentant un storefront Commerce connecté à un serveur principal commercial tiers](../assets/architecture/adobe-commerce-optimizer-standalone-detailed.drawio.png){width="800" zoomable="yes"}

**Limite clé** : le [!DNL Adobe Commerce Optimizer] autonome possède les expériences de découverte de catalogues et de marchandisage, mais pas le serveur principal Commerce transactionnel. Saisie des données de catalogue et de prix via l’API REST Data Ingestion. Le storefront Edge Delivery Services utilise les API GraphQL des services de marchandisage pour les expériences produit et se connecte au serveur principal tiers pour le panier et le passage en caisse.

**Références:**

- [Qu’est-ce que Adobe Commerce Optimizer ?](/help/optimizer/overview.md)
- [Commerce Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- [Services de marchandisage Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Référence rapide de terminologie

| Terme préféré | Signification | Évitez d’utiliser comme libellé d’architecture actuel |
| --- | --- | --- |
| **Commerce Foundation** | Fonctionnalités commerciales et transactionnelles de base | Core Commerce, Couche de base PHP |
| **Services Storefront** | API orientées magasin pour le service de catalogue, la recherche en direct et les recommandations de produits | Un libellé limité à une seule plateforme Commerce |
| **Services de marchandisage** | API Optimizer pour la découverte de catalogues et les expériences de marchandisage | API Commerce Foundation |
| **Commerce Storefront avec Edge Delivery Services** | Implémentation du storefront face au client | Une famille d’API |

## Conseils connexes

- [Architectures de référence](reference-architectures.md)
- [Choisir une option Commerce](../portfolio/choose-commerce-option.md)
- [Storefronts](../storefronts/overview.md)
- [API](../apis/commerce-apis.md)
