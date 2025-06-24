---
title: Synchronisation des données
description: Découvrez comment synchroniser vos données de catalogue avec  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 0%

---

# Synchronisation des données

La page **Synchronisation des données** présente un aperçu du statut de synchronisation des données de produit transférées de votre source de données (catalogue Commerce existant, système de gestion des informations produit (PIM), système de planification des ressources de l’entreprise (ERP), etc.) vers [!DNL Adobe Commerce Optimizer].

La page **Synchronisation des données** fournit des informations précieuses sur la disponibilité des données de produit pour votre storefront, en veillant à ce qu’elles puissent être rapidement affichées pour vos clients.

La page **Synchronisation des données** se trouve à l’emplacement *Configuration* > **Synchronisation des données**.

![Synchronisation des données](../assets/data-sync.png)

La page **Synchronisation des données** contient les champs suivants :

| Champ | Description |
|--- |--- |
| Source du catalogue | Paramètre régional spécifique pour les données synchronisées. |
| [!DNL Catalog Service] | Affiche la dernière mise à jour de synchronisation, le nombre total de produits reçus, un champ de recherche et un tableau des produits synchronisés pour [!DNL Catalog Service]. |
| Découverte de produits | Affiche la dernière mise à jour de synchronisation, le nombre total de produits reçus, un champ de recherche et un tableau des produits synchronisés pour la recherche. |
| Recommendations | Affiche la dernière mise à jour de synchronisation, le nombre total de produits reçus, un champ de recherche et un tableau des produits synchronisés pour Recommendations. |
| Produits reçus au cours des 3 dernières heures | Affiche le nombre de produits qui ont été transférés de la source du catalogue vers Adobe Commerce Optimizer au cours des trois dernières heures. Si vous effectuez des mises à jour peu fréquentes de votre catalogue, cette valeur est souvent égale à zéro. |
| Nombre total de produits dans le catalogue | Indique le nombre total de produits de catalogue disponibles pour Adobe Commerce Optimizer. |
| Produits synchronisés | Fournit des détails sur les produits synchronisés avec Adobe Commerce Optimizer. Par défaut, ce tableau est trié par « Dernière mise à jour ». Pour rechercher un produit spécifique, utilisez le champ **[!UICONTROL Search by Name or SKU]** . |

## Liste des produits synchronisés

Pour afficher les détails d’un produit synchronisé au format JSON, cliquez sur l’icône de code ![lien du code](../assets/data-sync-details.png) sur la ligne du produit dans le tableau des produits synchronisés.

![Détails du produit Syncd](../assets/synced-products.png)

## Resynchroniser les données du catalogue

Si vous ne voyez pas de produits spécifiques sur la page **Synchronisation des données**, vous devez lancer une resynchronisation à partir de votre système en amont. Gardez toutefois à l’esprit qu’une resynchronisation peut augmenter la charge sur les ressources matérielles. Néanmoins, une resynchronisation de votre catalogue peut être nécessaire dans les scénarios suivants :

- Lorsque des modifications importantes sont apportées à votre catalogue de produits, telles que l’ajout de nouveaux produits, la mise à jour des détails de produits ou la modification de catégories

- Si vous constatez des incohérences ou des problèmes de performances dans l’affichage des données de produits sur vos storefronts

>[!IMPORTANT]
>
>Le temps nécessaire à la synchronisation varie en fonction de la taille de votre catalogue et du volume de données mises à jour.
