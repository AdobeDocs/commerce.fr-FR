---
title: Référence du schéma de la table de flux
description: Découvrez le schéma de la table des flux utilisé par pour effectuer le suivi de l [!DNL Adobe Commerce Optimizer Connector] état, du statut d’exportation et des détails d’erreur de l’élément de flux.
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---


# Référence du schéma de la table de flux

Chaque flux comporte une table MySQL dédiée dans la base de données [!DNL Adobe Commerce]. Tous les tableaux de flux partagent la même structure de colonnes.

## Flux pris en charge

Pour obtenir la liste complète des flux pris en charge avec des points d’entrée d’API, des limites de lot, des noms d’indexeur et des noms de table de flux, voir [Modules de connecteur et points d’entrée de flux](connector-reference.md#supported-feeds).

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
| `status` | INT | Code d’état de l’envoi de la dernière tentative d’exportation. Voir [Envoi du flux et gestion des erreurs](../connector-sync-pipeline.md#feed-submission-and-error-handling). |
| `errors` | TEXTE | Détails d’erreur codés JSON renvoyés par l’API [!DNL Commerce Optimizer] pour cet élément |
| `metadata` | JSON | Indicateurs de synchronisation interne et informations de verrouillage des métadonnées utilisées par le framework d’exportation |

## Requêtes de diagnostic courantes

Utilisez les requêtes SQL suivantes pour inspecter directement l’état de la table de flux. La colonne `feed_data` stocke les données au format API [!DNL Adobe Commerce Optimizer]. Remplacez les valeurs d’espace réservé telles que `<SKU>`, `<ATTRIBUTE_CODE>`, `<SLUG>` et `<PRICE_BOOK_ID>` par les valeurs réelles de votre environnement.

**Flux de produits - par SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Flux d’attributs de produit - par code d’attribut :**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

**Flux des catégories - par chemin d’URL :**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**Flux de prix - par SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Flux des catalogues de prix - par ID de catalogue de prix :**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [Modules de connecteur et points d’entrée de flux](connector-reference.md)
>- [Pipeline de synchronisation du connecteur](../connector-sync-pipeline.md)
>- [Gérer la synchronisation](../data-sync-manage.md)
>- [Mappage de champ pour les flux du connecteur](field-mapping.md)
