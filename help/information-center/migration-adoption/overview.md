---
title: Migration et adoption
description: Découvrez les itinéraires permettant d’adopter Adobe Commerce Optimizer, de moderniser un storefront existant ou de migrer entièrement vers Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/2iEJ6fA-wLr18bi9C8l-w3srx1AWlAtiGt1cG9RPv0Q'
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
  - id: 1783ae9f-7157-5aeb-a915-91e260301e46
    internal-label: Routes
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---

# Migration et adoption

L’adoption n’a pas besoin d’être un changement de plateforme unique et simultané. Sélectionnez une gamme selon que votre objectif immédiat est la modernisation du storefront, l&#39;amélioration du merchandising, la modernisation du serveur principal ou une transition complète vers le logiciel géré en tant que service (SaaS).

## Itinéraires d’adoption

### Moderniser le déploiement Adobe Commerce existant

- Conservez Commerce Foundation existant en tant que serveur principal transactionnel.
- Adoptez la vitrine Commerce optimisée par [!DNL Edge Delivery Services].
- Utilisez les services Storefront, App Builder, le maillage API et une intégration facultative d’AEM Assets.

### Utilisation de Commerce Optimizer comme pont

- Connectez-vous [!DNL Adobe Commerce] cloud ou sur site à l’aide de l’[!DNL Adobe Commerce Optimizer Connector] .
- Adoptez les services de marchandisage, la découverte, les recommandations et une vitrine Edge Delivery Services.
- Conservez [!DNL Adobe Commerce] comme système principal d’enregistrement des produits, des prix, de la structure du catalogue, du panier, de la commande, des clients et des commandes.
- Utilisez cette architecture comme une transition possible vers [!DNL Adobe Commerce as a Cloud Service].

### Migrer entièrement vers Adobe Commerce as a Cloud Service

- Évaluez l’application actuelle, les personnalisations, les intégrations, le storefront et les données.
- Modernisez les personnalisations à l’aide de modèles d’extensibilité compatibles avec SaaS.
- Recréez ou adaptez le storefront et les intégrations.
- Migrez et validez le catalogue, les clients, les commandes, la configuration et les données personnalisées prises en charge.
- Tester, couper et exploiter le nouvel environnement SaaS.

### Adopter un Adobe Commerce Optimizer autonome

- Ingérez des données de catalogue et de prix à partir d’une plateforme Commerce tierce, de PIM, d’ERP ou d’une autre source.
- Utilisez [!DNL Adobe Commerce Optimizer] Merchandising Services pour la récupération de catalogues, la découverte, les recommandations et le marchandisage.
- Utilisez le storefront Commerce optimisé par [!DNL Edge Delivery Services].
- Conservez le panier, le passage en caisse, les clients, les commandes, les paiements, les taxes, l’expédition et l’exécution dans les systèmes tiers connectés.

## Séquence recommandée

1. Évaluez l’état actuel et définissez la propriété du système.
1. Définissez les limites de l’intégration API-First.
1. Modernisez le storefront et la couche d’expérience.
1. Adoptez les services de marchandisage et AEM Assets en parallèle.
1. Migrez Commerce Foundation si nécessaire.
1. Valider, couper, surveiller et optimiser.

## Conseils connexes

- [Choisir une option Commerce](../portfolio/choose-commerce-option.md)
- [Options d’architecture](../architecture-options/overview.md)
- [Moderniser un storefront existant](../implementation-guides/modernize-storefront.md)
- [Activer Adobe Commerce Optimizer](../implementation-guides/enable-aco.md)
