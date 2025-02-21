---
title: GraphQL
description: L’espace de travail  [!DNL Live Search] GraphQL vous permet de créer des requêtes avec vos données actives.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

L’espace de travail *GraphQL* permet aux administrateurs de créer et de tester des requêtes GraphQL à l’aide de leurs propres données.

Cet espace de travail prend en charge les requêtes [`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) et [`attributeMetadata`](https://developer.adobe.com/commerce/services/graphql/live-search/attribute-metadata/).

![Espace de travail GraphQL](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
		name
      }
    }
    facets {
      title
    }
  }
}
```

Variables :

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```

