---
title: Prise En Main Par Rôle
description: Découvrez comment trouver le bon point de départ dans la documentation d’Adobe Commerce en fonction de votre rôle et de la plateforme Commerce actuellement utilisée par votre projet.
role: Admin, Developer, Leader, User
feature: Storefront, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:43:29.080Z'
TQID: 'https://experienceleague.adobe.com/P-GWpL9blAHwmSyN-eFzjUlsOVqyDTxiuLavocyeEdQ'
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
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '429'
ht-degree: 0%
---

# Prise en main par rôle

La documentation d’Adobe Commerce est organisée sur plusieurs référentiels et sites. Le bon point de départ dépend de votre rôle et, pour les administrateurs et les marchandiseurs, de la plateforme et du chemin de marchandisage que votre projet utilise. Consultez la section [&#x200B; Plateformes et services &#x200B;](../portfolio/platform-and-services.md) si vous ne savez pas encore quelle plateforme s’applique à vous.

## Pour les professionnels

Découvrez Adobe Commerce et comment l’administrateur et le storefront travaillent ensemble.

- [Vue d’ensemble des [!DNL Adobe Commerce as a Cloud Service]](/help/cloud-service/overview.md)

- [[!DNL Adobe Commerce Optimizer role-based workflows]](/help/optimizer/get-started.md#role-based-workflows)

- [Guide de prise en main d’Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/guide-overview)


## Pour les marchandiseurs

Adobe Commerce comporte deux chemins de marchandisage. Celui qui s’applique et qui est disponible dépend de votre serveur principal, et non de votre rôle :

- Extensions **[!DNL Live Search], [!DNL Product Recommendations] et [!DNL Catalog Service]** : utilisé avec [!DNL Adobe Commerce as a Cloud Service] et Adobe Commerce (sur le cloud ou sur site). Consultez les guides suivants :

- [Présentation de la recherche en direct](/help/live-search/overview.md)
- [Que sont les recommandations de produits ?](/help/product-recommendations/overview.md)
- [Service de catalogue pour Adobe Commerce](/help/catalog-service/overview.md).

- **Marchandisage natif dans[!DNL Adobe Commerce Optimizer]** : utilisé lorsqu’Adobe Commerce sur le cloud ou sur site se connecte aux [!DNL Adobe Commerce Optimizer] à l’aide de l’[!DNL Adobe Commerce Optimizer Connector]. Voir la [Présentation du marchandisage](/help/optimizer/merchandising/overview.md).

## Pour les administrateurs

La configuration diffère selon la plateforme et selon que votre projet utilise [!DNL Adobe Commerce Optimizer] :

- **[!DNL Adobe Commerce as a Cloud Service]** : les services Commerce sont installés et configurés automatiquement. Voir [Prise en main d’Adobe Commerce as a Cloud Service](/help/cloud-service/getting-started.md).

- **[!DNL Adobe Commerce Optimizer]** : produit SaaS (Software as a Service) que vous configurez indépendamment de votre serveur principal Commerce. Voir [Prise en main de Adobe Commerce Optimizer](/help/optimizer/get-started.md).

- **[!DNL Adobe Commerce Optimizer Connector]et[!DNL Adobe Commerce Optimizer Connector for B2B]** : connecte Adobe Commerce (sur le cloud ou sur site) à Adobe Commerce Optimizer. Voir [Prise en main du connecteur Adobe Commerce Optimizer](/help/aco-connector/get-started.md).

- **Adobe Commerce sur le cloud ou sur site (PaaS)**—Installez chaque extension des services Commerce avant de la configurer. Consultez les guides de chaque extension pour obtenir des instructions détaillées.

- [Prise en main de Live Search](/help/live-search/install.md)
- [Installation et configuration de Product Recommendations](/help/product-recommendations/install-configure.md)
- [Installation du service de catalogue](/help/catalog-service/installation.md).

- Pour l’administration de la plateforme pour Adobe Commerce sur le cloud ou sur site, voir :

- [Guide de Commerce sur les infrastructures cloud](https://experienceleague.adobe.com/fr/docs/commerce-on-cloud/user-guide/overview)
- [Guides opérationnels d’](https://experienceleague.adobe.com/fr/docs/commerce-operations/operational-guides/home) pour la version locale.

## Pour les développeurs

Extension, personnalisation et intégration d’Adobe Commerce, et création de storefronts.

- [Documentation destinée aux développeurs d’Adobe Commerce](https://developer.adobe.com/commerce/docs/)
- [Guide du développeur d’Adobe Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/)
- [[!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/overview.md) (à utiliser si vous vous connectez à un Commerce on Cloud ou à un serveur principal local vers [!DNL Adobe Commerce Optimizer]).

## Pour les architectes de solutions

Examinez les recommandations d’architecture et les modèles de référence qui s’étendent sur plusieurs produits Commerce.

- [Options d’architecture](../architecture-options/overview.md)

## Pour les partenaires

Recherchez les guides d’activation, les parcours de certification et les ressources du programme partenaire.

- [Programme de partenariat Adobe](https://partners.adobe.com/digitalexperience/about)
- [Nœud d’activation d’Adobe](https://partners.adobe.com/digitalexperience/learn/enablement-node)
