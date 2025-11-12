---
title: Connecteur Adobe Commerce Optimizer pour Commerce
description: Découvrez comment connecter vos données de votre projet cloud ou local Commerce à Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
hidefromtoc: true
hide: true
source-git-commit: 5d0cfb2c389bf11f89815e7d1fbc2861a6b48962
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 0%

---


# Vue d’ensemble

Le connecteur Adobe Commerce est le pont d’intégration qui synchronise les données de catalogue et de tarification entre un déploiement Adobe Commerce Cloud on cloud ou on-premise existant et le modèle de données de catalogue composable Adobe Commerce Optimizer. Cela permet d’accéder à des fonctionnalités telles que la recherche IA dynamique, les recommandations, les storefronts découplés à chargement rapide, y compris les storefronts Adobe Commerce sur Edge Delivery Services, et l’analyse des performances en temps réel.

>[!NOTE]
>
>Cette documentation décrit un produit en développement à accès anticipé et ne reflète pas toutes les fonctionnalités destinées à une disponibilité générale.

## Architecture et expérience

Le connecteur Adobe Commerce fonctionne en mappant la hiérarchie de catalogue de `website/store/storeview` Commerce au modèle de données de `channel/policy/source` Adobe Commerce Optimizer.

Au lieu de configurer et de gérer les services Commerce (recherche en direct et recommandations de produits) à partir de l’administration Commerce, vous utilisez [les outils de marchandisage Adobe Commerce Optimizer](../optimizer/merchandising/overview.md) pour gérer la découverte de produits (recherche en direct) et la configuration de règles (recommandations de produits).  L’instance Adobe Commerce devient l’origine des données pour les données de catalogue et de prix. Lorsque les données sont mises à jour dans Commerce, les mises à jour sont synchronisées avec l’instance Adobe Commerce Optimizer.

## Workflows

Le connecteur permet plusieurs workflows clés :

* **Exporter les données du catalogue Commerce vers Adobe Commerce Optimizer** : les données des prix et du catalogue des prix sont exportées au niveau `website`. Les données de produit et d’attribut de produit sont exportées au niveau du `store view`. Par défaut, la synchronisation des données de catalogue est activée pour toutes les portées de Commerce (sites web et vues de magasin).

  Pour activer ce workflow, utilisez le compositeur afin d’installer l’extension PHP `adobe-commerce/commerce-data-export-aco-adapter`, puis fournissez les informations d’identification IMS pour authentifier la connexion entre le projet Commerce.

* **Mapper les données de `website/store/storeview` Commerce à exporter vers Adobe Commerce Optimizer**

  Vous avez la possibilité de personnaliser les paramètres de l’exportateur Adobe Commerce Optimizer pour exporter des données uniquement pour des portées spécifiques en mettant à jour la configuration de l’exportateur à partir de la grille de magasin dans Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* **Configuration et gestion des règles de marchandisage**

  Lorsque le connecteur est activé, les règles de marchandisage pour la découverte de produits et les recommandations sont définies et gérées à partir de l’interface utilisateur de Adobe Commerce Optimizer, et non à partir des pages [!UICONTROL Live Search] et [!UICONTROL Product Recommendations] de l’administration Commerce.

* **Déploiement de votre storefront Commerce sur Edge Delivery Services**

  Après avoir configuré l’intégration avec Adobe Commerce Optimizer, vous pouvez configurer et déployer un storefront Commerce sur les services Edge Delivery pour offrir des performances, une évolutivité, une création de contenu transparente, une personnalisation intégrée et des coûts opérationnels réduits à l’aide de l’architecture composable pilotée par les API et des composants modulaires disponibles avec Adobe Commerce Optimizer.

## Conditions requises pour utiliser l’intégration

* Adobe Commerce 2.4.5+

   * PHP 8.1, 8.2, 8.3 ou 8.4
   * Compositeur 2.x

* Licence Adobe Commerce Optimizer avec une instance sandbox configurée.

* Accès à [repo.magento.com](https://repo.magento.com) pour télécharger le métapaquet du connecteur Commerce à l’aide du compositeur.

* Accès administrateur à une instance sandbox Adobe Commerce Optimizer [&#128279;](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

L’utilisateur d’Adobe Commerce configurant l’intégration doit disposer des éléments suivants :

* Accès des administrateurs à l’administration Adobe Commerce.

* [Accès en ligne de commande au serveur applicatif Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-on-cloud/user-guide/project/user-access).

* Accès des développeurs à l’organisation [IMS](https://experienceleague.adobe.com/fr/docs/core-services/interface/administration/organizations?) où le projet Adobe Commerce Optimizer est configuré.

## Prise en main

1. **Configurer l’intégration**

   1. [Installez le package Connecteur Commerce](#install-the-commerce-connector-package).

   1. [Obtenez les valeurs requises pour configurer la connexion Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [Activez l’intégration de Adobe Commerce Optimizer](#enable-the-adobe-commerce-optimizer-integration).

   1. [Vérifiez que la synchronisation des données fonctionne](#verify-that-the-data-sync-is-working).

   1. [&#x200B; Personnaliser la configuration de l’exportation des données &#x200B;](#customize-commerce-data-export-configuration) (facultatif).

1. **[Configuration des magasins Adobe Commerce Optimizer](#configure-adobe-commerce-optimizer-stores)**

1. **[Configuration d’un storefront Commerce sur Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Installation du package Connecteur Commerce

Le métapaquet du compositeur de connecteur Adobe Commerce est disponible pour tous les commerçants Commerce disposant d’une licence active pour Adobe Commerce Optimizer.

### Etapes d&#39;installation

1. Ajoutez le module `adobe-commerce/commerce-data-export-aco-adapter` à l’aide du compositeur :

```shell
 composer require adobe-commerce/commerce-data-export-aco-adapter
```

1. Déployez les modifications dans votre environnement d’évaluation Adobe Commerce.

Une fois vos modifications déployées, l’option Commerce Optimizer Optimizer est disponible dans le menu Admin de Commerce.

>[!NOTE]
>
>Pour obtenir des instructions d’installation d’extension détaillées, consultez les guides suivants :
>
>[Installation de l’extension sur Adobe Commerce sur une infrastructure cloud](https://experienceleague.adobe.com/fr/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Installation de l’extension Adobe Commerce sur site](https://experienceleague.adobe.com/fr/docs/commerce-operations/installation-guide/tutorials/extensions)

## Obtenir les valeurs requises pour la configuration de la connexion Commerce Optimizer

### Obtention des informations d’identification d’API

>[!NOTE]
>
>Si vous disposez déjà d’un projet App Builder Developer dans l’organisation IMS où votre instance Commerce Optimizer est déployée, vous pouvez obtenir les informations d’identification d’API et d’organisation requises à partir des informations d’identification de serveur à serveur OAUTH de ce projet.

Créez un projet de développement dans la console Adobe Developer afin d’obtenir des informations d’identification d’API pour configurer l’intégration entre les instances Commerce et Commerce Optimizer. Pour obtenir des instructions détaillées, voir [Création d’un projet App Builder](https://developer.adobe.com/commerce/extensibility/events/project-setup/) dans la documentation destinée aux développeurs.

Après avoir créé le projet, enregistrez les valeurs suivantes à partir de la page des informations d’identification de serveur à serveur OAUTH :

* **Identifiant de l’organisation** (`org_id`)

* **`client_id` et`client_secret`** IMS

### Obtention des détails de l’instance Adobe Commerce Optimizer

Enregistrez les valeurs suivantes à partir des détails de votre instance Adobe Commerce Optimizer.

* **Identifiant d’instance : &#x200B;** identifiant unique de votre instance Adobe Commerce Optimizer. Également appelé identifiant client.

  Obtenez l’ID d’instance à partir de l’URL pour accéder à votre instance Adobe Commerce Optimizer. Par exemple, dans le `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef` URL, l’ID d’instance est `1234567890abcdef`.

* **Region—**&#x200B;Région dans laquelle votre instance Sandbox Adobe Commerce Optimizer est hébergée.

  Récupérez la région à partir de l’URL Adobe Commerce Optimizer. Par exemple, dans le `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef` URL, la région est `na1`.

## Activation de l’intégration de Adobe Commerce Optimizer

>[!IMPORTANT]
>
>Le traitement de la synchronisation des données commence lorsque vous exécutez la commande de configuration. Par défaut, la synchronisation des données de catalogue est activée pour toutes les portées de Commerce (sites web et vues de magasin). Selon la taille de votre catalogue, le processus de synchronisation des données peut prendre plusieurs heures.

À l’aide des informations d’identification d’API et des détails d’instance que vous avez rassemblés lors des étapes précédentes, vous pouvez maintenant configurer l’intégration entre vos instances Commerce et Adobe Commerce Optimizer.

1. Dans l’Administration de Commerce, sélectionnez **[!UICONTROL Adobe Commerce Optimizer]** pour afficher la page de configuration avec les instructions.

   ![Page de configuration de Adobe Commerce Optimizer](../assets/aco-connector-config-page.png)

1. À partir de la ligne de commande, [utilisez SSH](https://experienceleague.adobe.com/fr/docs/commerce-on-cloud/user-guide/develop/secure-connections) pour vous connecter à l’environnement d’évaluation Commerce.

1. Exécutez la commande de l’interface de ligne de commande Commerce suivante pour configurer l’intégration et remplacer les valeurs d’espace réservé par les valeurs de votre projet Commerce Optimizer :

```terminal
bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
```

1. Vérifiez la connexion en revenant à l’administration Commerce et en sélectionnant l’option [!UICONTROL Adobe Commerce Optimizer] .

   Lorsque vous cliquez sur cette option, elle ouvre l’interface utilisateur de Adobe Commerce Optimizer dans un nouvel onglet.

## Vérifier que la synchronisation des données fonctionne

Vous pouvez vérifier la synchronisation des données à partir de l’administration Commerce et de Commerce Optimizer.

* La **[page Statut de la synchronisation des flux de données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)** indique la progression de la synchronisation des données du catalogue de Commerce vers Adobe Commerce Optimizer.

* La **[[!UICONTROL Data Sync]page &#x200B;](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/setup/data-sync)** dans Adobe Commerce Optimizer affiche les données de catalogue transférées à partir de votre instance Commerce.

1. Vérifiez que les données du catalogue circulent de Commerce vers Commerce Optimizer :

   Dans Commerce Admin, ouvrez la page [!UICONTROL Data Feed Sync Status] en sélectionnant [!UICONTROL System] **&#x200B; > [!UICONTROL Data Transfer] > &#x200B;** [!UICONTROL Data Feed Sync Status]**.

   ![Page État de synchronisation des flux de données avec rapport sur l’état des éléments de flux](./assets/data-feed-sync-status.png)

   Si la synchronisation des données a commencé, les données de flux affichent les enregistrements envoyés avec succès. Vous pouvez également afficher et résoudre les problèmes de synchronisation en affichant les détails de chaque flux.

1. Vérifiez que Adobe Commerce Optimizer reçoit les données du catalogue :

   Dans le menu Commerce Optimizer , sélectionnez **[!UICONTROL Data Sync]** pour ouvrir la page Synchronisation des données .

   ![Synchronisation des données](./assets/data-sync.png)

### Dépannage

Si la synchronisation des données n’a pas démarré, assurez-vous que les index de catalogue sont valides. Si les index ne sont pas valides, exécutez la commande suivante à partir de l’interface de ligne de commande Commerce pour réindexer les données du catalogue :

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## Personnaliser la configuration de l’exportation des données Commerce

Vous avez la possibilité de personnaliser les paramètres de l’exportateur Adobe Commerce Optimizer pour exporter des données uniquement pour des portées spécifiques en mettant à jour la configuration de l’exportateur à partir de la grille de magasin dans Admin (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* Au niveau `website`, la désactivation du paramètre de l’exportateur arrête l’exportation des prix et des données du catalogue des prix vers Adobe Commerce Optimizer.

* Au niveau du `storeview`, la désactivation du paramètre de l’exportateur arrête l’exportation des produits et des attributs de produit vers Adobe Commerce Optimizer.

Lorsque la configuration est modifiée, les index correspondants sont invalidés afin de déclencher la réexportation des entités affectées.

## Configuration des magasins Adobe Commerce Optimizer

Configurez les magasins Adobe Commerce Optimizer en créant des vues de catalogue et des politiques&#x200B; Voir [Création de vues de catalogue](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/setup/catalog-view) dans le guide de Adobe Commerce Optimizer.

Notez que les tarifs sont créés automatiquement à partir des groupes de clients Adobe Commerce.

## Configuration d’un storefront Commerce sur Edge Delivery Services

Cette section présente de manière générale les étapes requises pour configurer votre storefront Commerce. Des informations détaillées sont disponibles sur le site de documentation [Adobe Commerce Storefront] (https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr).

1. Clonez et déployez le standard Adobe Commerce Storefront sur EDS à l’aide de l’outil [Site Creator](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. [Configurer un environnement de développement local](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=fr#set-up-local-environment).

1. [Installer le package de compatibilité GraphQL Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/?lang=fr).&#x200B;

1. [Configurez les en-têtes CORS pour l’instance Commerce dans l’environnement cloud](#configure-cors-headers-for-commerce-instance).

1. [Connecter le storefront aux sources de données Commerce](#connect-the-storefront-to-commerce-data-sources).

### Configuration des en-têtes CORS pour l’instance Commerce

Pour autoriser les requêtes GraphQL à provenir d’un storefront Edge Delivery Services (EDS) vers un environnement Adobe Commerce sur le cloud ou on-premise, utilisez l’une des options suivantes pour ajouter des en-têtes CORS (Cross-Origin Resource Sharing) spécifiques aux points d’entrée Adobe Commerce GraphQL&#x200B;

1. Ajoutez des en-têtes CORS (Cross-Origin Resource Sharing) aux points d’entrée GraphQL Adobe Commerce&#x200B;

   **Option 1 : Implémenter un module personnalisé PHP pour Adobe Commerce Foundation afin de pouvoir ajouter des en-têtes CORS.&#x200B;**

   **Option 2 : installer un module communautaire tiers graycore/magento2-cors&#x200B;** - Voir [Configuration CORS](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/?lang=fr) dans la documentation *Adobe Commerce Storefront*.

1. Ajoutez les variables CORS suivantes au fichier de configuration de l’environnement `app.yaml` de l’instance Commerce on cloud :

   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_HEADERS: *`
   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_ORIGINS: *`

### Connecter le storefront aux sources de données Commerce

Dans le référentiel GitHub du code standard Storefront, mettez à jour le fichier de configuration storefront, `config.json` avec les paramètres suivants :

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"` - Obtenez cette valeur à partir de la page des détails de l’instance Commerce Optimizer [&#128279;](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/get-started#get-instance-details)&#x200B;

* `"AC-Environment-Id": "Customer organization ID"` - Obtenez cette valeur à partir du projet cloud Commerce [&#128279;](https://experienceleague.adobe.com/fr/docs/commerce-on-cloud/user-guide/project/overview#project-overview)

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"` - Obtenez cette valeur auprès de l’administrateur Adobe Commerce Optimizer.

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"` — Obtenir cette valeur auprès de l&#39;administrateur Adobe Commerce Optimizer&#x200B;

* `"AC-Source-Locale": "Catalog source – Store View code from Commerce cloud instance"`

Pour plus d’informations, voir [Configuration de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/?lang=fr) dans la documentation de *Adobe Commerce Storefront*.


