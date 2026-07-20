---
title: Notes de mise à jour de Adobe Commerce Optimizer
description: Informations de mise à jour mensuelles pour  [!DNL Adobe Commerce Optimizer], y compris les mises à jour de l’API REST d’ingestion de données et de l’API GraphQL pour la récupération des données du catalogue storefront.
feature: Release Notes
role: Admin, Developer, User, Leader
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: e420d461-9ea2-4e32-aa37-230b14a297d7
TQID: https://experienceleague.adobe.com/apcpxN0AOniRcHDCa5MMAVWysxRO5mTcudXXXjET-Lo
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 27cbf66e4851f0d21ecc039fd53aa838b4c211ba
workflow-type: tm+mt
source-wordcount: 1365
ht-degree: 0%

---

# Notes de mise à jour

Les notes de mise à jour suivantes contiennent des mises à jour de [!DNL Adobe Commerce Optimizer], notamment :

* Nouvelles fonctionnalités et améliorations de [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour).
* Mises à jour de l’[API REST d’ingestion de données](https://developer.adobe.com/commerce/services/reference/rest/) et de l’API [GraphQL pour la récupération des données du catalogue de storefront](https://developer.adobe.com/commerce/services/reference/graphql/).

  {{aco-api-updates-and-dropins}}

## Juillet 2026

>[!BEGINSHADEBOX]

_20 juillet 2026_

![Correctif](../assets/fix.svg) **Performances de navigation par catégorie** : optimisation des performances appliquée au service de catégorie, ce qui se traduit par un débit plus élevé et une latence P99 plus faible pour la requête `CategoryNavigation`, ce qui améliore la réactivité du service et l’expérience utilisateur globale sous une charge élevée.
<!--DATA-7131 DATA-7250-->

{{aco-release}}

>[!ENDSHADEBOX]

## Juin 2026

>[!BEGINSHADEBOX]

_24 juin 2026_

<!-- v1.3 -->

![Nouveau](../assets/new.svg) **Nouveau champ de `canEditQuantity`**—Ajout de `canEditQuantity` aux `ProductViewOptionValueProduct` dans le GraphQL du service de catalogue. Il expose le paramètre de quantité facultatif **défini par l’utilisateur** pour les sélections de bundle effectuées par l’administrateur Commerce, afin que les consommateurs du storefront puissent déterminer si la quantité d’une sélection de bundle est modifiable.
<!--COMOPT-2050-->

### Recherche sémantique

[!DNL Adobe Commerce Optimizer] prend désormais en charge la **[recherche sémantique]** dans l’onglet [**Recherche avancée**](./settings.md#advanced-search) de **[!UICONTROL Settings]**. La recherche sémantique utilise l’IA pour faire correspondre les produits par signification et par contexte, ainsi que la recherche par mot-clé, ce qui réduit les pages de recherche vides pour les requêtes en langage naturel. Elle est activée par défaut pour les catalogues anglais éligibles. Vous pouvez éventuellement régler **[!UICONTROL Semantic boost]**, **[!UICONTROL Similarity threshold]** et **[!UICONTROL Fuzzy search]** sur le même onglet. Aucune configuration d’attribut ou modification du storefront n’est requise. [En savoir plus](./setup/semantic-search.md).

### Filtres de prix recommandés (version bêta)

Les unités de recommandation de produit prennent désormais en charge [**filtres de prix**](./merchandising/recommendations/filters.md#price) à l’étape **[!UICONTROL Filter products]**. Incluez ou excluez des candidats à l’aide de règles **statiques** minimales et maximales ou **dynamiques** sur la page des détails du produit qui comparent les produits recommandés au **prix calculé final** du produit actuellement consulté à partir du catalogue des prix actifs du storefront. Les règles de prix filtrent le jeu de candidats. Ils ne reclassent pas les produits. [En savoir plus](./merchandising/recommendations/filters.md#price).

{{aco-release}}

>[!ENDSHADEBOX]

## Mai 2026

>[!BEGINSHADEBOX]

### Amplification intelligente du classement

[Les règles de marchandisage](./merchandising/rules/add.md#intelligent-ranking-boost) pour la recherche, les listes de produits par défaut et les [pages de catégories](./merchandising/rules/add.md#rule-types) incluent désormais **[!UICONTROL Intelligent Ranking Boost]**. Vous pouvez ajuster la mesure dans laquelle des stratégies telles que **Les plus consultés** ou **Tendance** influencent l’ordre des produits par rapport à la pertinence textuelle sur la recherche et les signaux comportementaux sur les listes de catégories. L’aperçu des règles reflète vos paramètres. L’amplification est appliquée au moment de la requête. Vous n’avez donc pas besoin d’une resynchronisation du catalogue lorsque vous la modifiez.

### Mises à jour des API

_28 mai 2026_

<!-- v1.2 -->

![Correction](../assets/fix.svg) **Arborescences de navigation complètes** : les catégories descendantes balisées sont désormais correctement incluses dans les arborescences de `navigation` filtrées par famille lorsqu’un nœud intermédiaire non balisé existe dans le chemin d’accès. Ce correctif garantit que les acheteurs voient toutes les catégories pertinentes dans la navigation, ce qui facilite la navigation et la découverte d’articles.
<!--DATA-7183-->

![Correction](../assets/fix.svg) **Gestion des slugs vides dans les requêtes `categoryTree`**—Correction d’un problème où la requête [`categoryTree`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) renvoyait une erreur de serveur interne lorsque l’argument `slugs` incluait une chaîne vide. Les valeurs slug vides sont désormais ignorées, de sorte que les storefronts et les intégrations continuent de résoudre les données de catégorie sans requêtes ayant échoué.
<!--DATA-7184-->

![Correction](../assets/fix.svg) les requêtes **`searchCategory`renvoient des résultats insensibles à la casse et classés par ordre alphabétique** : la requête `searchCategory` trie désormais les résultats de recherche par ordre alphabétique sans respect de la casse, ce qui garantit un ordre cohérent et prévisible. Les catégories comportant des préfixes plus courts apparaissent en premier lorsque les noms sont par ailleurs identiques.
<!--COMOPT-2142-->

_4 mai 2026_

<!--v1.53-->

**Affichage correct de la devise** : les prix des produits Storefront affichent désormais le code de devise correct (par exemple, USD) pour tous les types de produits. Auparavant, certains produits affichaient des `NONE` au lieu de la devise attendue, ce qui entraînait des prix manquants.

<!--DATA-7115-->

{{aco-release}}

>[!ENDSHADEBOX]

## Avril 2026

**Date de publication** : 7 avril 2026

>[!BEGINSHADEBOX]

### Règles de catalogue

[Règles de catégorie](./merchandising/rules/add.md) étendez les règles de marchandisage afin de cibler les catégories et de contrôler l’ordre des produits sur les pages de catégorie avec le même classement et les mêmes actions (épingler, booster, enterrer) que la recherche.

### Filtre de prix (version bêta)

Les filtres de recommandation incluent désormais un [&#x200B; filtre de plage de prix &#x200B;](./merchandising/recommendations/filters.md#price) (minimum et maximum).

### Mises à jour des API

_29 avril 2026_

<!--v1.52 release-->

**Traitement par lots des requêtes requis** — L’API GraphQL applique désormais un maximum de 100 SKU par requête lorsque vous récupérez des données de catalogue. Voir [limites et limites documentées](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits#product-discovery).

<!--DATA-7156-->

_17 avril 2026_

<!--v1.51 release-->

**Rechercher des catégories par nom avec GraphQL** — La nouvelle requête [`searchCategory`](https://developer.adobe.com/commerce/services/reference/graphql/) renvoie les catégories correspondantes avec pagination pour les vitrines et les intégrations. Voir la référence de l’API pour les paramètres et les champs de réponse. <!--COMOPT-1819-->

_7 avril 2026_

<!--v1.50 release-->

**Recherches de catégorie simplifiées** — La requête [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) traite les `family` comme facultatives, de sorte que vous pouvez résoudre les catégories par slug sans fournir de famille.

{{aco-release}}

>[!ENDSHADEBOX]

## Mars 2026

Il n’y a pas eu de version [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) ce mois-ci. Voir les mises à jour des API ci-dessous.

>[!BEGINSHADEBOX]

### Mises à jour des API

_24 mars 2026_

Les bundles dynamiques renvoient désormais une plage de prix calculée. <!--DATA-7014-->

{{aco-release}}

>[!ENDSHADEBOX]

## Février 2026

**Date de publication** : 19 février 2026

>[!BEGINSHADEBOX]

### Vue Catalogue pour les règles et recommandations de marchandisage

Vous pouvez désormais spécifier une vue de catalogue lorsque vous [créez des unités de recommandation](./merchandising/recommendations/create.md) ou [&#x200B; des règles de marchandisage](./merchandising/rules/add.md).

### Mises à jour des API

_19 février 2026_

<!--v1.48-->

**Contenu de catégorie plus riche pour les storefronts** — La requête [categoryTree](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#query-categoryTree) renvoie désormais des descriptions, des images et des balises META d’optimisation pour les moteurs de recherche afin que les storefronts puissent rendre des pages de catégorie plus riches.<!--DATA-6933-->

_12 février 2026_

<!--v1.49-->

**Amélioration des données de produit par catégorie** — L’API GraphQL ajoute le type de [`CategoryProductView`](https://developer.adobe.com/commerce/services/graphql-api/merchandising-api/index.html#definition-CategoryProductView){target="blank"} afin que vous puissiez interroger et filtrer les produits par catégorie avec moins d’allers-retours.

{{aco-release}}

>[!ENDSHADEBOX]

## Janvier 2026

Il n’y a pas eu de version [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) ce mois-ci. Voir les mises à jour des API ci-dessous.

>[!BEGINSHADEBOX]

### Mises à jour des API

_19 janvier 2026_

* **Les catégories plus riches sont prises en charge avec l’API REST** — Les opérations [API Catégories](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) acceptent désormais les valeurs `metaTags`, `images` et `description` facultatives en plus de `families`, afin que vous puissiez fournir des détails de merchandising et d’optimisation du moteur de recherche plus riches pour les catégories.

{{aco-release}}

>[!ENDSHADEBOX]

## Décembre 2025

**Date de publication** : 10 décembre 2025

>[!BEGINSHADEBOX]

### Opportunités

Les marchandiseurs peuvent désormais obtenir des recommandations optimisées par l’IA via [Adobe Sites Optimizer](./manage-results/opportunities.md) pour détecter les problèmes de site et suggérer des correctifs de performances.

### Calques de catalogue

Les marchandiseurs peuvent désormais utiliser les [calques de catalogue](./setup/catalog-layer.md) pour superposer les données de produit sans modifier le catalogue source, gérer la priorité des calques et utiliser le correctif automatique d’Adobe Sites Optimizer.

{{aco-release}}

>[!ENDSHADEBOX]

## Novembre 2025

Il n’y a pas eu de version [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) ce mois-ci. Voir les mises à jour des API ci-dessous.

>[!BEGINSHADEBOX]

### Mises à jour des API

_21 novembre 2025_

**Instructions d’authentification mises à jour pour l’API REST d’ingestion de données** — Les instructions font désormais référence aux jetons d’accès OAuth et aux portées d’informations d’identification Developer Console correctes pour le service d’ingestion de données. Si les portées de vos informations d’identification sont obsolètes, régénérez-les pour conserver l’accès.

_3 novembre 2025_

<!-- v1.43 -->

**Contenu de produit localisé et superposé dans GraphQL** — Vous pouvez désormais diffuser du contenu de produit spécifique à un canal et prenant en compte les paramètres régionaux depuis [!DNL Adobe Commerce Optimizer].

* Personnaliser le contenu des produits par segment client
* Appliquer des remplacements spécifiques aux paramètres régionaux sans dupliquer les données du catalogue de base
* Contrôle des remplacements au niveau du champ avec des masques de calque
* Utilisez des calques de contenu premium, saisonniers et optimisés pour les appareils mobiles

Aucun changement de schéma de l’API GraphQL : les calques s’appliquent à travers les en-têtes de requête et de requête `products` existants. Voir [Couche Catalogue](./setup/catalog-layer.md).

{{aco-release}}

>[!ENDSHADEBOX]

## Octobre 2025

**Date de publication** : 14 octobre 2025

>[!BEGINSHADEBOX]

### Connecteur Commerce Commerce Optimizer Salesforce

Le [!DNL Commerce Optimizer Salesforce Commerce Connector] est un nouveau kit de démarrage App Builder qui synchronise les données du catalogue Commerce B2C Salesforce dans [!DNL Commerce Optimizer].<!--COMOPT-536-->

**Pour les administrateurs :**

* Les modifications du catalogue Salesforce (produits, prix, métadonnées, tarifs) se synchronisent automatiquement avec [!DNL Commerce Optimizer].
* S’exécute en dehors de [!DNL Adobe Commerce] pour réduire le nombre de points de contact d’intégration.
* Les mises à jour planifiées actualisent [!DNL Commerce Optimizer] données pour le marchandisage et les recommandations.

**Pour les développeurs :**

* Framework extensible pour l’ingestion de catalogues Salesforce dans les services de marchandisage SaaS.
* Référencez des implémentations, des documents de conception et des exemples de code pour accélérer les builds et le dépannage.

### Recherche superposée

* **Recherche en couches (GA)** — La recherche de produits prend désormais en charge la correspondance `startsWith` et `contains`. Voir [Recherche par couches et types de recherche développés](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#layered-search-and-expansion-of-search-types).

### Mises à jour des API

* _17 octobre 2025_

  **Ajouter la prise en charge de l’API REST pour ingérer des couches de produit** — Utilisez l’[API Catalog layer](https://developer.adobe.com/commerce/services/reference/rest/#tag/Product-Layers) pour personnaliser et remplacer les données de produit de base pour des contextes, des paramètres régionaux ou des besoins commerciaux spécifiques. Après avoir créé des calques, vous pouvez les appliquer et les gérer à partir de [Adobe Commerce Optimizer Studio](./setup/catalog-layer.md).<!--DATA-6632-->

* _14 octobre 2025_

  **Arborescences de catégories programmatiques** — Créez, mettez à jour et gérez des arborescences de catégories pour la navigation et le regroupement via REST (global ou spécifique à un canal), à grande échelle (jusqu’à 10 000 arborescences et 500 catégories par arborescence). Voir [Catégories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="blank"} dans la section _Référence de l’API REST d’ingestion des données de catalogue_.<!--DCAT-2649-->

* _8 octobre 2025_

  **Mappage de catégorie plus clair pour l’ingestion de données** — De nouvelles directives expliquent le format et les règles de hiérarchie des slugs de catégorie et précisent que les valeurs de `routes.path` de produit doivent correspondre à un slug de catégorie existant (par exemple, `men/clothing`).

{{aco-release}}

>[!ENDSHADEBOX]

## Septembre 2025

Il n’y a pas eu de version [[!DNL Adobe Commerce Optimizer Studio]](overview.md#quick-tour) ce mois-ci. Voir les mises à jour des API ci-dessous.

>[!BEGINSHADEBOX]

### Mises à jour des API

_23 septembre 2025_

* **Gérer les catégories à l’aide de l’API REST** — Utilisez l’[API Catégories](https://developer.adobe.com/commerce/services/reference/rest/#operation/createCategories) pour créer et gérer des catégories. Les catégories organisent les produits en groupes logiques et prennent en charge les hiérarchies imbriquées par le biais de chemins basés sur des slugs. Après avoir affecté des catégories à des produits, récupérez-les à l’aide du `[navigation](https://developer.adobe.com/commerce/services/reference/graphql/#navigation)` GraphQL et `[categoryTree](https://developer.adobe.com/commerce/services/reference/graphql/#categorytree)` des requêtes pour effectuer le rendu des menus de storefront et des arborescences de catégories.<!--DCAT-2626-->

{{aco-release}}

>[!ENDSHADEBOX]

## Août 2025

**Date de publication** : 28 août 2025

>[!BEGINSHADEBOX]

### Région de l’UE désormais disponible

La région de production de l’UE (**eu1**) est disponible pour les organisations IMS. Lorsque vous [ajoutez une [!DNL Commerce Optimizer] instance](./get-started.md#step-1-create-an-instance) dans Cloud Manager, choisissez **[!UICONTROL European Union]** comme **[!UICONTROL Region]** (production uniquement).

Les URL de production de base pour la région de l’Union européenne sont les suivantes :

* Administrateur : `https://eu1.admin.commerce.adobe.com`
* REST et GraphQL : `https://eu1.api.commerce.adobe.com`

Boîte de dialogue de création d’instance de ![Cloud Manager avec le champ Région](./assets/create-instance.png){width="600" align="center" zoomable="yes"}

{{aco-release}}

>[!ENDSHADEBOX]

