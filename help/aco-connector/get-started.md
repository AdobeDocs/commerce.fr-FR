---
title: Prise en main du connecteur Adobe Commerce Optimizer
description: Découvrez comment installer et configurer le connecteur, personnaliser la configuration de l’exportation, vous connecter à Adobe Commerce Optimizer et surveiller le statut de synchronisation des données.
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 79a422b1de81b33c68078af5c082e84d3dfe5bec
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---


# Prise en main

Installez et configurez le connecteur Commerce Optimizer pour synchroniser les données de votre catalogue Adobe Commerce avec [!DNL Adobe Commerce Optimizer], puis surveillez le statut de synchronisation des données pour vous assurer que votre storefront est à jour.

## Conditions requises pour utiliser l’intégration

* Adobe Commerce 2.4.7+

   * PHP 8.2, 8.3 ou 8.4
   * Compositeur 2.x

* [!DNL Adobe Commerce Optimizer] une licence avec une instance sandbox configurée.

* Accès à [repo.magento.com](https://repo.magento.com) pour télécharger le métapaquet du connecteur Commerce à l’aide du compositeur.

* Accès administrateur à une instance sandbox Adobe Commerce Optimizer [&#128279;](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

L’utilisateur d’Adobe Commerce configurant l’intégration doit disposer des éléments suivants :

* Accès des administrateurs à l’administration Adobe Commerce.

* [Accès en ligne de commande au serveur applicatif Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Accès des développeurs à l’organisation [IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) où le projet [!DNL Adobe Commerce Optimizer] est configuré.

>[!BEGINSHADEBOX]

## Conditions préalables

Si l’une des extensions suivantes est installée, désinstallez-la avant d’installer le connecteur Commerce Optimizer :

* Adobe Commerce Live Search (`magento/live-search`)
* Recommandations de produits Adobe Commerce (`magento/product-recommendations`)
* Service de catalogue Adobe Commerce (`magento/catalog-service`, `magento/catalog-service-installer`)
* Tableau de bord de gestion des données (`magento-catalog-sync-admin`)

Les données associées à ces extensions sont toujours disponibles dans la base de données Commerce. Toutefois, il n’est pas exporté vers [!DNL Adobe Commerce Optimizer] lorsque le connecteur est activé. Pour implémenter les fonctionnalités de recherche et de merchandising fournies par ces extensions après l’activation du connecteur, configurez-les à partir de l’interface utilisateur d’administration [[!DNL Adobe Commerce Optimizer] Admin](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!ENDSHADEBOX]

## Étapes de configuration

1. **Configurer l’intégration**

   1. **[Installez le package Connecteur Commerce Optimizer](#install-the-commerce-connector-package)** à l’aide du compositeur pour connecter votre instance Commerce à [!DNL Adobe Commerce Optimizer].

   1. **[Examinez et personnalisez la configuration de l’exportation des données](#customize-commerce-data-export-configuration)** à partir de l’Administration.

   1. **[Obtenez les informations d’identification d’API requises pour établir la connexion entre Commerce et Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)**.

   1. **[Activez l [!DNL Adobe Commerce Optimizer] intégration](#enable-the-adobe-commerce-optimizer-integration)**.

   1. **[Vérifiez que la synchronisation des données fonctionne](#verify-that-the-data-sync-is-working)**.


## Installation du package Connecteur Commerce Optimizer

Le connecteur Adobe Commerce Optimizer est fourni en tant que métapaquet Compositeur disponible pour tous les commerçants Commerce disposant d’une licence active pour [!DNL Adobe Commerce Optimizer].

### Etapes d&#39;installation

1. Ajoutez le module `adobe-commerce/commerce-data-export-aco-adapter` à l’aide du compositeur :

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Déployez les modifications dans votre environnement d’évaluation Adobe Commerce.

Une fois le déploiement terminé, l’option Commerce Optimizer est disponible dans le menu Commerce Admin . Cliquez sur **[!UICONTROL Commerce Optimizer]** pour ouvrir votre instance Commerce Optimizer directement depuis Commerce Admin.

>[!NOTE]
>
>Pour obtenir des instructions d’installation d’extension détaillées, consultez les guides suivants :
>
>[Installation de l’extension sur Adobe Commerce sur une infrastructure cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Installation de l’extension sur Adobe Commerce On-premise](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

### Obtenir les détails de connexion requis

Dans Adobe Developer Console, créez un projet de développement activé pour le service d’ingestion [!DNL Adobe Commerce Optimizer] et générez des informations d’identification OAuth de serveur à serveur. Pour obtenir des instructions détaillées, voir [Obtention des informations d’identification IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) dans le *Guide du développeur du marchandisage*.

>[!TIP]
>
>Si vous avez déjà configuré un projet de développement avec l’API Data Ingestion dans la même organisation IMS que votre instance Commerce Optimizer, vous pouvez réutiliser les informations d’identification de serveur à serveur OAuth existantes.

Enregistrez les valeurs suivantes à partir de la page des informations d’identification :

* **Identifiant de l’organisation** (`org_id`)
* **Identifiant client** (`client_id`)
* **Secret client** (`client_secret`)

### Obtention des détails de l’instance [!DNL Adobe Commerce Optimizer]

Enregistrez l’ID d’instance (également appelé ID client) à partir de votre instance [!DNL Adobe Commerce Optimizer]. Elle se trouve dans l’URL d’accès à l’instance. Par exemple, dans `https://experience.adobe.com/#/@<project-id>/in:TToyu73daQRn66KAYaq8YZ/commerce-optimizer-studio/home`, l’ID d’instance est `TToyu73daQRn66KAYaq8YZ`.

## Personnaliser la configuration de l’exportation des données de Commerce

Par défaut, la synchronisation des données de catalogue est activée pour toutes les portées de Commerce (sites web et vues de magasin). Vous pouvez personnaliser les paramètres d’exportation pour synchroniser les données uniquement pour des portées spécifiques en fonction des besoins de votre entreprise. Par exemple, si vous disposez de plusieurs vues de magasin, mais que vous souhaitez exporter les données de l’une d’elles uniquement, vous pouvez désactiver l’exportateur des autres vues de magasin.

>[!IMPORTANT]
>
>La modification des paramètres d’exportation déclenche une réindexation complète, ce qui peut prendre beaucoup de temps en fonction de la taille de votre catalogue. Planifiez ces modifications pendant les périodes de faible trafic afin de minimiser l’impact sur les performances.

### Exportation des données par portée

Le tableau suivant décrit les données exportées à chaque niveau de l’étendue :

| Portée | Données exportées | Remarques |
| ------- | --------------- | ------- |
| Site internet | Prix et registres des prix | Chaque ensemble de prix est exporté sous la forme d’un [catalogue de prix](../optimizer/setup/pricebooks.md) en utilisant la `website::customergroupcode` de convention d’affectation des noms. Tous les groupes de clients du site web sont inclus. |
| Affichage de la boutique | Produits et attributs de produit | Chaque vue de magasin crée une source de catalogue distincte dans [!DNL Adobe Commerce Optimizer]. |

### Activer et désactiver le comportement

| Action | Résultat |
| -------- | -------- |
| Désactivation d’une vue de magasin | La source du catalogue reste en [!DNL Adobe Commerce Optimizer], mais toutes les données sont supprimées. |
| Désactiver puis réactiver une vue de magasin | La même source de catalogue est renseignée à nouveau avec une resynchronisation complète des données. |

### Mise à jour de la configuration de l’exportation

Après avoir installé le package Connecteur, la grille de magasin dans l’Administration affiche désormais les paramètres de configuration de l’exportation pour Commerce Optimizer.

![Grille de magasin avec paramètres de synchronisation Commerce Optimizer](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**Pour modifier les paramètres d’une vue de site web ou de boutique :**

1. Dans Commerce Admin, accédez à **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**.

1. Sélectionnez le site web ou la vue de magasin que vous souhaitez configurer.

1. Dans les paramètres de l’exportateur de **[!DNL Adobe Commerce Optimizer]**, cochez la case pour activer ou désactiver la synchronisation des données si nécessaire.

   ![Mettre à jour la configuration de la synchronisation des données](./assets/aco-connector-store-website-export-settings.png){width="500" zoomable="yes"}

1. Enregistrez vos modifications.

## Activation de l’intégration [!DNL Adobe Commerce Optimizer]

>[!IMPORTANT]
>
>Le traitement de la synchronisation des données démarre dès que vous exécutez la commande de configuration. Par défaut, la synchronisation des données de catalogue est activée pour toutes les portées de Commerce (sites web et vues de magasin). Selon la taille de votre catalogue, le processus de synchronisation des données peut prendre de quelques minutes à plusieurs heures.

À l’aide des informations d’identification d’API et des détails d’instance que vous avez rassemblés lors des étapes précédentes, vous pouvez maintenant configurer l’intégration entre vos instances Commerce et [!DNL Adobe Commerce Optimizer].

1. Dans l’Administration de Commerce, sélectionnez **[!UICONTROL Adobe Commerce Optimizer]** pour afficher la page de configuration avec les instructions.

   ![[!DNL Adobe Commerce Optimizer] page de configuration](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. À partir de la ligne de commande, [utilisez SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) pour vous connecter à l’environnement d’évaluation Commerce.

1. Exécutez la commande de l’interface de ligne de commande Commerce suivante pour configurer l’intégration et remplacer les valeurs d’espace réservé par les valeurs de votre projet Commerce Optimizer :

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. Vérifiez la connexion en revenant à l’administration Commerce et en sélectionnant l’option [!UICONTROL Adobe Commerce Optimizer] .

   Lorsque vous cliquez sur l’option , elle ouvre l’interface utilisateur de [!DNL Adobe Commerce Optimizer] dans un nouvel onglet.

## Vérifier que la synchronisation des données fonctionne

Une fois l’intégration activée, la synchronisation des données commence automatiquement. Selon la taille du catalogue, la synchronisation initiale peut prendre de quelques minutes à plusieurs heures.

1. **Vérification du statut de synchronisation dans l’administration Commerce :**

   Accédez à **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**.

   ![Page État de synchronisation des flux de données avec rapport sur l’état des éléments de flux](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   Lorsque la synchronisation est en cours, les données de flux affichent les enregistrements envoyés avec succès. Sélectionnez un flux pour afficher les détails ou résoudre les problèmes de synchronisation.

1. **Les données de confirmation sont arrivées dans Commerce Optimizer :**

   Dans le menu [!DNL Adobe Commerce Optimizer], sélectionnez **[!UICONTROL Data Sync]**.

   ![Synchronisation des données](./assets/data-sync.png){width="500" zoomable="yes"}

   Vérifiez que les produits, prix et attributs attendus s’affichent.

>[!TIP]
>
>Si vous rencontrez des problèmes avec la synchronisation des données, reportez-vous à la section [Dépannage](/help/data-export/troubleshooting-logging.md) de la documentation *Exportation de données SaaS*.

## Étapes suivantes

1. **[Configurer [!DNL Adobe Commerce Optimizer] les vues de catalogue et les politiques](#configure-adobe-commerce-optimizer-stores)**

   Créer des vues de catalogue et des politiques dans le guide de [!DNL Adobe Commerce Optimizer]. Notez que les tarifs sont créés automatiquement à partir des groupes de clients Adobe Commerce.

1. **[Configuration d’un storefront Commerce sur Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

   Suivez la [documentation de configuration de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/) pour connecter votre storefront à l’instance [!DNL Adobe Commerce Optimizer] et commencer à diffuser des expériences commerciales personnalisées.


