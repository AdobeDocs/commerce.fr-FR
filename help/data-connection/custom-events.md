---
title: Créer des événements personnalisés
description: Découvrez comment créer des événements personnalisés pour connecter vos données Adobe Commerce à d’autres produits Adobe DX.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 4e8cf0ad3f8f94d4f59bc8d78a44f4b3e86cbc3e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Créer des événements personnalisés

Vous pouvez étendre la [plateforme d’événements](events.md) en créant vos propres événements de storefront pour collecter des données propres à votre secteur d’activité. Lorsque vous créez et configurez un événement personnalisé, il est envoyé au [collecteur d’événements Adobe Commerce](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector).

## Gérer les événements personnalisés

Les événements personnalisés sont pris en charge pour le Adobe Experience Platform uniquement. Les données personnalisées ne sont pas transférées vers les tableaux de bord et les dispositifs de suivi des mesures d’Adobe Commerce.

Pour tout événement `custom`, le collecteur :

- Ajoute des `identityMap` avec `ECID` comme identité principale
- Inclut `email` dans `identityMap` comme identité secondaire _si_ `personalEmail.address` est défini dans l’événement
- Enveloppe l’événement complet dans un objet `xdm` avant le transfert vers Edge

Exemple :

Événement personnalisé publié via Adobe Commerce Events SDK :

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

Dans Experience Platform Edge :

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> L’utilisation d’événements personnalisés peut affecter les rapports Adobe Analytics par défaut.

## Gérer les remplacements d’événement (attributs personnalisés)

Pour tout événement défini avec un `customContext`, le collecteur remplace ou étend les champs de la payload d&#39;événement à partir des champs de la `custom context`. Le cas d’utilisation des remplacements se présente lorsqu’un développeur souhaite réutiliser et étendre des contextes définis par d’autres parties de la page dans des événements déjà pris en charge.

Les remplacements d’événement ne s’appliquent que lors du transfert vers Experience Platform. Elles ne sont pas appliquées aux événements d’analyse Adobe Commerce et Sensei. Le collecteur d’événements Adobe Commerce [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md) fournit des informations supplémentaires.

>[!NOTE]
>
>Lors de l’ajout d’attributs personnalisés aux `productListItems` dans les payloads d’événement Experience Platform, faites correspondre les produits en utilisant le SKU. Cette exigence ne s’applique pas aux événements `product-page-view`.

### Utilisation

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### Exemple 1

Cet exemple montre comment ajouter du contexte personnalisé lors de la publication de l’événement.

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### Exemple 2

Cet exemple montre comment ajouter du contexte personnalisé avant de publier l’événement.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### Exemple 3

Cet exemple définit le contexte personnalisé dans l’éditeur et remplace le contexte personnalisé précédemment défini dans la couche de données client Adobe.

Dans cet exemple, l’événement `pageView` aura **Nom de page personnalisé 2** dans le champ `web.webPageDetails.name`.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### Exemple 4

Cet exemple montre comment ajouter du contexte personnalisé aux événements `productListItems` avec plusieurs produits.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

Magasins basés sur Luma :

Les magasins Luma implémentent de manière native des événements de publication afin que vous puissiez définir des données personnalisées en étendant les `customContext`.

Par exemple :

```javascript
mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name'
    },
  },
});
```

>[!NOTE]
>
> Le remplacement des événements par des attributs personnalisés peut affecter les rapports Adobe Analytics par défaut.
