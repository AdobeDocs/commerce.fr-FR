---
title: Architectures de référence
description: Découvrez les modèles d’architecture de référence pour les implémentations d’Adobe Commerce courantes, telles que les storefronts, les services et les pipelines de synchronisation de catalogue.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T11:42:09.021Z'
TQID: 'https://experienceleague.adobe.com/GVbGyRZz8llMWcUykcXXZwWnTaAomHVCTcV3ft49IEc'
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
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%
---

# Architectures de référence

La documentation suivante fournit des modèles d’architecture de référence pour les plateformes et services Adobe Commerce dans différents modèles de déploiement et cas d’utilisation.

- [Architecture d’Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md#architecture)
- [Architecture de référence d’entreprise Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/implementation-playbook/architecture/enterprise-blueprint){target="_blank"}
- [Architecture du storefront d’Adobe Commerce](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/){target="_blank"}
- [Architecture d’Adobe Commerce sur les infrastructures cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/architecture/cloud-architecture){target="_blank"}

## Storefront optimisé par Edge Delivery Services

Un storefront construit sur la norme Adobe Commerce, utilisant des composants de dépôt et des blocs de contenu, connectés à Adobe Commerce ou [!DNL Adobe Commerce Optimizer] comme serveur principal. Consultez la [présentation du storefront &#x200B;](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

- [Architecture du storefront d’Adobe Commerce](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)

## Pipeline de synchronisation des catalogues

Flux de données permettant de synchroniser les données de catalogue, de prix et d’inventaire entre Adobe Commerce et les services Adobe Commerce (Commerce Optimizer, Live Search, Catalog Service, Product Recommendations et autres [services Commerce connectés](../../landing/home.md)).

- Pour les déploiements Adobe Commerce as a Cloud Service, sur les infrastructures cloud ou sur site, voir [&#x200B; Synchronisation des données avec l’exportation de données SaaS &#x200B;](/help/data-export/sync-overview.md)

- Pour Adobe Commerce sur l’infrastructure cloud ou local configuré avec le connecteur Adobe Commerce Optimizer, consultez [Pipeline de synchronisation du connecteur](/help/aco-connector/connector-sync-pipeline.md).


## Conseils connexes

- [Architectures d’implémentation](implementation-architectures.md)
