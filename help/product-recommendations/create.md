---
title: Créer une recommandation
description: Découvrez comment créer une unité de recommandation de produit.
exl-id: 1d5f83c4-1613-4236-9d98-d455f45a47da
TQID: https://experienceleague.adobe.com/K3cKFg-m22bUzlupyhsHgDVxaJka7xhOvFnOt8wDdII
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 1491
ht-degree: 0%

---

# Créer une recommandation

Lorsque vous créez une recommandation, vous créez une _unité de recommandation_, ou widget, qui contient les _éléments_ de produit recommandés.

![Unité de recommandation](assets/unit.png)
_Unité de recommandation_

Lorsque vous activez l’unité de recommandation, Adobe Commerce commence à [collecter des données](workspace.md) pour mesurer les impressions, les vues, les clics, etc. Le tableau [!DNL Product Recommendations] affiche les mesures de chaque unité de recommandation afin de vous aider à prendre des décisions commerciales éclairées.

>[!NOTE]
>
>Les mesures de recommandations de produits sont optimisées pour les storefronts Luma. Si votre storefront n’est pas basé sur Luma, la manière dont les mesures effectuent le suivi des données dépend de la manière dont vous [implémentez la collecte d’événements](events.md).

1. Dans la barre latérale _Admin_, accédez à **Marketing** > _Promotions_ > **Recommandations de produit** pour afficher l’espace de travail _Recommandations de produit_.

1. Spécifiez l’[Affichage de la boutique](https://experienceleague.adobe.com/en/docs/commerce-admin/start/setup/websites-stores-views) où vous souhaitez que les recommandations s’affichent.

   >[!NOTE]
   >
   > Les unités de recommandation Page Builder doivent être créées dans la vue de magasin par défaut, mais peuvent ensuite être utilisées n’importe où. Pour en savoir plus sur la création de recommandations de produit avec Page Builder, voir [Ajouter du contenu - Recommandations de produit](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations).

1. Cliquez sur **Créer une recommandation**.

1. Dans la section _Nommer votre recommandation_, saisissez un nom explicite à des fins de référence interne, tel que `Home page most popular`.

1. Dans la section _Sélectionner le type de page_, sélectionnez la page sur laquelle vous souhaitez que la recommandation apparaisse parmi les options suivantes :

   >[!NOTE]
   >
   > Les recommandations de produits ne sont pas prises en charge sur la page Panier lorsque votre boutique est configurée pour [afficher la page du panier immédiatement après l’ajout d’un produit au panier](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration).

   * Page d’accueil
   * Catégorie
   * Détails du produit
   * Panier
   * Confirmation
   * [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations)

   Vous pouvez créer jusqu’à 50 unités de recommandation actives pour chaque type de page. Le type de page est grisé lorsque la limite est atteinte.

   ![Nom et page de la recommandation](assets/create-recommendation.png)
   _Nom de la recommandation et emplacement de la page_

1. Dans la section _Sélectionner le type de recommandation_, indiquez le [type de recommandation](type.md) qui doit apparaître sur la page sélectionnée. Pour certaines pages, l’[emplacement](placement.md) des recommandations est limité à certains types.

1. Dans la section _Étiquette d’affichage du storefront_, saisissez l’[étiquette](placement.md#recommendation-labels) visible par vos acheteurs, telle que « Meilleurs vendeurs ».

1. Dans la section _Choisir le nombre de produits_, utilisez le curseur pour indiquer le nombre de produits à afficher dans l’unité de recommandation.

   La valeur par défaut est `5`, avec un maximum de `20`.

1. Dans la section _Sélectionner l’emplacement_, indiquez l’emplacement où l’unité de recommandation doit apparaître sur la page.

   * En bas du contenu principal
   * En haut du contenu principal

1. (Facultatif) Pour modifier l’ordre des recommandations, sélectionnez et déplacez les lignes du tableau _Choisir la position_.

   La section _Choisir la position_ affiche toutes les recommandations (le cas échéant) créées pour le type de page que vous avez sélectionné.

   ![Ordre des recommandations](assets/create-recommendation-select-placement.png)
   _Ordre des recommandations sur la page_

1. (Facultatif) Pour contrôler quels produits apparaissent dans l’unité de recommandation, [appliquez des filtres](filters.md) dans la section _Filtres_.

   ![Filtres recommandés](assets/create-recommendation-filter-products.png)
   _Filtres de produit recommandés_

1. Une fois l’opération terminée, cliquez sur l’une des options suivantes :

   * **Enregistrer en tant que brouillon** pour modifier ultérieurement l’unité de recommandation. Vous ne pouvez pas modifier le type de page ou de recommandation d’une unité de recommandation à l’état de brouillon.

   * **Activer** pour activer l’unité de recommandation sur votre storefront.

>[!IMPORTANT]
>
>Certains navigateurs peuvent bloquer des scripts critiques qui empêchent le fonctionnement attendu de Product Recommendations.

## Indicateurs de préparation

Les indicateurs de préparation indiquent les types de recommandations les plus performants avec vos données de catalogue et comportementales disponibles. Utilisez-les pour identifier les problèmes d’événement ou le trafic insuffisant pour renseigner un type de recommandation.

Les indicateurs de préparation se répartissent en deux catégories : [basé sur statique](#static-based) et [basé sur dynamique](#dynamic-based). Les recommandations statiques utilisent uniquement des données de catalogue. Les recommandations dynamiques utilisent les données comportementales des acheteurs pour entraîner des modèles de machine learning, générer des recommandations personnalisées et calculer le score de préparation de chaque recommandation.

### Comment les indicateurs de préparation sont calculés

Les indicateurs de préparation sont une indication de la formation du modèle. Les indicateurs dépendent des types d’événements collectés, de l’ampleur des produits avec lesquels il y a eu interaction et de la taille du catalogue.

Le pourcentage d’indicateur de préparation estime la proportion de produits qui peuvent être recommandés pour un type de recommandation donné. Il est calculé à l’aide de la taille du catalogue, du volume d’interaction et du pourcentage de SKU qui enregistrent les événements pertinents dans une fenêtre temporelle définie. Par exemple, les indicateurs de préparation peuvent être plus élevés pendant le trafic de pointe des vacances que pendant les périodes de trafic normal.

En raison de ces variables, le pourcentage de l’indicateur de préparation peut fluctuer. Cela explique pourquoi les types de recommandations fluctuent entre « Prêt à être déployé ».

Les indicateurs de préparation sont calculés en fonction de deux facteurs :

* Taille suffisante du jeu de résultats : y a-t-il suffisamment de résultats renvoyés dans la plupart des scénarios pour éviter d’utiliser les [recommandations de sauvegarde](events.md#backuprecs) ?

* Les produits retournés représentent-ils une variété de produits de votre catalogue ? Ce facteur permet de s’assurer que les recommandations sur l’ensemble de votre site ne se limitent pas à un petit sous-ensemble de produits.

En fonction des facteurs ci-dessus, une valeur de préparation est calculée et affichée comme suit :

* 75 % ou plus signifie que les recommandations suggérées pour ce type de recommandation seront très pertinentes.
* Au moins 50 % signifie que les recommandations suggérées pour ce type de recommandation seront moins pertinentes.
* Moins de 50 % signifie que les recommandations suggérées pour ce type de recommandation peuvent ne pas être pertinentes. Dans ce cas, les [recommandations de sauvegarde](events.md#backuprecs) sont utilisées.

En savoir plus sur [pourquoi les indicateurs de préparation peuvent être faibles](#what-to-do-if-the-readiness-indicator-percent-is-low).

### Basé sur statique

Les types de recommandations suivants sont basés sur des données statiques, car ils ne nécessitent que des données de catalogue. Aucune donnée comportementale n’est utilisée.

* _Plus Comme Ceci_
* _Similarité visuelle_

### Basé sur Dynamic

Les types de recommandations suivants sont basés sur les dynamiques, car ils utilisent les données comportementales de storefront.

Données comportementales des six derniers mois du storefront :

* _A consulté ceci, a consulté cela_
* _J&#39;ai vu ceci, j&#39;ai acheté cela_
* _J&#39;ai acheté ceci, acheté cela_
* _Recommandé_

Sept derniers jours de données comportementales storefront :

* _Les plus consultés_
* _Les plus achetés_
* _Les plus ajoutés au panier_
* _En Tendance_
* _Afficher pour acheter la conversion_
* _Conversion de l’affichage au panier_

Données comportementales les plus récentes sur les acheteurs (vues uniquement) :

* _Récemment consultés_

### Visualiser la progression

Pour visualiser plus facilement la progression de l’entraînement pour chaque type de recommandation, la section _Sélectionner le type de recommandation_ affiche une mesure de préparation pour chaque type.

![Type de recommandation](assets/create-recommendation-select-type.png)
_Type de recommandation_

>[!NOTE]
>
>Les indicateurs peuvent ne jamais atteindre 100 %.

Le pourcentage de préparation pour les types de recommandations basées sur des catalogues change généralement peu, car les catalogues sont relativement stables. En revanche, le pourcentage de préparation pour les types de recommandations basé sur les données comportementales de l’acheteur peut changer fréquemment avec l’activité quotidienne de l’acheteur.

#### Que faire si le pourcentage d’indicateur de préparation est faible

Un faible pourcentage de préparation indique que peu de produits de votre catalogue peuvent être inclus dans les recommandations pour ce type de recommandation. Cela signifie qu’il existe une forte probabilité que les [recommandations de sauvegarde](events.md#backup-recommendations) soient renvoyées si vous déployez quand même ce type de recommandation.

>[!IMPORTANT]
>
>Les types de produits _Bundle_, _grouped_ et personnalisés ne sont pas pris en charge. Si votre catalogue contient un grand nombre de ces types de produits, vous pouvez vous attendre à un faible score de préparation. En outre, tout SKU avec des espaces peut réduire la pertinence des recommandations et doit être évité.

Vous trouverez ci-dessous la liste des raisons possibles et des solutions aux faibles scores de préparation courants :

* **Basé sur une statique** - L’absence de données de catalogue pour les produits affichables entraîne de faibles pourcentages pour ces indicateurs. S’ils sont inférieurs aux prévisions, une synchronisation complète peut résoudre ce problème.
* **Basé sur la dynamique** - Les facteurs suivants entraînent de faibles pourcentages pour les indicateurs basés sur la dynamique :

  * Champs manquants dans les [événements storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations) requis pour les types de recommandation respectifs (requestId, contexte du produit, etc.)
  * Faible trafic sur le magasin : le volume d’événements comportementaux que nous recevons est donc faible.
  * La variété d’événements comportementaux de storefront sur différents produits de votre magasin est faible. Par exemple, si seulement 10 % de vos produits sont consultés ou achetés la plupart du temps, les indicateurs de préparation respectifs seront faibles.

## Aperçu de Recommendations {#preview}

Le panneau _Aperçu des produits recommandés_ est toujours disponible avec un exemple de sélection de produits qui apparaissent dans l’unité de recommandation lorsqu’elle est déployée sur le storefront.

Pour tester une recommandation lorsque vous travaillez dans un environnement hors production, vous pouvez récupérer les données de recommandation d’une [autre source](settings.md). Cela permet aux commerçants de tester les règles et de prévisualiser les recommandations avant le déploiement en production.

| Champ | Description |
|---|---|
| Nom | Nom du produit. |
| SKU | Unité de gestion des stocks affectée au produit |
| Prix | Prix du produit. |
| Type de résultat | Principal : indique que les données d’identification collectées sont suffisantes pour afficher une recommandation.<br />Sauvegarde : indique qu’il n’y a pas suffisamment de données d’identification collectées ; une recommandation de sauvegarde est donc utilisée pour remplir le slot. Accédez à [Données comportementales](events.md) pour en savoir plus sur les modèles de machine learning et les recommandations de sauvegarde. |

Pour voir quels produits une unité de recommandation inclut en temps réel, testez le type de page, le type de recommandation et les filtres au fur et à mesure que vous le créez. Ensuite, configurez l&#39;unité pour répondre aux besoins de votre entreprise en fonction des produits qu&#39;elle renvoie.

Lorsque plusieurs unités de recommandation sont déployées sur la même page, Adobe Commerce a utilisé [filtres](#filters.md) pour supprimer les produits en double des recommandations qu’il affiche. Par conséquent, le panneau de prévisualisation peut afficher un ensemble de produits différent de celui du storefront.

>[!NOTE]
>
> Vous ne pouvez pas prévisualiser le type de recommandation `Recently viewed`, car les données ne sont pas disponibles dans l’Administration.
