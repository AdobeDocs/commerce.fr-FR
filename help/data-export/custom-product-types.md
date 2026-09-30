---
title: Prise en charge des types de produits personnalisés dans l’exportation de données de catalogue SaaS
description: Découvrez comment le module d’activation du catalogue MCP de Commerce Storefront permet à l’exportation de données SaaS de représenter des types de produits tiers personnalisés et non reconnus en tant que produits simples dans les données de catalogue envoyées à Live Search et Catalog Service.
role: Admin, Developer
hide: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
source-git-commit: fd87417a494987f33009d386019d870b306dcf73
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---
# Prise en charge des types de produits personnalisés dans l’exportation de données de catalogue SaaS

>[!IMPORTANT]
>
>La prise en charge des types de produits personnalisés est actuellement en **accès anticipé** dans le cadre du [!DNL Commerce Storefront MCP]. Ce module est pris en charge dans Adobe Commerce versions 2.4.4 et ultérieures. Les exigences en matière de disponibilité, d’emballage et d’installation peuvent changer avant la disponibilité générale. Pour demander une invitation à ce **accès anticipé**, envoyez un e-mail à [commerceeap@adobe.com](mailto:commerceeap@adobe.com). L’équipe d’Adobe répondra avec les étapes suivantes et les conditions d’éligibilité.

## Vue d’ensemble

[!DNL SaaS Data Export] reconnaît les types de produits Adobe Commerce standard (simples, configurables, groupés, etc.) lorsqu’il prépare les données de catalogue pour les services Commerce connectés tels que [Recherche en direct](../live-search/overview.md) et [Service de catalogue](../catalog-service/overview.md). Les extensions tierces peuvent introduire des **types de produits personnalisés** que [!DNL SaaS Data Export] ne reconnaît pas nativement.

Le module d’activation du catalogue MCP de Commerce Storefront [!DNL SaaS Data Export] permet de représenter ces types de produits personnalisés et non reconnus en tant que **produits simples** dans la payload du catalogue sortant, de sorte que les acheteurs qui utilisent le [!DNL Commerce Storefront MCP] puissent les découvrir via des services de catalogue.

## Portée du comportement

- Le module d’activation du catalogue MCP de Commerce Storefront ne modifie pas le type de produit stocké dans Adobe Commerce. La représentation d’un type de produit personnalisé en tant que produit simple s’applique uniquement aux données de catalogue envoyées à [!DNL Live Search] et [!DNL Catalog Service].
- Aucun paramètre d’administration ou configuration d’exécution n’est requis. Les types de produits standard continuent à être exportés normalement.
- Le module cible les types de produits personnalisés introduits par des extensions tierces, et non les types de produits Commerce standard.

## Installation du module

Pour activer le module d’activation du catalogue MCP de Commerce Storefront, exécutez la ligne de commande suivante :

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## Resynchroniser les données du catalogue

L’installation du module ne modifie pas les données de produit sous-jacentes dans Adobe Commerce. Par conséquent, les éléments existants de type produit personnalisé ne sont pas automatiquement réexportés. Pour appliquer la nouvelle représentation simple du produit aux données de catalogue déjà synchronisées avant l’installation du module, resynchronisez manuellement les données de votre catalogue. Voir [resynchronisation manuelle des données](data-sync-manage.md#manually-resync-data).
