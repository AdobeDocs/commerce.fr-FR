---
title: Limites et limites
description: Découvrez les limites et les limites de pour  [!DNL Live Search]  assurer qu’il répond aux besoins de votre entreprise.
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Limites et limites

En ce qui concerne la recherche de site, Adobe Commerce vous propose des options. Examinez les limites suivantes pour vous assurer que [!DNL Live Search] et [!DNL Catalog Service] répondent aux besoins de votre entreprise. Si vous avez besoin de fonctionnalités de recherche avancées telles que la recherche de contenu, l’algorithme Bring-your-own-algorithm (BYOA) ou le marchandisage basé sur les attributs, pensez à une solution de recherche tierce.

## Général

- Le module [Recherche avancée](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) est désactivé lors de l’installation de [!DNL Live Search] et le lien Recherche avancée dans le pied de page du storefront est supprimé.
- [Tarification de niveau](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier) n’est pas pris en charge dans le champ [!DNL Live Search] et le widget de page de liste de produits.
- Les prix des produits ne comprennent pas la taxe sur la valeur ajoutée (TVA).
- La recherche de contenu (pages et blocs CMS) n’est pas prise en charge.
- Il existe une limite de 10 000 produits pouvant être paginés. Bien que cette limite puisse être augmentée, elle peut avoir un impact sur les performances. Veillez à fournir des moyens significatifs de filtrer les produits au cas où une catégorie ou un résultat de recherche comporte un grand nombre de produits afin que les acheteurs n’aient pas à utiliser une pagination profonde.
- La limite stricte est de 1 Mo par attribut, y compris la description et les attributs personnalisés.
- L’adaptateur de recherche ne prend pas en charge les attributs de produit créés avec un modèle source personnalisé et utilisés comme facettes. Pour prendre en charge cette fonctionnalité, vous devez utiliser le [widget de page de liste de produits](plp-styling.md).
- Les types de produits personnalisés ne sont pas pris en charge.
- Les attributs personnalisés créés par programmation avec `"is_user_defined": false` ne sont pas pris en charge.
- Vous pouvez filtrer les résultats à l’aide des conditions « commence par » ou « contient » avec certaines limitations comme décrit [ici](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/#limitations).
- Vous ne pouvez effectuer le suivi des mesures de performances que l’année dernière.

## Indexation

- [!DNL Live Search] [index](indexing.md) jusqu’à un total de 450 attributs de produit par vue de magasin. Ils sont répartis comme suit :
   - 50 attributs triables
   - 200 attributs filtrables
   - 200 attributs interrogeables
- [!DNL Live Search] indexe uniquement les produits de la base de données Adobe Commerce.
- Les pages CMS ne sont pas indexées.
- Les attributs SKU, name et category peuvent être recherchés par défaut et ne peuvent pas être exclus de la recherche. Veillez à annuler l’affectation des produits des catégories s’ils ne sont pas censés s’y trouver.

## Facettes

- Un maximum de 100 attributs peuvent être configurés en tant que facettes à partir des 200 attributs filtrables qui peuvent être indexés.
- Dans une facette, 100 intervalles au maximum peuvent être renvoyés. Si vous devez renvoyer plus de 100 compartiments, [créez un ticket d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) afin qu’Adobe puisse analyser l’impact sur les performances et déterminer s’il est possible d’augmenter cette limite pour votre environnement.
- Les facettes dynamiques peuvent entraîner des problèmes de performances dans les index volumineux et les index de haute ordinalité. Si vous avez créé des facettes dynamiques et que vous constatez une dégradation des performances ou que la page ne se charge pas avec des erreurs de délai d’expiration, essayez de remplacer vos facettes par épinglées afin de déterminer si cela résout votre problème de performances.
- L’état des stocks (`quantity_and_stock_status`) n’est pas pris en charge en tant que facette. Vous pouvez utiliser `inStock: 'true'` pour filtrer les produits en rupture de stock. Cette fonctionnalité est prise en charge prête à l’emploi dans le module `LiveSearchAdapter` lorsque la valeur « True » est affectée à « Afficher les produits en rupture de stock » dans l’Administration des [!DNL Commerce].
- Les attributs de type date ne sont pas pris en charge sous la forme d’une facette.
- Les modifications apportées aux métadonnées d’attribut après l’ajout de cet attribut en tant que facette ne sont pas répercutées dans la facette .

## Requête

- [!DNL Live Search] utilise un point d’entrée [GraphQL unique](https://developer.adobe.com/commerce/services/graphql/live-search/) pour que les requêtes prennent en charge des fonctionnalités telles que la facettisation dynamique et la recherche en cours de saisie. Bien que similaire à l’API [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/), il existe quelques différences et certains champs peuvent ne pas être entièrement compatibles.
- Le nombre maximal de résultats pouvant être renvoyés dans une requête de recherche est de 10 000.
- Le nombre maximal de résultats par page est de 500.
- Il n’est pas possible de filtrer les résultats à l’aide d’un attribut de type date.

## Règles

- Le nombre maximal de [règles](rules.md) de marchandisage de recherche par vue de magasin est de 50.
- Le marchandisage de catégorie peut comporter une règle par catégorie.
- Le nombre maximal de conditions par règle est de 10.
- Le nombre maximal d’événements par règle est de 25.
- Pour éviter des résultats imprévisibles dans les réponses paginées, le nombre de produits épinglés ne doit pas dépasser la taille de page demandée.

## Synonymes

- [!DNL Live Search] pouvez gérer jusqu’à 200 [synonymes](synonyms.md) par affichage de magasin.

## Marchandisage de catégorie

- Une règle par catégorie peut être créée pour chaque vue de magasin. Chaque règle peut avoir :
   - Jusqu’à dix conditions
   - Jusqu’à 25 événements

## Autorisations B2B et de catégorie

- Les produits ne s’affichent pas s’ils ne sont pas ajoutés à un catalogue partagé par défaut.
- Pour restreindre les groupes de clients à l’aide des [autorisations de catégorie](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions) :
   - Les produits doivent être affectés à la catégorie racine.
   - Le groupe de clients « Non connecté » doit se voir attribuer des autorisations de navigation « Autoriser ».
   - Pour limiter les produits au groupe de clients « Non connecté », accédez à chaque catégorie et définissez des autorisations pour chaque [groupe de clients](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- La prise en charge prête à l’emploi du B2B avec le widget PLP sur PWA Studio n’est pas prise en charge à ce stade. Cependant, vous pouvez [utiliser l’API](install.md#pwa-support) pour implémenter cette fonctionnalité.
- Les facettes de catégories dans [!DNL Live Search] peuvent afficher des catégories qui ne sont pas affichables pour un [groupe de clients](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage) spécifique.
- [!DNL Live Search] peut prendre en charge jusqu’à 1 000 groupes de clients.

## [!DNL Storefront popover]

- Le [[!DNL popover]](storefront-popover.md) est disponible uniquement pour les magasins qui utilisent le thème *Luma* ou un thème personnalisé basé sur *Luma*. Les chemins de navigation de la page des résultats de recherche n’auront pas de style *Luma*.
- Le [!DNL popover] ne prend pas en charge le thème *vierge*.
- Le [!DNL popover] n’est pas pris en charge dans le formulaire de commande rapide.
- Les listes de souhaits et les comparaisons de produits ne sont pas prises en charge.
- Le symbole monétaire du sol péruvien (PEN) n&#39;est pas pris en charge.

## Dépannage

Pour obtenir de l’aide sur la résolution de certains problèmes courants dans [!DNL Live Search], consultez les articles de la base de connaissances suivants :

- [[!DNL Live Search] catalogue non synchronisé](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync)
- [[!DNL Live Search] le tableau de bord et le classement des résultats de recherche sont incorrects](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect)
- [[!DNL Live Search] affiche les produits en rupture de stock, quels que soient les paramètres d’état de stock dans Admin](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-displays-out-of-stock-products)
- [[!DNL Live Search] les facettes ne sont pas triées par ordre alphabétique](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted)

Si vous avez besoin d’aide supplémentaire, contactez l’[assistance ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
