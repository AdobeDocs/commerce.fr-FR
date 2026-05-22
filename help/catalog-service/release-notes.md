---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: Dernières informations de mise  [!DNL Catalog Service]  jour pour Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4bd744e26afca4519fb1c04edcb7d2a118369ff9
workflow-type: tm+mt
source-wordcount: 2782
ht-degree: 0%

---

# Notes de mise à jour de [!DNL Commerce Storefront Catalog Service]

Ces notes de mise à jour couvrent les dernières mises à jour du service de catalogue Commerce, notamment :

- **[Versions du service de catalogue Storefront](#storefront-catalog-service)**

   - Améliorations du schéma de l’API Catalog Service pour une meilleure récupération des données
   - Amélioration de la sécurité, des performances et de la fiabilité de l’API Catalog Service et de l’infrastructure sous-jacente.

  Voir [Schéma Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/) dans la documentation du développeur Commerce pour plus d’informations sur ces API.

- **[Versions des métapaquets du service de catalogue](#catalog-service-metapackage)**

   - Mise à jour des dépendances pour améliorer les performances, la stabilité et la compatibilité avec d’autres composants Adobe Commerce.

- **[Versions du programme d’installation du service de catalogue](#catalog-service-installer)**

   - Mise à jour des dépendances pour maintenir la compatibilité entre le service de catalogue et votre pile Commerce.

>[!NOTE]
>
>Si votre projet Commerce utilise Adobe Commerce Optimizer pour diffuser des données de catalogue vers le service Commerce Edge Delivery ou les storefronts découplés, consultez les [notes de mise à jour de Adobe Commerce Optimizer](../optimizer/release-notes.md) pour connaître les dernières mises à jour de l’API.

Les mises à jour sont classées par type :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correctifs](../assets/fix.svg) Correctifs et améliorations
![Bogue](../assets/bug.svg) Problèmes connus

La prise en charge est fournie pour la dernière version. Les notes de mise à jour des versions plus anciennes sont incluses à titre de référence.

## Service de catalogue Storefront

### Mai 2026

**Date de publication** : 20 mai 2026
<!-- v1.55 -->

![Nouveau](../assets/new.svg) Limite imposée de 100 SKU maximum par demande pour les clients Adobe Commerce et Adobe Commerce as a Cloud Service conformément [limites et limites documentées](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits).
<!--DATA-7163-->

**Date de publication** : 13 mai 2026
<!--v1.54-->

![Nouveau](../assets/new.svg) **Ordre de tri des catégories dans GraphQL** : le type de GraphQL `CategoryView` inclut désormais un champ de position, de sorte que les storefronts peuvent afficher les catégories dans l’ordre configuré par les commerçants dans la hiérarchie du catalogue.
<!--DATA-7166-->

**Date de publication** : 4 mai 2026
<!-- v1.53 -->

![Corriger](../assets/fix.svg) les prix des produits Storefront affichent désormais le code de devise correct (par exemple, USD) pour tous les types de produits. Auparavant, certains produits affichaient des `NONE` au lieu de la devise attendue, ce qui entraînait des prix manquants. Cette mise à jour garantit un rendu des prix cohérent et précis sur l’ensemble du storefront.<!--DATA-7115-->

### Avril 2026

**Date de publication** : 29 avril 2026
<!--v1.52-->

![Nouveau &#x200B;](../assets/new.svg) limite forcée de 100 SKU maximum par demande pour Adobe Commerce Optimizer et Adobe Commerce as a Cloud Service
clients conformément [limites et limites documentées](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits). <!--DATA-7156-->

**Date de publication** : 17 avril 2026
<!--v1.51-->

![Nouveau](../assets/new.svg) Ajout d’une nouvelle requête `searchCategory` GraphQL qui permet aux clients de rechercher des catégories par nom avec des résultats paginés. La requête accepte un `searchTerm` obligatoire (3 caractères minimum) et des paramètres facultatifs `family`, `pageSize` et `currentPage`. Les résultats incluent la correspondance d’objets `CategoryTreeView` avec des métadonnées de catégorie complètes, une `totalCount` et des `pageInfo` pour la pagination. <!--COMOPT-1819-->

Cette requête est disponible uniquement pour les clients qui utilisent les services de marchandisage Adobe Commerce Optimizer. Voir [searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/).

### Mars 2026

**Date de publication** : 24 mars 2026
<!--v1.49-->

![Nouveau](../assets/new.svg) Ajout de la prise en charge pour calculer et renvoyer la plage de prix des lots dynamiques.
<!--DATA-7115-->

### Décembre 2025

**Date de publication** : 11 décembre 2025
<!-- v1.46 -->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer les performances et la stabilité.
<!--DATA-6852, DATA-6864-->

### Novembre 2025

**Date de publication** : 17 novembre 2025
<!-- v1.45 -->

![Nouveau](../assets/new.svg) **Filtrage des attributs par nom**-La requête GraphQL `productSearch` prend désormais en charge le filtrage des attributs de produit avec le champ `names`. <!--DATA-6831--> Avec ce filtre, vous pouvez :

- Réduire la taille de la payload de réponse en demandant uniquement des attributs spécifiques
- Combinez-la avec le filtre `roles` existant pour affiner par rôle de visibilité et nom d’attribut
- Exemples :

  **Filtrer uniquement par nom d’attribut**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **Filtrez par rôles et noms :**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>Pour récupérer tous les attributs sans filtrer, omettez l’argument `names` ou fournissez un tableau vide.

**Date de publication** : 6 novembre 2025
<!-- v1.44 -->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer les performances et la stabilité. <!--DATA-6852, DATA-6864-->

![Correctif](../assets/fix.svg) Les produits regroupés peuvent désormais être interrogés lorsque le parent n’a pas de tarification ; les produits enfants renvoient leurs propres rôles de visibilité.<!--DATA-6779-->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer les performances et la stabilité. <!--DATA-6721, DATA-6864-->

### Septembre 2025

**Date de publication** : 8 septembre 2025
<!-- v1.42 -->

![Nouvelle](../assets/new.svg) **Prise en charge de la tarification de niveau ajoutée** pour interroger la tarification de volume :<!--DATA-6643-->

Pour récupérer la tarification de niveau :

1. Utilisez la requête `products` avec les SKU de votre choix.
2. Pour **SimpleProductView**, accédez à `price.tiers`
3. Pour **ComplexProductView**, accédez aux `priceRange.minimum.tiers` et aux `priceRange.maximum.tiers`
4. Chaque niveau contient le prix `tier` réduit et les conditions de `quantity`
5. Définir des seuils de quantité avec `gte` (supérieur ou égal à) et `lt` (inférieur à)

**Exemple:**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![Fixe](../assets/fix.svg) **Prix de base filtrés par le prix final minimum** <!--DATA-6643-->

L’API renvoie désormais uniquement les niveaux dont le prix réduit est **inférieur** au prix final minimum du produit. Les niveaux supérieurs sont omis, car le prix final minimum s’appliquerait sur le storefront à la place.

Application :

- **Produits simples** : `price.tiers` comprend uniquement les niveaux avec `tier.amount.value` &lt; `price.final.amount.value` (final minimum).
- **Produits complexes** : `priceRange.minimum.tiers` et `priceRange.maximum.tiers` utilisent la même règle lors de la création de la gamme de prix.

**Date de publication** : 2 septembre 2025
<!-- v1.41 -->

![Correctif](../assets/fix.svg) **Amélioration de la gestion des erreurs en cas d’informations de prix manquantes** : lorsque les données de prix ne sont pas encore reçues, l’API renvoie des `null` pour le champ de prix au lieu de générer une erreur, ce qui permet aux clients de gérer les données manquantes de manière élégante.<!--DATA-6612-->

![Correctif](../assets/fix.svg) améliorations au niveau du système et de l’infrastructure pour améliorer les performances et la stabilité.<!--DATA-6671-->

### Juillet 2025

**Date de publication** : 30 juillet 2025
<!-- v1.40 -->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.<!--DATA-6619-->

**Date de publication** : 24 juillet 2025
<!-- v1.39 -->

![Nouveau](../assets/new.svg) **Récupérer les unités de recommandation par ID d’unité**-Nouveau point d’entrée GraphQL `recommendationsByUnitIds` récupère les unités de recommandation par leur ID unique pour un accès plus flexible et ciblé.

- `unitIds` est obligatoire (liste des recId à récupérer).
- Les paramètres de contexte (`currentSku`, `cartSkus`, `userViewHistory`, `userPurchaseHistory`, `category`) se comportent de la même manière que dans la requête Recommendations existante.

- **Exemple**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.<!--DATA-6316-->

**Date de publication** : 15 juillet 2025
<!-- v1.38 -->

![Nouveau](../assets/new.svg) **Types de produits de cartes-cadeaux**-Le service Storefront de catalogue prend désormais en charge les attributs de produit en tant qu’objets ou tableaux JSON, ce qui permet une gestion flexible de types complexes tels que les cartes-cadeaux.<!--DATA-6573-->

+++Versions précédentes

### Juin 2025

**Date de publication** : 20 juin 2025
<!-- v1.37 -->

![Nouveau](../assets/new.svg) **Configuration hiérarchique du catalogue des prix** : plages de prix précises pour les catalogues des prix parent-enfant. Les calculs respectent la hiérarchie et les règles héritées ; réduit les erreurs de tarification lorsque plusieurs tarifs sont liés. Adobe Commerce Optimizer uniquement. Voir [Livres de prix](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![Nouvelles](../assets/new.svg) **clés non sensibles à la casse** : les recherches de clés dans les requêtes ne sont désormais plus sensibles à la casse, ce qui réduit les erreurs de casse des clés. <!--DATA-6494, DCAT-2495-->

**Date de publication** : 20 juin 2025
<!-- v1.36 -->

![Nouvel &#x200B;](../assets/new.svg) **Événements d’E/S publics pour Catalog Storefront** : ajout d’événements d’E/S publics pour une intégration et une observabilité en temps réel (CSS et EDS).<!--DATA-6329-->

![Nouveau](../assets/new.svg) **Rendu côté serveur (SSR)** : améliorations architecturales pour prendre en charge le rendu côté serveur afin d’améliorer les performances, l’optimisation du moteur de recherche et l’expérience utilisateur sur les catalogues volumineux.<!--DATA-6278, DATA-6280-->

![Nouveau](../assets/new.svg) **Infrastructure et sécurité** : nouveaux rôles AWS, intégration de ServiceNow et pipelines CI/CD pour le service d’événements.

![Nouveau](../assets/new.svg) **Formats d’événement et observabilité** : payloads rationalisés, surveillance améliorée, données d’événement de variante améliorées.<!--DATA-6332, DATA-6402, -->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.<!--DATA-6404, DATA-6410, -->

**Date de publication** : 13 juin 2025
<!-- v1.35 -->

![Nouveau](../assets/new.svg) **Récupérer les données non mises en cache**-Activez l’en-tête `Magento-Is-Preview` pour transmettre les données non mises en cache du point d’entrée du catalogue au service de recherche<!--DATA-6345-->.

![Nouvelle](../assets/new.svg) **Options de produit à sélection multiple**-L’API GraphQL indique désormais si les options de produit permettent des sélections multiples (par exemple, le lot « Choisir plusieurs éléments »).<!--DATA-6487-->

![Nouveau](../assets/new.svg) Mise à jour de la validation des prix sur l’ingestion des données pour prendre en charge les produits sans prix.<!--DATA-6098-->

![Correctif](../assets/fix.svg) Amélioration de la gestion des erreurs pour une tarification simple des offres groupées dans Adobe Commerce Optimizer.<!--DATA-6541-->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.<!--DATA-6273, DATA-6485, -->

### Avril 2025

**Date de publication**: 8 avril 2025
<!-- v1.34 -->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.<!--DATA-5732-->

<!-- v1.33 -->
L’infrastructure ![Fix](../assets/fix.svg) prend désormais en charge des catalogues extrêmement volumineux (jusqu’à 440 millions de SKU) sans affecter les charges de travail existantes.

### Mars 2025

**Date de publication** : 28 mars 2025
<!-- v1.32 -->

![Correction](../assets/fix.svg) Les attributs sans rôles ne sont plus indexés par défaut pour le catalogue composable, ce qui améliore le temps d’indexation et réduit le stockage. Le comportement hérité peut être réactivé à l’aide d’un indicateur de fonctionnalité.

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.
<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### Février 2025

**Date de publication** : 18 février 2025
<!-- v1.31 -->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.<!--DATA-6389, DATA-6367, DATA-6373-->

### Décembre 2024

**Date de publication**: 9 décembre 2024
<!-- v1.30 -->

Version majeure : [modèle de données de catalogue composable](https://developer.adobe.com/commerce/services/optimizer/) pour les storefronts découplés, la gestion des en-têtes et la gestion des données de produit.

![Nouveau](../assets/new.svg) **Modèle de données de catalogue composable (CCDM)** : prend en charge les clients qui utilisent le catalogue composable pour les vitrines découplées. Les nouveaux points d’entrée acceptent les ID de vue de catalogue et de politique (rétrocompatible). Détails et prix des produits configurables avec pagination intégrée.<!--DATA-6018, DATA-6288-->

![Nouveau](../assets/new.svg) **Gestion des en-têtes**-`AC-Locale` renommé en `AC-Scope-Locale` pour les opérations de l’API de catalogue composable ; mappage des en-têtes et valeurs par défaut spécifiés.<!--DATA-6303, DATA-6078-->

![Nouveau](../assets/new.svg) **Données et tarification des produits**-Prise en charge du modèle de données de catalogue composable et amélioration de la gestion des prix des produits configurables.<!--DATA-6279-->

`CurrencyEnum` mis à jour pour prendre en charge les `NONE` pour les requêtes de recherche de produit, en s’alignant sur la logique de fédération.<!--DATA-6285-->

![Correctif](../assets/fix.svg) **Infrastructure et mises à niveau** : améliorations au niveau du système pour la sécurité, les performances et la stabilité.

![Correctif](../assets/fix.svg) les options de regroupement des produits n’affichent désormais que les produits activés.<!--DATA-6347-->

**Date de publication**: 9 décembre 2024
<!-- v1.29 -->

![Nouveau](../assets/new.svg) **Ordre des images dans les requêtes de produit**—Les images de produit dans le champ `images` GraphQL suivent désormais les `sortOrder` d’exportation de catalogue pour un comportement cohérent du storefront et de l’API.<!--DATA-6258-->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.<!--DATA-6619-->

**Date de publication** : décembre 2024
<!-- v1.28 -->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.
<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### Octobre 2024

**Date de publication** : 22 octobre 2024
<!-- v1.26 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) le schéma GraphQL inclut désormais des `lastModifiedAt` dans les informations produit pour des plans de site et une réindexation du moteur de recherche précis (par exemple, Google).
<!--DATA-6209-->

### Septembre 2024

**Date de publication** : 26 septembre 2024
<!-- v1.27 -->

![Correctif](../assets/fix.svg) améliorations apportées au niveau du système et de l’infrastructure pour améliorer la sécurité, les performances et la stabilité.
<!--DATA-6243-->

### Août 2024

**Date de publication** : 22 août 2024
<!-- v1.23 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg) Les informations sur les produits peuvent désormais être récupérées sans données de remplacement de produit (prix). Auparavant, ces requêtes renvoyaient : `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.`
<!--DATA-6121-->

**Date de publication** : 13 août 2024
<!-- v1.22 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de la récupération de toutes les variantes par SKU de produit. Voir [Référence de l’API Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).
<!--DATA-6067-->

### Mai 2024

**Date de publication** : 23 mai 2024
<!-- v1.19 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures


![Correction](../assets/fix.svg) l’indicateur `InStock` pour les valeurs d’option respecte désormais le statut de `enabled` étendue de la variante de produit.

<!--DATA-5033-->

![Correctif](../assets/fix.svg) Ajout de la prise en charge des prix des produits avec jusqu’à 16 chiffres et 4 décimales. Resynchronisez à partir du [tableau de bord de gestion des données](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) ou de l’[interface de ligne de commande](../data-export/data-export-cli-commands.md) pour appliquer les mises à jour.
<!--DATA-5033-->

#### Limites connues

Les fonctionnalités suivantes ne sont pas encore prises en charge :

- La taille maximale de la payload des attributs dynamiques est de 9 Mo.
- Le prix des produits du Groupe peut être calculé avec des prix de produits simples.
- Dans un tableau d’images, seule la première image contient des rôles.

Utilisez le maillage API et l’API Core GraphQL pour :

- Prix minimum annoncé
- Tarification par niveau
- Offre groupée de produits à prix fixes

Pour plus d’informations et des exemples, voir [Service de catalogue et maillage API](mesh.md).

### Avril 2024

**Date de publication** : 11 avril 2024
<!-- v1.18 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de PHP 8.3.

![Nouveau &#x200B;](../assets/new.svg) les requêtes [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) et [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) renvoient désormais des données d’options personnalisables pour les produits simples et complexes.<!--DATA-5538-->

### Février 2024

**Date de publication** : 22 février 2024
<!-- v1.17 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau &#x200B;](../assets/new.svg) l’[[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) est désormais disponible pour les flux de données (recommandations de produits, recherche en direct, service de catalogue). Nécessite `catalog-service` métapaquet v3.1.0+.

**Date de publication** : 13 février 2024
<!-- v1.16 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Les nouvelles vidéos produit &#x200B;](../assets/new.svg) sont désormais prises en charge par l’API Catalog Service.
![Correctif](../assets/fix.svg) Les options en rupture de stock s’affichent désormais dans le widget PDP.

#### Limites connues

Ces fonctionnalités ne sont pas encore prises en charge :

- La taille maximale de la payload des attributs dynamiques est de 9 Mo.
- Prix du produit du groupe. Cette valeur peut être calculée avec des prix de produit simples.
- Dans un tableau d’images, seule la première image contient des rôles.

Utilisez le maillage API et l’API Core GraphQL pour :

- Prix minimum annoncé
- [Tarification par niveau](mesh.md)

### Octobre 2023

**Date de publication** : 12 octobre 2023
<!-- v1.13 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Catalog Service prend en charge l’indicateur `inStock` pour les variantes de produits.
![Nouveau](../assets/new.svg) Les champs `urlKey` et `externalId` ont été ajoutés au schéma GraphQL.
![Nouveau](../assets/new.svg) Les produits téléchargeables et les cartes-cadeaux sont désormais pris en charge.

### Septembre 2023

**Date de publication** : 19 septembre 2023
<!-- v1.12 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Catalog Service utilise désormais l’indexation des prix [SaaS](../price-index/price-indexing.md).
![Correctif](../assets/fix.svg) cette version contient des correctifs et des améliorations du côté des services.

### Juillet 2023

**Date de publication** : 18 juillet 2023
<!-- v1.11 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) le service de catalogue prend désormais en charge la requête [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL pour les recommandations de produits.

### Juin 2023

**Date de publication** : 27 juin 2023
<!-- v1.10 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) l’API Catalog Service prend désormais en charge `related products`.

### Avril 2023

**Date de publication** : 12 avril 2023
<!-- v1.7 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) le service de catalogue nettoie désormais les variantes de produits supprimées.
![Correctif](../assets/fix.svg) Évolutivité de l’infrastructure et améliorations des performances.

### Mars 2023

**Date de publication** : 28 mars 2023
<!-- v1.6 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Des échantillons ont été ajoutés à la requête [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Nouveau](../assets/new.svg) Ajout de la possibilité de `entityId` à l’aide du [maillage API](mesh.md).

**Date de publication** : 6 mars 2023
<!-- v1.5 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la fonctionnalité [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) GraphQL.
![Correctif](../assets/fix.svg) Amélioration des performances et de l’évolutivité des API.

### Février 2023

**Date de publication** : 7 février 2023
<!-- v1.4 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) métapaquet de service de catalogue publié pour simplifier les étapes d’installation.
![Correctif](../assets/fix.svg) Amélioration de l’évolutivité et des performances de l’API.

### Janvier 2023

**Date de publication** : 17 janvier 2023
<!-- v1.3 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Expérience d’intégration simplifiée et améliorée.
![Nouveau &#x200B;](../assets/new.svg) de nouveaux points d’entrée de sandbox client sont disponibles pour les tests de pré-production.
![Nouveau](../assets/new.svg) Ajout de la prise en charge des produits virtuels.
![Correctif](../assets/fix.svg) Amélioration de l’évolutivité et des performances de l’API.

### Novembre 2022

**Date de publication** : 18 novembre 2022
<!-- v1.1 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) le service de catalogue prend désormais en charge Adobe [maillage API](https://developer.adobe.com/graphql-mesh-gateway/).
![Correctif](../assets/fix.svg) Amélioration de l’évolutivité et des performances globales des API.

### Octobre 2022

**Date de publication** : 4 octobre 2022
<!-- v1.0 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Prise en charge des produits groupés.
![Nouveau](../assets/new.svg) Ajout de remplacements de visibilité B2B. Les produits peuvent désormais faire l’objet de recherches et peuvent être ajoutés au panier pour des groupes de clients spécifiques.
Le service ![Fix](../assets/fix.svg) est désormais plus stable et offre de meilleures performances.

### Septembre 2022

**Date de publication** : 12 septembre 2022
<!-- v0.3 -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouvelle](../assets/new.svg) Images de variante : images de produit renvoyées en fonction des options sélectionnées.
![Nouveau](../assets/new.svg) Rôles de prix : seuls les membres de groupes de clients spécifiques peuvent voir les prix des produits.
![Correctif](../assets/fix.svg) Amélioration de la stabilité et des performances du service.
![Nouveau](../assets/new.svg) Des mises à jour sont reçues lorsque des produits sont supprimés du catalogue.

### Août 2022

**Date de publication** : 9 août 2022
<!-- Beta -->

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Les requêtes `products` et `refineProduct` renvoient les données suivantes :

- Attributs de produit (système) prédéfinis.
- Attributs de produit dynamiques et les filtrer par rôle (page d’affichage du produit/page de liste des produits).
- Options du produit.
- Images de produit et filtrage par rôle (PDP/PLP).
- Prix spécifique pour les produits simples et plages de prix pour les produits configurables.
- Prix et fourchettes de prix du groupe de clients. Ils renvoient un prix de secours par défaut pour les acheteurs sans groupe de clients.
- Types de produits qui utilisent une tarification spécifique au client B2B.

+++

## Métapaquet du service de catalogue

Mises à jour du métapaquet PHP du service de catalogue (`magento/catalog-service`).

- Pour les clients Adobe Commerce as a Cloud Service, la dernière version est installée dans votre environnement.

- Pour Adobe Commerce on cloud ou on-premise, Adobe recommande d’utiliser le compositeur pour mettre à niveau le métapaquet du service de catalogue dans vos environnements cloud vers la dernière version.

### version v3.3.0

**Date de publication** : 14 octobre 2025

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) **Mise à niveau des services de données**—Dépendance `magento/data-services` mise à jour vers ^8.0.0. Vérifiez l’environnement et l’utilisation de l’API Data Services personnalisée pour la compatibilité 8.x avant la mise à niveau.

![Nouveau](../assets/new.svg) Mise à jour de la version et des métadonnées pour la version 3.3.0.

### version v3.2.0

**Date de publication** : 12 avril 2024

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouvelle](../assets/new.svg) Version et métadonnées mises à jour pour 3.2.0. Aucune autre modification de dépendance.

### version v3.1.0

**Date de publication** : 26 janvier 2024

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![New](../assets/new.svg) Ajout de nouvelles dépendances de package :

- **Exportateur de données d’autorisation de catégorie** (`magento/module-category-permission-data-exporter`) pour exporter les données d’autorisation de catégorie utilisées par le service de catalogue.
- **Administration de la synchronisation des catalogues** `magento/module-catalog-sync-admin` pour l’interface utilisateur d’administration et la configuration liée à la synchronisation des catalogues.

![Nouveau](../assets/new.svg) Mise à jour de la version et des métadonnées pour la version 3.1.0.

## Programme d’installation du service de catalogue

Le programme d’installation est fourni avec l’extension du service de catalogue qui gère les vérifications d’installation et d’environnement afin que le service de catalogue corresponde à votre pile Commerce.

- Pour les clients **Adobe Commerce as a Cloud Service**, la dernière version du programme d’installation est installée dans votre environnement.

- Pour **Adobe Commerce sur l’infrastructure cloud** ou **sur site**, veillez à ce que le programme d’installation soit aligné sur le métapaquet [Service de catalogue](#catalog-service-metapackage).

Chaque fois que vous utilisez le compositeur pour mettre à niveau le `magento/catalog-service`, le package du programme d’installation est automatiquement mis à jour vers la dernière version. Vous pouvez également utiliser le compositeur pour mettre à niveau les `magento/catalog-service-installer` séparément lorsque ces notes de mise à jour décrivent une modification dont vous avez besoin, par exemple, la prise en charge d’une nouvelle version de PHP. Ainsi, vos outils d’installation restent compatibles avec la version du service de catalogue que vous exécutez.

### version 1.0.6

**Date de publication** : 25 mars 2026

![Nouveau](../assets/new.svg) **PHP 8.5** : garantit la compatibilité lorsque le service de catalogue fonctionne sur PHP 8.5.

## Documentation connexe

- Pour les projets déployés sur **Adobe Commerce sur le cloud, sur site ou Adobe Commerce as a Cloud Service, consultez la documentation suivante :

   - [Guide de Catalog Service](overview.md)
   - [Référence de l’API GraphQL du service de catalogue](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Guide de l’administrateur Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Guide d’Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Guide d’Adobe Commerce sur Cloud](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- Pour les projets utilisant **&#x200B;**&#x200B;ou **Adobe Commerce Optimizer Connector**, consultez la documentation suivante :

   - [Guide du développeur des services de marchandisage](https://developer.adobe.com/commerce/services/optimizer/)
   - [Référence de l’API Merchandising GraphQL](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Guide de Adobe Commerce Optimizer](../optimizer/overview.md)
