---
title: Mappage des champs pour les flux [!DNL Adobe Commerce Optimizer Connector]
description: Découvrez [!DNL Adobe Commerce Optimizer Connector] mappage des champs des données de catalogue [!DNL Adobe Commerce] aux formats d’API d’ingestion [!DNL Adobe Commerce Optimizer] pour tous les flux.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%
---

# Mappage des champs pour les flux du connecteur

Cette page décrit comment l’[!DNL Adobe Commerce Optimizer Connector] transforme [!DNL Adobe Commerce] champs du catalogue au format requis par le [!DNL Catalog Data Ingestion API] [!DNL Commerce Optimizer]. Consultez la [référence du connecteur](connector-reference.md#supported-feeds) pour obtenir la liste des flux pris en charge et leurs points d’entrée d’API.

## Produits

Le flux de `products` envoie des données au point d’entrée [Products](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}.

| champ [!DNL Adobe Commerce] | Champ API [!DNL Commerce Optimizer] | Détails du mappage |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | Définit `origin` sur `"AdobeCommerce"` |
| `status` | `status` | Convertit le statut en majuscules. Utilise `DISABLED` si le statut est manquant ou si un produit configurable ou groupé ne comporte aucune valeur d’option. |
| `description` | `description` | Utilise une chaîne vide si la description est manquante. |
| `shortDescription` | `shortDescription` | Utilise une chaîne vide si la description courte est manquante. |
| `visibility` | `visibleIn` | Divise la valeur séparée par des virgules et mappe les `Catalog` à `CATALOG` et les `Search` à `SEARCH`. Ignore les autres valeurs. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Divise les mots-clés séparés par une nouvelle ligne en un tableau et supprime les espaces. |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | Ajoute toujours une entrée `aco_ac_attributes` comme premier attribut. Sa valeur JSON inclut des `inStock` et des `lowStock` sous forme de chaînes. Cela inclut les `weight` et les `weightType` lorsque ces valeurs sont disponibles. |
| `attributes[]` | `attributes[]` | Mappe chaque entrée à son code d’attribut, à ses valeurs de chaîne et à l’identifiant de référence de variante correspondant, le cas échéant. Ignore `inStock`, `lowStock`, `categories`, `weight` et `weightType`. Les valeurs liées au stock sont incluses dans `aco_ac_attributes`. Les catégories sont exportées sous forme d’itinéraires. |
| `images[]` | `images[]` | Ignore les images sans URL.<br>Exporte les `url`, les `label` (vides si manquants) et les `sortOrder` (entiers, par défaut `0`).<br>Trie les images par `sortOrder` dans l’ordre croissant.<br>Mappe les rôles standard : `image` à `BASE`, `small_image` à `SMALL`, `thumbnail` à `THUMBNAIL` et `swatch_image` à `SWATCH`. Exporte les autres rôles en tant que `customRoles[]`. |
| `categoryData[].categoryPath` | `routes[].path` | Ignore les entrées dont le chemin d’accès à la catégorie est vide. |
| `categoryData[].productPosition` | `routes[].position` | Utilise `0` si la position du produit est manquante. |
| `links[].type` + `links[].sku` | `links[]` | `type` mis en majuscules ; entrées sans `sku` supprimées |
| `parents[].productType` + `parents[].sku` | `links[]` | Mappe les `configurable` à `VARIANT_OF` et les `bundle` ou `bundle_fixed` à `IN_BUNDLE`. Convertit d’autres types de produits en majuscules. Ignore les parents sans SKU. |
| `configurable options` | `configurations[]` | Exporte les options qui ont un identifiant et au moins une valeur.<br>Mappe les `id` aux `attributeCode`. Définit `type` sur `SWATCH` en cas de `swatchType` et sur `CONFIGURABLE` dans le cas contraire.<br>Utilise l’identifiant de la valeur par défaut en tant que `defaultVariantReferenceId`.<br>Mappe chaque valeur sur `variantReferenceId`, `label`, `colorHex` et `imageUrl`. |
| `bundle options` | `bundles[]` | Exporte les options contenant au moins un élément.<br>Utilise le libellé de l’option comme `group` ou `Bundle group` si le libellé est vide. Copie le `required` vers la sortie.<br>Définit `multiSelect` sur `true` pour les types de rendu `checkbox` et `multi`.<br>Répertorie les SKU par défaut dans `defaultItemSkus`. Chaque élément comprend `sku`, `qty` (par défaut `0`) et `userDefinedQty` (de `qtyMutability`, par défaut `false`). |

## Métadonnées des attributs de produit

Le flux de `productAttributes` envoie des données au point d’entrée [Métadonnées](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}.

| champ [!DNL Adobe Commerce] | Champ API [!DNL Commerce Optimizer] | Détails du mappage |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | Voir le tableau de conversion ci-dessous |
| `dataType` et `frontendInput` | `dataType` | Utilise les règles de conversion ci-dessous. |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | Lorsqu’un indicateur est `true`, ajoute sa valeur correspondante : <br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### Conversion du type de données

Lorsqu’`dataType` est `int`, le connecteur vérifie les `frontendInput`. Pour les autres types de données, `frontendInput` n’affecte pas la conversion.

| `dataType` d’entrée | `frontendInput` d’entrée | `dataType` de sortie |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` ou `select` | `TEXT` |
| `int` | Toute autre valeur, y compris une valeur manquante | `INTEGER` |
| `decimal` | Non utilisé | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | Non utilisé | `TEXT` |
| `OBJECT` | Non utilisé | `OBJECT` |
| Toute autre valeur | Non utilisé | `TEXT` |

>[!NOTE]
>
>Lorsqu’un attribut utilise le type de données `OBJECT`, l’API [Products](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} tente d’analyser sa valeur stockée au format JSON. Si l’analyse réussit, l’API renvoie la valeur sous la forme d’un objet imbriqué. Utilisez des `OBJECT` pour les données d’attribut structurées qui ne peuvent pas être représentées comme une valeur unique. Pour obtenir des instructions, voir [Ajouter dynamiquement des attributs de produit](../../data-export/add-attribute-dynamically.md).

## Catalogues de prix

Le flux de `priceBooks` envoie des données au point d’entrée [Prix des livres](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}.

Contrairement aux autres flux du connecteur, le flux de `priceBooks` n’est pas collecté par un indexeur de [!DNL SaaS Data Export] dans [!DNL Adobe Commerce]. Le connecteur génère ce flux à partir de la configuration du site web et du groupe de clients dans l’Admin.

Pour chaque site web, le connecteur crée un catalogue des prix de base et un catalogue des prix enfant pour chaque groupe de clients.

Utilisez ces formules pour les `priceBookId` :

- Livres de prix de base pour les prix réguliers : `priceBookId = websiteCode`.
- Annuaires de prix enfants pour les groupes de clients : `priceBookId = websiteCode::sha1(customerGroupId)`, où `sha1(customerGroupId)` correspond au résumé hexadécimal SHA-1 de l&#39;ID entier du groupe de clients.

Le flux des prix utilise la même formule pour affecter chaque entrée de prix à un catalogue des prix. Pour plus d’informations sur la façon dont un storefront résout les `priceBookId` pour une session client, voir [Intégration de storefront découplé](../headless-storefront.md#graphql-commerceoptimizer-query).


| Champ ou valeur Source | Champ API [!DNL Commerce Optimizer] | Détails du mappage |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | Ajoute ce champ aux tarifs enfant. Sa valeur identifie le prix comptable de base. |
| Nom du site web | `name` | Utilise le nom du site Web pour les livres de prix de base. Utilise des `Customer group name (Website name)` pour les livres de prix enfant. |
| `websiteCode` | `parentId` | Présent uniquement sur les livres de prix enfant ; pointe vers le livre de prix de base |
| Devise de base du site Web | `currency` | Inclut ce champ uniquement dans les registres de prix de base. Les livres sur le prix des enfants l&#39;omettent. |

## Prix

Le flux de `prices` envoie [!DNL Adobe Commerce] données au point d’entrée [Prix](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}.

| Champ de saisie du flux | Champ API [!DNL Commerce Optimizer] | Détails du mappage |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | Transmet le SKU sans le modifier. |
| `websiteCode`, `customerGroupCode` | `priceBookId` | Combine `websiteCode` avec le hachage SHA-1 de l’ID de groupe client dans `customerGroupCode`. Si `customerGroupCode` est `0`, utilise `websiteCode` seul. |
| `regular` | `regular` | Fait passer le prix normal inchangé. |
| `discounts[]` | `discounts[]` | Si la valeur source est `null`, exporte un tableau vide.<br>Pour les entrées dont `code` est défini sur `special_price` et un `percentage`, définit `percentage` sur `100 - percentage` lorsque la valeur est comprise entre `0` et `100`. Définit cette valeur sur `0` à cette plage ou en dehors.<br>Transmet les autres entrées, y compris les prix spéciaux basés sur les prix, par inchangé. |
| `tierPrices[]` | `tierPrices[]` | Utilise un tableau vide si la valeur source est manquante ou `null`. |

## Catégories

Le flux de `categories` envoie [!DNL Adobe Commerce] données au point d’entrée [Catégories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}.

Les éléments avec un `urlPath` vide (catégories racine logique) sont ignorés et ne sont jamais envoyés.

| champ [!DNL Adobe Commerce] | Champ API [!DNL Commerce Optimizer] | Détails du mappage |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | Exporte la position de la catégorie, le cas échéant. Omet le champ lorsqu’il est manquant. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Chaîne délimitée par une nouvelle ligne divisée en tableau |
| `image` | `images[].url` | Tableau à un seul élément ; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` lorsque les deux `true`, `[]` dans le cas contraire |

| `metaKeywords` | `metaTags/keywords` | Divise les mots-clés délimités par une nouvelle ligne en un tableau et supprime les espaces. |
| `image` | `images[].url` | Lorsqu’`image` est présent, exporte une image avec le rôle `BASE`. Exporte un tableau vide lorsque l’image est vide ou manquante. |
| `isActive` + `includeInMenu` | `families` | Ajoute des `top_menu` uniquement lorsque les deux valeurs sont `true`. Sinon, exporte un tableau vide. |
| `attributes[]` | `attributes[]` | Exporte les entrées dont le `attributeCode` n’est pas vide en tant que `{code, values[]}`. Convertit les valeurs en chaînes. Omet `attributes` lorsqu’il n’existe aucune entrée éligible. |

>[!MORELIKETHIS]
>
> - [Ingérer des données de produit et de prix avec l’API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"} — Découvrez le modèle de données de catalogue pour les métadonnées, les produits, les catégories, les livres de prix et les prix
> - [Référence de l’API REST d’ingestion de données de catalogue](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"} — Consultez les schémas de requête et de réponse pour chaque point d’entrée de flux
> - [Fonctionnement de  [!DNL Commerce Optimizer Connector]  [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce) — Découvrez comment les affichages de magasin, les sites Web et les groupes de clients sont associés aux sources de catalogue et aux tarifs
> - [Classeurs de prix dans  [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md) — Gérer les classeurs de prix créés par l&#39;exportation du connecteur
> - [Intégration de storefront découplé](../headless-storefront.md#graphql-commerceoptimizer-query) — Résolution des `priceBookId` pour les sessions client
