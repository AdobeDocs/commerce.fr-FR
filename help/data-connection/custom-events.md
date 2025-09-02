---
title: Créer des événements personnalisés
description: Découvrez comment créer des événements personnalisés pour connecter vos données Adobe Commerce à d’autres produits Adobe DX.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 81fbcde11da6f5d086c2b94daeffeec60a9fdbcc
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

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

Les remplacements d’attributs pour les événements standard sont pris en charge pour Experience Platform uniquement. Les données personnalisées ne sont pas transférées vers les tableaux de bord et les dispositifs de suivi des mesures de Commerce.

Pour tout événement avec `customContext`, le collecteur remplace les champs de jointure définis dans les contextes appropriés par des champs dans `customContext`. Le cas d’utilisation des remplacements se présente lorsqu’un développeur souhaite réutiliser et étendre des contextes définis par d’autres parties de la page dans des événements déjà pris en charge.

### Exemples

Vue de produit avec remplacements publiée via Adobe Commerce Events SDK :

```javascript
mse.publish.productPageView({
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

Dans Experience Platform Edge :

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

Magasins basés sur Luma :

Dans les magasins Luma, les événements de publication sont implémentés en mode natif. Par conséquent, vous pouvez définir des données personnalisées en étendant `customContext`.

Par exemple :

```javascript
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
```

Voir [remplacement d’événement personnalisé](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md) pour en savoir plus sur la gestion des données personnalisées.

>[!NOTE]
>
> Le remplacement des événements par des attributs personnalisés peut affecter les rapports Adobe Analytics par défaut.
