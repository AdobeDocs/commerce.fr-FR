---
title: Mappage des champs pour  [!DNL Adobe Commerce Optimizer Connector]  flux
description: Découvrez le mappage  [!DNL Adobe Commerce Optimizer Connector]  champs des données  [!DNL Adobe Commerce]  catalogue aux formats d’API  [!DNL Adobe Commerce Optimizer] ’ingestion pour tous les flux.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
source-git-commit: 1f901b4a72c10dc4e710742b98c03e88cbc8739f
workflow-type: tm+mt
source-wordcount: 465
ht-degree: 0%

---


# Mappage des champs pour les flux du connecteur

Cette page décrit comment l’[!DNL Adobe Commerce Optimizer Connector] transforme [!DNL Adobe Commerce] champs du catalogue au format requis par le [!DNL Catalog Data Ingestion API] [!DNL Commerce Optimizer]. Consultez la [référence du connecteur](connector-reference.md#supported-feeds) pour obtenir la liste des flux pris en charge et leurs points d’entrée d’API.

## Produits

| champ [!DNL Adobe Commerce] | Champ API [!DNL Commerce Optimizer] | Remarques |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin` fixe à `"AdobeCommerce"` |
| `status` | `status` | Mise en majuscule ; défini sur `DISABLED` pour les produits composites sans enfants affectés |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | Séparation des valeurs par des virgules et mappage : →`CATALOG`, `Search`→`SEARCH` ; valeurs non mappées ignorées`Catalog` |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Chaîne délimitée par une nouvelle ligne divisée en tableau |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | `{inStock, lowStock, weight, weightType}` d’objet codé JSON ; toujours présent comme première entrée d’attribut |
| `attributes[]` | `attributes[]` | Chaque entrée mappée à `{code, values[], variantReferenceId}` ; `inStock`, `lowStock`, `weight` et `weightType` sont exclus (ils vont dans `aco_ac_attributes`). |
| `images[]` | `images[]` | `url`, `label` ; rôles standard mappés : `image`→`BASE`, `small_image`→`SMALL`, `thumbnail`→`THUMBNAIL`, `swatch_image`→`SWATCH` ; les rôles non standard vont dans `customRoles[]` |
| `categoryData[].categoryPath` | `routes[].path` | |
| `categoryData[].productPosition` | `routes[].position` | |
| `links[].type` + `links[].sku` | `links[]` | `type` mis en majuscules ; entrées sans `sku` supprimées |
| `parents[].productType` + `parents[].sku` | `links[]` | Type mappé : →`VARIANT_OF`, `bundle`/`bundle_fixed`→`IN_BUNDLE`&#x200B;`configurable` |
| `configurable options` | `configurations[]` | →`attributeCode`, `label` ; type d’option `SWATCH` lorsque `swatchType` est défini, sinon `CONFIGURABLE` ; variante par défaut de `isDefault` ; les valeurs comprennent `variantReferenceId`, `label`, `colorHex`, `imageUrl`&#x200B;`id` |
| `bundle options` | `bundles[]` | →`group`; `required`; `renderType` `checkbox`/`multi`→`multiSelect: true`; SKU par défaut de `isDefault`; les éléments comprennent `sku`, `qty`, `userDefinedQty` (`qtyMutability`)`label` |

## Métadonnées des attributs de produit

| champ [!DNL Adobe Commerce] | Champ API [!DNL Commerce Optimizer] | Remarques |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | Voir le tableau de conversion ci-dessous |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | Ajouté au tableau lors de l’`true` |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | Ajouté au tableau lors de l’`true` |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | Ajouté au tableau lors de l’`true` |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | Ajouté au tableau lors de l’`true` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

**Conversion du type de données :**

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | `dataType` de l’API [!DNL Commerce Optimizer] |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` ou `select` | `TEXT` |
| `int` | tout autre | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| tout autre | - | `TEXT` |

## Catalogues de prix

Contrairement aux autres flux du connecteur, le flux de `priceBooks` n’est pas collecté par un indexeur de [!DNL SaaS Data Export] dans [!DNL Adobe Commerce]. Le connecteur génère ce flux à partir de la configuration du site web et du groupe de clients dans l’Admin.

Un **catalogue des prix de base** est créé par site web, plus un **catalogue des prix enfant** par paire site web-groupe client.

**Formule de l&#39;ID du catalogue des prix :**

- **De base** (prix réguliers) : `priceBookId = websiteCode`
- **Enfant** (groupe de clients ou catalogue partagé) : `priceBookId = websiteCode::sha1(customerGroupId)` où `sha1(customerGroupId)` correspond au résumé hexadécimal SHA-1 de l’ID entier du groupe de clients

Le flux de prix utilise la même formule lors de la résolution du portefeuille de prix auquel appartient une entrée de prix. Pour savoir comment les storefronts résolvent le `priceBookId` d’une session client, voir [Intégration de storefront découplé](../headless-storefront.md#graphql-commerceoptimizer-query).

| Champ généré | Champ API [!DNL Commerce Optimizer] | Remarques |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| Nom du site web | `name` | Prix de base du livre : nom du site web. Enfant : `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | Présent uniquement sur les livres de prix enfant ; pointe vers le livre de prix de base |
| Devise de base du site Web | `currency` | Présent uniquement sur les livres de prix de base ; hérité par les enfants |

## Prix

| champ [!DNL Adobe Commerce] | Champ API [!DNL Commerce Optimizer] | Remarques |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | exemple de remises : prix spécial, prix de règle de catalogue, prix de catalogue partagé |
| `tierPrices[]` | `tierPrices[]` | |

## Catégories

Les éléments avec un `urlPath` vide (catégories racine logique) sont ignorés et ne sont jamais envoyés.

| champ [!DNL Adobe Commerce] | Champ API [!DNL Commerce Optimizer] | Remarques |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Chaîne délimitée par une nouvelle ligne divisée en tableau |
| `image` | `images[].url` | Tableau à un seul élément ; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` lorsque les deux `true`, `[]` dans le cas contraire |

>[!MORELIKETHIS]
>
> - [Ingérer des données de produit et de prix avec l’API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — Découvrez le modèle de données de catalogue pour les métadonnées, les produits, les catégories, les livres de prix et les prix
> - [Référence de l’API REST d’ingestion de données de catalogue](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — Consultez les schémas de requête et de réponse pour chaque point d’entrée de flux
> - [Fonctionnement de  [!DNL Commerce Optimizer Connector]  [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) — Découvrez comment les affichages de magasin, les sites Web et les groupes de clients sont associés aux sources de catalogue et aux tarifs
> - [Classeurs de prix dans  [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — Gérer les classeurs de prix créés par l&#39;exportation du connecteur
> - [Intégration de storefront découplé](../headless-storefront.md#graphql-commerceoptimizer-query) — Résolution des `priceBookId` pour les sessions client
