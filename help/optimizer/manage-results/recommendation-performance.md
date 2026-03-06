---
title: Performances de Recommendations
description: La page Performances de Recommendations fournit à insight des informations sur les performances de vos recommandations de produits.
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: 1b77e2ea-412b-4c78-9d38-390bd8fda87e
source-git-commit: 9cb231055df45bbfcff3303c6e1c257c883cb852
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 0%

---

# Performances de Recommendations

La page Performances des recommandations affiche une liste des recommandations configurées ainsi que des mesures clés pour vous aider à évaluer leur efficacité. Vous pouvez configurer la vue pour afficher les mesures du dernier jour, de la dernière semaine ou du dernier mois. Ces informations indiquent la fréquence à laquelle chaque unité de recommandation est consultée ou fait l’objet d’un clic, ce qui vous permet d’évaluer les performances et d’identifier les opportunités d’optimisation.

>[!INFO]
>
>Une unité de recommandation est un widget qui contient les _éléments_ de produit recommandés.

![Performances de Recommendations](../assets/rec-performance.png){zoomable="yes"}

## Affichage d’un rapport

1. Sélectionnez la **vue Catalogue**, par exemple *Toutes les vues* où vos recommandations s’appliquent.

   En savoir plus sur les [vues de catalogue](#select-catalog-view) dans Recommendations.

1. Cliquez sur le **[!UICONTROL Date Range]** et sélectionnez l’une des plages suivantes :

   ![Période des recommandations](../assets/rec-perf-date-range.png)

   Le tableau de recommandations est mis à jour pour afficher les mesures de cette période et de cette vue de catalogue.

## Personnaliser le tableau

1. Dans le coin supérieur gauche, cliquez sur l’icône ![Sélecteur de colonne](../assets/icon-show-hide-columns.png) pour personnaliser le tableau.

   Les colonnes visibles comportent une coche.

1. Dans le menu, effectuez l’une des opérations suivantes :

   - Pour afficher une colonne masquée, cliquez sur un nom de colonne sans coche.
   - Pour masquer une colonne visible, cliquez sur un nom de colonne avec une coche.

   Le tableau est actualisé pour n’inclure que les colonnes sélectionnées.

## Afficher les détails

1. Dans le tableau, cliquez sur l’icône (![Plus de sélecteur](../assets/btn-more.png)) en regard de la recommandation à examiner.

1. Pour modifier le statut de la recommandation, cliquez sur **Activer** ou **Désactiver**.

## Création ou gestion de recommandations

Découvrez comment [créer ou gérer une recommandation existante](../merchandising/recommendations/create.md).

## Contrôles Workspace

| Contrôle | Description |
|---|---|
| ![Période](../assets/rec-perf-date-range.png) | Détermine la période utilisée pour les calculs des mesures. |
| ![Sélecteur de colonnes](../assets/icon-show-hide-columns.png) | Détermine les colonnes qui apparaissent dans le tableau Recommendations. |
| Créer une recommandation | Ouvre la page [ Créer une recommandation ](../merchandising/recommendations/create.md). |
| [Vue Catalogue](#select-catalog-view) | Sélectionnez la vue de catalogue pour filtrer la table afin d’afficher uniquement les recommandations qui s’appliquent à la vue de catalogue sélectionnée. Cette sélection est également utilisée comme vue du catalogue lorsque vous [créez](../merchandising/recommendations/create.md) une recommandation. Les options sont *Toutes les vues* ou une [vue de catalogue](../setup/catalog-view.md) spécifique. |

## Descriptions des colonnes

| Colonne | Description |
|---|---|
| Nom | Nom de la recommandation. |
| Page | Page sur laquelle s’affiche la recommandation. |
| Type | Type de recommandation. |
| Statut | Statut de la recommandation. Options : Inactive/Active/Draft |
| Créé | Date de création de la recommandation. |
| Dernière édition | Date de la dernière modification de la recommandation. |
| Impressions | Nombre de fois qu’une unité de recommandation est chargée et rendue sur une page. Une unité de recommandation située sous le pli de la fenêtre d’affichage du navigateur est rendue sur la page, même si elle n’est pas consultée par l’acheteur. Dans ce cas, l’unité rendue est comptabilisée comme une impression, mais une vue n’est comptabilisée que si l’acheteur fait défiler l’unité vers la vue. |
| vImpressions | (Impressions visibles) Nombre d’unités de recommandation qui enregistrent au moins une vue. Par exemple, si l’unité de recommandation comporte deux lignes, chacune avec deux produits, et que les deux derniers produits ne sont pas vus par l’acheteur, mais que les deux premiers le sont, l’activité comptera toujours comme une impression. |
| Vues | Nombre d’unités de recommandation qui apparaissent dans la fenêtre du navigateur de l’acheteur. Si l’acheteur fait défiler la page vers le haut ou vers le bas plusieurs fois, l’événement se déclenche plusieurs fois, chaque fois que l’unité est visible. |
| Clics | Somme du nombre de fois où un acheteur clique sur un article dans l’unité de recommandation et du nombre de fois où l’acheteur clique sur le bouton **Ajouter au panier** dans l’unité de recommandation |
| Chiffre d’affaires | Chiffre d’affaires généré par la recommandation pour la période actuelle. |
| Lt Revenue | (Chiffre d’affaires cumulé sur toute la durée de vie) Chiffre d’affaires cumulé sur une recommandation. |
| Visibilité | Pourcentage d&#39;unités de recommandation qui s&#39;enregistrent pour la vue. |
| CTR | (Taux de clic publicitaire) Pourcentage d’impressions d’unité pour la recommandation qui enregistre un clic. Le CTR comptabilise toutes les impressions même si l’unité n’entre pas dans la vue de l’acheteur. Si l’unité de recommandation n’est pas consultée, il est peu probable qu’elle soit cliquée. Cependant, ces impressions invisibles sont prises en compte dans le score de RCT et réduisent le pourcentage de RCT global. |
| vCTR | (Taux de clic publicitaire visible) mesure les clics en fonction uniquement des impressions visibles (recommandations qui se sont en fait affichées dans la partie visible de l’écran de l’acheteur), offrant ainsi une mesure plus précise de l’engagement de l’acheteur. |

## Sélectionner la vue du catalogue

>[!IMPORTANT]
>
>Cette fonctionnalité est actuellement en version bêta.

Le sélecteur de **[!UICONTROL Catalog view]** de la page **Recommendations** effectue deux opérations :

1. **Filtre le tableau** - Affiche uniquement les recommandations (et leurs mesures) qui s’appliquent à la vue de catalogue sélectionnée.
1. **Définit la portée des nouvelles recommandations** - Lorsque vous [créez](../merchandising/recommendations/create.md) une recommandation, la vue de catalogue sélectionnée est utilisée comme portée de l’unité. Les options sont *Toutes les vues* ou une [vue de catalogue](../setup/catalog-view.md) spécifique.

   - **Toutes les vues** - La recommandation s’applique à toutes les vues de catalogue (la disponibilité du produit est toujours filtrée par vue).
   - **Vue Catalogue** - La recommandation s’applique uniquement à la vue de catalogue sélectionnée (par exemple, un storefront, une langue ou une marque).

En spécifiant une vue de catalogue pour chaque recommandation, vous pouvez :

- Configurez des recommandations pour toutes les vues de catalogue (globales) ou pour une vue de catalogue.
- Prévisualisez et filtrez les produits par vue de catalogue sur la page de recommandation [créer](../merchandising/recommendations/create.md).
- Afficher uniquement les produits disponibles pour chaque storefront.
- Affichage des mesures et du comportement du storefront par vue de catalogue.

### Filtrage des produits par la vue Catalogue

La disponibilité du produit est appliquée par vue de catalogue même pour les unités de recommandation sous la sélection **Toutes les vues**. Cette opération s’ajoute aux [filtres d’inclusion ou d’exclusion](../merchandising/recommendations/filters.md) définis sur l’unité de recommandation.

**Exemple : recommandation avec filtres d’inclusion sous la sélection Toutes les vues**

- **Toutes les vues** la recommandation inclut les SKU : SKU_ABC, SKU_CDE, SKU_XYZ.
- **Vue catalogue : Kingsbluff** ne peut pas vendre SKU_ABC ou SKU_CDE. **Affiché :** SKU_XYZ plus tout autre SKU valide pour Kingsbluff.
- **Vue catalogue : Arkbridge** ne peut vendre aucun des SKU inclus. **Affiché :** uniquement les SKU autorisés par Arkbridge. Si aucune unité de recommandation n’est disponible, elle n’apparaît pas sur ce storefront.
