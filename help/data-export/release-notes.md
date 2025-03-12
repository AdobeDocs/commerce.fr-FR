---
title: Notes de mise à jour de [!DNL SaaS Data Export Extension]
description: Dernières informations de mise  [!DNL Data Export Extension]  jour pour Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
exl-id: 8ae51d3d-8c12-4607-b7e5-985033143a84
source-git-commit: e30210e6aac469929e4767e3747bd819bc10b9f4
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# Notes de mise à jour de l’extension [!DNL SaaS Data Export]

Ces notes de mise à jour décrivent les dernières versions de l’extension [!DNL SaaS data export]. La prise en charge est assurée pour la version majeure publiée actuelle. Les notes de mise à jour des anciennes versions sont fournies à titre de référence.

Les mises à jour incluent :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correctifs](../assets/fix.svg) Correctifs et améliorations
![Bogue](../assets/bug.svg) Problèmes connus


>[!NOTE]
>
>L’extension d’exportation de données SaaS est un ensemble de modules installés automatiquement avec Live Search, Product Recommendations et Catalog Service. Vous pouvez vérifier la version installée sur votre système à l’aide du compositeur. Dans certains cas, vous souhaiterez peut-être mettre à niveau l’extension d’exportation de données sur votre système pour relever les correctifs ou les nouvelles fonctionnalités sans mettre à jour la version du service Commerce.

## Version majeure actuelle

## Version 103.3.21

![Correctif](../assets/new.svg) Ajout d’une fonctionnalité pour synchroniser partiellement les flux de `product`, de `productOverrides` et de `productAttributes` en fonction d’une liste spécifiée de SKU de produit. Utilisez la nouvelle fonctionnalité en ajoutant l’option `--by-ids` à la commande de l’interface de ligne de commande `bin/magento saas:resync --feed=<FEED_NAME>`. <!--MDEE-606-->
![Correctif](../assets/fix.svg) Réduction des problèmes de compatibilité potentiels avec PHP 8.4 en résolvant les fonctionnalités obsolètes. <!--MDEE-1002-->

## Version 103.3.20

![Correction](../assets/fix.svg) Correction des erreurs de `BulkException` non traçables dans le `cron.log` en améliorant la messagerie pour les erreurs liées aux échecs de la tâche cron d’exportation des données de catalogue.<!--MDEE-966-->
![Correctif](../assets/fix.svg) Amélioration des performances du processus de resynchronisation du produit sur les instances comportant un grand nombre de vues de magasin. <!--MDEE-974-->

## Version 103.3.19

![Correctif](../assets/fix.svg) Mise à jour de l’extension d’exportation des données pour améliorer l’extensibilité des flux. <!--MDEE-936-->
![Correction](../assets/fix.svg) Le processeur d’exportation de données vérifie désormais le statut de l’indexeur avant une resynchronisation complète afin d’éviter toute perte accidentelle de données dans la table de flux.

## Version 103.3.18

![Correctif](../assets/fix.svg) Les mises à jour d’évaluation des entités de produit et de catégorie sont désormais correctement déclenchées lors des mises à jour des données d’exportation de données.<!--MDEE-963-->

## Version 103.3.17

![Correctif](../assets/fix.svg) Ajout de la compatibilité pour PHP 8.4. <!--MDEE-941-->

## Version 103.3.16

![Correctif](../assets/fix.svg) Les valeurs d’option peuvent être vides pour les produits configurables pour plusieurs vues de magasin. <!--MDEE-926-->

## Version 103.3.15

![Correctif](../assets/fix.svg) Fonctionnement stable des tests d’intégration sur les anciennes configurations. <!--MDEE-869-->
![Correctif](../assets/fix.svg) Arrêtez la propagation des options d’attribut inutiles. <!--MDEE-882-->
![Correction](../assets/fix.svg) Correction du message d’erreur envoyé au journal d’exportation des données lorsque la sérialisation des données échouait. <!--MDEE-913-->
![Correctif](../assets/fix.svg) Amélioration de la fiabilité des mises à jour simples des produits avec une couverture de test supplémentaire. <!--MDEE-886-->

## Version 103.3.14

![Correction](../assets/fix.svg) L’indexeur de l’exportateur conserve désormais le statut correct pour les indexeurs dépendants. Auparavant, ces index étaient incorrectement invalidés et nécessitaient des vérifications et une validation supplémentaires qui ralentissaient les performances de l’indexation. <!--MDEE-866-->

## Version 103.3.13

![Correctif](../assets/fix.svg) Amélioration des performances du processus de synchronisation des données en ajoutant un cache local pour les données des options d’attribut.<!--MDEE-864-->

## Version 103.3.12

![Correctif](../assets/fix.svg) Résolution d’un problème qui augmentait le temps de synchronisation pour les produits simples et virtuels. <!--MDEE-861-->

## Version 103.3.11

![Correctif](../assets/fix.svg) Le service d’exportation de données envoie désormais des données de prix spéciales pour les produits groupés sous la forme d’un pourcentage, corrigeant un problème précédent en raison duquel elles étaient envoyées sous la forme d’un prix final. <!--MDEE-854-->
![Correctif](../assets/fix.svg) Mise à jour de l’implémentation de Monolog pour la compatibilité avec Monolog 3. <!--MDEE-858-->

## Version 103.3.10

![Correction](../assets/fix.svg) Correction du filtrage de plusieurs magasins pour le flux d’options personnalisées du produit. <!--MDEE-842-->
![Correction](../assets/fix.svg) Les flux non valides ne sont pas renvoyés tant que la valeur de hachage du flux n’a pas changé.<!--MDEE-848-->

## Version 103.3.9

![Correctif](../assets/fix.svg) Lorsqu’une entité est supprimée, l’indicateur de `deleted` est désormais propagé pour les flux du service de définition de la portée pour le site web (`scopesWebsite`) et le groupe de clients (`scopesCustomerGroup`).<!--MDEE-839-->

## Version 103.3.8

![Correctif](../assets/fix.svg) Les options de configuration désactivées ne sont plus exportées en tant qu’options actives.<!--MDEE-812-->
![Correctif](../assets/fix.svg) Les options et les valeurs sont désormais mises à jour sur un produit configurable lorsque des modifications sont apportées à un produit enfant. <!--MDEE-835-->
![Nouveau](../assets/new.svg) Ajout de la possibilité d’inclure des données d’attributs système supplémentaires dans le flux d’attributs de produit.

## Version 103.3.7

![Fix](../assets/fix.svg) Suppression des dépendances inutiles du module InventoryDataExporter.
![Correctif](../assets/fix.svg) Modification des versions requises des modules d’inventaire inclus dans le module CatalogInventoryDataExporter afin de prendre en charge Adobe Commerce version 2.4.4.

## Version 103.3.6

![Correctif](../assets/fix.svg) Correction des blocages qui se produisaient lors de la réindexation des flux en mode multi-thread. Les requêtes sont désormais séparées dans les opérations Insérer et Mettre à jour .
![Correctif](../assets/fix.svg) Optimisation de la requête Prix pour les catalogues volumineux avec de nombreux sites web.
![Nouveau](../assets/new.svg) Ajout d’une logique de reprise pour réexécuter les transactions ayant échoué lorsque des blocages se produisent.

## Version 103.3.5

![Correctif](../assets/fix.svg) Définissez la dépendance pour la dernière version d’exportation de données compatible pour le module commun SaaS.

![Correctif](../assets/fix.svg) Remplacement de `ScopeConfig` instance par `ServiceConfigInterface` pour prendre en charge différentes configurations de service.

## Version 103.3.4

![Correctif](../assets/fix.svg) Ajout de la prise en charge de la journalisation d’audit du transfert de données en ajoutant un mécanisme pour distribuer un événement `data_sent_outside` chaque fois que des données sont transmises de l’instance Commerce à un <!--MDEE-785--> de service Commerce

## Version 103.3.3

L’exportation de données ![New](../assets/new.svg) SaaS met désormais en cache les attributs Entity-Attribute-Value (EAV) pour la requête de métadonnées d’attribut.

![Correction](../assets/fix.svg) correction d’un problème en raison duquel le flux de `InventoryStockStatus` n’était pas enregistré lors de la reprise si le produit était supprimé.

## Version 103.3.2

![Correction](../assets/fix.svg) Correction d’un problème en raison duquel le champ `modifiedAt` était absent des flux d’entités supprimés.

## Version 103.3.1

![Correction](../assets/fix.svg) correction d’un problème en raison duquel un message `Invalid Template File` s’affichait lors de la réindexation du flux de produits lors de l’installation de Page Builder.

## Version 103.3.0

![Nouveau](../assets/new.svg) Tables de flux d&#39;export immédiat migrées vers la structure unifiée :
`id`, `source_entity_id`, `feed_id`, `modified_at`, `is_deleted`, `status`, `feed_data`, `feed_hash`, `errors`

![Nouveau](../assets/new.svg) Flux de catalogue et d’inventaire migrés vers la solution d’exportation immédiate.

![Nouveau](../assets/new.svg) les tâches cron du flux d’exportation immédiat ont été renommées `*_feed_resend_failed_items`.

![Nouveau](../assets/new.svg) Flux d’exportation immédiats renommés, ID de vue d’indexeur et tables de journaux des modifications.
- tables de flux (et ID de vue de l’indexeur) :
   - `catalog_data_exporter_products` -> `cde_products_feed`
   - `catalog_data_exporter_product_attributes` -> `cde_product_attributes_feed`
   - `catalog_data_exporter_categories` -> `cde_categories_feed`
   - `catalog_data_exporter_product_prices` -> `cde_product_prices_feed`
   - `catalog_data_exporter_product_variants` -> `cde_product_variants_feed`
   - `inventory_data_exporter_stock_status` -> `inventory_data_exporter_stock_status_feed`
- modifier les noms des tables de logs : suit le même modèle de dénomination que les tables de flux, mais la modification des noms des tables de logs ajoute un suffixe `_cl`.  Par exemple `catalog_data_exporter_products_cl`-> `cde-products_feed_cl`
Si du code personnalisé fait référence à l’une de ces entités, mettez à jour les références avec les nouveaux noms pour vous assurer que votre code continue à fonctionner correctement.

![Correctif](../assets/fix.svg) Définissez `modified_at` champ dans les données de flux uniquement pour les flux qui le nécessitent.

![Correctif](../assets/fix.svg) modifiez la requête `productAttributes` pour récupérer uniquement les attributs de produit.

## Version 103.2.6

![Correctif](../assets/fix.svg) Correction d’un problème qui empêchait la réindexation des flux lorsque les tables avaient un préfixe.

## Version 103.2.5

![Correctif](../assets/fix.svg) Optimisation de la requête Prix.

## Version 103.2.4

![Correctif](../assets/fix.svg) Correction d’un statut Stock incorrect qui s’affichait pour un produit lorsque Commerce Inventory management était activé.

## Version 103.2.3

![Fixe](../assets/fix.svg) Tarification spéciale fixe au niveau du site web.
![Correctif](../assets/fix.svg) Ajout d’un mutex pour tous les flux traités.


## Version 103.2.2

![Correctif](../assets/fix.svg) Amélioration de la stratégie de traitement par lots des flux pour les catalogues volumineux. Le tableau des lots est maintenant rempli avec un nombre limité d’identifiants afin de réduire l’utilisation de la mémoire.

![Correctif](../assets/fix.svg) Suppression de la dépendance matérielle de CommerceInventoryDataExporter aux modules MSI.

![Correctif](../assets/fix.svg) Amélioration des journaux `commerce-data-exporter` pour collecter plus d’informations et les organiser par différentes étapes d’exportation.

## Version 103.2.1

- Version mise à jour publiée.

## Version 103.2.0

- Ajout de la synchronisation des données multithread pour les produits et les prix.
