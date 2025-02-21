---
title: Modifier la recommandation
description: Découvrez comment modifier une recommandation de produit.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Modifier la recommandation

La page Modifier la recommandation vous permet d’ajuster les paramètres individuels qui constituent la recommandation. Tous les paramètres peuvent être modifiés, à l’exception du type de page et du type de recommandation. Les paramètres suivants peuvent être modifiés :

- [Nom de la recommandation](#name)
- [Libellé du storefront](#label)
- [Nombre de produits](#number)
- [Emplacement et position](#placement)
- [Filtrer les produits](#filters)

L’aperçu sur le côté droit de la page montre comment la recommandation avec les paramètres actuels peut apparaître dans le storefront. L’aperçu _Produits recommandés_ reste visible à titre de référence lorsque vous faites défiler la page vers le bas. L’aperçu affiche une image miniature du produit, le nom du produit, le SKU, le prix et le type de résultat pour chaque produit renvoyé. Le type de résultat indique s’il existe suffisamment de données comportementales principales pour générer la recommandation ou s’il utilise des données comportementales de sauvegarde.

![Modifier les recommandations](assets/edit-recommendation.png)

## Modification d’une recommandation

1. Dans la barre latérale _Admin_, accédez à **Marketing** > _Promotions_ > **Recommandations de produits**.

1. Sélectionnez la recommandation à modifier.

1. Cliquez sur **Modifier**. Suivez ensuite les instructions ci-dessous pour apporter les modifications dont vous avez besoin.

1. Une fois l’opération terminée, cliquez sur **Enregistrer les modifications**.

### Nom de la recommandation {#name}

Choisissez un nom explicite qui indique l’objectif de la recommandation. Le nom est destiné à une référence interne et n’apparaît pas dans le storefront.

![Modifier le nom](assets/edit-name.png)

### Libellé du storefront {#label}

Saisissez le texte à utiliser comme libellé pour l’unité de recommandation dans le storefront.

![Modifier le libellé](assets/edit-storefront-label.png)

### Nombre de produits {#number}

Réglez le curseur pour afficher jusqu’à 20 produits dans l’unité de recommandation.

![Modifier le nombre de produits](assets/edit-number-of-products.png)

### Emplacement et position {#placement}

1. Choisissez l’emplacement de la page où l’unité de recommandation doit apparaître dans le storefront.

   - En bas du contenu principal
   - En haut du contenu principal

   ![Modifier l’emplacement](assets/edit-placement.png)

1. Pour modifier l’ordre des recommandations incluses dans l’unité, utilisez la commande **Déplacer** ![Déplacer](assets/icon-move.png) pour faire glisser les recommandations en position.

   ![Modifier la position](assets/edit-position.png)

### Filtrer les produits {#filters}

Toutes les modifications apportées au produit [filtres](filters.md) sont répercutées dans l’_aperçu des produits recommandés_. Seuls les produits correspondant aux filtres d’inclusion peuvent être recommandés. Les produits qui correspondent à des filtres d’exclusion ne sont pas recommandés.

Les onglets _Inclusions_ et _Exclusions_ répertorient les filtres disponibles de chaque type. Dans la liste, chaque filtre actif est marqué d’un point bleu.

- Pour afficher les détails de chaque filtre, cliquez sur son nom.
- Pour modifier le statut du filtre, définissez le bouton bascule **Activer le filtre** sur la position `on` ou `off`.

![Modifier les filtres](assets/edit-filters.png)

Les paramètres de filtre décrivent les produits à inclure ou à exclure dans l’unité de recommandation. Par exemple, les paramètres d’inclusion de filtre _Catégorie_ indiquent au système d’inclure uniquement les produits des catégories sélectionnées.

![Modifier le filtre de catégorie](assets/edit-filter-category.png)
