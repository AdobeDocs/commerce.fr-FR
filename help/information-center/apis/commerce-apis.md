---
title: API COMMERCE
description: Comparez les familles d’API d’Adobe Commerce, y compris Commerce Foundation, Storefront Services, Commerce Optimizer Merchandising Services et Data Ingestion.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
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
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%
---

# API

| Famille d’API | objectif du Principal | Utilisé par |
| --- | --- | --- |
| **API Commerce Foundation GraphQL** | Fonctionnalités commerciales et transactionnelles principales telles que les opérations de catalogue, le panier, le passage en caisse, les clients et les commandes | [!DNL Adobe Commerce] sur le cloud, [!DNL Adobe Commerce] sur site et [!DNL Adobe Commerce as a Cloud Service] |
| **API GraphQL de Storefront Services** | Expériences de catalogue, de recherche et de recommandation orientées magasin via [!DNL Catalog Service], [!DNL Live Search] et [!DNL Product Recommendations] | [!DNL Adobe Commerce] sur le cloud ou sur site avec des services configurés, et [!DNL Adobe Commerce as a Cloud Service] |
| **API GraphQL des services de marchandisage Commerce Optimizer** | Récupérer le catalogue géré par Optimizer, les vues de catalogue, les contextes de prix, la recherche, les recommandations et les résultats de marchandisage | [!DNL Adobe Commerce] sur le cloud ou sur site avec le connecteur Optimizer et les [!DNL Adobe Commerce Optimizer] autonomes |
| **API REST d’ingestion de données** | Ajout de données de catalogue et de prix à une implémentation [!DNL Adobe Commerce Optimizer] autonome | [!DNL Adobe Commerce Optimizer] autonomes connectés à une source de données externe |

## API Commerce Foundation GraphQL

Fonctionnalités commerciales principales, notamment le catalogue, le panier, le passage en caisse, les clients et les commandes. Utilisé par [!DNL Adobe Commerce] sur le cloud, [!DNL Adobe Commerce] sur site et [!DNL Adobe Commerce as a Cloud Service]. Voir l’API Commerce GraphQL [&#128279;](https://developer.adobe.com/commerce/webapi/graphql/).

## API GraphQL de Storefront Services

Expériences de catalogue, de recherche et de recommandation orientées magasin via [!DNL Catalog Service], [!DNL Live Search] et [!DNL Product Recommendations]. Utilisé par [!DNL Adobe Commerce] sur le cloud, sur site et [!DNL Adobe Commerce as a Cloud Service]. Reportez-vous au schéma [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## API GraphQL des services de marchandisage Commerce Optimizer

Récupérez le catalogue géré par Optimizer, les vues de catalogue, les contextes de prix, la recherche, les recommandations et les résultats de marchandisage. Utilisé par [!DNL Adobe Commerce] sur le cloud, sur site avec le [!DNL Adobe Commerce Optimizer Connector] et [!DNL Adobe Commerce Optimizer] autonome. Voir [Services de marchandisage &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/).

## API REST d’ingestion de données Commerce Optimizer

Ajoutez des données de catalogue et de prix à une implémentation [!DNL Adobe Commerce Optimizer] autonome à partir d’une source de données externe. Voir [Commerce Optimizer Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).

## Intégrations Commerce Optimizer

[!DNL Adobe Commerce Optimizer] se connecte à d’autres systèmes par le biais de plusieurs chemins d’intégration, selon qu’il est associé à [!DNL Adobe Commerce] ou à un serveur principal tiers.

### Connecteur Adobe Commerce Optimizer

Synchronise les données de catalogue et de prix de [!DNL Adobe Commerce] sur le cloud ou sur site vers [!DNL Adobe Commerce Optimizer], en [!DNL Adobe Commerce] le système de transaction tandis qu&#39;Optimizer fournit la détection et le marchandisage. Voir [Intégrations &#x200B;](/help/optimizer/integrations/integrations-overview.md).

### Intégrations commerciales tierces

Ingère les données de catalogue et de prix d’une plateforme commerciale tierce, PIM, ERP ou d’une autre source dans des [!DNL Adobe Commerce Optimizer] autonomes via l’API REST Data Ingestion, tandis que la plateforme tierce reste le système d’enregistrement transactionnel.

### Maillage API et App Builder

Utilisez le maillage API pour orchestrer les API Adobe Commerce avec des API privées ou tierces. Utilisez Adobe Developer App Builder pour créer des applications et des intégrations personnalisées. Pour obtenir des conseils sur l’extensibilité des Commerce, voir [Maillage API](https://developer.adobe.com/graphql-mesh-gateway/) et [Extensibilité d’Adobe Commerce](https://developer.adobe.com/commerce/extensibility/).

Pour les intégrations basées sur un événement en particulier, consultez [Adobe I/O Events pour Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events).


### Transfert de panier et de passage en caisse

Pour les [!DNL Adobe Commerce Optimizer] autonomes avec un serveur principal externe, le storefront utilise les API GraphQL des services de marchandisage pour les expériences produit, puis transfère le panier, le passage en caisse, le client, la commande, le paiement, la taxe, l’expédition et l’exécution au serveur principal via le maillage API, App Builder ou une intégration directe.

### AEM Assets

AEM Assets est une intégration facultative et transversale de la gestion des ressources numériques qui peut être ajoutée à n’importe quelle architecture Commerce ou Optimizer plutôt qu’à un chemin d’intégration distinct à part entière. Voir [Intégration d’AEM Assets pour Commerce](../aem-assets/aem-assets-integration.md).

## Conseils connexes

- [Aperçu de l’architecture](../architecture-options/overview.md)
- [Storefronts](../storefronts/overview.md)
- [Intégration d’AEM Assets pour Commerce](../aem-assets/aem-assets-integration.md)
