---
title: Limites et limites
description: Découvrez les limites et les limites de pour  [!DNL Product Recommendations]  assurer qu’il répond aux besoins de votre entreprise.
role: Admin, Developer
source-git-commit: 66830c9d950a27269aca1bda0dcc7d0d86f05647
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Limites et limites

Examinez les limites suivantes pour vous assurer qu’[!DNL Product Recommendations] répond aux besoins de votre entreprise. La connaissance de ces contraintes vous permet de planifier l’implémentation, de configurer des filtres et d’éviter les problèmes courants.

## Général

- **Types de produits** - Les types de produits pris en charge sont les suivants _simple_, _configurable_, _virtuel_, _téléchargeable_ et _chèque-cadeau_. Les types de produits _Bundle_, _grouped_ et personnalisés ne sont pas pris en charge. Si votre catalogue contient un grand nombre de types de produits non pris en charge, vous pouvez vous attendre à un faible [score de préparation](create.md#readiness-indicators). Voir [Filtrer par type de produit](filters.md#type).
- **SKU avec espaces** : les SKU qui contiennent des espaces peuvent réduire la pertinence des recommandations et doivent être évitées dans la mesure du possible.
- **Page du panier** - Les recommandations de produits ne sont pas prises en charge sur la page du panier lorsque votre boutique est configurée pour [afficher la page du panier immédiatement après l’ajout d’un produit au panier](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration). Voir [Création de recommandations](create.md).
- **Produits enfants** - Les produits enfants d’un produit configurable (visibilité _Non visible individuellement_) ne s’affichent pas dans une unité de recommandation. Seul le produit configurable (parent) peut apparaître. Voir [Filtrer les produits](filters.md#product).
- **Produits désactivés ou non visibles** - Les produits désactivés ou non visibles individuellement ne peuvent jamais apparaître dans les recommandations et ne peuvent pas être sélectionnés dans les filtres de produit.
- **Prix spéciaux** - [Prix spéciaux](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/products/pricing/product-price-special) avec dates de début et de fin ne sont pas pris en charge dans les unités de recommandation. Un produit avec un prix spécial peut apparaître dans les recommandations, mais l&#39;unité n&#39;affiche pas le prix spécial, la date de début ou la date de fin. Les acheteurs voient le prix normal (ou d’autres données de prix fournies par votre catalogue/flux de prix) jusqu’à ce qu’ils ouvrent la page du produit.

## Unités de recommandation

- **Unités actives par type de page** - Vous pouvez créer jusqu’à 50 unités de recommandation actives pour chaque type de page (Accueil, Catégorie, Détails du produit, Panier, Confirmation). Le type de page est grisé dans le flux de création lorsque la limite est atteinte.
- **Produits par unité** - Le nombre de produits affichés dans une unité de recommandation peut être défini de 5 (par défaut) à 20 maximum.
- **État de brouillon** - Après avoir enregistré une recommandation en tant que brouillon, vous ne pouvez pas modifier le type de page ou de recommandation pour cette unité. D’autres paramètres peuvent être modifiés avant l’activation.

## Filtres et conditions

- **Conditions dynamiques** - Les conditions dynamiques (par exemple, « produits de la même catégorie que le produit actuel » ou « plage de prix relative ») sont disponibles sur chaque type de page, à l’exception de la page d’accueil. Ils ne sont pas non plus disponibles sur les pages où des recommandations sont placées avec Page Builder. Voir [Conditions](filters.md#conditions).

## Environnements de prévisualisation et hors production

- **Aperçu récemment consulté** - Le type de recommandation _Récemment consulté_ ne peut pas être prévisualisé dans l’administration, car les données sont basées sur l’historique du navigateur et ne sont pas disponibles dans le contexte de l’administration. Voir [Aperçu des recommandations](create.md#preview).
- **Recommandations à partir d’un autre espace de données** - Lorsque vous [récupérez des recommandations à partir d’un autre espace de données SaaS](settings.md) (par exemple, de production) dans un storefront hors production, vous pouvez afficher les recommandations, mais vous ne pouvez pas cliquer dessus pour accéder aux pages de produits. Il en est ainsi pour la prévisualisation et le test.
- **GraphQL et autre espace de données** - Lors de l’utilisation de Product Recommendations via [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/), le paramètre `alternateEnvironmentId` (utilisé pour récupérer les recommandations d’un autre espace de données) n’est pas disponible. Utilisez l’API REST ou les paramètres d’administration pour changer la source de recommandations en mode hors production.

## API et configuration

- **Clés API (4.x et ultérieures)** - Vous devez fournir des clés API publiques et privées pour les environnements de sandbox et de production. Si vous ne fournissez pas les deux paires de clés API, vous ne pouvez pas accéder à la fonctionnalité de recommandations de produits dans l’Administration. La collecte de données sur votre storefront et les recommandations existantes continuent de fonctionner. Voir [&#x200B; Installation et configuration &#x200B;](install-configure.md).

## Restrictions des cookies

- Lorsque le [mode de restriction des cookies](setting-cookie.md) est activé et que les acheteurs n’ont pas accepté les cookies, certains types de recommandations qui reposent sur des données comportementales peuvent ne pas s’afficher ou présenter des résultats limités.
- Les types de recommandations qui ne reposent pas sur des données comportementales (par exemple, _Les plus consultés_, _Similarité visuelle_) continuent à fonctionner lorsque les restrictions sur les cookies sont activées.
- Lorsque les restrictions de cookie sont activées, Product Recommendations ne collecte ni ne stocke de données comportementales dans les cookies ou le stockage local tant que l’acheteur n’a pas donné son consentement.

## Page Builder

- **Mesures et vues de magasin** - Les mesures des unités de recommandation de Page Builder s’affichent uniquement sur la vue de magasin par défaut dans l’espace de travail des recommandations de produits. Pour afficher les mesures de recommandation de Page Builder sur une vue de magasin autre que la vue par défaut, vous devez ouvrir et [modifier](edit.md) l’unité de recommandation Page Builder dans cette vue de magasin et l’enregistrer ; les mesures s’affichent alors pour cette vue de magasin. Voir [&#x200B; Intégration de Page Builder &#x200B;](page-builder.md).

## B2B

- Les recommandations de produits respectent les [autorisations de catégorie](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html), [catalogues partagés](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) et la tarification spécifique au groupe de clients. Les acheteurs ne voient que les recommandations des produits auxquels ils peuvent accéder en fonction de leur affectation de segment et de catalogue. Voir [&#x200B; Intégration &#x200B;](onboarding.md).

## Données et préparation

- **Données comportementales** - De nombreux types de recommandations nécessitent des données comportementales storefront suffisantes (vues, ajout au panier, achats). Les nouveaux magasins ou les magasins à faible trafic peuvent afficher des résultats limités, voire inexistants, pour ces types de magasins jusqu’à ce que des données adéquates soient collectées. Surveillez les [indicateurs de préparation](create.md#readiness-indicators) dans l’administrateur.
- **Évaluation sans données de production** - Dans un environnement hors production sans données comportementales, le seul type de recommandation que vous pouvez tester sans extraire des données de production est _Plus similaire à ceci_, qui utilise uniquement la similarité catalogue. Voir [Environnement d’évaluation](staging-environment.md).

## Dépannage

Pour obtenir de l’aide sur la synchronisation des catalogues, les recommandations qui ne s’affichent pas ou d’autres problèmes courants, recherchez dans la [Base de connaissances de Commerce](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/overview) ou contactez l’[assistance technique](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
