---
title: Correspondance automatique personnalisée
description: Découvrez comment la correspondance automatique personnalisée est particulièrement utile pour les commerçants avec une logique de correspondance complexe ou ceux qui dépendent d’un système tiers qui ne peut pas renseigner de métadonnées dans AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: dfc4aaf1f780eb4a57aa4b624325fa24e571017d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 1%

---

# Correspondance automatique personnalisée

Si la stratégie de correspondance automatique par défaut (**correspondance automatique prête à l’emploi**) n’est pas alignée avec les besoins spécifiques de votre entreprise, sélectionnez l’option Correspondance personnalisée . Cette option prend en charge l’utilisation de [Adobe Developer App Builder](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) pour développer une application de correspondance personnalisée qui gère une logique de correspondance complexe, ou des ressources provenant d’un système tiers qui ne peut pas renseigner de métadonnées dans AEM Assets.

## Configuration de la correspondance automatique personnalisée

1. Dans l’Administration Commerce, accédez à **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Sélectionnez **[!UICONTROL Custom Matcher]** comme règle correspondante.

1. Lorsque vous sélectionnez cette règle de correspondance, Admin affiche des champs supplémentaires pour configurer les **points d’entrée** et les **paramètres d’authentification** nécessaires à la logique de correspondance personnalisée.

### workspace.json

Le champ **[!UICONTROL Adobe I/O Workspace Configuration]** permet de configurer votre correspondant personnalisé de manière simplifiée en important votre fichier de configuration de `workspace.json` App Builder.

Vous pouvez télécharger le fichier `workspace.json` à partir de [Adobe Developer Console](https://developer.adobe.com/console). Le fichier contient toutes les informations d’identification et de configuration pour votre espace de travail App Builder.

+++Exemple de `workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. Effectuez un glisser-déposer de votre fichier `workspace.json` de votre projet App Builder vers le champ **[!UICONTROL Adobe I/O Workspace Configuration]** . Vous pouvez également cliquer sur pour parcourir et sélectionner le fichier.

![Configuration Workspace](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. Le système effectue automatiquement les opérations suivantes :

   * Valide la structure JSON.
   * Extrait et renseigne les informations d’identification OAuth
   * Récupère les actions d’exécution disponibles pour l’espace de travail
   * Remplit les options de liste déroulante pour les champs **[!UICONTROL Product to Asset URL]** et **[!UICONTROL Asset to Product URL]**

1. Sélectionnez les actions d’exécution appropriées dans les menus déroulants de chaque flux.

1. Cliquez sur **[!UICONTROL Save Config]**.

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
| `assetId` | String | Représente l’ID de ressource mis à jour. |
| `eventData` | String | Renvoie la payload de données associée à l’ID de ressource. |

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
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `productSKU` | String | Représente le SKU de produit mis à jour. |
| `eventData` | String | Renvoie la payload de données associée au SKU du produit. |

**Réponse**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"],
      "asset_position": 1,
      "asset_format": image
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
      "asset_position": 2,
      "asset_format": image     
    }
  ]
}
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `productSKU` | String | Représente le SKU de produit mis à jour. |
| `asset_matches` | String | Renvoie toutes les ressources associées à un SKU de produit spécifique. |

Le paramètre `asset_matches` contient les attributs suivants :

| Attribut | Type de données | Description |
| --- | --- | --- |
| `asset_id` | String | Représente l’ID de ressource mis à jour. |
| `asset_roles` | String | Renvoie tous les rôles de ressources disponibles. Utilise les [rôles de ressources Commerce pris en charge](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) tels que `thumbnail`, `image`, `small_image` et `swatch_image`. |
| `asset_format` | String | Fournit les formats disponibles pour la ressource. Les valeurs possibles sont `image` et `video`. |
| `asset_position` | String | Affiche la position de la ressource. |
