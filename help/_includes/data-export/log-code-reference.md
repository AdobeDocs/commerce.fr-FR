---
source-git-commit: 7d6fa8fa8a93d7d89ca97885f1b9363667a22c7e
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---
# Référence des codes journaux MDEE

Format du code journal : `CDE<group_id>-<log_id>` (par exemple, `CDE01-02`)

Sources : `commerce-data-export`, `commerce-data-export-ee`, `saas-export`

Les codes sont attribués uniquement aux messages de journal de niveau `error`, `warning` et `critical`. Les messages de niveau `info`, `notice` et `debug` sont exclus.

## Groupe 01 - Phase de collecte de données

Enregistrez les codes liés aux erreurs ou aux avertissements qui se produisent lors de la collecte de données à partir des entités sources, généralement au sein des fournisseurs de données.
- Les entités affectées peuvent être traitées avec des données partielles ou entièrement ignorées en cas d’erreur. Voir le message du journal pour plus de détails.
- Des avertissements peuvent indiquer une intégration incorrecte avec l’extension d’exportation de données par des modules tiers. Toutefois, les opérations de synchronisation se poursuivent généralement.

| Code de journal | Niveau | Message |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------|
| CDE01-01 | erreur | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-02 | avertissement | `CDE01-02 Field "{field}" is missing in row {row_data}` |
| CDE01-03 | avertissement | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` |
| CDE01-04 | erreur | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` |
| CDE01-05 | erreur | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` |
| CDE01-06 | erreur | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` |
| CDE01-07 | erreur | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` |
| CDE01-08 | erreur | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` |
| CDE01-09 | erreur | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` |
| CDE01-10 | erreur | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` |
| CDE01-11 | erreur | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` |
| CDE01-12 | avertissement | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` |
| CDE01-13 | erreur | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` |
| CDE01-14 | erreur | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` |
| CDE01-15 | erreur | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` |
| CDE01-16 | erreur | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` |
| CDE01-17 | avertissement | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` |
| CDE01-18 | avertissement | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` |
| CDE01-19 | avertissement | `CDE01-19 GiftCard {sku} does not have shopper input options` |
| CDE01-20 | avertissement | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` |
| CDE01-21 | erreur | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` |
| CDE01-22 | erreur | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` |
| CDE01-23 | erreur | `CDE01-23 Unable to assemble "ac_customizable_options" attribute. Error: {exception_message}` |

## Groupe 02 - Envoi de données à la phase SaaS

Enregistrez les codes liés aux erreurs ou aux avertissements qui se produisent lors de l’envoi de données de flux aux points d’entrée SaaS.
- Les erreurs indiquent généralement des échecs lors des requêtes HTTP, de la gestion des réponses ou de la validation des données qui empêchent l’acceptation des données.
- Les avertissements indiquent généralement des conditions transitoires (telles que la limitation du débit ou les erreurs du serveur) dans lesquelles les demandes sont automatiquement retentées.

| Code de journal | Niveau | Message |
|-----------|---------|---------|
| CDE02-01 | erreur | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-02 | erreur | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` |
| CDE02-03 | avertissement | `CDE02-03 Cannot parse the API response because the request was not successful.` |
| CDE02-04 | erreur | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` |
| CDE02-05 | erreur | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` |
| CDE02-06 | erreur | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` |
| CDE02-07 | avertissement | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` |
| CDE02-08 | avertissement | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-09 | erreur | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` |
| CDE02-10 | avertissement | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` |
| CDE02-11 | avertissement | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` |
| CDE02-12 | erreur | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` |
| CDE02-13 | avertissement | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` |

## Groupe 03 - Planification de la synchronisation lors de la mise à jour de l’entité

Codes de journal associés aux erreurs ou aux avertissements qui se produisent lors de la planification ou du déclenchement de la synchronisation en réponse aux modifications d&#39;entité.
- Les erreurs peuvent empêcher la planification de la synchronisation incrémentielle et nécessitent souvent une resynchronisation complète ou partielle pour la restauration.
- Les avertissements indiquent qu’une opération de synchronisation a été ignorée ou reportée en raison d’une entrée non prise en charge, d’identifiants manquants ou de problèmes de configuration.

| Code de journal | Niveau | Message |
|----------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| CDE03-01 | erreur | `CDE03-01 Cannot schedule resync for feeds` |
| CDE03-02 | avertissement | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` |
| CDE03-03 | erreur | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` |
| CDE03-04 | erreur | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` |
| CDE03-05 | erreur | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` |
| CDE03-06 | erreur | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` |
| CDE03-07 | avertissement | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` |
| CDE03-08 | erreur | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` |
| CDE03-09 | avertissement | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs, or an unsupported identifier type was specified.` |
| CDE03-10 | avertissement | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` |
| CDE03-11 | erreur | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` |
| CDE03-12 | avertissement | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` |
| CDE03-13 | erreur | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` |
| CDE03-14 | erreur | `CDE03-14 Failed to read config values. Indexer invalidation skipped. Error: {error_message}` |
| CDE03-15 | erreur | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` |
| CDE03-16 | erreur | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` |
| CDE03-17 | critique | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` |
| CDE03-18 | critique | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` |
| CDE03-19 | erreur | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` |
| CDE03-20 | erreur | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` |
| CDE03-21 | erreur | `CDE03-21 Product sync scheduling error on attribute {%s} option change. Run resync. Error: %s` |
| CDE03-22 | avertissement | `CDE03-22 StagedCategoryUrlKeyChangeDetector: no active row at version {version_id} for entity_id(s) [{entity_ids}]; skipping.` |
| CDE03-23 | erreur | `CDE03-23 StagedCategoryUrlKeyChangeDetector: catalog_category url_key attribute not found; failing open.` |
| CDE03-24 | erreur | `CDE03-24 InvalidateProductFeedOnCategoryUrlKeyChange: scheduler failed for path "{path}": {error_message}` |
| CDE03-25 | erreur | `CDE03-25 InvalidateProductFeedOnCategoryUrlKeyChange: gate query failed: {error_message}` |
| CDE03-26 | erreur | `CDE03-26 InvalidateProductFeedOnCategoryUrlKeyChange: unable to expand staged url_key category reindex scope: {error_message}` |
| CDE03-27 | erreur | `CDE03-27 Failed to invalidate indexers after config "{config_section}" change. Error: {error_message}` |
| CDE03-28 | avertissement | `CDE03-28 StagedCategoryUrlKeyChangeDetector: catalog category staging schema is not present; skipping staged url_key change detection.` |

## Groupe 04 - Erreurs générales liées à l’indexation ou à la configuration

Codes de journal liés aux erreurs lors du processus d’indexation ou dues à une mauvaise configuration.

| Code de journal | Niveau | Message |
|-----------|---------|---------|
| CDE04-02 | erreur | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` |
| CDE04-03 | avertissement | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` |
| CDE04-04 | erreur | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` |
| CDE04-05 | erreur | `CDE04-05 Cannot load feed indexer for feed` |
| CDE04-06 | erreur | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` |
| CDE04-07 | erreur | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` |
| CDE04-08 | erreur | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` |
| CDE04-09 | erreur | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` |
| CDE04-10 | erreur | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` |
| CDE04-11 | avertissement | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` |
| CDE04-12 | avertissement | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` |
| CDE04-13 | erreur | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` |
| CDE04-14 | erreur | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` |
| CDE04-15 | avertissement | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` |
| CDE04-16 | avertissement | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` |
| CDE04-17 | avertissement | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` |
| CDE04-18 | avertissement | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` |
| CDE04-19 | avertissement | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` |
| CDE04-20 | avertissement | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` |
| CDE04-21 | erreur | `CDE04-21 Failed to clean up deleted feed items for feed "{feed_name}". Error: {error_message}` |
