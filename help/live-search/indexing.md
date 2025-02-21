---
title: Indexation
description: Découvrez comment indexer  [!DNL Live Search]  propriétés des attributs de produit.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# Indexation

Le processus d’indexation [!DNL Live Search] lit le catalogue des attributs de produit et crée un index afin que les produits puissent être recherchés, filtrés et présentés rapidement.

Les propriétés d’attribut de produit (métadonnées) déterminent les éléments suivants :

* Utilisation d’un attribut dans le catalogue
* Son apparence et son comportement dans le magasin
* Données incluses dans les opérations de transfert de données

La portée des métadonnées d’attribut est `website/store/store view`.

L’API [!DNL Live Search] permet à un client de trier en fonction de n’importe quel attribut de produit dont la propriété [storefront](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) `Use in Search` définie sur `Yes` dans l’administration Adobe Commerce. Lorsqu’il est activé, `Search Weight` peut être défini pour l’attribut .

[!DNL Live Search] n’indexe pas les produits supprimés ou les produits définis sur `Not Visible Individually`.

>[!NOTE]
>
> Les clients Commerce avec [!DNL Live Search] peuvent bénéficier de mises à jour de modifications de prix et de temps de synchronisation plus rapides sur leurs sites web avec l’indexeur de prix [SaaS](../price-index/price-indexing.md).

## Pipeline d’indexation

Le client appelle le service de recherche du storefront pour récupérer les métadonnées d’index (filtrables, triables). Seuls les attributs de produit pouvant faire l’objet d’une recherche dont la propriété *Utiliser dans la navigation à plusieurs niveaux* définie sur `Filterable (with results)` et *Utiliser pour le tri dans la liste de produits* définie sur `Yes` peuvent être appelés par le service de recherche.

Pour construire une requête dynamique, le service de recherche doit connaître les attributs pouvant faire l’objet d’une recherche et leur [poids](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results). [!DNL Live Search] respecte les poids de recherche Adobe Commerce (1 à 10, où 10 est la priorité la plus élevée). La liste des données synchronisées et partagées avec le service de catalogue se trouve dans le schéma , qui est défini dans :

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search] le diagramme de recherche du client d’indexation](assets/indexing-pipeline.svg)

1. Vérifiez les droits d’[!DNL Live Search] auprès du commerçant.
1. Obtenez des vues de magasin avec des modifications apportées aux métadonnées d’attribut.
1. Stockez les attributs d’indexation.
1. Réindexez l’index de recherche.

### Index complet

Lorsque [!DNL Live Search] est configuré et synchronisé lors de l’intégration, la création de l’index initial peut prendre jusqu’à 60 minutes. L’indexation des catalogues volumineux peut prendre plus de temps. Le processus commence une fois que `cron` a envoyé le flux et a terminé son exécution.

Les événements suivants déclenchent une synchronisation complète et une version d’index :

* Intégration [synchronisation des données de catalogue](install.md#synchronize-catalog-data)
* Modifications apportées aux métadonnées d’attribut

Par exemple, la modification de la propriété `Use in Search` de l’attribut `color` de `No` à `Yes` modifie les métadonnées de l’attribut en `searchable=true` et déclenche une synchronisation complète ainsi qu’une réindexation. Les métadonnées d’attribut suivantes déclenchent une synchronisation complète et une réindexation en cas de modification :

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### Diffusion de mises à jour de produits en continu

Une fois l’index initial créé lors de l’intégration [onboarding](install.md#synchronize-catalog-data), les mises à jour incrémentielles de produits suivantes sont continuellement synchronisées et réindexées :

* Nouveaux produits ajoutés au catalogue
* Modifications des valeurs d’attribut de produit

Par exemple, l’ajout d’une nouvelle valeur d’échantillon à l’attribut `color` est géré comme une mise à jour de produit en flux continu.

Workflow de mise à jour en flux continu :

1. Les produits mis à jour sont synchronisés entre l’instance Adobe Commerce et le service de catalogue.
1. Le service d’indexation recherche en permanence des mises à jour de produit à partir du service de catalogue. Les produits mis à jour sont indexés au fur et à mesure qu’ils arrivent dans le service de catalogue.
1. La disponibilité d’une mise à jour produit dans [!DNL Live Search] peut prendre jusqu’à 15 minutes.

#### Mises à jour affectant la visibilité des produits

Lorsque vous effectuez des mises à jour des paramètres de configuration d’administration [!DNL Live Search], des paramètres de configuration d’administration Adobe Commerce ou des données de catalogue, vous pouvez vous attendre à un délai avant que ces modifications n’apparaissent sur le storefront.

Le tableau suivant décrit diverses modifications et le temps d’attente approximatif avant leur affichage dans le storefront.

| Mises à jour | Délai jusqu’à ce que visible sur le storefront |
|---|---|
| [!DNL Live Search] Admin modifie les facettes, les paramètres de prix, les règles de marchandisage de recherche ou de catégorie. | 15-20 minutes. |
| [!DNL Live Search] modifications administratives nécessitant une réindexation : paramètres de langue ou synonymes. | Jusqu’à 15 minutes après la fin de la réindexation. |
| Modifications d’Adobe Commerce Admin qui nécessitent une réindexation complète : métadonnées d’attribut pouvant faire l’objet de recherches, triables ou filtrables | Jusqu’à 15 minutes après la fin de la réindexation. |
| Modifications incrémentielles des données de catalogue qui n’ont pas besoin d’être réindexées : inventaire des produits, prix, nom, etc. | Jusqu’à 15 minutes après la mise à jour de l’index de recherche élastique avec les dernières données. |

## Recherche de clients

L’API [!DNL Live Search] permet à un client de trier en fonction de n’importe quel attribut de produit triable en définissant la [propriété storefront](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes), *utilisée pour le tri dans les listes de produits* sur `Yes`. En fonction du thème, ce paramètre entraîne l’inclusion de l’attribut en tant qu’option dans le contrôle de pagination [Trier par](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation) sur les pages de catalogue. Jusqu’à 200 attributs de produit peuvent être indexés par [!DNL Live Search], avec des [propriétés storefront](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) qui peuvent faire l’objet de recherches et de filtres.

Les métadonnées d’index sont stockées dans le pipeline d’indexation et sont accessibles par le service de recherche.

Diagramme API de métadonnées d’index ![[!DNL Live Search]](assets/index-metadata-api.svg)

### Workflow des attributs triables

1. Le client appelle le service de recherche.
1. Le service de recherche appelle le service d’administration de recherche.
1. Le service de recherche appelle le pipeline d’indexation.

## Indexé pour tous les produits

L’ordre des champs de cette liste reflète l’ordre type des colonnes dans les données de produit exportées.

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

Le champ suivant est indexé pour tous les produits configurables :

* `childrenSkus`
