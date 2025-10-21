---
title: Configuration de Live Search
description: L’espace  [!DNL Live Search]  travail permet de configurer, de gérer et de surveiller les performances des recherches.
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: 4ba9734946f551784cd429ffa7cb23358f0f9710
workflow-type: tm+mt
source-wordcount: '2013'
ht-degree: 0%

---

# Configuration de Live Search

L’espace de travail vous permet de configurer, de gérer et de surveiller les performances d’[!DNL Live Search]. Le menu en haut permet d’accéder aux outils dans chaque domaine fonctionnel. Les fonctions disponibles reflètent la sélection actuelle du menu.

![Workspace](assets/workspace.png)

## Collecte de données

Pour vous assurer que chaque domaine fonctionnel de l’espace de travail contient les données correctes, vous devez configurer la collecte de données en fonction de l’implémentation de storefront sélectionnée :

1. Luma - La collecte de données est disponible par défaut.
1. Découplé - La collecte de données doit être configurée manuellement, en fonction de l’implémentation du storefront.

Si vous utilisez un storefront découplé, reportez-vous à la documentation suivante pour obtenir plus d’informations sur les événements requis à ajouter :

- [Événements requis](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search) pour le tableau de bord Live Search.
- [collecteur d’événements Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) qui doit être ajouté comme condition préalable.
- [Exemples](https://github.com/adobe/commerce-events/tree/main/examples) de la structure des événements.

### Clients du secteur de la santé

Si vous êtes un client du secteur de la santé et que vous avez installé l’extension [Data Services HIPAA](../data-connection/hipaa-readiness.md#installation), qui fait partie de l’extension [Data Connection](../data-connection/overview.md), les données d’événement de storefront utilisées par [!DNL Live Search] ne sont plus capturées. En effet, les données d’événement de storefront sont générées côté client. Pour continuer à capturer et à envoyer des données d’événement de storefront, réactivez la collecte d’événements pour [!DNL Live Search]. Voir [configuration générale](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services) pour en savoir plus.

## Définir la portée

Au départ, la [portée](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) de tous les paramètres [!DNL Live Search] est définie sur `Default Store View`. Si votre installation [!DNL Commerce] comprend plusieurs vues de magasin, définissez **Portée** sur la vue [magasin](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) où s’appliquent les paramètres de facettes.

## Options de menu

| Option | Description |
|--- |--- |
| [Performances](performance.md) | Le tableau de bord fournit à insight des informations sur les performances de recherche de produits. |
| [Facettage](facets.md) | Filtrage haute performance qui utilise plusieurs dimensions de valeurs d’attribut pour affiner les critères de recherche. |
| [&#x200B; Synonymes &#x200B;](synonyms.md) | Étendez la portée de la recherche afin d’inclure les mots que les acheteurs peuvent utiliser pour trouver des produits différents de ceux de votre catalogue. |
| [Recherche de marchandisage](rules.md) | Donnez forme à l’expérience de recherche avec des règles logiques qui déclenchent des actions planifiées. Boostez, enfouissez, épinglez ou masquez des produits pour étalonner les résultats de recherche afin de soutenir les objectifs de votre entreprise. |
| [Marchandisage de catégorie](category-merch.md) | Appliquez des règles et un marchandisage intelligent au niveau de la catégorie. |
| [GraphQL](graphql.md) | Les développeurs connectés à l’administrateur de votre boutique peuvent composer et tester des requêtes avec des données de catalogue réelles. Pour en savoir plus, accédez à la section [Présentation de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) dans la documentation destinée aux développeurs [!DNL Live Search]. |
| [Paramètres](settings.md) | Déterminez comment les valeurs de facette de prix sont regroupées par plage de prix dans le storefront et définissez la langue d’indexation. |

## Définir les attributs comme pouvant faire l’objet d’une recherche

Pour obtenir des résultats hautement ciblés, passez en revue l’ensemble des attributs de produit [consultables](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) (`searchable=true`). Pour garantir la pertinence, assurez-vous que les attributs ne peuvent être recherchés que s’ils contiennent du contenu ayant une signification claire et concise. Évitez d’utiliser des attributs contenant du texte moins précis et plus long, comme `description`, qui bien que la recherche soit activée par défaut, peut réduire la précision des résultats de recherche. Par exemple, si une personne recherche un « short » et qu’il existe des chemises dont la description inclut le terme « manches courtes », les chemises sont incluses dans les résultats de la recherche.

Pour que les attributs puissent faire l’objet de recherches, procédez comme suit :

1. Dans l’administration, accédez à **Magasins** > *Attribut* > **Produit**.
1. Sélectionnez l’attribut pour lequel vous souhaitez pouvoir effectuer des recherches, par exemple `color`.
1. Sélectionnez **Propriétés du storefront** et définissez **Utiliser dans la recherche** sur `yes`.

[!DNL Live Search] respecte également le [poids](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search) d’un attribut de produit, tel que défini dans Adobe Commerce. Les attributs ayant un poids plus élevé apparaissent plus haut dans les résultats de la recherche.

Les attributs suivants peuvent toujours faire l’objet de recherches :

- `sku`
- `name`
- `categories`

### Recherche en couches et développement de types de recherche

La recherche en couches, ou recherche dans une recherche, est un puissant système de filtrage basé sur les attributs qui étend la fonctionnalité de recherche traditionnelle pour inclure des paramètres de recherche supplémentaires. Ces paramètres de recherche supplémentaires permettent une découverte de produit plus précise et plus flexible.

>[!NOTE]
>
>La recherche en couches est disponible dans la version 4.6.0 de Live Search.

Avec la recherche par couches, vous pouvez :

- Permettre aux acheteurs de rechercher dans les résultats de la recherche.
- Utilisez l’indexation de la recherche `startsWith` et `contains` dans le deuxième calque de la recherche superposée pour affiner davantage les résultats.

Les fonctionnalités de recherche avancée sont implémentées via le paramètre `filter` dans la requête [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) à l’aide d’opérateurs spécifiques :

- **Recherche superposée** - Effectuez une recherche dans un autre contexte de recherche - Grâce à cette fonctionnalité, vous pouvez effectuer jusqu’à deux couches de recherche pour vos requêtes de recherche. Par exemple :

   - **Recherche de la couche 1** - Recherchez « moteur » sur `product_attribute_1`.
   - **Recherche de la couche 2** - Recherchez « numéro de pièce 123 » sur `product_attribute_2`. Dans cet exemple, le « moteur » est recherché dans les résultats par « numéro de pièce 123 ».

  La recherche en couches est disponible pour l’indexation de la recherche `startsWith` et l’indexation de la recherche `contains` dans le deuxième calque de la recherche en couches, comme décrit ci-dessous :

- **startsWith search indexation** - Effectuez une recherche à l’aide de l’indexation `startsWith`. Cette nouvelle fonctionnalité permet :

   - Recherche de produits dont la valeur d’attribut commence par une chaîne spécifiée.
   - La configuration d’une recherche « se termine par » afin que les acheteurs puissent rechercher des produits pour lesquels la valeur d’attribut se termine par une chaîne particulière. Pour activer une recherche « se termine par », l’attribut de produit doit être ingéré en inverse et l’appel API doit également être une chaîne inversée. Par exemple, si vous souhaitez rechercher un nom de produit qui se termine par « pantalon », vous devez l’envoyer sous la forme « stnap ».

- **contient l’indexation de la recherche** - Recherchez un attribut à l’aide de l’indexation contient. Cette nouvelle fonctionnalité permet :

   - Recherche d’une requête dans une chaîne plus grande. Par exemple, si un acheteur recherche le numéro de produit « PE-123 » dans la chaîne « HAPE-123 ».

      - Remarque : ce type de recherche est différent de la recherche existante [expression](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase), qui effectue une recherche de saisie automatique. Par exemple, si la valeur de l’attribut de votre produit est « pantalon extérieur », une expression de recherche renvoie une réponse pour « out pan », mais ne renvoie pas de réponse pour « oor ants ». Une recherche Contient , cependant, renvoie une réponse pour « fourmis ».

Ces nouvelles conditions améliorent le mécanisme de filtrage des requêtes de recherche pour affiner les résultats de recherche. Ces nouvelles conditions n’affectent pas la requête de recherche principale.

#### Mise en œuvre

1. Dans Admin, [définissez un attribut de produit](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) pour pouvoir effectuer des recherches.

   Voir la liste des [attributs](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) pouvant faire l’objet d’une recherche.

1. Spécifiez la fonctionnalité de recherche de cet attribut, par exemple **Contient** (par défaut) ou **Commence par**. Vous pouvez spécifier un maximum de six attributs à activer pour **Contient** et de six attributs à activer pour **Commence par**. En outre, pour l’indexation **Contient**, la longueur de la chaîne est limitée à 50 caractères ou moins.

   ![Spécifier la fonctionnalité de recherche](./assets/search-filters-admin.png)

1. Consultez la [documentation pour les développeurs](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) pour obtenir des exemples de mise à jour de vos appels API [!DNL Live Search] à l’aide des nouvelles fonctionnalités de recherche `contains` et `startsWith`.

   Vous pouvez implémenter ces nouvelles conditions sur votre page de résultats de recherche. Par exemple, vous pouvez ajouter une nouvelle section sur la page où l’acheteur peut affiner davantage ses résultats de recherche. Vous pouvez permettre aux acheteurs de sélectionner des attributs de produit spécifiques, tels que « Fabricant », « Numéro de pièce » et « Description ». À partir de là, ils effectuent une recherche dans ces attributs à l’aide des conditions `contains` ou `startsWith`.

### Cas d’utilisation de la recherche par couches plutôt que des facettes

La recherche superposée et les facettes ont des objectifs différents dans la découverte de produits, et le choix entre ces objectifs dépend de votre cas d’utilisation spécifique :

**Utiliser la recherche par couches lorsque :**

- Vous devez effectuer une recherche dans les résultats de recherche à l’aide de plusieurs critères.
- Utiliser des numéros de pièce, des SKU ou des spécifications techniques lorsque les utilisateurs connaissent des informations partielles.
- Les acheteurs doivent affiner les résultats étape par étape avec des critères imbriqués.
- Vous souhaitez réduire le nombre d’appels API en combinant plusieurs critères de recherche dans une seule requête.
- Vous devez implémenter des modèles de recherche spécifiques à l’entreprise qui vont au-delà de la navigation à facettes standard.

**Utilisation des facettes lorsque :**

- Filtrage standard des catégories, prix, marques et attributs
- Offrir des options de filtre intuitives que les utilisateurs peuvent facilement comprendre et sélectionner
- Affichage des options disponibles en fonction des résultats de la recherche actuelle
- Affichage du nombre de filtres et des plages qui aident les utilisateurs à comprendre les options disponibles
- Utiliser des caractéristiques de produit courantes telles que la couleur, la taille, le matériau, etc.

**Bonne pratique :** utilisez la recherche par couches pour les recherches techniques complexes où les utilisateurs et utilisatrices disposent de critères spécifiques et utilisez des facettes pour le filtrage standard d’e-commerce lorsque les utilisateurs et utilisatrices souhaitent explorer et réduire les options visuellement.

## Facettes et synonymes

Les facettes et les synonymes sont un autre moyen d’améliorer l’expérience de recherche de vos clientes et clients.

[Facettes](facets.md) sont des attributs de produit définis dans [!DNL Live Search] pour pouvoir être filtrés. Vous pouvez définir n’importe quel attribut filtrable en tant que facette dans [!DNL Live Search], mais il existe des [limites](boundaries-limits.md) au nombre de facettes que vous pouvez rechercher en même temps.

>[!NOTE]
>
>Un attribut de produit ne peut être filtré que si la configuration de l’attribut de produit possède les propriétés requises : *Utiliser dans la recherche = Non*, *Utiliser dans les résultats de recherche Navigation superposée=oui* et *Utiliser dans la navigation superposée=Filtrable (avec résultats)*. Si ces propriétés sont manquantes ou ne sont pas correctement définies, l’attribut n’est pas visible dans la configuration de facettes. Pour obtenir des instructions de configuration, voir [Ajouter une facette](facets-add.md#add-a-facet).

[Synonymes](synonyms.md) sont des termes que vous pouvez définir pour aider les utilisateurs à trouver le bon produit. Les utilisateurs qui recherchent un pantalon peuvent taper « pantalon » ou « pantalon ». Vous pouvez définir des synonymes afin que ces termes de recherche amènent les utilisateurs aux résultats « pantalons ».

## Paramètres de configuration de Commerce

La section suivante décrit les paramètres de configuration Commerce pris en charge et non pris en charge pour [!DNL Live Search].

### Valeurs de configuration prises en charge

>[!IMPORTANT]
>
>Il est vivement recommandé d’utiliser les widgets de liste de produits, activés par défaut dans Live Search 4.0.0. Les widgets sont destinés à remplacer complètement l&#39;implémentation de l&#39;adaptateur dans les prochaines versions. Pour en savoir plus, voir [Activation des widgets de liste de produits](install.md#enable-product-listing-widgets).

| Paramètre de configuration Commerce | Description | Prise en charge par une fenêtre contextuelle | Pris en charge par l&#39;adaptateur |
|---|---|---|---|
| Magasins > Configuration > Catalogue > Catalogue > Recherche catalogue > Autoriser tous les produits par page | S’il est défini sur `Yes`, inclut l’option `ALL` dans le contrôle « Afficher par page ». | Oui. 500 produits max. | Oui. 500 produits max. |
| Magasins > Configuration > Catalogue > Catalogue > Recherche catalogue > Longueur de requête minimale | Nombre minimum de caractères autorisés dans une recherche catalogue. | Oui | Oui |
| Magasins > Configuration > Catalogue > Catalogue > Recherche catalogue > Produits par page sur la grille Valeurs autorisées | Détermine le nombre de produits affichés dans la vue Grille. | Oui | Oui |
| Magasins > Configuration > Catalogue > Catalogue > Recherche catalogue > Produits par page sur la valeur par défaut de la grille | Détermine le nombre de produits affichés par défaut par page dans la vue Grille. | Oui. 500 produits max. | Oui. 500 produits max. |
| Magasins > Configuration > Catalogue > Inventaire > Afficher les produits en rupture de stock | Affiche les produits en rupture de stock. | Oui | Oui |
| Magasins > Configuration > Devise > Devise d’affichage par défaut | Devise principale utilisée pour afficher les prix. | Oui | Oui |
| Magasins > Configuration > Général > Configuration de la devise > Options de devise > Devise de base | Devise principale utilisée pour tous les paiements en ligne. | Oui | Oui |

Les prix dans la page de liste de produits du widget et la fenêtre contextuelle sont convertis en devise d’affichage par défaut à l’aide des taux de change configurés.

### Valeurs de configuration non prises en charge

| Paramètre de configuration Commerce | Description | Remarques |
|---|---|---|
| Magasins > Configuration > Catalogue > Storefront > Mode Liste | Détermine le format de la liste des résultats de recherche. | Effectue correctement le rendu, mais les événements ne sont pas envoyés pour certaines interactions de page |
| Magasins > Configuration > Catalogue > Catalogue > Recherche catalogue > Longueur maximale de la requête | Nombre maximal de caractères autorisés dans une recherche catalogue. | Non implémenté ; les services de recherche acceptent jusqu’à 255 caractères |
| Configuration > Ventes > Taxe > Paramètres D’Affichage Des Prix > Afficher Les Prix Des Produits Dans Le Catalogue | Détermine si les prix des produits publiés dans le catalogue incluent ou excluent la taxe, ou affichent deux versions du prix ; l&#39;une avec et l&#39;autre sans taxe |  |
| Magasins > Configuration > Catalogue > Storefront > Liste des produits Trier par | Détermine l’ordre de tri de la liste des résultats de recherche. | Ne s’applique pas au [!DNL Live Search] [&#x200B; Widget de page de liste de produits &#x200B;](plp-styling.md) |

### Termes de recherche

[!DNL Live Search] prend en charge les [redirections de termes de recherche](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html) dans les implémentations où Adobe Commerce gère le routage, par exemple sur Luma et d’autres thèmes basés sur php.

## Valeurs d’attribut par défaut

Les attributs de produit suivants possèdent des [propriétés storefront](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) qui sont utilisées par [!DNL Live Search] et activées par défaut.

| Propriété | Storefront, propriété | Attribut |
|---|---|---|
| Triable | Utilisé pour le tri dans la liste de produits | `price` |
| Indexable | Utiliser dans la recherche | `price` <br />`sku`<br />`name` |
| FiltrableInSearch | Utilisation dans la navigation superposée - Filtrable (avec les résultats) | `price`<br />`visibility`<br />`category_name` |

## Propriétés d’attribut non système par défaut

Le tableau suivant présente les propriétés de recherche et de filtrage par défaut des attributs non système, y compris ceux qui sont spécifiques aux données d’exemple Luma. La définition de la propriété d’attribut *Utiliser dans la recherche* sur `Yes` rend l’attribut consultable dans [!DNL Live Search] et dans Adobe Commerce natif.

| Code attribut | Indexable | Utilisation dans la navigation superposée |
|--- |--- |--- |
| activité | Oui | Filtrable (avec résultats) |
| attributes_brand | Oui | Non |
| marque | Oui | Non |
| climat | Oui | Filtrable (avec résultats) |
| collier | Oui | Filtrable (avec résultats) |
| couleur | Oui | Filtrable (avec résultats) |
| coût | Oui | Non |
| eco_collection | Oui | Filtrable (avec résultats) |
| sexe | Oui | Filtrable (avec résultats) |
| fabricant | Oui | Filtrable (avec résultats) |
| matériau | Oui | Filtrable (avec résultats) |
| objectif | Oui | Filtrable (avec résultats) |
| strap_bag | Oui | Filtrable (avec résultats) |
| style_general | Oui | Filtrable (avec résultats) |

## Propriétés d’attribut système par défaut

Le tableau suivant présente les propriétés de recherche et de filtrage par défaut des attributs système.

| Code attribut | Indexable | Utilisation dans la navigation superposée |
|--- |--- |--- |
| allow_open_amount | Oui | Filtrable (avec résultats) |
| description | Oui | Non |
| name | Oui | Non |
| prix | Oui | Filtrable (avec résultats) |
| short_description | Oui | Non |
| sku | Oui | Non |
| statut | Oui | Non |
| tax_class_id | Oui | Non |
| url_key | Oui | Non |
| poids | Oui | Non |
