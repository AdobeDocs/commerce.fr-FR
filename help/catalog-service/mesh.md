---
title: '[!DNL Catalog Service and API Mesh]'
description: '[!DNL API Mesh] pour Adobe Commerce permet d’intégrer plusieurs sources de données par le biais d’un point d’entrée GraphQL commun.'
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 903f4f96-6dba-4c45-8106-76d9845544ec
source-git-commit: ca0b2b2a158b9a376724b30c80a6bf9a60e3d1ba
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# [!DNL Catalog Service and API Mesh]

Le [maillage API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permet aux développeurs d’intégrer des API privées ou tierces et d’autres interfaces aux produits Adobe à l’aide de Adobe I/O Runtime.

![Diagramme d’architecture de catalogue](assets/catalog-service-architecture-mesh.png)

Pour utiliser le maillage API avec le service de catalogue, vous devez connecter le maillage API à votre instance, puis ajouter la source de maillage API [CommerceCatalogServiceGraph](https://github.com/adobe/api-mesh-sources/blob/main/connectors/) qui fournit la configuration pour la connexion au service de catalogue.

## Connectez-vous et configurez le maillage API.

1. Connectez le maillage API à votre instance Adobe Commerce en suivant les instructions de la section [Création d’un maillage](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/) du guide de développement du _maillage API_.

   Si c’est la première fois que vous utilisez le maillage API, suivez le processus [Prise en main](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/) avant de créer le maillage.

1. Créez un fichier JSON, tel que `variables.json` qui contient la clé API Catalog Service pour votre projet à l’aide du format suivant.

   ```json
   {
       "CATALOG_SERVICE_API_KEY":"your_api_key"
   }
   ```

1. Ajoutez la source `CommerceCatalogServiceGraph` à votre maillage à l’aide de l’[interface de ligne de commande Adobe I/O extensible](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/#install-the-aio-cli).

   ```bash
   aio api-mesh source install "CommerceCatalogServiceGraph" -f variables.json
   ```

   L’option `-f variables.json` fournit la valeur de clé API Catalog Service requise pour mettre à jour la configuration.

Après avoir exécuté cette commande, le service de catalogue doit s’exécuter via le maillage API. Utilisez la commande `aio api-mesh get` pour afficher la configuration du maillage mis à jour.

## Exemples de maillage API

Le maillage API permet aux utilisateurs de consommer des sources de données externes afin d’améliorer votre instance Adobe Commerce. Il peut également être utilisé pour configurer les données Commerce existantes afin d’activer une nouvelle fonctionnalité.

### Activer les prix de niveau

Dans cet exemple, le maillage API est utilisé pour activer les prix de niveau dans Adobe Commerce.
Remplacez les valeurs `name `, `endpoint` et `x-api-key`.

```json
{
  "meshConfig": {
    "sources": [
      {
        "name": "<Commerce Instance Name>",
        "handler": {
          "graphql": {
            "endpoint": "<Adobe Commerce GraphQL endpoint>"
          }
        },
        "transforms": [
            {
                "prefix": {
                    "includeRootOperations": true,
                    "value": "Core_"
                }
            }
        ]
      },
      {
        "name": "CommerceCatalogServiceGraph",
        "handler": {
          "graphql": {
            "endpoint": "https://commerce.adobe.io/catalog-service/graphql/",
            "operationHeaders": {
              "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
              "Magento-Website-Code": "{context.headers['magento-website-code']}",
              "Magento-Store-Code": "{context.headers['magento-store-code']}",
              "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
              "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
            },
            "schemaHeaders": {
              "x-api-key": "<YOUR API-KEY>"
            }
          }
        }
      }
    ],
    "additionalTypeDefs": "extend interface ProductView {\n  price_tiers: [Core_TierPrice]\n}\n extend type SimpleProductView {\n  price_tiers: [Core_TierPrice]\n}\n extend type ComplexProductView {\n  price_tiers: [Core_TierPrice]\n}\n",
    "additionalResolvers": [
        {  
            "targetTypeName": "ProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        },
        {  
            "targetTypeName": "SimpleProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        },
        {  
            "targetTypeName": "ComplexProductView",
            "targetFieldName": "price_tiers",
            "sourceName": "MagentoStageCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{\n    items {\n  sku\n    price_tiers {\n        quantity,\n        final_price {\n          value\n          currency\n        }\n      }\n    }\n  }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].price_tiers"
        }
    ]
   }
}
```

Une fois configuré, interrogez le maillage pour obtenir une tarification échelonnée :

```graphql
query {
  products(skus: ["24-MB04"]) {
    sku
    description
    price_tiers {
        quantity
        final_price {
          value
          currency
        }
      }
    ... on SimpleProductView {
      id
       
      price {
        final {
          amount {
            value
          }
        }
      }
    }
  }
}
```

### Obtenir un ID d’entité

Ce maillage ajoute le `entityId` à l’interface ProductView. Remplacez les valeurs `name `, `endpoint` et `x-api-key`.

```json
{
    "meshConfig": {
      "sources": [
        {
          "name": "<Commerce Instance Name>",
          "handler": {
            "graphql": {
              "endpoint": "<Adobe Commerce GraphQL endpoint>"
            }
          },
          "transforms": [
              {
                  "prefix": {
                      "includeRootOperations": true,
                        "value": "Core_"
                  }
              }
          ]
        },
        {
          "name": "CommerceCatalogServiceGraph",
          "handler": {
            "graphql": {
              "endpoint": "https://catalog-service.adobe.io/graphql",
              "operationHeaders": {
                "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
                "Magento-Website-Code": "{context.headers['magento-website-code']}",
                "Magento-Store-Code": "{context.headers['magento-store-code']}",
                "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
                "x-api-key": "<YOUR_CATALOG_SERVICE_API_KEY>",
                "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
              },
              "schemaHeaders": {
                "x-api-key": "<YOUR_CATALOG_SERVICE_API_KEY>"
              }
            }
          }
        }
      ],
      "additionalTypeDefs": "extend interface ProductView {\n  entityId: String\n}\n extend type SimpleProductView {\n  entityId: String\n}\n extend type ComplexProductView {\n  entityId: String\n}\n",
      "additionalResolvers": [
        {  
            "targetTypeName": "ComplexProductView",
            "targetFieldName": "entityId",
            "sourceName": "MagentoCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{ sku\n }",
            "sourceSelectionSet": "{\n    items {\n  sku\n uid\n  }\n    }",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].uid",
            "resultType": "String"
          },
          {
            "targetTypeName": "SimpleProductView",
            "targetFieldName": "entityId",
            "sourceName": "MagentoCore",
            "sourceTypeName": "Query",
            "sourceFieldName": "Core_products",
            "requiredSelectionSet": "{ sku\n }",
            "sourceSelectionSet": "{\n items {\n  sku\n uid\n }}",
            "sourceArgs": {
                "filter.sku.eq": "{root.sku}"
            },
            "result": "items[0].uid",
            "resultType": "String"
          }
      ]
    }
  }
```

`entityId` peut maintenant être interrogé :

```graphql
query {
  products(skus: ["MH07"]){
    sku
    name
    id
    entityId
  }
}
```
