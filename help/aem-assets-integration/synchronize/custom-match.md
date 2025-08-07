---
title: Correspondance automatique personnalisée
description: Découvrez comment la correspondance automatique personnalisée est particulièrement utile pour les commerçants avec une logique de correspondance complexe ou ceux qui dépendent d’un système tiers qui ne peut pas renseigner de métadonnées dans AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: ff6affa5bcc4111e14054f3f6b3ce970619ca295
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 1%

---

# Correspondance automatique personnalisée

Si la stratégie de correspondance automatique par défaut (**correspondance automatique prête à l’emploi**) n’est pas alignée avec les besoins spécifiques de votre entreprise, sélectionnez l’option Correspondance personnalisée . Cette option prend en charge l’utilisation de [Adobe Developer App Builder](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) pour développer une application de correspondance personnalisée qui gère une logique de correspondance complexe, ou des ressources provenant d’un système tiers qui ne peut pas renseigner de métadonnées dans AEM Assets.

## Configuration de la correspondance automatique personnalisée

1. Dans l’Administration Commerce, accédez à **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Sélectionnez **[!UICONTROL Custom Matcher]** comme règle correspondante.

1. Lorsque vous sélectionnez cette règle de correspondance, Admin affiche des champs supplémentaires pour configurer les **points d’entrée** et les **paramètres d’authentification** nécessaires à la logique de correspondance personnalisée.

## Points d’entrée de l’API de correspondance personnalisés

Lorsque vous créez une application de correspondance personnalisée à l’aide d’[App Builder](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, l’application doit exposer les points d’entrée suivants :

* **Ressource App Builder vers l’URL du produit** point d’entrée
* **Point d’entrée du produit App Builder vers l’URL de la ressource**

### Ressource App Builder vers le point d’entrée de l’URL du produit

Ce point d’entrée récupère la liste des SKU associés à une ressource donnée :

#### Exemple d’utilisation

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Requête**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `assetId` | String | Représente l’ID de ressource mis à jour |
| `eventData` | String | Renvoie la payload des données associée à la `assetId` |

**Réponse**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### Produit App Builder vers le point d’entrée de l’URL de la ressource

Ce point d’entrée récupère la liste des ressources associées à un SKU donné :

#### Exemple d’utilisation

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Requête**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `productSKU` | String | Représente le SKU de produit mis à jour. |
| `asset_matches` | String | Renvoie toutes les ressources associées à un `productSku` spécifique. |

Le paramètre `asset_matches` contient les attributs suivants :

| Attribut | Type de données | Description |
| --- | --- | --- |
| `asset_id` | String | Représente l’ID de ressource mis à jour. |
| `asset_roles` | String | Renvoie tous les rôles de ressources disponibles. Utilise les [rôles de ressources Commerce pris en charge](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) tels que `thumbnail`, `image`, `small_image` et `swatch_image`. |
| `asset_format` | String | Fournit les formats disponibles pour la ressource. Les valeurs possibles sont `image` et `video`. |
| `asset_position` | String | Affiche la position de la ressource. |

**Réponse**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```
