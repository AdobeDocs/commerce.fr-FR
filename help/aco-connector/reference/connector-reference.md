---
title: Modules [!DNL Adobe Commerce Optimizer Connector] et points d’entrée de flux
description: Découvrez les modules, les points  [!DNL Adobe Commerce Optimizer Connector] ’entrée de l’API de flux du catalogue, les limites de lots et les chemins de configuration core_config_data pour  [!DNL Adobe Commerce].
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 289
ht-degree: 1%

---

# Modules de connecteur et points d’entrée de flux

Cette référence répertorie les packages de modules [!DNL Adobe Commerce Optimizer Connector], les points d’entrée d’API de flux pris en charge et les chemins d’accès aux clés de configuration stockés dans `core_config_data`. Pour découvrir comment ces composants fonctionnent ensemble pendant la synchronisation, consultez [Pipeline de synchronisation du connecteur](../connector-sync-pipeline.md).

## Modules

Le connecteur comprend plusieurs modules Magento qui collectent des données de catalogue, mappent les données de flux au format pris en charge par l’API [!DNL Commerce Optimizer] et gèrent le contrôle de l’envoi et de la portée. Le tableau suivant résume chaque module et son rôle.

| Module | Rôle |
| ------ | ---- |
| `DataExporterAdapter` | Mappe les flux [!DNL Adobe Commerce] au format requis par l’API [!DNL Adobe Commerce Optimizer]. Il remplace la configuration du pool de flux et du schéma. |
| `SaasExportAdapter` | Achemine les flux [!DNL Commerce Optimizer] vers l’API d’ingestion et bloque l’envoi des flux non pris en charge. |
| `CommerceAcoExporter` | Gère les informations d’identification [!DNL Commerce Optimizer] et fournit des commandes de configuration de l’interface en ligne de commande |
| `CommerceAdapter` | [!DNL Commerce Optimizer] de compatibilité de l’API (GraphQL, ajout au panier groupé, interface utilisateur de configuration) |
| `PriceBookDataExporter` | Flux de catalogue des prix indexé par site web et groupe de clients |
| `SaasPriceBook` | Infrastructure SaaS pour la soumission du catalogue de prix |
| `CommerceOptimizerScopeMapper` | Activation de la synchronisation par site web et par magasin |

## Flux pris en charge

Le connecteur envoie plusieurs types de flux au [!DNL Catalog Data Ingestion API] [!DNL Commerce Optimizer]. Le tableau ci-dessous répertorie chaque flux avec son point d’entrée, sa limite de lots, le nom de l’indexeur et sa table de flux en [!DNL Adobe Commerce].

| Flux | Point d’entrée de l’API [!DNL Commerce Optimizer] | Limite de lot | Nom de l’index AC | Tableau de flux |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

Les flux `products`, `productAttributes`, `categories` et `prices` réutilisent les données collectées par les indexeurs [!DNL SaaS Data Export]. Le connecteur génère le flux de `priceBooks` à partir de la configuration du site web et du groupe client et ne repose pas sur un indexeur de [!DNL SaaS Data Export].

Pour plus d’informations sur le mappage au niveau du champ de chaque flux, voir [Mappage des champs pour  [!DNL Commerce Optimizer Connector]  flux](field-mapping.md).

## Chemins de configuration

[!DNL Commerce Optimizer Connector] informations d’identification et les URL de service sont stockées dans `core_config_data` sous le préfixe de chemin d’accès `aco_exporter/general/` . Exécutez `bin/magento aco:config:show` pour passer en revue les valeurs actuelles. La commande n’affiche pas le secret client.

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
