---
title: Filtrer les produits
description: Définissez des conditions qui incluent ou excluent l’utilisation de produits comme recommandations.
exl-id: 140bf047-4f6a-48da-b536-d96e78ae3d17
source-git-commit: 59aa4ae67a1a8a853b72d78cd65a6cc44a6bc662
workflow-type: tm+mt
source-wordcount: '800'
ht-degree: 0%

---

# Filtrer les produits

Adobe Commerce applique automatiquement des filtres par défaut non configurables aux unités de recommandation. Si plusieurs unités de recommandation sont déployées sur une page, Adobe Commerce filtre tous les produits qui se répètent dans les unités. Seule la première référence à un produit répété est utilisée, afin de laisser de la place à d’autres produits à recommander. Adobe Commerce filtre également les produits achetés précédemment et ceux qui se trouvent dans le panier.

Lorsque vous [créez](create.md) une unité de recommandation, vous pouvez définir des filtres qui contrôlent les produits pouvant être affichés dans les recommandations. Ces filtres sont basés sur un ensemble de conditions d’inclusion ou d’exclusion que vous définissez. Seuls les produits qui correspondent à toutes les conditions d’inclusion apparaissent dans les recommandations. Les produits qui correspondent à l’une des conditions d’exclusion ne sont pas recommandés.

Vous pouvez configurer plusieurs filtres et n’activer que ceux de votre choix en cliquant sur le bouton (bascule) de chaque page de filtre. Vous pouvez ainsi créer des brouillons de filtres pour une utilisation ultérieure. Le nombre de filtres activés s’affiche sur chaque onglet.

## Conditions

Les conditions peuvent être statiques ou dynamiques.

- Une condition statique utilise des attributs de produit existants pour déterminer quels produits peuvent apparaître dans l’unité. Par exemple, vous pouvez spécifier que seuls les produits en stock dont le prix est supérieur à 25 $ apparaissent dans l’unité. Les conditions statiques sont disponibles sur tous les types de page.

- Condition dynamique clé du contexte actuel d’un acheteur, tel que la catégorie ou le produit actuellement consulté. Par exemple, lors de la création d’une recommandation de produit à déployer sur les pages de détails du produit, vous pouvez créer une condition pour recommander uniquement des produits qui se trouvent dans une plage de prix relative du produit actuellement consulté. Les conditions dynamiques sont disponibles sur chaque type de page, à l’exception de la page d’accueil, ainsi que sur les pages comportant des recommandations placées avec Page Builder.

### Opérateurs logiques

Les opérateurs logiques `AND` et `OR` sont utilisés pour joindre plusieurs conditions. Si vous utilisez à la fois des filtres d’inclusion et d’exclusion, les inclusions sont d’abord évaluées afin de déterminer tous les produits possibles qui peuvent être recommandés, puis les produits qui correspondent à n’importe quel filtre d’exclusion sont supprimés de la liste.

- `AND` - Rejoint deux conditions de filtrage des inclusions
- `OR` - Rejoint deux conditions de filtrage des exclusions

>[!NOTE]
>
> Les filtres d’inclusion et d’exclusion remplacent les exclusions de catégorie héritées des versions 3.2.2 et ultérieures du module `magento/product-recommendations`. Voir les [notes de mise à jour](release-notes.md) pour en savoir plus sur les versions d’Adobe Commerce.

## Types de filtres {#filtertypes}

![ Filtres ](assets/rec-conditions.png)

### Catégorie

[!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}

Filtre les produits selon leur catégorie. Le filtre de catégorie utilise des affectations de catégorie directes et leurs sous-catégories. Par exemple, l’activation d’une condition d’exclusion pour la catégorie `Gear` exclut les produits affectés à `Gear` et à toutes ses sous-catégories, telles que `Gear/Bags` ou `Gear/Fitness Equipment`. Il en va de même pour un filtre d’inclusion sur une catégorie. Par exemple, l’activation d’une condition d’inclusion pour la catégorie `Gear` inclut les produits affectés à `Gear` et à toutes ses sous-catégories, telles que `Gear/Bags` ou `Gear/Fitness Equipment`.

Le champ Catégorie affiche les catégories qui appartiennent à la boutique actuelle.

>[!NOTE]
>
>Pour les commerçants B2B, le filtre Catégorie adhère à toutes les [catégories de produits spécifiques aux clients](https://experienceleague.adobe.com/docs/commerce-admin/catalog/categories/category-permissions.html?lang=fr) que vous avez configurées.

Adobe Commerce vous recommande d’utiliser la configuration de filtre de catégorie suivante lorsque vous déployez des recommandations sur vos types de page :

| Page | Filtrer par |
|---|---|
| Accueil | Ne filtrez pas les produits. |
| Catégorie | Filtrez les produits dans la catégorie spécifique. |
| Détails du produit | Filtrez les produits appartenant aux mêmes catégories. |
| Panier | Filtrez les catégories de produits du panier. |
| Confirmation de commande | Filtrez les catégories de produits achetés. |

### Produit

Les filtres de produit indiquent les produits spécifiques éligibles ou non éligibles à afficher dans les recommandations. Vous ne pouvez pas sélectionner de produits désactivés ou non visibles individuellement, car ces produits ne peuvent jamais apparaître dans les recommandations.

>[!NOTE]
>
>Les produits enfants d’un produit configurable ne sont pas affichés dans une unité de recommandation, car ces produits enfants ont la visibilité de _Non visible individuellement_.

### Type

[!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}

Un filtre basé sur le type de produit inclut ou exclut tous les produits d’un type spécifique. Les types pris en charge sont les suivants : _simple_, _configurable_, _virtuel_, _téléchargeable_ ou _carte cadeau_. Les types de produits _Bundle_, _grouped_ et personnalisés ne sont pas pris en charge.

### Visibilité

[!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."}

Filtre les produits en fonction de leur visibilité, par exemple : _Catalogue_, _Recherche_ ou les deux.

### Prix

Un filtre basé sur le prix du produit utilise le prix final pour effectuer la comparaison. Le prix final inclut toutes les remises ou tous les tarifs spéciaux disponibles pour les acheteurs anonymes. Pour les commerçants B2B, le prix affiché reflète le [prix de groupe spécifique au client](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html?lang=fr) que vous avez configuré.

### Statut des stocks

Les filtres d’exclusion suivants peuvent être utilisés pour filtrer les produits en fonction du statut du stock :

- En rupture de stock - (Exclusion uniquement) Exclut les produits en rupture de stock.
- Faible en stock - (Exclusion uniquement) Exclut les produits peu en stock. Le statut de stock faible est basé sur la valeur _Seuil gauche X uniquement_ dans [Configuration du stock](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/inventory.html?lang=fr).
