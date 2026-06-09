---
title: Source du catalogue
description: Découvrez les sources de catalogue et comment elles définissent la portée faisant autorité des produits, attributs et catégories pour le comportement de recherche, de filtrage et de tri.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
source-git-commit: dc50e4d7bcd118b2b9a800779c600ade5560e0bf
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Source du catalogue

Une source de catalogue représente une étendue faisant autorité en matière de produits, d’attributs et de catégories. Les sources de catalogue mappent généralement les limites de langue, d’audience ou de système d’origine et déterminent le comportement de la recherche, du filtrage et du tri.

## Source du catalogue et concepts connexes

Comprendre la manière dont une source de catalogue est liée à d’autres concepts [!DNL Adobe Commerce Optimizer] vous permet de modéliser correctement vos données :

* **Source du catalogue** - Contexte de données sous-jacent qui fournit des informations sur les produits. Une source de catalogue est généralement un paramètre régional (par exemple, `en-US`, `fr-CA`) ou un système externe tel qu’un PIM ou un ERP. Les produits, les attributs, les métadonnées et les catégories sont tous inclus dans la portée par source de catalogue. Considérez une source de catalogue comme *d’où* les données de catalogue brutes proviennent et *comment* elles affectent la découverte de produits (résultats de recherche, filtrage et comportement de tri).

* **[Vue Catalogue](catalog-view.md)** - Une vue configurée de votre catalogue pour un besoin professionnel spécifique. Lorsque vous créez une vue de catalogue, vous sélectionnez la source de catalogue (ou le paramètre régional) à utiliser, puis ajoutez des [politiques](policies.md) pour filtrer les produits visibles et lier des [livres de prix](pricebooks.md) pour contrôler les prix. Une seule source de catalogue peut alimenter de nombreuses vues de catalogue (par exemple, une source de `en-US` avec des vues de catalogue distinctes pour différentes marques ou régions). Considérez une vue de catalogue comme *comment* vous exposez ces données à un storefront, un canal ou une audience.

* **[Couche Catalogue](catalog-layer.md)** - Couche appliquée sur les données du catalogue de base pour modifier les attributs de produit (nom, description, images, métadonnées) sans modifier les données source. Utilisez les calques de catalogue lorsque les différences doivent affecter uniquement l’affichage du storefront, et non la découverte de produits.

## Règles et limitations

* Une source de catalogue est créée en ingérant un produit via l’API Data Ingestion. Consultez [Documentation pour les développeurs - Ingestion des données](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) pour plus d’informations.
* L’unicité du produit est déterminée par le SKU + la source du catalogue.
* Les acheteurs n’accèdent pas directement aux sources du catalogue. Les données de catalogue sont exposées au storefront via [vues de catalogue](catalog-view.md).

## Conseils de modélisation

Suivez les conseils suivants pour décider de la structure de vos sources de catalogue :

* Créez une source de catalogue distincte pour chaque langue de catalogue.
* Utilisez des sources de catalogue distinctes lorsque les différences de produit et d’attribut doivent affecter le comportement de la recherche, du filtrage ou du tri (par exemple, une recherchabilité, une filtrabilité ou une configuration de facettes différentes pour le même attribut).
* Utilisez les [&#x200B; calques de catalogue &#x200B;](catalog-layer.md) lorsque les différences entre les produits et les attributs doivent affecter uniquement l’affichage du storefront, et non la découverte de produits.

>[!MORELIKETHIS]
>
> * [Vues catalogue](catalog-view.md) - Configurez des vues filtrées et tarifées au-dessus d’une source de catalogue.
> * [Calques de catalogue](catalog-layer.md) - Modifiez la présentation du produit sans modifier les données sources
> * [Politiques](policies.md) - Créez des filtres basés sur les attributs pour les vues de catalogue
> * [Classeurs de prix](pricebooks.md) - Gérez les structures de prix pour différents segments de clientèle
