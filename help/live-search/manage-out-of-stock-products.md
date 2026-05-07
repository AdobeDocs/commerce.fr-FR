---
title: Gestion des produits en rupture de stock dans  [!DNL Live Search]
description: Découvrez comment gérer les produits en rupture de stock dans  [!DNL Live Search]  pour Adobe Commerce. Configurez l’affichage de l’inventaire, le filtre inStock et le filtrage de l’API GraphQL.
feature: Services, Search
role: Admin, Developer
level: Intermediate
source-git-commit: bc8f35434c9f01f1a920745fe42617df2003ca60
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Gestion des produits en rupture de stock

Vous pouvez contrôler l’affichage des produits en rupture de stock dans [!DNL Live Search] résultats de recherche et de catégorie à l’aide de la configuration de l’inventaire, des filtres de temps de requête et des indicateurs de fonctionnalité d’arrière-plan facultatifs. Ces options présentent des limites importantes, que cette rubrique explique.

## Filtres de statut des stocks

L’attribut Adobe Commerce stock `quantity_and_stock_status` n’est pas pris en charge sous la forme d’une facette et n’apparaît pas dans la boîte de dialogue **[!UICONTROL Add Facet]**. Cependant, [!DNL Live Search] expose un champ `inStock` que vous pouvez utiliser comme filtre au moment de la requête.

## Masquer les produits en rupture de stock

Utilisez l’une des méthodes suivantes pour masquer les produits en rupture de stock.

### Configuration de Commerce

1.Depuis l’*Admin*, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Catalog]**>**[!UICONTROL Inventory]**.

1.Set **[!UICONTROL Display Out of Stock Products]** to **[!UICONTROL No]**.

1. Cliquez sur **[!UICONTROL Save Config]**.

Lorsque **[!UICONTROL Display Out of Stock Products]** est défini sur `No`, [!DNL Live Search] ajoute des `inStock = 'no` aux requêtes de storefront via le widget PLP, de sorte que les produits en rupture de stock ne soient pas renvoyés.

### Filtre API

Lorsque vous appelez directement l’API [!DNL Live Search] (GraphQL ou REST), filtrez explicitement les produits en rupture de stock, par exemple :

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

Utilisez cette approche lorsque vous n’acheminez pas la requête via le [widget PLP de recherche en direct](plp-styling.md).

### Afficher les résultats en rupture de stock après stockage

Pour conserver les produits en rupture de stock dans le jeu de résultats, mais toujours après les produits en stock lors du tri par pertinence, Adobe peut activer un indicateur de fonctionnalité interne pour votre environnement.

- Cet indicateur de fonctionnalité n’est pas exposé dans l’interface utilisateur d’administration [!DNL Live Search].
- Pour en faire la demande, [contactez l’assistance Adobe](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"} et référencez la fonctionnalité afin de déplacer les produits en rupture de stock vers la fin des résultats de recherche.

>[!NOTE]
>
>Une fois l’indicateur activé, tous les produits en rupture de stock restants dans le jeu de résultats sont déplacés vers le bas lors du tri par *pertinence*. Les autres ordres de tri (par exemple, *Prix* ou *Nom du produit*) ne sont pas affectés.

### Rechercher des règles de marchandisage et des stocks

Les règles de marchandisage de recherche sont basées sur des requêtes et ciblent des produits individuels, et non des groupes entiers par état de stock ou valeur de facette :

- Les conditions de la règle dépendent uniquement de l’expression de recherche de l’acheteur (`Query is`, `Query contains`, `Query starts with`, `Query ends with`).
- Les événements de règle (amplification, enterrement, épingle, masquage) s’appliquent à un SKU par événement.

En raison de ces contraintes :

- Vous ne pouvez pas créer de règle qui enterre ou masque tous les produits en rupture de stock en fonction de leur statut de stock uniquement.
- Vous pouvez masquer ou masquer manuellement des SKU spécifiques que vous ajoutez en tant qu’événements dans une règle (avec une limite de 50 règles et de 25 événements par règle).

Pour masquer ou modifier la priorité des produits en rupture de stock dans le catalogue, utilisez la configuration de l’inventaire et le filtre de `inStock` (et l’indicateur de fonctionnalité facultatif) décrits dans cette rubrique au lieu de rechercher des règles de marchandisage.

>[!MORELIKETHIS]
>
> - [Rechercher des règles de marchandisage](rules.md)
> - [Configurer les options globales d’Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/configuration)
