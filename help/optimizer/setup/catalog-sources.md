---
title: Sources de catalogue
description: Découvrez les sources de catalogue et comment elles définissent la portée faisant autorité des produits, attributs et catégories pour le comportement de recherche, de filtrage et de tri.
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
autotag-review: '2026-06-09T19:36:23.516Z'
TQID: 'https://experienceleague.adobe.com/MiLbuYx6Pf95n3jvrgvou05Ery9XHXskx8p6KrN6CYg'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 94ba07437d532d0d101c166f58114c2aa0bd4be4
workflow-type: tm+mt
source-wordcount: 446
ht-degree: 0%

---

# Sources de catalogue

Les sources de catalogue représentent les étendues de produits, d’attributs et de catégories faisant autorité. Ils sont généralement associés à la langue, à l’audience ou au système d’origine et déterminent le comportement de la recherche, du filtrage et du tri.

## Sources de catalogue et concepts connexes

Comprendre comment les sources de catalogue sont liées à d’autres concepts [!DNL Adobe Commerce Optimizer] vous permet de modéliser correctement vos données :

* **Source du catalogue** - Contexte de données sous-jacent qui fournit des informations sur les produits. Une source de catalogue est généralement un paramètre régional (par exemple, `en-US`, `fr-CA`) ou un système externe tel qu’un PIM ou un ERP. Les produits, les attributs, les métadonnées et les catégories sont tous inclus dans la portée par source de catalogue. Considérez une source de catalogue comme *d’où* les données de catalogue brutes proviennent et *comment* elles affectent la découverte de produits (résultats de recherche, filtrage et comportement de tri).

* **[Vue Catalogue](catalog-view.md)** - Une vue configurée de votre catalogue pour un besoin professionnel spécifique. Lorsque vous créez une vue de catalogue, vous sélectionnez la source de catalogue (ou le paramètre régional) à utiliser, puis ajoutez des [politiques](policies.md) pour filtrer les produits visibles et lier des [livres de prix](pricebooks.md) pour contrôler les prix. Une seule source de catalogue peut alimenter de nombreuses vues de catalogue (par exemple, une source de `en-US` avec des vues de catalogue distinctes pour différentes marques ou régions). Considérez une vue de catalogue comme *comment* vous exposez ces données à un storefront, un canal ou une audience.

* **[Couche Catalogue](catalog-layer.md)** - Couche appliquée sur les données du catalogue de base pour modifier les attributs de produit (nom, description, images, métadonnées) sans modifier les données source. Utilisez les calques de catalogue lorsque les différences doivent affecter uniquement l’affichage du storefront, et non la découverte de produits.

## Règles et limitations

* Chaque source de catalogue est créée en ingérant un produit via l’API Data Ingestion. Consultez [Documentation pour les développeurs - Ingestion des données](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) pour plus d’informations.
* L’unicité du produit est déterminée par le SKU + la source du catalogue.
* Les acheteurs n’accèdent pas directement aux sources du catalogue. Les données de catalogue sont exposées au storefront via [vues de catalogue](catalog-view.md).

## Conseils de modélisation

Suivez les conseils suivants pour décider de la structure de vos sources de catalogue :

* Créez une source de catalogue distincte pour chaque langue du catalogue.
* Utilisez des sources de catalogue distinctes lorsque les différences de produit et d’attribut doivent affecter le comportement de la recherche, du filtrage ou du tri (par exemple, une recherchabilité, une filtrabilité ou une configuration de facettes différentes pour le même attribut).
* Utilisez les [&#x200B; calques de catalogue &#x200B;](catalog-layer.md) lorsque les différences entre les produits et les attributs doivent affecter uniquement l’affichage du storefront, et non la découverte de produits.

>[!MORELIKETHIS]
>
> * [Vues catalogue](catalog-view.md) - Configurez des vues filtrées et tarifées au-dessus d’une source de catalogue.
> * [Calques de catalogue](catalog-layer.md) - Modifiez la présentation du produit sans modifier les données sources
> * [Politiques](policies.md) - Créez des filtres basés sur les attributs pour les vues de catalogue
> * [Classeurs de prix](pricebooks.md) - Gérez les structures de prix pour différents segments de clientèle

