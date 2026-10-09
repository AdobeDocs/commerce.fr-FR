---
title: Gestion des produits en rupture de stock dans [!DNL Live Search]
description: Découvrez comment gérer les produits en rupture de stock dans [!DNL Live Search] pour Adobe Commerce. Configurez l’affichage de l’inventaire, le filtre inStock et le filtrage de l’API GraphQL.
feature: Services, Search
role: Admin, Developer
level: Intermediate
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '451'
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
- Pour en faire la demande, [contactez l’assistance Adobe](https://experienceleague.adobe.com/fr/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide){target="_blank"} et référencez la fonctionnalité afin de déplacer les produits en rupture de stock vers la fin des résultats de recherche.

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
> - [Configurer les options globales d’Inventory management](https://experienceleague.adobe.com/fr/docs/commerce-admin/inventory/configuration/configuration)
