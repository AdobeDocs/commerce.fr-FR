---
title: Présentation de l’architecture de Commerce
description: Découvrez le modèle de produit Adobe Commerce et où trouver des options d’architecture détaillées, un storefront et des conseils sur les API.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
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
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
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
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---

# Présentation de l’architecture de Commerce

Les architectures Adobe Commerce combinent généralement trois couches : un serveur principal de commerce ([!DNL Adobe Commerce] ou [!DNL Adobe Commerce Optimizer]), un storefront et un ensemble de services et d’intégrations connectés. Cette section vous oriente vers le modèle de produit et vous guide vers les comparaisons détaillées, les diagrammes et les références d’API gérés dans chaque page dédiée.

## Prise en main

| Section | Utilisez-le pour |
| ------- | --------- |
| [ Plateformes et services ](../portfolio/platform-and-services.md) | comprendre ce qu’est chaque produit Commerce : Adobe Commerce, Commerce Foundation, Adobe Commerce Optimizer et Adobe Commerce as a Cloud Service ; |
| [Choisir une option Commerce](../portfolio/choose-commerce-option.md) | Comparez les options de Commerce en fonction de la propriété de la transaction, du modèle de déploiement et des besoins de marchandisage. |
| [Options d’architecture](../architecture-options/implementation-architectures.md) | Comparez en détail les quatre architectures prises en charge, y compris les diagrammes système et les liens de référence. |
| [Storefronts](../storefronts/overview.md) | Découvrez les options de storefront et comment elles se connectent à chaque architecture. |
| [API](../apis/commerce-apis.md) | Comparez les familles d’API utilisées dans Commerce Foundation, Storefront Services et Commerce Optimizer. |
| [Intégration d’AEM Assets pour Commerce](../aem-assets/aem-assets-integration.md) | Ajoutez la gestion centralisée des ressources numériques à toute architecture Commerce ou Optimizer. |
| [Migration et adoption](../migration-adoption/overview.md) | Planifiez un passage entre les architectures ou une adoption progressive de Adobe Commerce Optimizer. |

## Référence rapide de terminologie

| Terme préféré | Signification | Évitez d’utiliser comme libellé d’architecture actuel |
| --- | --- | --- |
| **Commerce Foundation** | Fonctionnalités commerciales et transactionnelles de base | Couche de base de Commerce et PHP |
| **Services Storefront** | API orientées magasin pour le service de catalogue, la recherche en direct et les recommandations de produits | Un libellé limité à une seule plateforme Commerce |
| **Services de marchandisage** | API Optimizer pour la découverte de catalogues et les expériences de marchandisage | API Commerce Foundation |
| **Commerce Storefront avec Edge Delivery Services** | Implémentation du storefront face au client | Une famille d’API |

## Conseils connexes

- [Architectures d’implémentation](implementation-architectures.md)
- [Architectures de référence](reference-architectures.md)
- [Créer une nouvelle vitrine](../implementation-guides/build-new-storefront.md)
