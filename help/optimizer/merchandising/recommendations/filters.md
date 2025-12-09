---
title: Filtres de recommandation
description: Découvrez comment utiliser des filtres pour contrôler quels produits apparaissent dans les recommandations  [!DNL Adobe Commerce Optimizer] .
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: f6100538-23c0-4e90-9834-a895d4707282
source-git-commit: 032a19183b79cea1bfe27e8a4e20c60ba5ac6b8b
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Filtrer les produits

[!DNL Adobe Commerce Optimizer] applique automatiquement des filtres par défaut non configurables aux unités de recommandation. Si plusieurs unités de recommandation sont déployées sur une page, [!DNL Adobe Commerce Optimizer] filtre tous les produits qui se répètent dans les unités. Seule la première référence à un produit répété est utilisée, afin de laisser de la place à d’autres produits à recommander. [!DNL Adobe Commerce Optimizer] filtre également tous les produits achetés précédemment et ceux qui se trouvent dans le panier.

Lorsque vous [créez](create.md) une unité de recommandation, vous pouvez définir des filtres qui contrôlent les produits pouvant être affichés dans les recommandations. Ces filtres sont basés sur un ensemble de conditions d’inclusion ou d’exclusion que vous définissez. Seuls les produits qui correspondent à toutes les conditions d’inclusion apparaissent dans les recommandations. Les produits qui correspondent à l’une des conditions d’exclusion ne sont pas recommandés.

Vous pouvez configurer plusieurs filtres et n’activer que ceux de votre choix en cliquant sur le bouton (bascule) de chaque page de filtre. Vous pouvez ainsi créer des brouillons de filtres pour une utilisation ultérieure. Le nombre de filtres activés s’affiche sur chaque onglet.

## Conditions

Les conditions peuvent être statiques ou dynamiques.

- Une condition statique utilise des attributs de produit existants pour déterminer quels produits peuvent apparaître dans l’unité. Par exemple, vous pouvez spécifier que seuls les produits en stock dont le prix est supérieur à 25 $ apparaissent dans l’unité.

- Condition dynamique clé du contexte actuel d’un acheteur, tel que la catégorie ou le produit actuellement consulté. Par exemple, lors de la création d’une recommandation de produit à déployer sur les pages de détails du produit, vous pouvez créer une condition pour recommander uniquement des produits qui se trouvent dans une plage de prix relative du produit actuellement consulté.

### Opérateurs logiques

Les opérateurs logiques `AND` et `OR` sont utilisés pour joindre plusieurs conditions. Si vous utilisez à la fois des filtres d’inclusion et d’exclusion, les inclusions sont d’abord évaluées afin de déterminer tous les produits possibles qui peuvent être recommandés, puis les produits qui correspondent à n’importe quel filtre d’exclusion sont supprimés de la liste.

- `AND` - Rejoint deux conditions de filtrage des inclusions
- `OR` - Rejoint deux conditions de filtrage des exclusions

## Types de filtres

![&#x200B; Filtres &#x200B;](../../assets/rec-conditions.png)

### Produit

Les filtres de produit indiquent les produits spécifiques éligibles ou non éligibles à afficher dans les recommandations. Vous ne pouvez pas sélectionner de produits désactivés ou non visibles individuellement, car ces produits ne peuvent jamais apparaître dans les recommandations.

>[!NOTE]
>
>Les produits enfants d’un produit configurable ne sont pas affichés dans une unité de recommandation, car ces produits enfants ont la visibilité de _Non visible individuellement_.

<!--### Price

A filter based on the product price uses the final price to perform the comparison. The final price includes any discounts or special pricing available to anonymous shoppers.

### Attribute

You can filter products based on attribute criteria, including attribute values. Selected values use OR logic to either include or exclude products when any of the specified values are found.-->
