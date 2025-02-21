---
title: Afficher les prix taxés avec le maillage API
description: Utilisez  [!DNL API Mesh]  pour Adobe Commerce et Catalog Service pour afficher les prix, taxes comprises.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Afficher les prix taxés avec le maillage API pour Adobe Developer App Builder

Le [maillage API](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permet aux développeurs d’intégrer des API privées ou tierces et d’autres interfaces aux produits Adobe à l’aide de Adobe I/O Runtime.

Dans cette rubrique, le maillage API est utilisé pour afficher les prix des produits sur une page Détails du produit avec les taxes figurant dans .

## Configurer des taux de taxe

Les taxes doivent être configurées pour qu’elles s’affichent sur la page Détails du produit.

1. [Configurer des taux de taxe](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/taxes/tax-rules.html).
1. Activez l’affichage des taxes [dans le catalogue](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/taxes/display-settings.html#step-1%3A-configure-catalog-prices-display-settings) et définissez-les sur `Including and Excluding Tax` ou `Including Tax`.

Vérifiez que le service de catalogue fonctionne en consultant une page de détails du produit.

![Taxes affichées sur la page Détails du produit](assets/display-tax.png)

## Configurer le maillage API

Si ce n’est pas déjà fait, connectez le maillage API avec le service de catalogue à votre instance. Consultez les instructions détaillées dans la rubrique [Prise en main](https://developer.adobe.com/graphql-mesh-gateway/gateway/getting-started/) du guide de développement du maillage API.

Dans le fichier `mesh.json`, remplacez les valeurs `name `, `endpoint` et `x-api-key`.

```json
{
    "meshConfig": {
      "sources": [
        {
          "name": "<NAME OF MESH>",
          "handler": {
            "graphql": {
              "endpoint": "<COMMERCE INSTANCE GQL ENDPOINT URL>"
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
              "endpoint": "https://catalog-service-sandbox.adobe.io/graphql/",
              "operationHeaders": {
                "Magento-Store-View-Code": "{context.headers['magento-store-view-code']}",
                "Magento-Website-Code": "{context.headers['magento-website-code']}",
                "Magento-Store-Code": "{context.headers['magento-store-code']}",
                "Magento-Environment-Id": "{context.headers['magento-environment-id']}",
                "x-api-key": "API_KEY",
                "Magento-Customer-Group": "{context.headers['magento-customer-group']}"
              },
              "schemaHeaders": {
                "x-api-key": "<YOUR API_KEY>"
              }
            }
          }
        }
      ],
      "additionalTypeDefs": "extend type ComplexProductView {\n  priceWithTaxes: Core_PriceRange\n}\n extend type SimpleProductView {\n  priceWithTaxes: Core_PriceRange\n}\n",
      "additionalResolvers": [
            {  
              "targetTypeName": "ComplexProductView",
              "targetFieldName": "priceWithTaxes",
              "sourceName": "MagentoQACore",
              "sourceTypeName": "Query",
              "sourceFieldName": "Core_products",
              "requiredSelectionSet": "{\n items {\n sku, \n price_range {\n minimum_price {\n final_price {\n value\n currency\n }\n }\n }\n }\n }",
                "sourceArgs": {
                    "filter.sku.eq": "{root.sku}"
                },
                "result": "items[0].price_range"
            },
            {  
              "targetTypeName": "SimpleProductView",
              "targetFieldName": "priceWithTaxes",
              "sourceName": "MagentoQACore",
              "sourceTypeName": "Query",
              "sourceFieldName": "Core_products",
              "requiredSelectionSet": "{\n items {\n sku, \n price_range {\n minimum_price {\n final_price {\n value\n currency\n }\n }\n }\n }\n }",
                "sourceArgs": {
                    "filter.sku.eq": "{root.sku}"
                },
                "result": "items[0].price_range"
            }
        ]
     }
  }
```

Ce fichier de configuration `mesh.json` :

* Transforme l’application principale Commerce en exigeant « Core_ » précédé de l’une de ses requêtes ou de ses types. Cela empêche d’éventuels conflits de noms avec le service de catalogue.
* Étend les types `ComplexProductView` et `SimpleProductView` avec un nouveau champ appelé `priceWithTaxes`.
* Ajoute un programme de résolution personnalisé pour le nouveau champ.

Créez le maillage à l’aide de la commande [create](https://developer.adobe.com/graphql-mesh-gateway/gateway/create-mesh/#create-a-mesh-1) avec le fichier `mesh.json`.

### Requête GraphQL

Vous pouvez récupérer les nouvelles données `priceWithTaxes` à l’aide de GraphQL.

Exemple de requête :

```graphql
query {
    products(skus:[MH07]) {
        __typename
        id
        sku
        name
        description
        shortDescription
        addToCartAllowed
        url
        ... on ComplexProductView {
            priceWithTaxes {
              minimum_price {
                final_price {
                  value
                }
              }
              maximum_price {
                final_price {
                  value
                }
              }
            }
            priceRange {
                maximum {
                    final {
                        amount {
                            value
                            currency
                        }
                    }
                    regular {
                        amount {
                            value
                            currency
                        }
                    }
                    roles
                }
                minimum {
                    final {
                        amount {
                            value
                            currency
                        }
                    }
                    regular {
                        amount {
                            value
                            currency
                        }
                    }
                    roles
                }
            }
        }
    }
}
```

Réponse à la requête :

```json
{
  "data": {
    "products": [
      {
        "__typename": "ComplexProductView",
        "id": "VFVnd053AFpHVm1ZWFZzZEEAWkRWa09Ua3hNVFl0WTJJd015MDBaRGMwTFRnME16a3RNak01TVRVNE9ESTBOemd4AGJXRnBibDkzWldKemFYUmxYM04wYjNKbABZbUZ6WlEAVFVGSE1EQTFPRFEyTVRjeA",
        "sku": "MH07",
        "name": "Hero Hoodie13",
        "description": "<p>Gray and black color blocking sets you apart as the Hero Hoodie keeps you warm on the bus, campus or cold mean streets. Slanted outsize front pockets keep your style real . . . convenient.</p>\r\n<p>* Full-zip gray and black hoodie.<br />* Ribbed hem.<br />* Standard fit.<br />* Drawcord hood cinch.<br />* Water-resistant coating.</p>",
        "shortDescription": "",
        "addToCartAllowed": true,
        "url": "http://commerce_url/hero-hoodie.html",
        "priceWithTaxes": {
          "minimum_price": {
            "final_price": {
              "value": 8.330001
            }
          },
          "maximum_price": {
            "final_price": {
              "value": 13355.524701
            }
          }
        },
        "priceRange": {
          "maximum": {
            "final": {
              "amount": {
                "value": 39.02,
                "currency": "USD"
              }
            },
            "regular": {
              "amount": {
                "value": 54,
                "currency": "USD"
              }
            },
            "roles": [
              "visible"
            ]
          },
          "minimum": {
            "final": {
              "amount": {
                "value": 39.02,
                "currency": "USD"
              }
            },
            "regular": {
              "amount": {
                "value": 54,
                "currency": "USD"
              }
            },
            "roles": [
              "visible"
            ]
          }
        }
      }
    ]
  },
  "extensions": {}
}
```
