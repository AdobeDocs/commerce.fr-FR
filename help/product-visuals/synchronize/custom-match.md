---
title: Correspondance automatique personnalisée
description: Découvrez comment la correspondance automatique personnalisée est particulièrement utile pour les commerçants avec une logique de correspondance complexe ou ceux qui dépendent d’un système tiers qui ne peut pas renseigner les métadonnées des visuels de produit dans AEM Assets.
feature: CMS, Media, Integration
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Correspondance automatique personnalisée

Si la stratégie de correspondance automatique par défaut (**correspondance automatique prête à l’emploi**) n’est pas alignée avec les besoins spécifiques de votre entreprise, sélectionnez l’option Correspondance personnalisée . Cette option prend en charge l’utilisation de [Adobe Developer App Builder](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) pour développer une application de correspondance personnalisée qui gère une logique de correspondance complexe, ou des ressources provenant d’un système tiers qui ne peut pas renseigner les métadonnées des visuels de produit dans AEM Assets.

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
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**Requête**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `assetId` | String | Représente l’ID de ressource mis à jour |

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
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**Requête**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `productSKU` | String | Représente le SKU de produit mis à jour |

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

>[!TIP]
>
> Dans la clé `asset_roles`, utilisez les rôles de ressources [Commerce pris en charge](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) tels que `thumbnail`, `image`, `small_image` et `swatch_image`.
