---
title: Référence Des Codes Du Journal [!Data Export]
description: Liste de référence pour les codes de journal d’exportation des données, les messages et les niveaux de gravité afin de résoudre les problèmes de synchronisation et de décider quand une resynchronisation partielle ou complète est requise.
autotag-review: '2026-06-17T15:08:59.000Z'
feature: Services
exl-id: c1341863-1ec4-4d67-8ff2-821ef0a61f33
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: ea4d7562942cdf1f827f9926dd3fb7278d084f37
workflow-type: tm+mt
source-wordcount: 568
ht-degree: 0%

---

# [!DNL Data Export] référence des codes journaux

Cette page fournit une référence pour les messages du journal d’exportation de données afin de résoudre les problèmes de synchronisation et de déterminer quand une resynchronisation partielle ou complète est requise. Il comprend uniquement les codes d’erreur, d’avertissement et de journal critique émis par l’extension [!DNL Data Export].

Voir [Vérification des journaux et dépannage](logging.md) pour plus d’informations sur les fichiers journaux et obtenir des conseils de dépannage.

## Détails du code journal

<!--
Source of truth: https://github.com/magento-commerce/commerce-data-export (docs/log-codes.md)
When log codes, messages, or log levels change in that repository, update this page to match.
Only columns retained here: Log Code, Message, Level. File paths are intentionally omitted.
-->

**Format du code journal :** `CDE<group_id>-<log_id>` (par exemple, `CDE01-02`)

**Sources :**, `commerce-data-export`, `commerce-data-export-ee`, `saas-export`

Les codes sont affectés aux messages de journal de niveau `error`, `warning` et `critical` uniquement, les messages de niveau `info`, `notice` et `debug` sont exclus.

## Groupe 01 - Phase de collecte de données

Enregistrez les codes liés aux erreurs ou aux avertissements qui se produisent lors de la collecte de données à partir des entités sources, généralement au sein des fournisseurs de données.
- Les entités affectées peuvent être traitées avec des données partielles ou entièrement ignorées en cas d’erreur. Voir le message du journal pour plus de détails.
- Les avertissements peuvent indiquer une intégration incorrecte avec l’extension d’exportation de données par des modules tiers. Toutefois, les opérations de synchronisation se poursuivent généralement.

| Code de journal | Niveau | Message | Chemin du fichier |
|----------|---------|------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| CDE01-01 | erreur | `CDE01-01 Failed to add stock info to "ac_inventory" attribute for ids "{ids}". Error: {exception_message}` | `commerce-data-export/ExtraProductAttributes/Provider/AdvancedInventoryProvider.php:69` |
| CDE01-02 | avertissement | `CDE01-02 Field "{field}" is missing in row {row_data}` | `commerce-data-export/ExtraProductAttributes/Provider/AdvancedInventoryProvider.php:101` |
| CDE01-03 | avertissement | `CDE01-03 Invalid field "{field}" requested from inventory config {config_data}` | `commerce-data-export/ExtraProductAttributes/Provider/AdvancedInventoryProvider.php:146` |
| CDE01-04 | erreur | `CDE01-04 Was not able to add data to "ac_attribute_set" attribute for ids "{ids}". Error: {exception_message}` | `commerce-data-export/ExtraProductAttributes/Provider/AttributeSetProvider.php:55` |
| CDE01-05 | erreur | `CDE01-05 Unable to sync feed "{feed}" for ids "{ids}". Affected data provider: "{provider}". Error: {exception_message}` | `commerce-data-export/DataExporter/Export/Processor.php:94` |
| CDE01-06 | erreur | `CDE01-06 Unable to sync feed "{feed}" for ids "{ids}". Error: {exception_message}` | `commerce-data-export/DataExporter/Export/Processor.php:127` |
| CDE01-07 | erreur | `CDE01-07 Source entity id is null. Item sync was skip for feed "{feed}". field: "{field}", item: {item}` | `commerce-data-export/DataExporter/Model/Indexer/DataSerializer.php:123` |
| CDE01-08 | erreur | `CDE01-08 Cannot collect "inStock" for products "{product_ids}": no sales channel data for stores "{store_view_codes}"` | `commerce-data-export/CatalogInventoryDataExporter/Model/Query/InventoryData.php:125` |
| CDE01-09 | erreur | `CDE01-09 Cannot get status attribute. Product variants ignore stock status. Error: {exception_message}` | `commerce-data-export/ConfigurableProductDataExporter/Model/Provider/Product/Options.php:434` |
| CDE01-10 | erreur | `CDE01-10 Unable to retrieve gift card product options for products "{values}". Error: {exception_message}` | `commerce-data-export-ee/GiftCardProductDataExporter/Model/Provider/Product/Options.php:148` |
| CDE01-11 | erreur | `CDE01-11 Unable to retrieve gift card shopper input options for products "{values}". Error: {exception_message}` | `commerce-data-export-ee/GiftCardProductDataExporter/Model/Provider/Product/ShopperInputOptions.php:119` |
| CDE01-12 | avertissement | `CDE01-12 Catalog Permissions: Global Configuration path was not found for path {path}. {config_dump}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Model/Provider/ConfigurationProvider.php:183` |
| CDE01-13 | erreur | `CDE01-13 Catalog Permissions: wrong state in global config. item: {item}, config: {config}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Model/Provider/ConfigurationProvider.php:245` |
| CDE01-14 | erreur | `CDE01-14 Failed to assign UUIDs for type: {type}, ids: {ids}` | `commerce-data-export/DataExporter/Uuid/UuidManager.php:90` |
| CDE01-15 | erreur | `CDE01-15 Failed to assign UUIDs for type: {type}, ids: {ids}. duplicates: {duplicates}` | `commerce-data-export/DataExporter/Uuid/UuidManager.php:106` |
| CDE01-16 | erreur | `CDE01-16 "{feed_name}" feed sync error: cannot build identifier for "{field}". Item skipped: {item}` | `commerce-data-export/DataExporter/Model/FeedHashBuilder.php:82` |
| CDE01-17 | avertissement | `CDE01-17 Failed to create attribute "{attribute_code}". Will be retried on next sync. Error: {message}` | `commerce-data-export/CatalogDataExporter/Service/SystemAttributeRegistrar.php:182` |
| CDE01-18 | avertissement | `CDE01-18 Error on getting datetime for catalog price rule fetch. Using system time. website: "{website_id}", store: "{store_id}"` | `commerce-data-export/ProductPriceDataExporter/Model/Query/DateWebsiteProvider.php:75` |
| CDE01-19 | avertissement | `CDE01-19 GiftCard {sku} does not have shopper input options` | `commerce-data-export-ee/GiftCardProductDataExporter/Plugin/GiftCardAsAttribute.php:102` |
| CDE01-20 | avertissement | `CDE01-20 GiftCard {sku} doesn't have valid options: {options}` | `commerce-data-export-ee/GiftCardProductDataExporter/Plugin/GiftCardAsAttribute.php:131` |
| CDE01-21 | erreur | `CDE01-21 Unable to resolve url_path for category {id} with path "{path}", url_key "{urk_key}", store "{store}"` | `commerce-data-export/CatalogDataExporter/Model/Provider/Categories.php:204` |
| CDE01-22 | erreur | `CDE01-22 Unable to resolve url_path for category{id} with path "{path}" for store view "{store}"` | `commerce-data-export/CatalogDataExporter/Model/Provider/Product/CategoryData.php:96` |

## Groupe 02 - Envoi de données à la phase SaaS

Enregistrez les codes liés aux erreurs ou aux avertissements qui se produisent lors de l’envoi de données de flux aux points d’entrée SaaS.
- Les erreurs indiquent généralement des échecs lors des requêtes HTTP, de la gestion des réponses ou de la validation des données qui empêchent l’acceptation des données.
- Les avertissements indiquent généralement des conditions transitoires (telles que la limitation du débit ou les erreurs du serveur) dans lesquelles les demandes sont automatiquement retentées.

| Code de journal | Niveau | Message | Chemin du fichier |
|-----------|---------|---------|-----------|
| CDE02-01 | erreur | `CDE02-01 Application error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:261` |
| CDE02-02 | erreur | `CDE02-02 Unexpected error on sending data to SaaS for feed "{feed_name}". Error: {error_message}` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:280` |
| CDE02-03 | avertissement | `CDE02-03 Cannot parse the API response because the request was not successful.` | `saas-export/SaaSCommon/Model/Http/ResponseParser.php:81` |
| CDE02-04 | erreur | `CDE02-04 Cannot obtain feed metadata for feed name "{feed_name}". Sync terminated. Error: {error_message}` | `saas-export/SaaSCommon/Cron/SubmitFeed.php:206` |
| CDE02-05 | erreur | `CDE02-05 Failed to submit feed batch for feed {feed_name}. Error: {error_message}` | `saas-export/SaaSCommon/Cron/SubmitFeed.php:310` |
| CDE02-06 | erreur | `CDE02-06 Failed to retry feed items submission for feed {feed_name}. Error: {error_message}` | `saas-export/SaaSCommon/Cron/SubmitFeed.php:257` |
| CDE02-07 | avertissement | `CDE02-07 Feed "{feed_name}" sync error: too many requests (HTTP 429). Request will be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:351` |
| CDE02-08 | avertissement | `CDE02-08 Feed "{feed_name}" sync error: Server error (HTTP {http_status_code}). Request will be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:356` |
| CDE02-09 | erreur | `CDE02-09 Feed "{feed_name}" sync error: data validation failed. Check logs. Request will not be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:362` |
| CDE02-10 | avertissement | `CDE02-10 Feed "{feed_name}" sync error: Client error (HTTP {http_status_code}). Request will be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:368` |
| CDE02-11 | avertissement | `CDE02-11 Feed "{feed_name}" sync error: application-level error. Request will be retried.` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:374` |
| CDE02-12 | erreur | `CDE02-12 Feed "{feed_name}" sync error API request was not successful (status code: {status_code}).` | `saas-export/SaaSCommon/Model/Http/Command/SubmitFeed.php:379` |
| CDE02-13 | avertissement | `CDE02-13 The zlib-ext is not loaded. Request body can't be compressed and will proceed with regular json` | `saas-export/SaaSCommon/Model/Http/Converter/Factory.php:96` |

## Groupe 03 - Planification de la synchronisation lors de la mise à jour de l’entité

Codes de journal associés aux erreurs ou aux avertissements qui se produisent lors de la planification ou du déclenchement de la synchronisation en réponse aux modifications d&#39;entité.
- Les erreurs peuvent empêcher la planification de la synchronisation incrémentielle et nécessitent souvent une resynchronisation complète ou partielle pour la restauration.
- Les avertissements indiquent qu’une opération de synchronisation a été ignorée ou reportée en raison d’une entrée non prise en charge, d’identifiants manquants ou de problèmes de configuration.

| Code de journal | Niveau | Message | Chemin du fichier |
|-----------|----------|---------|-----------|
| CDE03-01 | erreur | `CDE03-01 Cannot schedule resync for feeds` | `commerce-data-export/DataExporter/Service/FeedItemsResyncScheduler.php:119` |
| CDE03-02 | avertissement | `CDE03-02 Skipping product feed update scheduling. Category path "{category_path}" is wrongly formatted` | `commerce-data-export/CatalogDataExporter/Plugin/Category/ScheduleProductUpdateOnCategoryChange.php:55` |
| CDE03-03 | erreur | `CDE03-03 Categories sync error on category "{category_id}" save. Run resync. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Category/ReindexCategoryFeedOnSave.php:64` |
| CDE03-04 | erreur | `CDE03-04 Product sync scheduling error on url key change ({old_url_key} -> {new_url_key}). Run resync. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Category/ResyncProductsOnCategoryChange.php:71` |
| CDE03-05 | erreur | `CDE03-05 Product sync scheduling error on category path change ({old_path} -> {new_path}). Run resync. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Category/ResyncProductsOnCategoryChange.php:115` |
| CDE03-06 | erreur | `CDE03-06 Product sync scheduling error on attribute "{attribute_code}" deletion. Run full resync. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Eav/Attribute/ProductAttributeDelete.php:102` |
| CDE03-07 | avertissement | `CDE03-07 Product sync scheduling error on inventory source save for SKUs: {product_skus}. Error: {error_message}` | `commerce-data-export/CatalogInventoryDataExporter/Model/Plugin/ScheduleProductUpdate.php:61` |
| CDE03-08 | erreur | `CDE03-08 Product variants sync scheduling error on product "{sku_or_id}" save. Run resync. Error: {error_message}` | `commerce-data-export/ProductVariantDataExporter/Plugin/ReindexVariantsAfterSave.php:76` |
| CDE03-09 | avertissement | `CDE03-09 The '{feed_name}' feed does not support partial resync by IDs, or an unsupported identifier type was specified.` | `saas-export/SaaSCommon/Model/ResyncManager.php:295` |
| CDE03-10 | avertissement | `CDE03-10 There are no {id_field}s found to reindex for provided identifiers list: {identifiers}` | `saas-export/SaaSCommon/Model/ResyncManager.php:313` |
| CDE03-11 | erreur | `CDE03-11 Categories Permissions feed sync scheduling error on category "{category_id_and_name}" delete. Error: {error_message}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Plugin/MarkEntityAsDeletedOnCategoryRemove.php:86` |
| CDE03-12 | avertissement | `CDE03-12 Product Overrides sync failed. Marked indexer as invalid. Error: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/Indexer/Category/TriggerFullResync.php:58` |
| CDE03-13 | erreur | `CDE03-13 Cannot invalidate indexers "{indexer_ids}" for event "{event_name}". Error: {error_message}` | `commerce-data-export/DataExporter/Service/IndexInvalidationManager.php:58` |
| CDE03-14 | erreur | `CDE03-14 Failed to read config values. Indexer invalidation for event "{event_name}" skipped. Error: {error_message}` | `commerce-data-export/CatalogDataExporter/Plugin/Index/InvalidateOnConfigChange.php:80` |
| CDE03-15 | erreur | `CDE03-15 Categories Permissions feed sync scheduling error on config save: {error_message}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Plugin/InvalidateOnConfigChange.php:120` |
| CDE03-16 | erreur | `CDE03-16 Failed to reindex category permissions global configuration after full reindex: {error_message}` | `commerce-data-export-ee/CategoryPermissionDataExporter/Plugin/GlobalConfigurationReindex.php:73` |
| CDE03-17 | critique | `CDE03-17 Failed to recreate product override view subscriptions on customer group save: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/CreateViewAfterChangeCustomerGroup.php:61` |
| CDE03-18 | critique | `CDE03-18 Failed to recreate product override view subscriptions on customer group delete: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/CreateViewAfterChangeCustomerGroup.php:85` |
| CDE03-19 | erreur | `CDE03-19 Failed to remove product override view subscriptions during table maintenance: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/CreateViewAfterTableMaintenance.php:69` |
| CDE03-20 | erreur | `CDE03-20 Failed to recreate product override view subscriptions after table maintenance: {error_message}` | `commerce-data-export-ee/ProductOverrideDataExporter/Plugin/CreateViewAfterTableMaintenance.php:93` |

## Groupe 04 - Erreurs générales liées à l’indexation ou à la configuration

Codes de journal liés aux erreurs lors du processus d’indexation ou dues à une mauvaise configuration.

| Code de journal | Niveau | Message | Chemin du fichier |
|-----------|---------|---------|-----------|
| CDE04-02 | erreur | `CDE04-02 Cannot set indexer to Update On Schedule mode for indexer {indexer_id}. Error: {message}` | `commerce-data-export/DataExporter/Setup/Recurring.php:84` |
| CDE04-03 | avertissement | `CDE04-03 Partial sync failed for changelog "{changelog_name}". Should be retried. Error: {message}` | `commerce-data-export/DataExporter/Plugin/MviewUpdatePlugin.php:63` |
| CDE04-04 | erreur | `CDE04-04 Feed metadata does not contain indexer name. Check di.xml config` | `commerce-data-export/DataExporter/Service/FeedIndexerProvider.php:50` |
| CDE04-05 | erreur | `CDE04-05 Cannot load feed indexer for feed` | `commerce-data-export/DataExporter/Service/FeedIndexerProvider.php:60` |
| CDE04-06 | erreur | `CDE04-06 Failed to reset MView triggers for "{affected_views}" on index table switch. Run reindex. Error: {message}` | `commerce-data-export/CatalogDataExporter/Plugin/DDLTrigger/ResetTriggers.php:73` |
| CDE04-07 | erreur | `CDE04-07 Error on partial resync for feed "{feed_name}". Error: {message}` | `commerce-data-export/DataExporter/Model/Batch/FeedChangeLog/Generator.php:104` |
| CDE04-08 | erreur | `CDE04-08 Error retrying failed items sync for feed "{feed_name}". Error: {message}` | `commerce-data-export/DataExporter/Model/Batch/Feed/Generator.php:94` |
| CDE04-09 | erreur | `CDE04-09 Error on full resync for feed "{feed_name}". Error: {message}` | `commerce-data-export/DataExporter/Model/Batch/FeedSource/Generator.php:97` |
| CDE04-10 | erreur | `CDE04-10 Error during full sync. Message: "{message}". The following IDs were skipped: [{ids}]` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexProcessorCreateUpdate.php:172` |
| CDE04-11 | avertissement | `CDE04-11 Feed "{feed_name}" sync failed. Resync will be run on next cron run. Error: {message}` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexProcessorCreateUpdate.php:232` |
| CDE04-12 | avertissement | `CDE04-12 Partial sync failed for feed "{feed_name}". Retry has been scheduled. Error: {message}` | `commerce-data-export/DataExporter/Model/Indexer/ViewMaterializer.php:170` |
| CDE04-13 | erreur | `CDE04-13 Sync completed, but failed to persist status to feed table for "{feed_name}" feed. Error: {message}` | `commerce-data-export/DataExporter/Model/Indexer/FeedUpdater.php:125` |
| CDE04-14 | erreur | `CDE04-14 Cannot delete feed items for feed "{feed_name}" for ids: "{ids}". Error: {message}` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexProcessorCreateUpdateDelete.php:98` |
| CDE04-15 | avertissement | `CDE04-15 Failed to serialize metadata after sync. Error: {message}` | `commerce-data-export/DataExporter/Model/FeedExportStatus.php:93` |
| CDE04-16 | avertissement | `CDE04-16 Batch table insert query "{query}" returned unexpected result. Expected: {expected_class}, Actual: {actual_type}` | `commerce-data-export/DataExporter/Model/Batch/BatchTable.php:130` |
| CDE04-17 | avertissement | `CDE04-17 Failed to check indexer type when setting schedule mode: {message}` | `commerce-data-export/DataExporter/Plugin/ForceExporterIndexerModeOnSchedule.php:59` |
| CDE04-18 | avertissement | `CDE04-18 Fixture generator: failed to filter indexer changelog tables from fixture SQL: {message}` | `commerce-data-export/CatalogDataExporter/Plugin/FilterChangeLogTable.php:43` |
| CDE04-19 | avertissement | `CDE04-19 The identifier for a feed item is empty. Sync is skipped for the entity.` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexProcessorCreateUpdate.php:439` |
| CDE04-20 | avertissement | `CDE04-20 Unexpected call: feed "{feed_name}" is not locked, trace: {stack_trace}` | `commerce-data-export/DataExporter/Model/Indexer/FeedIndexer.php:204` |

>[!MORELIKETHIS]
>
> - [Consulter les journaux et résoudre les problèmes](logging.md)
> - [Dépannage des scénarios](troubleshooting-scenarios.md)
> - [Schéma de la table des flux](../reference/feed-table-reference.md)
