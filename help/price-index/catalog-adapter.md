---
title: Extension de la carte catalogue
description: Utilisation de l’adaptateur de catalogue pour effectuer le rendu des prix à partir des services Commerce
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
exl-id: e42101fa-9c30-482c-a649-44dc35376abb
source-git-commit: 74f6cb64724194651c4eeb538c0c69142b01ac5d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Catalog Adapter

L’extension `[!DNL Catalog Adapter]` désactive l’indexeur de prix de produit par défaut inclus dans l’application Commerce et utilise à la place les prix fournis par le [service de catalogue](../catalog-service/overview.md).

L&#39;adaptateur est conçu pour fonctionner avec l&#39;exportation de données [SaaS](../data-export/overview.md) et le service Adobe Commerce. L’exportation des données SaaS est chargée de soumettre les prix, et le [!DNL Catalog Adapter] récupère tous les prix auprès du service Adobe Commerce.

Lorsque vous activez la [!DNL Catalog Adapter], l’indexation des prix et les opérations sont affectées des manières suivantes :

- L’indexeur de prix inclus dans l’application Adobe Commerce est désactivé.
- Les prix sont gérés à l&#39;aide de l&#39;export de données SaaS et de l&#39;indexeur de prix [SaaS](price-indexing.md).
- Lorsqu’un client ouvre une page de produit, de catégorie ou autre qui affiche les prix des produits, les prix sont récupérés à partir du service Adobe Commerce.
- Les prix sont envoyés au service Adobe Commerce en synchronisant les données issues de l’exportation des données [SaaS](../data-export/overview.md).
- Le passage en caisse recalcule les prix de manière dynamique.

Vous pouvez réactiver l&#39;indexation des prix dans l&#39;application Commerce en supprimant ou en désactivant l&#39;extension Catalog Adapter.

## Conditions requises

- Adobe Commerce 2.4.4+
- L’un des services Commerce suivants doit être activé et configuré pour votre environnement Adobe Commerce :

   - [Recherche en direct](../live-search/install.md)
   - [Recommandations de produit](../product-recommendations/install-configure.md)
   - [Service de catalogue](../catalog-service/installation.md)

## Installation

L’extension Catalog Adapter est un métapaquet Composer qui installe les modules suivants :

- **Désactivation de l’indexeur de prix**-ce module désactive l’index de prix dans l’application Commerce afin que les prix soient diffusés via l’indexation des prix SaaS. L&#39;indexeur de prix de produit dans l&#39;application Commerce ne peut pas être activé lorsque l&#39;extension d&#39;indexation de prix SaaS est installée.
- **Fournisseur de prix**-Ce module fournit les prix des produits du service Adobe Commerce. Il forme la requête de recherche et obtient les prix des produits sur le serveur frontal.
- **Catalog Service Search Adapter** : ce module transfère les prix de l’application Adobe Commerce vers un service Adobe Commerce en réponse à une demande de recherche de produit.

## Etapes d&#39;installation

>[!BEGINTABS]

>[!TAB Infrastructure cloud]

Utilisez cette méthode pour installer le [!DNL Catalog Adapter] pour une instance Commerce Cloud.

1. Sur votre station de travail locale, accédez au répertoire du projet d’infrastructure cloud d’Adobe Commerce.

   >[!NOTE]
   >
   >Pour plus d’informations sur la gestion locale des environnements de projet Commerce, voir [Gestion des branches avec l’interface de ligne de commande](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) dans le _Guide d’utilisation d’Adobe Commerce sur les infrastructures cloud_.

1. Consultez la branche d’environnement pour effectuer la mise à jour à l’aide de l’interface de ligne de commande Adobe Commerce Cloud.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Ajoutez le module Catalog Adapter.

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Mettez à jour les dépendances de package.

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. Validez et envoyez les modifications de code pour les fichiers `composer.json` et `composer.lock`.

1. Ajoutez, validez et envoyez les modifications de code des fichiers `composer.json` et `composer.lock` à l’environnement cloud.

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   L’envoi des mises à jour à l’environnement cloud lance le processus de déploiement cloud de [Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) pour appliquer les modifications. Vérifiez le statut du déploiement dans le [journal de déploiement](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB Sur site]

Utilisez cette méthode pour installer le [!DNL Catalog Adapter] pour une instance locale.

1. Ajoutez l’adaptateur de catalogue à votre projet à l’aide du compositeur :

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Mettez à jour les dépendances et installez l’extension :

   ```bash
   composer update  "magento/catalog-adapter"
   ```

1. Mettre à niveau Adobe Commerce :

   ```bash
   bin/magento setup:upgrade
   ```

1. Effacez le cache :

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >Dans certains cas, en particulier lors d’un déploiement en production, vous pouvez éviter d’effacer le code compilé, car cela peut prendre un certain temps. Assurez-vous de sauvegarder votre système avant d’y apporter des modifications.

>[!ENDTABS]


## Réactivez l’indexeur des prix des produits Adobe Commerce

Si vous disposez d’applications tierces qui reposent sur l’indexeur de prix de produit par défaut d’Adobe Commerce, vous pouvez le réactiver à l’aide des commandes suivantes :

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## Désactiver l’indexeur des prix des produits pour le scénario Headless Storefront

Si vous disposez d’une instance Commerce découplée, vous devrez peut-être désactiver l’indexeur des prix des produits Adobe Commerce pour réduire la charge sur votre instance Adobe Commerce. Vous pouvez effectuer cette tâche en installant le module `magento/module-price-indexer-disabler` :

```bash
composer require magento/module-price-indexer-disabler
```

## Scénarios d’utilisation

Voici quelques scénarios de `[!DNL Catalog Adapter]` courants.

### Aucune dépendance à l’indexeur de prix de produit Adobe Commerce

- Vous êtes un commerçant de Luma ou Adobe Commerce Core GraphQL pour lequel un service requis est installé (recherche en direct, recommandations de produits, service de catalogue)
- Aucune intégration avec des extensions tierces qui reposent sur l’indexeur de prix de produit Adobe Commerce

1. Installez le [!DNL Catalog Adapter] .

### Avec des dépendances de l’indexeur de prix de produit Adobe Commerce

- Vous êtes un commerçant de Luma ou Adobe Commerce Core GraphQL pour lequel un service pris en charge est installé (recherche en direct, recommandations de produits, service de catalogue)
- Vous utilisez une extension tierce qui repose sur l’indexeur de prix de produit Adobe Commerce

1. Installez le [!DNL Catalog Adapter] .
1. Réactivez l’indexeur des prix des produits Adobe Commerce par défaut.

### Instances de Commerce découplées

- Un commerçant disposant d’une instance Commerce découplée avec les services requis installés (recherche en direct, recommandations de produits, service de catalogue)
- Pas de dépendance à l’indexeur de prix de produit par défaut d’Adobe Commerce

1. Installez le module `magento/module-price-indexer-disabler` à partir du package [!DNL Catalog Adapter].
