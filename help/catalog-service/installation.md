---
title: Intégration et installation
description: Découvrez comment installer  [!DNL Catalog Service]
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# Intégration et installation

Installez Catalog Service pour demander et recevoir des données de produit d’une instance Commerce à l’aide de l’[API GraphQL Catalog Service](https://developer.adobe.com/commerce/services/graphql/catalog-service/). Le service de catalogue est fourni en tant que métapaquet de compositeur à partir du référentiel repo.magento.com.

>[!NOTE]
>
>Si votre instance de Commerce utilise Live Search ou Product Recommendations, le service de catalogue est installé ou mis à jour automatiquement lorsque vous intégrez ou mettez à niveau ces services. Pour plus d’informations, consultez les instructions d’installation de [Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) et [Product Recommendations](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure).



## Configuration requise

**Configuration logicielle requise**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3, 8.4
- Compositeur : 2.x

**Plateformes prises en charge**

- Adobe Commerce sur les infrastructures cloud : 2.4.4+
- Adobe Commerce on-premise : 2.4.4+

## Points d’entrée

[!DNL Catalog Service] dispose de deux points d’entrée disponibles pour l’intégration :

- Sandbox (`https://catalog-service-sandbox.adobe.io/graphql`) : utilisé à des fins de test et de validation avant la mise en ligne
- Production (`https://catalog-service.adobe.io/graphql`) : utilisé pour le trafic en direct pour les commerçants et les sites Web Commerce

Toutes les instances de test Commerce utilisent le point d’entrée Sandbox.

Effectuez tous les tests de chargement sur le point d’entrée Sandbox. Avant de commencer les tests de chargement, envoyez un [ticket d’assistance](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) afin que l’équipe des services puisse anticiper le trafic supplémentaire du serveur.

## Installation et configuration

Pour commencer à utiliser [!DNL Catalog Service] pour Adobe Commerce, les étapes sont les suivantes :

- Installation de l’extension du service de catalogue (`magento/catalog-service`)
- Configuration du service et de l&#39;export des données
- Accès au service

### Installation de l’extension du service de catalogue

>[!BEGINSHADEBOX]

**Prérequis**

- Accédez à [repo.magento.com](https://repo.magento.com) pour installer l’extension. Pour la génération des clés et l’obtention des droits nécessaires, voir [ Obtenir vos clés d’authentification ](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Pour les installations cloud, consultez le guide [Commerce sur les infrastructures cloud](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- Accès à la ligne de commande du serveur applicatif Adobe Commerce.

>[!ENDSHADEBOX]

Installez la dernière version de l’extension Catalog Services (`magento/catalog-service`) sur une instance Adobe Commerce qui exécute Adobe Commerce version 2.4.4 ou ultérieure. Le service de catalogue est fourni en tant que métapaquet de compositeur à partir du référentiel [repo.magento.com](https://repo.magento.com).

>[!BEGINTABS]

>[!TAB Infrastructure cloud]

Utilisez cette méthode pour installer le [!DNL Catalog Service] pour une instance Commerce Cloud.

1. Sur votre station de travail locale, accédez au répertoire du projet d’infrastructure cloud d’Adobe Commerce.

   >[!NOTE]
   >
   >Pour plus d’informations sur la gestion locale des environnements de projet Commerce, voir [Gestion des branches avec l’interface de ligne de commande](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) dans le _Guide d’utilisation d’Adobe Commerce sur les infrastructures cloud_.

1. Consultez la branche d’environnement pour effectuer la mise à jour à l’aide de l’interface de ligne de commande Adobe Commerce Cloud.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Ajoutez le module Service de catalogue .

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Mettez à jour les dépendances de package.

   ```bash
   composer update "magento/catalog-service"
   ```

1. Validez et envoyez les modifications de code pour les fichiers `composer.json` et `composer.lock`.

1. Ajoutez, validez et envoyez les modifications de code des fichiers `composer.json` et `composer.lock` à l’environnement cloud.

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   L’envoi des mises à jour à l’environnement cloud lance le processus de déploiement cloud de [Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) pour appliquer les modifications. Vérifiez le statut du déploiement dans le [journal de déploiement](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB Sur site]

Utilisez cette méthode pour installer le [!DNL Catalog Service] pour une instance locale.

1. Utilisez le compositeur pour ajouter le module Service de catalogue à votre projet :

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Mettez à jour les dépendances et installez l’extension :

   ```bash
   composer update  "magento/catalog-service"
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

### Configuration du service et de l&#39;export des données

Après avoir installé le [!DNL Catalog Service], effectuez les tâches suivantes pour intégrer le service de catalogue à votre instance Adobe Commerce. Cette intégration permet la synchronisation des données et la communication entre l’instance Commerce, le service de catalogue et d’autres services d’assistance. La synchronisation des données est gérée par l’extension [Exportation de données SaaS](../data-export/overview.md).

1. Configurez [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) en spécifiant les clés API et en sélectionnant un espace de données SaaS.

   La configuration du connecteur de services Commerce est un processus unique requis pour utiliser les services Adobe Commerce tels que le service de catalogue, la recherche en direct et les recommandations de produits. Si vous avez déjà configuré le connecteur pour un autre service, ignorez cette étape.

1. Effectuez une synchronisation initiale des données à partir du [Tableau de bord de gestion des données](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

   La synchronisation initiale peut prendre de quelques minutes à plusieurs heures selon la taille du catalogue. Vous pouvez surveiller le statut de la synchronisation à partir du tableau de bord de Data Management. Après la synchronisation initiale, le catalogue exporte les données de produit de manière continue pour maintenir les services à jour.

   >[!NOTE]
   >
   >Vous pouvez également démarrer la synchronisation initiale à partir de la ligne de commande à l’aide de l’interface de ligne de commande Commerce. Voir [Synchronisation initiale](../data-export/data-export-cli-commands.md#initial-sync) dans le _Guide d’exportation des données SaaS_.

Pour vous assurer que l’exportation du catalogue s’exécute correctement :

- [Vérifiez que les tâches cron sont en cours d’exécution](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Vérifiez que les indexeurs s’exécutent à partir de l’[Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) ou à l’aide de la `bin/magento indexer:info` de commande de l’interface de ligne de commande Commerce.
- Vérifiez que les indexeurs `Catalog Attributes Feed, Product Feed, Product Overrides Feed` et `Product Variant Feed` sont définis sur `Update by Schedule`.

### Surveillance et dépannage de la synchronisation des données

Dans l’administration Commerce, vous pouvez surveiller le processus de synchronisation à l’aide du tableau de bord [Data Management Dashboard](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Utilisez l’[interface de ligne de commande Commerce](../data-export/data-export-cli-commands.md#troubleshooting) et les journaux pour gérer et résoudre les problèmes liés au processus.

### Accès au service

L’API [!DNL Catalog Service] GraphQL est accessible à partir du point d’entrée ` https://catalog-service.adobe.io/graphql` à l’aide des commandes POST via HTTPS.

Dans vos requêtes GraphQL, vous devez spécifier plusieurs en-têtes HTTP, y compris la clé API publique que vous avez ajoutée à la configuration du connecteur de services Adobe Commerce dans l’administration. Pour plus d’informations, consultez la documentation [Storefront Services GraphQL](https://developer.adobe.com/commerce/services/graphql/).

### Configuration du pare-feu

Pour autoriser le [!DNL Catalog Service] à travers un pare-feu, ajoutez des `commerce.adobe.io` à la liste autorisée.

## Service de catalogue et maillage API

Le [maillage API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permet aux développeurs d’intégrer des API privées ou tierces et d’autres interfaces aux produits Adobe à l’aide d’Adobe IO.

Pour plus d’informations sur l’installation et la configuration[&#128279;](mesh.md) consultez la rubrique [!DNL Catalog Service]  et Maillage API .

## Tableau de bord de gestion des données

Pour plus d’informations sur la synchronisation des données [!DNL Catalog Service], consultez le [Tableau de bord de gestion des données](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).
