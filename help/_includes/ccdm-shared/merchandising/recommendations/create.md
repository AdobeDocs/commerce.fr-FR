---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '1555'
ht-degree: 0%
---
Lorsque vous créez une recommandation, vous créez une _unité de recommandation_, ou widget, qui contient les _éléments_ de produit recommandés.

![Unité de recommandation](/help/assets/ccdm-shared/recommendations/unit.png)
_Unité de recommandation_

Lorsque vous activez l’unité de recommandation, Adobe Commerce commence à [collecter des données](/help/optimizer/manage-results/recommendation-performance.md) pour mesurer les impressions, les vues, les clics, etc. Le tableau Recommandations affiche les mesures de chaque unité de recommandation afin de vous aider à prendre des décisions commerciales éclairées.

1. Dans le menu, accédez à _Marchandisage_ > **Recommandations** pour afficher l’espace de travail _Recommandations_.

1. Dans le champ **Vue du catalogue**, sélectionnez la vue du catalogue dans laquelle vous souhaitez que la recommandation soit disponible. En savoir plus sur [l’utilisation des vues de catalogue pour les recommandations](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view).

1. Cliquez sur **Créer une recommandation**.

   La recommandation que vous créez est disponible dans la vue de catalogue que vous avez précédemment sélectionnée.

1. Dans la section _Nommer votre recommandation_, saisissez un nom explicite pour référence interne, tel que `Home page most popular`.

1. Dans la section **Référence du storefront**, saisissez une clé de référence pour identifier cette unité de recommandation dans votre configuration de storefront. Après avoir créé la recommandation, vous pouvez [copier sa valeur](#get-the-storefront-reference-key) à partir des **détails de l’unité de recommandation** et l’utiliser comme `referenceKey` dans le bloc de recommandations. La clé de référence sert à la configuration du storefront. Le libellé d’affichage du storefront correspond au texte que les acheteurs voient.

1. Dans la section _Sélectionner le type de recommandation_, spécifiez le [type de recommandation](types.md) que vous souhaitez en fonction de votre stratégie.

1. Dans la section _Étiquette d&#39;affichage du storefront_, saisissez l&#39;étiquette [3&rbrace; visible par vos acheteurs, telle que « Meilleurs vendeurs ».](best-practice.md#recommendation-labels)

1. Dans la section _Choisir le nombre de produits_, utilisez le curseur pour indiquer le nombre de produits à afficher dans l’unité de recommandation.

   La valeur par défaut est `5`, avec un maximum de `20`.

1. (Facultatif) Dans la section _Filtres_, [appliquez des filtres](filters.md) pour contrôler quels produits apparaissent dans l’unité de recommandation.

1. Utilisez le panneau _Aperçu des produits recommandés_ pour mieux comprendre comment les filtres affectent les produits affichés dans l’unité de recommandation. En savoir plus sur la manière de [prévisualiser les recommandations](#preview-recommendations).

1. Une fois l’opération terminée, cliquez sur l’une des options suivantes :

   - **Enregistrez en tant que brouillon** pour modifier ultérieurement l’unité de recommandation. Vous ne pouvez pas modifier le type de recommandation d’une unité de recommandation à l’état de brouillon.

   - **Activer** pour activer l’unité de recommandation sur votre storefront.

   Votre recommandation apparaît dans l’espace de travail de Recommendations. Pour utiliser votre recommandation sur votre storefront, vous avez besoin de l’[ID de recommandation ou de la clé de référence](#get-the-storefront-reference-key).

>[!NOTE]
>
>Vous pouvez créer jusqu’à 50 unités de recommandation actives. Voir [Limites et limites](/help/optimizer/boundaries-limits.md) pour plus d’informations.

>[!IMPORTANT]
>
>Certains navigateurs peuvent bloquer les scripts critiques qui empêchent Recommendations de fonctionner comme prévu.

## Prévisualiser les recommandations

Le panneau de _prévisualisation des produits recommandés_ est toujours disponible avec un exemple de sélection de produits qui peuvent apparaître dans l’unité de recommandation lors de son déploiement sur le storefront.

![Aperçu De Recommendations](/help/assets/ccdm-shared/recommendations/rec-preview.png)

Pour tester une recommandation lorsque vous travaillez dans un environnement hors production, vous pouvez récupérer les données de recommandation d’une autre source. Cela permet aux commerçants de tester les règles et de prévisualiser les recommandations avant le déploiement en production.

| Champ | Description |
|---|---|
| Vue Catalogue |  |
| Nom | Nom du produit. |
| SKU | Unité de gestion des stocks affectée au produit |
| Prix | Prix du produit. |
| Type de résultat | Principal : indique que les données d’identification collectées sont suffisantes pour afficher une recommandation.<br />Sauvegarde : indique qu&#39;il n&#39;y a pas assez de données d&#39;identification collectées et qu&#39;une recommandation de sauvegarde est utilisée pour remplir le slot. Accédez à [Données comportementales](/help/optimizer/setup/events/overview.md) pour en savoir plus sur les modèles de machine learning et les recommandations de sauvegarde. |

Pour obtenir des commentaires en temps réel immédiats sur les produits qui seront inclus, testez le type et les filtres de recommandation au fur et à mesure que vous créez votre unité de recommandation. Pour répondre aux besoins de votre entreprise, configurez l’unité de recommandation au fur et à mesure que vous commencez à comprendre quels produits apparaissent.

[!DNL Product Recommendations] [filtrer](filters.md) les recommandations pour éviter d’afficher des produits en double lorsque plusieurs unités de recommandation sont déployées sur une seule page. Par conséquent, les produits qui s’affichent dans le panneau d’aperçu peuvent différer de ceux qui s’affichent dans le storefront.

Pour les configurations multi-storefront, multi-langues ou multi-marques, vous pouvez configurer si chaque recommandation s&#39;applique à toutes les vues de catalogue (globales) ou à une seule [vue de catalogue](/help/optimizer/setup/catalog-view.md). En savoir plus sur la façon de [définir la vue du catalogue](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view) lors de l’utilisation de recommandations.

## Obtenir la clé de référence du storefront

Après avoir créé une recommandation, utilisez sa clé de référence pour configurer l’unité de recommandation sur votre storefront.

1. Sur la page **Recommandations**, cliquez sur l’icône d’information (![icône d’information](/help/assets/ccdm-shared/recommendations/info-icon.png)) à côté du nom de la recommandation pour ouvrir la page **Détails de l’unité de recommandation**.

   ![Obtenir l’ID de recommandation](/help/assets/ccdm-shared/recommendations/get-ref-id.png)

1. Copiez la valeur de la section **Clé de référence Storefront**.

1. Dans le bloc storefront `product-recommendations`, utilisez cette clé de référence pour configurer la [liste déroulante de recommandations](https://experienceleague.adobe.com/en/tools/commerce-storefront/merchants/blocks/product-recommendations/) sur votre storefront Edge Delivery Services.

## Gestion des recommandations existantes

Vous pouvez modifier, désactiver ou supprimer une recommandation existante.

1. Dans le menu, accédez à _Marchandisage_ > **Recommandations**.

1. Sélectionnez la recommandation à modifier.

1. Cliquez sur le sélecteur (![Plus](/help/assets/ccdm-shared/recommendations/btn-more.png)) Plus .

1. Dans le menu, vous pouvez **Désactiver**, **Supprimer** ou **Modifier** la recommandation. Si vous sélectionnez **Modifier**, vous pouvez ajuster les paramètres suivants selon vos besoins :

   - Nom de la recommandation
   - Clé de référence
   - Libellé du storefront
   - Nombre de produits
   - Filtrer les produits

   Vous ne pouvez pas modifier le type de recommandation ni la vue du catalogue. La vue Catalogue est définie lors de la création de la recommandation. Pour en savoir plus, voir [sélectionner la vue de catalogue](/help/optimizer/manage-results/recommendation-performance.md#select-catalog-view).

1. Une fois l’opération terminée, cliquez sur **Enregistrer les modifications**.

## Indicateurs de préparation

Les indicateurs de préparation indiquent les types de recommandations les plus performants en fonction du catalogue et des données comportementales disponibles. Ils peuvent également vous aider à identifier les problèmes potentiels liés à la [collecte des événements](/help/optimizer/setup/events/overview.md) ou à déterminer si un type de recommandation ne reçoit pas suffisamment de trafic pour générer des résultats.

Les indicateurs de préparation sont classés en [basé sur statique](#static-based) ou [basé sur dynamique](#dynamic-based). Les recommandations statiques utilisent uniquement les données de catalogue, tandis que les recommandations dynamiques utilisent les données comportementales de vos acheteurs. Ces données comportementales sont utilisées pour [entraîner des modèles de machine learning](/help/optimizer/setup/events/overview.md) afin de créer des recommandations personnalisées et de calculer leur score de préparation.

### Comment les indicateurs de préparation sont calculés

Les indicateurs de préparation sont une indication de la formation du modèle. Les indicateurs dépendent des types d’événements collectés, de l’ampleur des produits avec lesquels il y a eu interaction et de la taille du catalogue.

Le pourcentage d’indicateur de préparation est dérivé d’un calcul qui indique le nombre de produits pouvant être recommandés en fonction du type de recommandation. Les statistiques sont appliquées aux produits en fonction de la taille globale du catalogue, du volume des interactions (vues, clics, ajouts au panier) et du pourcentage de SKU qui enregistrent ces événements dans une certaine fenêtre temporelle. Par exemple, pendant le trafic pendant la haute saison des fêtes, les indicateurs de préparation peuvent afficher des valeurs plus élevées qu’en période de volume normal.

En raison de ces variables, le pourcentage de l’indicateur de préparation peut fluctuer. Cette fluctuation explique pourquoi les types de recommandations changent entre « Prêt pour le déploiement » et non.

Les indicateurs de préparation sont calculés en fonction de plusieurs facteurs :

- Taille suffisante du jeu de résultats : y a-t-il suffisamment de résultats renvoyés dans la plupart des scénarios pour éviter d’utiliser les [recommandations de sauvegarde](/help/optimizer/setup/events/overview.md#backup-recommendations) ?
- Variété suffisante du jeu de résultats : les produits renvoyés représentent-ils une variété de produits de votre catalogue ? L’objectif avec ce facteur est d’éviter d’avoir une minorité de produits comme seuls éléments recommandés sur le site.

En fonction des facteurs ci-dessus, une valeur de préparation est calculée et affichée comme suit :

- 75 % ou plus signifie que les recommandations suggérées pour ce type de recommandation sont très pertinentes.
- Au moins 50 % signifie que les recommandations suggérées pour ce type de recommandation sont moins pertinentes.
- Moins de 50 % signifie que les recommandations suggérées pour ce type de recommandation peuvent ne pas être pertinentes. Dans ce cas, [recommandations de sauvegarde](/help/optimizer/setup/events/overview.md#backup-recommendations) sont utilisées.

En savoir plus sur [les raisons pour lesquelles les indicateurs de préparation peuvent être faibles](#what-to-do-if-the-readiness-indicator-is-low).

### Basé sur statique

Les types de recommandations suivants sont basés sur des données statiques, car ils ne nécessitent que des données de catalogue. Aucune donnée comportementale n’est utilisée.

- _Plus D&#39;Informations Comme Ceci_

### Basé sur Dynamic

Les types de recommandations suivants sont basés sur les dynamiques, car ils utilisent les données comportementales de storefront.

Données comportementales des six derniers mois du storefront :

- _A consulté ceci, a consulté cela_
- _A consulté ceci, a acheté cela_
- _Acheté ceci, acheté cela_
- _Recommandé_

Sept derniers jours de données comportementales storefront :

- _Les Plus Consultés_
- _Les Plus Achetés_
- _Les plus ajoutés au panier_
- _En Tendance_
- _Afficher pour acheter la conversion_
- _Conversion de l’affichage au panier_

Données comportementales les plus récentes sur les acheteurs (vues uniquement) :

- _Récemment Consulté_

### Visualiser la progression

Pour vous aider à visualiser la progression de l’entraînement pour chaque type de recommandation, la section _Sélectionner le type de recommandation_ affiche une mesure de préparation pour chaque type.

![Type de recommandation](/help/assets/ccdm-shared/recommendations/create-recommendation-select-type.png)
_Type de recommandation_

>[!NOTE]
>
>Les indicateurs peuvent ne jamais atteindre 100 %.

L’indicateur de préparation pour les types de recommandations qui dépendent des données du catalogue ne change pas beaucoup, car le catalogue du commerçant change rarement. Cependant, l’indicateur de préparation pour les types de recommandations basé sur les données comportementales de l’acheteur peut changer souvent en fonction de l’activité quotidienne de l’acheteur.

#### Que faire si l’indicateur de préparation est faible

Un faible pourcentage de préparation indique que peu de produits de votre catalogue peuvent être inclus dans les recommandations pour ce type de recommandation. Cela signifie qu’il existe une forte probabilité que [les recommandations de sauvegarde](/help/optimizer/setup/events/overview.md#backup-recommendations) soient renvoyées si vous déployez quand même ce type de recommandation.

>[!IMPORTANT]
>
>Tout SKU avec des espaces peut réduire la pertinence des recommandations et doit être évité.

Vous trouverez ci-dessous la liste des raisons possibles et des solutions aux faibles scores de préparation courants :

- **Basé sur une base statique** : l&#39;absence de données de catalogue pour les produits affichables entraîne de faibles pourcentages pour ces indicateurs. S’ils sont inférieurs aux prévisions, une synchronisation complète peut résoudre ce problème.
- **Basé sur la dynamique** : les facteurs suivants entraînent de faibles pourcentages pour les indicateurs basés sur la dynamique :

  - Champs manquants dans les [événements storefront](/help/optimizer/setup/events/overview.md) obligatoires pour les types de recommandation respectifs (requestId, product context, etc.).
  - Faible trafic vers le magasin : le volume d’événements comportementaux reçus est donc faible.
  - La variété d’événements comportementaux de storefront sur différents produits de votre magasin est faible. Par exemple, si seulement 10 % de vos produits sont consultés ou achetés la plupart du temps, les indicateurs de préparation respectifs sont faibles.
