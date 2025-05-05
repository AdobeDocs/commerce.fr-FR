---
title: '[!DNL Product Recommendations] Workspace'
description: Découvrez comment configurer, gérer et surveiller les performances des recommandations de produits.
exl-id: eaf1f0b2-9d9d-4069-8269-06f30166f788
source-git-commit: 3d92f4afc3aef990f2e86e306f4c6c47324aed97
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 0%

---

# [!DNL Product Recommendations] Workspace

L’espace de travail [!DNL Product Recommendations] affiche une liste de recommandations précédemment configurées avec des mesures qui vous aident à suivre le succès de chaque recommandation. La liste peut être configurée pour calculer les mesures du dernier jour, de la dernière semaine ou du dernier mois. Vous pouvez utiliser les mesures pour créer des informations exploitables en fonction de la fréquence d’affichage ou de clic sur une unité de recommandation, ou pour analyser les performances de vos recommandations.

>[!INFO]
>
>Une unité de recommandation est un widget qui contient les _éléments_ de produit recommandés.

![Espace de travail Recommendations](assets/workspace.png)
_Workspace Recommendations_

## Collecte de données

Pour vous assurer que chaque domaine fonctionnel de l’espace de travail contient les données correctes, vous devez configurer la collecte de données en fonction de l’implémentation de storefront sélectionnée :

1. Luma - La collecte de données est disponible par défaut.
1. Découplé - La collecte de données doit être configurée manuellement, en fonction de l’implémentation du storefront.

Si vous utilisez un storefront découplé, reportez-vous à la documentation suivante pour obtenir plus d’informations sur les événements requis à ajouter :

- [Événements requis](events.md) pour le tableau de bord des recommandations de produits.
- [collecteur d’événements Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) qui doit être ajouté comme condition préalable.
- [Exemples](https://github.com/adobe/commerce-events/tree/main/examples) de la structure des événements.

## Définir la portée

Au départ, la [portée](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=fr) de tous les paramètres de recommandation est définie sur `Default Store View`. Si votre installation de Commerce comprend plusieurs vues de magasin, définissez **Portée** sur la vue de [magasin](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=fr#scope-settings) où vos recommandations s’appliquent.

## Définition de la période des mesures

1. Cliquez sur le contrôle **Calendrier** ![Sélecteur de calendrier](assets/icon-calendar.png).

1. Choisissez l’une des options suivantes :

   - Dernières 24 heures
   - 7 derniers jours
   - 30 derniers jours

   Les valeurs calculées dans les colonnes des mesures changent pour refléter la période actuelle.

   >[!NOTE]
   >
   >Les mesures de recommandations de produits sont optimisées pour les storefronts Luma. Si votre storefront n’est pas basé sur Luma, la manière dont les mesures effectuent le suivi des données dépend de la manière dont vous [implémentez la collecte d’événements](events.md).

## Afficher/masquer les colonnes

1. Dans le coin supérieur gauche, cliquez sur **Afficher/masquer** ![Sélecteur de colonne](assets/icon-show-hide-columns.png) colonnes.

   Les colonnes visibles comportent une coche bleue.

1. Dans le menu, effectuez l’une des opérations suivantes :

   - Pour afficher une colonne masquée, cliquez sur un nom de colonne sans coche.
   - Pour masquer une colonne visible, cliquez sur un nom de colonne avec une coche.

   Le tableau est actualisé pour n’inclure que les colonnes sélectionnées.

   ![Espace de travail Recommendations](assets/workspace-select-columns.png)
   _Afficher/masquer les colonnes_

## Paramètres

Les paramètres déterminent l’espace de données SaaS qui fournit les données comportementales de recommandation.

- Pour modifier l’origine des données comportementales de recommandation, choisissez un autre espace de données SaaS.

- Pour configurer un nouvel espace de données SaaS, cliquez sur **Modifier la configuration**. Pour en savoir plus, voir [Paramètres](settings.md).

![Paramètres Recommendations](assets/settings.png)
_Paramètres Recommendations_

## Afficher les détails

1. Dans le tableau, cliquez sur la recommandation à examiner.

   ![Espace de travail Recommendations](assets/recommendation-detail.png)
   _Détails sur le taux de conversion de la page d’accueil_

1. Pour modifier le statut de la recommandation, cliquez sur **Activer** ou **Désactiver**.

## Modifier la recommandation

Sur la page Détails de la recommandation, cliquez sur **Modifier**. Pour en savoir plus, rendez-vous sur [Modifier les recommandations](edit.md).

## Créer une recommandation

Sur la page Détails de la recommandation, cliquez sur **Créer**. Pour en savoir plus, rendez-vous sur [Créer des recommandations](create.md).

## Contrôles Workspace

| Contrôle | Description |
|---|---|
| ![ Sélecteur de calendrier ](assets/icon-calendar.png) | Détermine la période utilisée pour les calculs des mesures. Options : 24 heures / 7 jours / 30 jours |
| ![Sélecteur de colonnes](assets/icon-show-hide-columns.png) | Détermine les colonnes qui apparaissent dans le tableau [!DNL Product Recommendations]. |
| Paramètres | Détermine l’espace de données SaaS où sont récupérées les données comportementales de recommandation et active également le type de recommandation de similarité visuelle. |
| Créer une recommandation | Ouvre la page [ Créer une recommandation ](create.md). |

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
