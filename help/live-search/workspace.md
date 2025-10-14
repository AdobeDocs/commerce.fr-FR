---
title: Configuration de Live Search
description: L’espace  [!DNL Live Search]  travail permet de configurer, de gérer et de surveiller les performances des recherches.
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: bb212bf88ba7bad3deb2d2d699124413f4dd76ff
workflow-type: tm+mt
source-wordcount: '1068'
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

Si vous êtes un client du secteur de la santé et que vous avez installé l’extension [Data Services HIPAA](../data-connection/hipaa-readiness.md#installation), qui fait partie de l’extension [Data Connection](../data-connection/overview.md), les données d’événement de storefront utilisées par [!DNL Live Search] ne sont plus capturées. En effet, les données d’événement de storefront sont générées côté client. Pour continuer à capturer et à envoyer des données d’événement de storefront, réactivez la collecte d’événements pour [!DNL Live Search]. Voir [configuration générale](https://experienceleague.adobe.com/fr/docs/commerce-admin/config/general/general#data-services) pour en savoir plus.

## Définir la portée

Au départ, la [portée](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=fr#scope-settings) de tous les paramètres [!DNL Live Search] est définie sur `Default Store View`. Si votre installation [!DNL Commerce] comprend plusieurs vues de magasin, définissez **Portée** sur la vue [magasin](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=fr) où s’appliquent les paramètres de facettes.

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

Pour obtenir des résultats hautement ciblés, passez en revue l’ensemble des attributs de produit [consultables](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html?lang=fr) (`searchable=true`). Pour garantir la pertinence, assurez-vous que les attributs ne peuvent être recherchés que s’ils contiennent du contenu ayant une signification claire et concise. Évitez d’utiliser des attributs contenant du texte moins précis et plus long, comme `description`, qui bien que la recherche soit activée par défaut, peut réduire la précision des résultats de recherche. Par exemple, si une personne recherche un « short » et qu’il existe des chemises dont la description inclut le terme « manches courtes », les chemises sont incluses dans les résultats de la recherche.

Pour que les attributs puissent faire l’objet de recherches, procédez comme suit :

1. Dans l’administration, accédez à **Magasins** > *Attribut* > **Produit**.
1. Sélectionnez l’attribut pour lequel vous souhaitez pouvoir effectuer des recherches, par exemple `color`.
1. Sélectionnez **Propriétés du storefront** et définissez **Utiliser dans la recherche** sur `yes`.

   ![Workspace](assets/attribute-searchable.png)

[!DNL Live Search] respecte également le [poids](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html?lang=fr#weighted-search) d’un attribut de produit, tel que défini dans Adobe Commerce. Les attributs ayant un poids plus élevé apparaissent plus haut dans les résultats de la recherche.

Les attributs suivants peuvent toujours faire l’objet de recherches :

- `sku`
- `name`
- `categories`

[Facettes](facets.md) sont des attributs de produit définis dans [!DNL Live Search] pour pouvoir être filtrés. Vous pouvez définir n’importe quel attribut filtrable en tant que facette dans [!DNL Live Search], mais il existe des [limites](boundaries-limits.md) au nombre de facettes que vous pouvez rechercher en même temps.

>[!NOTE]
>
>Un attribut de produit ne peut être filtré que si la configuration de l’attribut de produit possède les propriétés requises : *Utiliser dans la recherche = Oui*, *Utiliser dans les résultats de recherche Navigation superposée = oui* et *Utiliser dans la navigation superposée = Filtrable (avec résultats)*. Si ces propriétés sont manquantes, l’attribut n’est pas visible dans la configuration des facettes. Pour obtenir des instructions de configuration, voir [Ajouter une facette](facets-add.md#add-a-facet).

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

[!DNL Live Search] prend en charge les [redirections de termes de recherche](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html?lang=fr) dans les implémentations où Adobe Commerce gère le routage, par exemple sur Luma et d’autres thèmes basés sur php.
