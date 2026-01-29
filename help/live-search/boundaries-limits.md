---
title: Limites et limites
description: Découvrez les limites et les limites de pour  [!DNL Live Search]  assurer qu’il répond aux besoins de votre entreprise.
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: 2b38d9f6cb0b45f81acabec4b90251c13e7f146b
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 0%

---

# Limites et limites

En ce qui concerne la recherche de site, Adobe Commerce vous propose des options. Examinez les limites suivantes pour vous assurer que [!DNL Live Search] et [!DNL Catalog Service] répondent aux besoins de votre entreprise. Si vous avez besoin de fonctionnalités de recherche avancées telles que la recherche de contenu, l’algorithme Bring-your-own-algorithm (BYOA) ou le marchandisage basé sur les attributs, pensez à une solution de recherche tierce.

## Général

- L’adaptateur de recherche est [obsolète](release-notes.md#live-search-400) depuis la [!DNL Live Search] 4.0.0. Le widget de page de liste de produits (PLP) est la solution prise en charge pour toutes les implémentations [!DNL Live Search] à l’avenir. La carte de recherche ne reçoit que les mises à jour liées à la sécurité. Pour plus d’informations sur la migration vers le widget PLP[&#x200B; consultez le &#x200B;](migrate-to-plp.md) guide de migration .
- Le module [Recherche avancée](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/catalog/search/search) est désactivé lors de l’installation de [!DNL Live Search] et le lien Recherche avancée dans le pied de page du storefront est supprimé.
- [Tarification de niveau](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/products/pricing/product-price-tier) n’est pas pris en charge dans le champ [!DNL Live Search] et le widget de page de liste de produits.
- Les prix des produits incluent la taxe sur la valeur ajoutée (TVA), mais [!DNL Live Search] ne pouvez pas afficher la TVA comme une valeur distincte.
- La recherche de contenu (pages et blocs CMS) n’est pas prise en charge.
- Le nombre maximal de résultats pouvant être paginés est de 10 000. Pour vous assurer que les acheteurs n’ont pas à utiliser une pagination profonde lorsqu’une catégorie ou un résultat de recherche inclut un grand nombre de produits, fournissez des moyens significatifs de filtrer les produits.
- La limite stricte est de 1 Mo par attribut, y compris la description et les attributs personnalisés.
- L’adaptateur de recherche ne prend pas en charge les attributs de produit créés avec un modèle source personnalisé et utilisés comme facettes. Pour prendre en charge cette fonctionnalité, vous devez utiliser le [widget de page de liste de produits](plp-styling.md).
- Les types de produits personnalisés ne sont pas pris en charge.
- Les attributs personnalisés créés par programmation avec `"is_user_defined": false` ne sont pas pris en charge.
- Vous pouvez filtrer les résultats à l’aide des conditions « commence par » ou « contient » avec certaines limitations, comme décrit dans la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations).
- Vous ne pouvez effectuer le suivi des mesures de performances que l’année dernière.
- Si une requête de recherche contient plusieurs mots, l’espace vide entre les mots les traite comme des termes de recherche distincts. Utilisez [synonymes](./synonyms.md) si vous souhaitez tenir compte des requêtes de recherche à plusieurs mots.
- [!DNL Live Search] ne prend pas en charge les [redirections de terme de recherche](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/catalog/search/search-terms) en mode natif. Implémentez des redirections à l’aide de Fastly ou d’une autre configuration personnalisée.

## Indexation

- [!DNL Live Search] [index](indexing.md) jusqu’à un total de 450 attributs de produit par vue de magasin. Ils sont répartis comme suit :
   - 50 attributs triables
   - 200 attributs filtrables
   - 200 attributs interrogeables
- [!DNL Live Search] indexe uniquement les produits de la base de données Adobe Commerce.
- Les pages CMS ne sont pas indexées.
- Les attributs SKU, name et category peuvent être recherchés par défaut et ne peuvent pas être exclus de la recherche. Veillez à annuler l’affectation des produits des catégories s’ils ne sont pas censés s’y trouver.

## Facettes

- À partir du jeu d’attributs filtrables définis, vous pouvez configurer jusqu’à 100 attributs sous forme de facettes.
- Dans une facette, 100 intervalles au maximum peuvent être renvoyés. Si vous devez renvoyer plus de 100 compartiments, [créez un ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) afin qu’Adobe puisse analyser l’impact sur les performances et déterminer s’il est possible d’augmenter cette limite pour votre environnement.
- Les facettes dynamiques peuvent entraîner des problèmes de performances dans les index volumineux et les index de haute ordinalité. Si vous avez créé des facettes dynamiques et que vous constatez une dégradation des performances ou que la page ne se charge pas avec des erreurs de délai d’expiration, essayez de remplacer vos facettes par épinglées afin de déterminer si cela résout votre problème de performances.
- L’état des stocks (`quantity_and_stock_status`) n’est pas pris en charge en tant que facette. Vous pouvez utiliser `inStock: 'true'` pour filtrer les produits en rupture de stock. Cette fonctionnalité est prise en charge prête à l’emploi dans le module `LiveSearchAdapter` lorsque la valeur « True » est affectée à « Afficher les produits en rupture de stock » dans l’Administration des [!DNL Commerce].
- Les attributs de type date ne sont pas pris en charge sous la forme d’une facette.
- Les modifications apportées aux métadonnées d’attribut après l’ajout de cet attribut en tant que facette ne sont pas répercutées dans la facette .
- Vous pouvez avoir jusqu’à 50 attributs triables et 200 attributs consultables.

## Requête

- [!DNL Live Search] utilise un point d’entrée [GraphQL unique](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) pour que les requêtes prennent en charge des fonctionnalités telles que la facettisation dynamique et la recherche en cours de saisie. Bien que similaire à l’API [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/), il existe quelques différences et certains champs peuvent ne pas être entièrement compatibles.
- Le nombre maximal de résultats pouvant être renvoyés dans une requête de recherche est de 10 000.
- Le nombre maximal de résultats par page est de 500.
- Il n’est pas possible de filtrer les résultats à l’aide d’un attribut de type date.

>[!NOTE]
>
>Le tri par position nécessite un filtre `categoryPath` ou `categoryIds` valide pour être actif. [En savoir plus](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#error-handling-for-categorypath-and-categoryids).

## Recherche de marchandisage

- Le nombre maximal de [règles](rules.md) de marchandisage de recherche par vue de magasin est de 50.
- Le nombre maximal de conditions par règle est de 10.
- Le nombre maximal d’événements par règle est de 25.
- Les règles et les produits classés manuellement sont appliqués aux résultats de la recherche lorsque l’ordre de tri par défaut « Trier par : les plus pertinents » est sélectionné. Si un acheteur modifie l’ordre de tri pour qu’il ressemble à un tri par nom ou prix, les règles et les classements manuels ne sont plus en vigueur.
- Pour éviter des résultats imprévisibles dans les réponses paginées, le nombre de produits épinglés ne doit pas dépasser la taille de page demandée.

## Synonymes

- [!DNL Live Search] pouvez gérer jusqu’à 200 [synonymes](synonyms.md) par affichage de magasin.

## Marchandisage de catégorie

- Vous pouvez créer une règle par catégorie pour chaque vue de magasin.
- Le nombre maximal de conditions par règle est de 10.
- Le nombre maximal d’événements par règle est de 25.
- Les règles sont appliquées lorsqu’une catégorie spécifique est ouverte sur le storefront et qu’il existe une règle pour cette catégorie. Pour les règles de marchandisage de catégorie, l’ordre de tri par défaut est « Trier par : Position ». Si un acheteur modifie l’ordre de tri, tous les produits masqués, épinglés et enfouis ne sont plus triés.

## Autorisations B2B et de catégorie

- Les produits ne s’affichent pas s’ils ne sont pas ajoutés à un catalogue partagé par défaut.
- Pour restreindre les groupes de clients à l’aide des [autorisations de catégorie](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/categories/category-permissions) :
   - Les produits doivent être affectés à la catégorie racine. (**Remarque :** vous pouvez supprimer cette limitation en mettant à jour l’extension d’exportation de données SaaS vers la version 103.4.0+. Voir [Gérer l’extension d’exportation des données](../data-export/manage-extension.md).
   - Le groupe de clients « Non connecté » doit se voir attribuer des autorisations de navigation « Autoriser ».
   - Pour limiter les produits au groupe de clients « Non connecté », accédez à chaque catégorie et définissez des autorisations pour chaque [groupe de clients](https://experienceleague.adobe.com/fr/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- La prise en charge prête à l’emploi du B2B avec le widget PLP sur PWA Studio n’est pas prise en charge à ce stade. Cependant, vous pouvez [utiliser l’API](install.md#pwa-support) pour implémenter cette fonctionnalité.
- Les facettes de catégories dans [!DNL Live Search] peuvent afficher des catégories qui ne sont pas affichables pour un [groupe de clients](https://experienceleague.adobe.com/fr/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage) spécifique.
- [!DNL Live Search] peut prendre en charge jusqu’à 1 000 groupes de clients.

## [!DNL Storefront popover]

- Le [[!DNL popover]](storefront-popover.md) est disponible uniquement pour les magasins qui utilisent le thème *Luma* ou un thème personnalisé basé sur *Luma*. Les chemins de navigation de la page des résultats de recherche n’auront pas de style *Luma*.
- Le [!DNL popover] ne prend pas en charge le thème *vierge*.
- Le [!DNL popover] n’est pas pris en charge dans le formulaire de commande rapide.
- Les listes de souhaits et les comparaisons de produits ne sont pas prises en charge.
- Le symbole monétaire du sol péruvien (PEN) n&#39;est pas pris en charge.

## Dépannage

Pour obtenir de l’aide sur la résolution des problèmes courants dans [!DNL Live Search], consultez les articles de la base de connaissances suivants :

- [[!DNL Live Search] catalogue non synchronisé](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) - Fournit des solutions pour les cas où les données de catalogue de produits ne se synchronisent pas correctement entre votre boutique Adobe Commerce et le service Live Search. Cet article explique comment vérifier le statut de la synchronisation, identifier les erreurs de synchronisation et résoudre les problèmes de synchronisation des données.
- [[!DNL Live Search] tableau de bord et classement des résultats de recherche incorrects](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect) - Résout les problèmes où les résultats de recherche ou les mesures de performances affichés dans le tableau de bord de la recherche en direct ne s’affichent pas comme prévu. Cet article explique comment résoudre les incohérences de classement et les incohérences des données du tableau de bord.
- [[!DNL Live Search] les facettes ne sont pas triées par ordre alphabétique](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted) - résout le problème où les valeurs de facette apparaissent dans un ordre inattendu plutôt que par ordre alphabétique. Cet article décrit les étapes à suivre pour configurer et corriger le comportement de tri à facettes sur votre storefront.

Si vous avez besoin d’aide supplémentaire, contactez l’[assistance &#x200B;](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
