---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%
---
Les sources de catalogue représentent les étendues de produits, d’attributs et de catégories faisant autorité. Ils sont généralement associés à la langue, à l’audience ou au système d’origine et déterminent le comportement de la recherche, du filtrage et du tri.

## Sources de catalogue et concepts connexes

Comprendre comment les sources de catalogue sont liées à d’autres concepts de services de marchandisage vous permet de modéliser correctement vos données :

* **Source du catalogue** - Contexte de données sous-jacent qui fournit des informations sur les produits. Une source de catalogue représente généralement un paramètre régional (par exemple, `en-US`, `fr-CA`) ou un contexte de données fourni par un système externe tel qu’un PIM ou un ERP. Les produits, métadonnées d’attribut et catégories sont tous inclus dans la portée par source de catalogue. Une source de catalogue définit l’origine des données de catalogue brutes et son effet sur la découverte de produits (résultats de recherche, filtrage et comportement de tri).

* **[Vue Catalogue](/help/optimizer/setup/catalog-view.md)** - Vue configurée de votre catalogue pour un besoin professionnel spécifique. Une vue de catalogue sélectionne des sources de catalogue (ou des paramètres régionaux), applique des [politiques](/help/optimizer/setup/policies.md) pour filtrer la visibilité des produits et associe des [tarifs](/help/optimizer/setup/pricebooks.md) à la vue. Une seule source de catalogue peut alimenter de nombreuses vues de catalogue (par exemple, une source `en-US` avec des vues de catalogue distinctes pour différentes marques ou régions). Considérez une vue de catalogue comme la *façon* d’exposer ces données à un storefront, un canal ou une audience.

* **[Couche Catalogue](catalog-layer.md)** - Couche appliquée sur les données de catalogue de base pour modifier les attributs de produit (nom, description, images, métadonnées) sans modifier les données source. Utilisez les calques de catalogue lorsque les différences doivent affecter uniquement l’affichage du storefront, et non la découverte de produits.

## Mode de remplissage des sources de catalogue

Les sources de catalogue sont renseignées par l’ingestion des données de catalogue. La manière dont vous fournissez ces données dépend de votre implémentation :

- **Adobe Commerce as a Cloud Service avec CCDM** : la synchronisation native fournit des données de catalogue à partir de Commerce Foundation. Gérez les produits sous-jacents et la configuration des vues de magasin dans Commerce Foundation, et surveillez la synchronisation dans l’espace de travail [Synchronisation des données](data-sync.md). Aucune intégration distincte de l’API Data Ingestion n’est requise.
- **Adobe Commerce Optimizer avec un serveur principal tiers** : votre intégration fournit des produits et des informations sur la source du catalogue via l’[API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).


## Règles et limitations

* Une source de catalogue est créée lorsque la couche de données des services de marchandisage reçoit pour la première fois des données de catalogue pour un nouveau paramètre régional ou système source.
* L’unicité du produit est déterminée par le SKU + la source du catalogue.
* Les acheteurs n’accèdent pas directement aux sources du catalogue. Les données de catalogue sont exposées au storefront via [les vues de catalogue](catalog-view.md).

## Conseils de modélisation

Suivez les conseils suivants lors de la planification de votre structure de catalogue. Pour Adobe Commerce as a Cloud Service avec CCDM, gérez la configuration sous-jacente dans Commerce Foundation plutôt que de créer des sources de catalogue par le biais d’une intégration d’ingestion distincte.

* Utilisez une source de catalogue distincte pour chaque langue du catalogue.
* Utilisez des sources de catalogue distinctes lorsque les différences de produit et d’attribut doivent affecter le comportement de recherche, de filtrage ou de tri, comme différents paramètres de recherche ou de filtrabilité.
* Utilisez les [calques de catalogue](catalog-layer.md) lorsque les différences de produit et d’attribut doivent affecter la présentation du produit sans modifier le comportement de recherche, de filtrage ou de tri.

>[!MORELIKETHIS]
>
> * [Vues du catalogue](catalog-view.md) - Configurez des vues filtrées et tarifées au-dessus d’une source de catalogue.
> * [Calques de catalogue](catalog-layer.md) - Modifiez la présentation du produit sans modifier les données sources
> * [Politiques](policies.md) - Créez des filtres basés sur les attributs pour les vues de catalogue
> * [Catalogues de prix](/help/optimizer/setup/pricebooks.md) - Gérez les structures de prix pour différents segments de clients
> * [Clés d’accès restreintes](restricted-access-keys.md) - Protégez une vue de catalogue avec l’authentification par jeton signé
