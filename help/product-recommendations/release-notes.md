---
title: Notes de mise à jour de [!DNL Product Recommendations]
description: Dernières informations de mise à jour pour  [!DNL Product Recommendations]  à partir d’Adobe Commerce.
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: ac1f3497292cc586810eb44a408f7d4d7088a96d
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 0%

---

# Notes de mise à jour de [!DNL Product Recommendations]

Les notes de mise à jour contiennent des mises à jour pour les modules [!DNL Product Recommendations] suivants :

* [!DNL Product Recommendations] métapaquet : `magento/product-recommendations`
* Prise en charge de Page Builder dans le module [!DNL Product Recommendations] (facultatif) : `magento/module-page-builder-product-recommendations`
* Prise en charge du type de recommandation de similarité visuelle pour le module [!DNL Product Recommendations] (facultatif) : `magento/module-visual-product-recommendations`

La prise en charge est assurée pour la dernière version publiée. Les notes de mise à jour des anciennes versions sont fournies à titre de référence.
Les notes de mise à jour incluent les éléments suivants :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correctifs](../assets/fix.svg) Correctifs et améliorations
![Bogue](../assets/bug.svg) Problèmes connus

Consultez la documentation destinée aux développeurs pour [en savoir plus sur la prise en charge des produits](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Mises à jour des services hébergés

Ces notes décrivent les mises à jour ou les problèmes connus qui ont été publiés ou découverts en dehors d’une version avec contrôle de version ou des améliorations apportées au service hébergé.

_31 janvier 2025_

![Nouveau](../assets/new.svg) Il existe une nouvelle politique de conservation des données pour les données de catalogue non interrogées dans votre environnement de test. [En savoir plus](overview.md#catalog-data-retention-policy).

_28 juin 2024_

![Bug](../assets/bug.svg) Les produits ajoutés au panier à partir d’une unité de [!DNL Product Recommendations] sur la page du panier ne sont pas supprimés de la liste des produits recommandés lors du rechargement de la page du panier.
![Bogue](../assets/bug.svg) Les produits supprimés du panier continuent à persister dans le tableau `cartSkus` jusqu’à ce que la page du panier se recharge.

_18 juillet 2023_

![Nouveau](../assets/new.svg) [!DNL Product Recommendations] dispose désormais d’une requête de [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) GraphQL.

_25 avril 2023_

![Nouveau](../assets/new.svg) [!DNL Product Recommendations] clients peuvent désormais profiter de l&#39;indexation des prix [SaaS](../price-index/price-indexing.md).

## Version majeure actuelle

### 6.4.0 magento/product-recommendations

_17 septembre 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg) Résolution d’un problème intermittent où les unités de recommandation de produit disparaissaient en raison d’une erreur JavaScript lorsque les données de stockage local n’étaient pas disponibles. Ce correctif garantit que PREX ne renvoie plus d’erreurs si le `ds-view-history-time-decay` est manquant dans le stockage local.
![Nouveau](../assets/new.svg) Mise à jour des URL du réseau CDN pour l’`recommendations-sdk` au domaine `adobe.io`.

### Versions précédentes

### 6.3.0 de magento/product-recommendations

_5 septembre 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de l’affichage des mesures pour les [unités de recommandation PageBuilder](page-builder.md) créées dans des vues de magasin autres que celles par défaut dans l’espace de travail [Recommandations de produits](workspace.md).
![Nouveau](../assets/new.svg) Product Recommendations respecte désormais entièrement le [mode de restriction des cookies](setting-cookie.md) en empêchant la collecte et le stockage de données dans les cookies/stockage local lorsque les restrictions sont activées.

### 6.2.1 de magento/product-recommendations

_14 juillet 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg) améliorations apportées au panneau [prévisualiser les recommandations](./create.md#preview-recommendations).

### 6.2.0 de magento/product-recommendations

_4 avril 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Mise à jour des URL du réseau CDN pour le `recommendations-admin-ui` au domaine `adobe.io`.

### 6.1.0 de magento/product-recommendations

_1 mars 2025_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de PHP 8.4.

### 6.0.3 de magento/product-recommendations

_6 novembre 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correctif](../assets/fix.svg) Correction d’un problème où le [filtre de catégorie](filters.md#category) incluait des catégories qui n’appartenaient pas au magasin actuel.
![Correctif](../assets/fix.svg) Correction d’un problème de dépendance dans le métapaquet `magento/product-recommendations`.

### 6.0.2 de magento/product-recommendations

_9 mai 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Correction](../assets/fix.svg) correction d’un problème en raison duquel le fait de cliquer sur le bouton **[!DNL Add to Cart]** d’un produit simple dans une unité de recommandations de produits redirigeait l’acheteur vers la page d’accueil plutôt que de rester sur la page active.
![Bogue](../assets/bug.svg) Une erreur de validation est due à l’élément `referenceBlock` dans le fichier XML `ProductRecommendations Layout`.

### 6.0.1 de magento/product-recommendations

_19 mars 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de PHP 8.3.

### 6.0.0 de magento/product-recommendations

_2 février 2024_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Le [!DNL Catalog Sync Dashboard] est désormais le [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Ce tableau de bord remanié fournit des informations sur les flux de données pour [!DNL Product Recommendations], [!DNL Live Search] et [!DNL Catalog Service].
![Correctif](../assets/fix.svg) Correction d’un problème qui provoquait des erreurs de passage en caisse pour [!DNL Product Recommendations].

+++5.0.0 et versions antérieures

### 5.0.1 de magento/product-recommendations

_15 septembre 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout de nouveaux modules pour la prise en charge de l’[Indexeur de prix Saas](../price-index/price-indexing.md).
![Nouveau](../assets/new.svg) Ajout de nouveaux modules d’exportation de données pour prendre en charge l’exportation d’autres types de produits, y compris les produits groupés et les cartes-cadeaux.
![Correctif](../assets/fix.svg) La taille de la table des flux Produits et Prix a été considérablement réduite. Les tableaux `catalog_data_exporter_products` et `catalog_data_exporter_product_prices` doivent présenter une réduction substantielle de la taille.

#### Limites connues

* La valeur `websiteCode` est renvoyée de manière incorrecte si elle contient un trait de soulignement (_).

### 5.0.0 de magento/product-recommendations

_Mars 2023_

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Mise à jour de la [!DNL Product Recommendations] pour la prise en charge d’Adobe Commerce 2.4.6.
![Nouveau](../assets/new.svg) Il s’agit d’une version majeure. [Modifier](install-configure.md#update) le fichier de `composer.json` racine de votre projet.
![Nouveau](../assets/new.svg) [!DNL Product Recommendations] prend désormais en charge les fonctionnalités [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) complètes dans Commerce (anciennement connu sous le nom de Multi-Source Inventory, ou MSI). Pour activer la prise en charge complète, vous devez [mettre à jour](install-configure.md#update) le module de dépendance `commerce-data-export` à la version 102.2.0+.

### 4.0.1 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Corriger](../assets/fix.svg) Auparavant, [!DNL Product Recommendations] affichait une erreur lorsque la devise d’affichage était remplacée par une devise différente de celle définie par défaut. Le changement de devise fonctionne désormais correctement.

### 4.0.0 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.4 et ultérieures

![Nouveau](../assets/new.svg) Ajout d’[indicateurs de préparation](create.md) pour vous aider à visualiser la progression de l’entraînement pour chaque type de recommandation.
![Nouveau](../assets/new.svg) Il s’agit d’une version majeure. [Modifier](install-configure.md#update) le fichier de `composer.json` racine de votre projet. Cette version nécessite également que vous fournissiez deux clés API lors de l’installation et de la configuration de [!DNL Product Recommendations] : [une clé de production et une clé sandbox](../landing/saas.md).

#### Limites connues

* La valeur `websiteCode` est renvoyée de manière incorrecte si elle contient un trait de soulignement (_).

### 3.3.7 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de PHP 8.1
![Nouveau ](../assets/new.svg) redimensionnement amélioré des images afin que le dimensionnement des images soit géré de manière plus cohérente dans le modèle d’affichage de référence

### 3.3.6 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Optimisation du métapaquet [!DNL Product Recommendations] en répertoriant explicitement les dépendances

### 3.3.5 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge [B2B](onboarding.md#b2bsupport) dans [!DNL Product Recommendations]
![Nouveau](../assets/new.svg) Ajout de nouveaux flux pour [synchroniser les données du catalogue](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) aux services Commerce via la ligne de commande.

### 3.3.3 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Ajout de nouveaux [types de recommandations](type.md) : Conversion (affichage au panier), Conversion (affichage à l’achat) et Récemment consultés. Ces nouveaux types de recommandations sont disponibles dans le module `magento/product-recommendations` version 3.2.2 et ultérieure.
![Correctif](../assets/fix.svg) Correction d’un problème en raison duquel le pare-feu d’application web (WAF) de Fastly bloquait incorrectement un cookie
![Correction](../assets/fix.svg) correction d’un problème en raison duquel les produits affectés à une vue de boutique autre que la vue par défaut n’étaient pas affichés dans le panneau _Aperçu du produit Recommendations_ lors de la création d’une recommandation pour cette vue de boutique spécifique
![Correction](../assets/fix.svg) correction d’un problème en raison duquel certains noms d’unités de recommandation dans Page Builder empêchaient l’affichage de l’unité de recommandation sur le storefront

### 3.3.2 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) Correction d’une dépendance manquante pour la prise en charge B2B

### 3.3.1 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de la tarification des groupes de clients B2B. Lorsque vous définissez un [filtre de prix](filters.md) sur une unité de recommandation, les clients B2B connectés voient le jeu de prix du groupe de clients pour les produits affichés.

### 3.3.0 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de la couche de données client Adobe pour normaliser la collecte de données comportementales sur les fonctionnalités et services Adobe Commerce. Consultez le [fichier lisez-moi](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md) pour en savoir plus.

### 3.2.6 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) Correction d’une erreur modale de JavaScript
![Correctif](../assets/fix.svg) Correction d’un problème en raison duquel le pare-feu d’application web (WAF) de Fastly bloquait incorrectement un cookie

### 3.2.5 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Services Magento renommés en [Services Commerce](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) et amélioration de la convivialité dans l’administration

### 3.2.4 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) Correction de l’erreur « Impossible de récupérer les données d’options de produit configurables » lors de l’indexation des attributs de produit

### 3.2.3 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) Correction de l’erreur « Impossible de récupérer les données d’options de produit configurables » lors de la synchronisation du catalogue
![Correctif](../assets/fix.svg) Correction d’un problème en raison duquel le code de magasin n’était pas défini correctement lorsque vous activiez la configuration « Ajouter le code de magasin à l’URL »
![Correctif](../assets/fix.svg) Amélioration de la détection des modifications de configuration du panneau d’administration pour s’assurer que ces modifications sont répercutées dans les données de synchronisation de catalogue

### 3.2.2 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Ajout de la possibilité de [prévisualiser les résultats des recommandations](create.md) au moment de la création. Cela peut nécessiter la mise à jour de votre module vers la dernière version.
![Nouveau](../assets/new.svg) Ajout de la possibilité de [surveiller et gérer](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) le processus de synchronisation du catalogue à partir de l’administration.
![Nouveau](../assets/new.svg) Ajout de [filtres](filters.md) pour contrôler quels produits sont affichés dans les recommandations.
![Nouveau](../assets/new.svg) Ajout du type de recommandation [Similarité visuelle](type.md#visualsim).

### 1.2.1 de magento/module-page-builder-product-recommendations pour Page Builder

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Ajout de la prise en charge de la version 3.2.0+ du module `magento/product-recommendations`

### 3.1.0 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) possibilité de [resynchroniser](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) votre catalogue avec les services SaaS via la ligne de commande.
![Nouveau](../assets/new.svg) Ajout de la prise en charge des préfixes de table de base de données
![Correctif](../assets/fix.svg) Suppression de la prise en charge de PHP 7.1

### 3.0.8 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) correction d’un problème en raison duquel des événements étaient envoyés pour la collecte de données avant la configuration du module, provoquant un trafic non valide

### 3.0.6 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) **(Beta)** Inclut la prise en charge du nouveau type de recommandation [Similarité visuelle](type.md#visualsim).

### 1.0.0 de magento/module-visual-product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) **(Beta)** [Similarité visuelle](type.md#visualsim). Avec le type de recommandation _Similarité visuelle_, vous pouvez déployer une unité de recommandation sur votre page de détails du produit qui affiche des produits visuellement similaires au produit affiché.

### 3.0.5 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) Correction de l’erreur « Impossible de récupérer les données des options du produit » qui pouvait se produire lors de l’exportation du catalogue.
![Correctif](../assets/fix.svg) Le symbole de devise dans la colonne _Chiffre d’affaires_ du tableau de bord _[!DNL Product Recommendations]_reflète désormais correctement la devise de base configurée.

### 3.0.4 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) Ajout de la prise en charge d’Adobe Commerce 2.4.0

### 3.0.3 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Correctif](../assets/fix.svg) Amélioration de l’implémentation des symboles dans le modèle de storefront

### 1.0.4 de magento/module-page-builder-product-recommendations pour Page Builder

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau ](../assets/new.svg) ajout du nom de la recommandation de produit lors de la modification du type de contenu Page Builder

### 3.0.2 magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) Ajout d’une colonne de statut sur la grille lors de la sélection des unités de recommandation dans Page Builder
![Correctif](../assets/fix.svg) Correction d’un problème lié à des protocoles http/https incorrects dans les URL de produit et d’image

### 3.0.1 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

Il s’agit d’une version majeure. [Modifiez](install-configure.md#update) le fichier racine composer.json de votre projet.

![Nouveau](../assets/new.svg) Récupérez les [!DNL Product Recommendations] des autres espaces de données SaaS. Vous pouvez ainsi utiliser des [!DNL Product Recommendations] calculées dans votre environnement de produit sur d’autres environnements hors production. [Switching SaaS Data Spaces](settings.md) décrit plus en détail cette fonctionnalité.

![Correctif](../assets/fix.svg) Correction d’un problème qui empêchait le passage en caisse pour les acheteurs qui utilisaient l’origine uBlock
![Correctif](../assets/fix.svg) correction d’un problème lié à l’envoi d’événements d’ajout au panier superflus

### 1.0.3 de magento/module-page-builder-product-recommendations pour Page Builder

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouveau](../assets/new.svg) prise en charge de Page Builder. Grâce à l’intégration de Page Builder, vous pouvez placer des unités de recommandation de manière précise et granulaire à n’importe quel emplacement arbitraire sur le contenu créé par Page Builder. Vous pouvez également mettre en forme les en-têtes et les unités de recommandation eux-mêmes. Accédez à [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) pour plus d’informations.

### 2.0.0 de magento/product-recommendations

[!BADGE Pris en charge]{type=Informative tooltip="Pris en charge"} Adobe Commerce versions 2.4.x et ultérieures

![Nouvelle](../assets/new.svg) Mise à jour de la disponibilité générale !

+++

## Documentation

Pour en savoir plus sur le développement [!DNL Product Recommendations] et [!DNL Product Recommendations] :

* [Guide d’utilisation](overview.md)
* [Documentation destinée aux développeurs](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
