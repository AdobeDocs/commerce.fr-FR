---
title: Correspondance automatique personnalisée
description: Découvrez comment la correspondance automatique personnalisée est particulièrement utile pour les commerçants avec une logique de correspondance complexe ou ceux qui dépendent d’un système tiers qui ne peut pas renseigner de métadonnées dans AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
TQID: https://experienceleague.adobe.com/RHRfW99iShMpajrEC8BhvoMEfQ-ABdipWTCdK-KaVH4
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7ecedcc7c17abdeb64507d8f74ec6fc103b361cc
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%
---
# Correspondance automatique personnalisée

Si la stratégie de correspondance automatique par défaut (**correspondance automatique prête à l’emploi**) n’est pas alignée avec les besoins spécifiques de votre entreprise, sélectionnez l’option Correspondance personnalisée . Cette option prend en charge l’utilisation de [&#128279;](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder) pour développer une application de correspondance personnalisée qui gère une logique de correspondance complexe, ou des ressources provenant d’un système tiers qui ne peut pas renseigner de métadonnées dans AEM Assets.

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

![Configuration &#x200B;](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. Le système effectue automatiquement les opérations suivantes :

   * Valide la structure JSON.
   * Extrait et renseigne les informations d’identification OAuth
   * Récupère les actions d’exécution disponibles pour l’espace de travail
   * Remplit les options de liste déroulante pour les champs **[!UICONTROL Product to Asset URL]** et **[!UICONTROL Asset to Product URL]**

1. Sélectionnez les actions d’exécution appropriées dans les menus déroulants de chaque flux.

1. Cliquez sur **[!UICONTROL Save Config]**.

## Enregistrement de la configuration asynchrone

Si l’option [Enregistrer la configuration asynchrone](https://experienceleague.adobe.com/en/docs/commerce-operations/performance-best-practices/configuration#asynchronous-configuration-save) est activée pour votre instance Commerce, les modifications de configuration sont mises en file d’attente et appliquées par un client asynchrone au lieu d’être enregistrées immédiatement dans la même requête. Pour charger un fichier `workspace.json` pour la correspondance automatique personnalisée dans ce mode, effectuez les étapes suivantes dans l’ordre :

1. Vérifiez que l’enregistrement de la configuration asynchrone de Commerce est [&#x200B; activé](https://experienceleague.adobe.com/en/docs/commerce-operations/performance-best-practices/configuration#asynchronous-configuration-save).

1. Dans l’administration, accédez à **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**.

1. Chargez le fichier App Builder `workspace.json` actuel.

1. Enregistrez la configuration.

1. Attendez que le client de configuration asynchrone termine de traiter l’enregistrement.

1. Vérifiez les valeurs OAuth et la configuration de l’intégration dépendante.

1. Vérifiez que l&#39;enregistrement du correspondant externe reflète la mise à jour.

>[!NOTE]
>
>Si l’option Enregistrement de la configuration asynchrone est désactivée, le comportement d’enregistrement synchrone normal s’applique et vous n’avez pas besoin d’attendre un client de file d’attente.

### Résolution des problèmes liés à l’enregistrement de la configuration asynchrone

| Symptôme | Que faire |
| --- | --- |
| Les valeurs OAuth restent inchangées après enregistrement | Vérifiez que vous exécutez la version 1.4.7 ou une version ultérieure de l’extension AEM Assets Integration, chargez un nouveau fichier `workspace.json` et attendez la fin du traitement de la file d’attente avant de vérifier à nouveau les valeurs. |
| L’enregistrement échoue après un chargement non valide | Vérifiez que le fichier est un fichier `workspace.json` bien formé et qu’il contient les informations d’identification App Builder attendues. |
| Aucun fichier n&#39;a été chargé | La configuration stockée existante reste inchangée. |
| L’enregistrement du mappeur externe n’est pas mis à jour | Vérifiez si le client de la file d’attente a terminé le traitement, consultez les journaux Commerce et confirmez le statut d’enregistrement du mappeur externe. |
| L&#39;enregistrement de la configuration asynchrone est désactivé | Le comportement normal d’enregistrement synchrone s’applique ; cette section de dépannage ne s’applique pas. |

>[!NOTE]
>
>Si vous développez un observateur de configuration pour l’intégration AEM Assets, ne dépendez pas des paramètres de requête HTTP bruts. L’enregistrement de la configuration asynchrone et d’autres enregistrements de configuration par programmation peuvent exécuter l’observateur sans contexte de requête d’administration.

## Points d’entrée de l’API de correspondance personnalisés

Lorsque vous créez une application de correspondance personnalisée à l’aide d’[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, l’application doit exposer les points d’entrée suivants :

* **Ressource App Builder vers l’URL du produit** point d’entrée
* **Point d’entrée du produit App Builder vers l’URL de la ressource**

### Ressource App Builder vers le point d’entrée de l’URL du produit

Ce point d’entrée récupère la liste des SKU associés à une ressource donnée :

#### Exemple d’utilisation

```javascript
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

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**Requête**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `assetId` | String | Représente l’ID de ressource mis à jour. |
| `eventData` | Objet | Payload d’événement associée à la ressource (par exemple, métadonnées de ressource que le mappeur lit dans `eventData.assetMetadata`). |

**Réponse**

```json
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail", "image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ],
  "skip": false
}
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `asset_id` | String | Identifiant de ressource correspondant. |
| `product_matches` | Tableau | Liste des produits associés à la ressource. |
| `skip` | Booléen | (Facultatif) Lorsqu’il est `true`, le moteur de règle ignore la synchronisation pour cette ressource (aucune mise à jour du mappage de produits). Lorsqu’il est `false` ou omis, le traitement normal s’exécute. Voir [Ignorer le traitement de la synchronisation](#skip-sync-processing). |

### Produit App Builder vers le point d’entrée de l’URL de la ressource

Ce point d’entrée récupère la liste des ressources associées à un SKU donné :

#### Exemple d’utilisation

```javascript
const { Core } = require('@adobe/aio-sdk')

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    // Set skip to true if the mapping hasn't changed
    const skipSync = false;

    return {
        statusCode: 200,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ],
            skip: skipSync
        }
    };
}

exports.main = main;
```

**Requête**

```text
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `productSku` | String | Représente le SKU de produit mis à jour. |
| `eventData` | Objet | Payload de l’événement associée au produit (par exemple, champs que le mappeur utilise à partir de l’événement entrant). |

**Réponse**

```json
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail", "image"],
      "asset_position": 1,
      "asset_format": "image"
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"],
      "asset_position": 2,
      "asset_format": "image"
    }
  ],
  "skip": false
}
```

| Paramètre | Type de données | Description |
| --- | --- | --- |
| `product_sku` | String | SKU du produit correspondant. |
| `asset_matches` | Tableau | Liste des ressources associées au produit. |
| `skip` | Booléen | (Facultatif) Lorsqu’il est `true`, le moteur de règles ignore la synchronisation pour ce produit (aucune mise à jour du mappage des ressources). Lorsqu’il est `false` ou omis, le traitement normal s’exécute. Voir [Ignorer le traitement de la synchronisation](#skip-sync-processing). |

Le paramètre `asset_matches` contient les attributs suivants :

| Attribut | Type de données | Description |
| --- | --- | --- |
| `asset_id` | String | Identifiant de la ressource. |
| `asset_roles` | Tableau | Rôles de ressources. Utilise les [rôles de ressources Commerce pris en charge](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) tels que `thumbnail`, `image`, `small_image` et `swatch_image`. Avec AEM Assets Integration extension 1.4.6 et versions ultérieures, les rôles d’image personnalisés (tels que `hero` ou `custom_role_1`) sont également acceptés. |
| `asset_format` | String | Format de la ressource. Les valeurs possibles sont `image` et `video`. |
| `asset_position` | Nombre | Position de la ressource dans la galerie de produits. |

## Ignorer le traitement de la synchronisation

Le paramètre `skip` permet à votre mappeur personnalisé de contourner le traitement de synchronisation pour des ressources ou des produits spécifiques.

Lorsque votre application App Builder renvoie des `"skip": true` dans la réponse, le moteur de règle n’envoie pas de requêtes de mise à jour ou de suppression d’API à Commerce pour cette ressource ou ce produit. Cette optimisation réduit les appels d’API inutiles et améliore les performances.
