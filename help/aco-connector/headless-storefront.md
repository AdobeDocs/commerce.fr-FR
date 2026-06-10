---
title: Intégration du storefront [!DNL Adobe Commerce Optimizer Connector] Headless
description: Découvrez comment intégrer des vitrines découplées à l’API  [!DNL Adobe Commerce Optimizer Connector] GraphQL, aux identifiants de catalogue de prix et au codage d’ajout au panier de lots.
feature: Storefront, Integration, GraphQL
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 0%

---

# Intégration de storefront découplé

Le module `CommerceAdapter` s’étend [!DNL Adobe Commerce] pour combler l’écart entre un storefront découplé et un [!DNL Adobe Commerce Optimizer]. Il fournit une requête GraphQL pour résoudre le contexte du catalogue des prix client et applique l’encodage du bundle de produits attendu par l’API [!DNL Adobe Commerce Optimizer] GraphQL.

Pour obtenir des instructions générales sur la configuration des storefronts, consultez [Configuration du marchandisage et des storefronts](./overview.md#merchandising-storefronts) dans la présentation du [!DNL Adobe Commerce Optimizer Connector].

## GraphQL : requête `commerceOptimizer` {#graphql-commerceoptimizer-query}

Les storefronts découplés appellent la requête `commerceOptimizer` GraphQL pour récupérer les `priceBookId` de la session client actuelle. Transmettez cette valeur à l’API [[!DNL Adobe Commerce Optimizer] &#x200B;](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"} lors de la récupération des prix.

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

Exemple de réponse :

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

Comment résoudre `priceBookId` problème :

| État de la session | `priceBookId` |
|-----------------------|---------------------------------------------------------------------|
| Invité (non connecté) | `websiteCode::sha1(0)`, où `0` est l’ID du groupe client invité |
| Client connecté | `websiteCode::sha1(customerGroupId)` |

L’en-tête de requête `Store` détermine la portée du site web et, par conséquent, le composant `websiteCode`. Le composant `sha1(customerGroupId)` correspond à la formule d’identifiant de catalogue des prix utilisée lors de la synchronisation des données. Voir [Prix des livres](reference/field-mapping.md#price-books).

## Produits groupés : format d’ajout au panier {#bundle-products-add-to-cart-format}

Autorisez les acheteurs à ajouter des produits groupés au panier à partir d’une vitrine découplée avec uniquement les `SKU` et `qty` pour chaque option de bundle sélectionnée.

Chaque valeur d’option sélectionnée ou saisie doit être codée en base64 au format suivant :

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

Le même SKU enfant peut apparaître une seule fois pour toutes les options.

Exemple ([!DNL JavaScript]) :

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
