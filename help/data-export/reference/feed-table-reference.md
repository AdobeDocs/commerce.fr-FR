---
title: Référence du schéma de la table de flux
description: Découvrez le schéma de la table des flux utilisé par  [!DNL SaaS Data Export]  pour effectuer le suivi de l’état de l’élément de flux, du statut d’exportation et des détails d’erreur.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: c70c1643afbf8e9633df89a613d6798416c8eb44
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 0%

---


# Référence du schéma de la table de flux

Chaque flux comporte une table MySQL dédiée dans la base de données [!DNL Adobe Commerce]. Tous les tableaux de flux partagent la même structure de colonnes. Le tableau ci-dessous répertorie chaque flux avec son nom de flux d’interface de ligne de commande, son identifiant d’indexeur et son nom de tableau de flux.

## Flux pris en charge

La liste réelle des flux dépend du package [!DNL SaaS Data Export] installé.


| Flux (`--feed`) | Objectif | ID de l’indexeur | Tableau de flux | Mode d’exportation |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | Catalogue de produits (attributs, catégories, images, etc.) | `catalog_data_exporter_products` | `cde_products_feed` | Immédiat |
| `productAttributes` | Définitions d’attributs et métadonnées. Utilisé pour définir le schéma de recherche. | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | Immédiat |
| `categories` | Données de catégories | `catalog_data_exporter_categories` | `cde_categories_feed` | Immédiat |
| `prices` | Prix des produits avec les prix du groupe de clients et les prix par niveau | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | Immédiat |
| `variants` | Variantes de produit configurables | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | Immédiat |
| `scopesWebsite` | Site web avec codes d’affichage de magasin | `scopes_website_data_exporter` | `scopes_website_data_exporter` | Hérité |
| `scopesCustomerGroup` | Définitions de groupes de clients | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | Hérité |
| `productOverrides` | Autorisations de produit calculées | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | Immédiat |
| `categoryPermissions` *(EE)* | Données brutes d’autorisations de catégorie | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | Immédiat |
| `orders` | Statut des commandes client | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | Hérité |

La colonne **Mode d’exportation** indique comment chaque flux collecte et envoie des données :

- **Flux en mode immédiat** : collectez des données, ignorez les éléments inchangés à l’aide de hachages de contenu (déduplication de hachage) et envoyez des mises à jour au cours de la même exécution de l’indexeur.
- **Flux en mode hérité** (`scopesWebsite`, `scopesCustomerGroup`, `orders`) : stockez d’abord les données assemblées dans la table de flux et envoyez-les via une tâche cron distincte.

Voir [Modes de synchronisation](../sync-overview.md#synchronization-modes).

## Schéma

| Colonne | Type | Description |
| --- | --- | ---------------- |
| `id` | INT (PK) | Incrémenter automatiquement la clé primaire |
| `source_entity_id` | INT | Identifiant d’entité de la table source de Commerce (par exemple, `catalog_product_entity.entity_id`) |
| `feed_id` | VARCHAR | Identifiant unique d’un élément de flux. Calculé en tant que hachage des champs d’identité de l’élément (par exemple, `sku + storeViewCode`), et non en tant que valeur d’incrémentation automatique. |
| `feed_data` | JSON | Payload de flux pour cet élément. Seules les informations minimales telles que l’identifiant d’entité et la portée sont renseignées. Lorsque `PERSIST_EXPORTED_FEED=1` est défini, la payload complète est stockée. |
| `feed_hash` | VARCHAR | Hachage de contenu utilisé pour la détection des modifications. Calculé à partir de la payload, horodatages exclus (`modifiedAt`, `updatedAt`). Si le hachage correspond à l’exportation précédente, l’élément n’est pas renvoyé. |
| `is_deleted` | TINYINT | Marqueur de suppression réversible. Définissez cette variable sur `1` lorsque l’entité est supprimée dans Commerce. |
| `modified_at` | DATE ET HEURE | Dernière modification de cet élément de flux |
| `status` | INT | Code d’état de l’envoi de la dernière tentative d’exportation. Voir [Envoi du flux et gestion des erreurs HTTP](../sync-overview.md#feed-submission-and-http-error-handling). |
| `errors` | TEXTE | Détails d’erreur codés JSON renvoyés par le service SaaS pour cet élément |
| `metadata` | JSON | Indicateurs de synchronisation interne et informations de verrouillage des métadonnées utilisées par le framework d’exportation |

## Requêtes de diagnostic courantes

Utilisez les requêtes SQL suivantes pour inspecter directement l’état de la table de flux. Remplacez les valeurs d’espace réservé telles que `<SKU>`, `<ATTRIBUTE_CODE>` et `<CATEGORY_ID>` par les valeurs réelles de votre environnement. Consultez [Flux pris en charge](#supported-feeds) pour obtenir la liste complète des noms de tableau.

**Flux de produits — par SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Flux d’attributs de produit — par code d’attribut :**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.attributeCode') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.attributeCode') IN ('<ATTRIBUTE_CODE>');
```

**Prix des aliments pour animaux — par SKU :**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, '-- (base price)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Le produit remplace le flux — par SKU :**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, 'NA (deleted)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_overrides_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Flux de catégories — par ID de catégorie :**

```sql
SELECT JSON_EXTRACT(feed_data, '$.categoryId') AS 'Category ID',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(feed_data, '$.categoryId') IN (<CATEGORY_ID>);
```

**Flux de variantes — par SKU de produit configurable :**

```sql
SELECT JSON_EXTRACT(feed_data, '$.parentSku') AS 'configurable SKU',
       JSON_EXTRACT(feed_data, '$.productSku') AS 'Variant SKU',
       JSON_EXTRACT(f.feed_data, '$.optionValues') AS 'options',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_variants_feed f
WHERE JSON_EXTRACT(feed_data, '$.parentSku') = '<SKU>';
```


>[!MORELIKETHIS]
>
>- [Synchroniser les données avec l’exportation de données SaaS](../sync-overview.md)
>- [Afficher et gérer la synchronisation](../data-sync-manage.md)
>- [Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce](../data-export-cli-commands.md)
