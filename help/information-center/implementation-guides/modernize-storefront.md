---
title: Moderniser un storefront existant
description: Découvrez comment planifier une migration incrémentielle d’un storefront Adobe Commerce hérité vers un storefront basé sur Edge Delivery Services et des composants de dépôt.
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T11:09:14.812Z'
TQID: 'https://experienceleague.adobe.com/1OR7uwncjLw-NpwMMuwKjDjpASdh74sfu6s5rNClqxg'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%
---

# Moderniser un storefront existant

Vous pouvez migrer les storefronts hérités de manière incrémentielle vers les composants additionnels Edge Delivery Services et Commerce au lieu de tout reconstruire en même temps.

>[!NOTE]
>
>Ce guide s’applique aux déploiements d’Adobe Commerce as a Cloud Service, d’Adobe Commerce sur les infrastructures cloud ou sur site à l’aide des services Storefront ou du connecteur Adobe Commerce Optimizer. Elle s’applique également à Adobe Commerce Optimizer autonome avec un serveur principal existant ou tiers. Pour confirmer quelle option s’applique à votre projet, consultez la section [Options d’architecture d’implémentation](../architecture-options/implementation-architectures.md).

## Prise en main

1. Pour comparer un storefront basé sur Edge Delivery Services à votre implémentation actuelle, consultez la [présentation du storefront Adobe Commerce](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

1. Utilisez le [guide de développement de Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/) pour définir la portée des pages ou des flux à migrer en premier.

1. Pour Adobe Commerce as a Cloud Service, conservez les connexions de services Commerce ([!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations], [!DNL Payment Services]) en place. Pour plus d&#39;informations, consultez la section [Configurer des services Commerce](set-up-commerce-services.md).

## Conseils connexes

- [Créer une nouvelle vitrine](build-new-storefront.md)
- [Options d’architecture](../architecture-options/overview.md)
