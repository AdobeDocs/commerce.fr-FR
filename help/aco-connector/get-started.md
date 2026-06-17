---
title: Prise en main du  [!DNL Adobe Commerce Optimizer Connector]
description: Découvrez comment installer  [!DNL Adobe Commerce Optimizer Connector], configurer les paramètres d’exportation de l’étendue, activer l’authentification IMS et vérifier la synchronisation des catalogues.
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T16:55:50.934Z'
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 1079
ht-degree: 0%

---


# Prise en main

Installez et configurez le [!DNL Adobe Commerce Optimizer Connector] pour synchroniser les données de votre catalogue [!DNL Adobe Commerce] avec [!DNL Adobe Commerce Optimizer], puis surveillez le statut de synchronisation des données pour vous assurer que votre storefront est à jour.

{{aco-integration-environment-alignment}}

## Conditions requises pour utiliser l’intégration {#requirements-to-use-the-integration}

* [!DNL Adobe Commerce] 2.4.7+

   * PHP 8.2, 8.3 ou 8.4
   * Compositeur 2.x

* [!DNL Commerce Optimizer] une licence avec une instance sandbox configurée.

* [Clés d’authentification](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) pour télécharger le métapaquet de connecteur à l’aide du compositeur.

* Accès administrateur à une [[!DNL Commerce Optimizer] instance sandbox](../optimizer/get-started.md).

L’utilisateur [!DNL Adobe Commerce] configurant l’intégration doit disposer des éléments suivants :

* Accès de l’administrateur à l’administrateur Commerce.

* [Accès en ligne de commande au serveur  [!DNL Adobe Commerce] ’applications](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Accès des développeurs à l’organisation [IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations ?) où le projet [!DNL Commerce Optimizer] est configuré.

>[!BEGINSHADEBOX]

## Supprimer les extensions en conflit {#remove-conflicting-extensions}

Si l’une des extensions suivantes est installée, désinstallez-la avant d’installer le [!DNL Adobe Commerce Optimizer Connector] :

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* **[!UICONTROL Data Management Dashboard]** (`magento-catalog-sync-admin`)

Les données associées à ces extensions sont toujours disponibles dans la base de données Commerce. Cependant, il n’est pas exporté vers [!DNL Commerce Optimizer] lorsque le connecteur est activé. Pour implémenter les fonctionnalités de recherche et de merchandising fournies par ces extensions après l’activation du connecteur, configurez-les à partir de l’interface utilisateur d’administration [[!DNL Commerce Optimizer] Admin](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Si ces extensions ne sont pas supprimées avant l’activation du connecteur, vous risquez de voir des écrans de configuration rompus, des données en double dans [!DNL Commerce Optimizer] car les mêmes données sont exportées à partir du connecteur et des extensions existantes, ainsi que des erreurs 401 ou 403 dans les journaux en raison de conflits dans la manière dont les extensions et le connecteur s’authentifient avec les services connectés.

>[!ENDSHADEBOX]

## Étapes de configuration {#configuration-steps}

Pour activer le [!DNL Adobe Commerce Optimizer Connector] et commencer à synchroniser les données de [!DNL Adobe Commerce] vers votre instance [!DNL Commerce Optimizer], procédez comme suit.

1. **[Installez le [!DNL Adobe Commerce Optimizer Connector] package](#install-the-adobe-commerce-optimizer-connector-package)** à l’aide du compositeur pour connecter votre instance [!DNL Adobe Commerce] à [!DNL Commerce Optimizer].

1. **[Personnalisez la configuration d’exportation des portées de Commerce](#customize-the-commerce-scopes-export-configuration)** depuis l’Administration.

1. **[Activez l [!DNL Commerce Optimizer] intégration](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Vérifiez que la synchronisation des données fonctionne](#verify-that-the-data-sync-is-working)**.

## Installation du package [!DNL Adobe Commerce Optimizer Connector] {#install-the-adobe-commerce-optimizer-connector-package}

Le [!DNL Adobe Commerce Optimizer Connector] est fourni en tant que métapaquet Compositeur disponible pour tous les commerçants Commerce disposant d’une licence active pour [!DNL Commerce Optimizer].

### Etapes d&#39;installation

1. Ajoutez le module `adobe-commerce/commerce-data-export-aco-adapter` à l’aide du compositeur :

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Déployez les modifications dans votre environnement d’évaluation [!DNL Adobe Commerce].

   Une fois le déploiement terminé, l’option [!DNL Commerce Optimizer] est disponible dans le menu Commerce Admin . Sélectionnez **[!UICONTROL Commerce Optimizer]** pour ouvrir votre instance [!DNL Commerce Optimizer] directement à partir de l’Administration Commerce.

>[!NOTE]
>
>Pour obtenir des instructions d’installation d’extension détaillées, consultez les guides suivants :
>
>[Installer l’extension sur [!DNL Adobe Commerce] sur une infrastructure cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Installer l’extension sur  [!DNL Adobe Commerce]  site](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Personnalisation de la configuration de l’exportation des étendues de Commerce {#customize-the-commerce-scopes-export-configuration}

Par défaut, la synchronisation des données de catalogue est activée pour toutes les portées de Commerce (sites web, groupes de clients et vues de magasin). Vous pouvez personnaliser les paramètres d’exportation pour synchroniser les données uniquement pour des portées spécifiques en fonction des besoins de votre entreprise. Par exemple, si plusieurs vues de magasin partagent la même langue, vous pouvez choisir d’exporter les données d’une seule vue de magasin et de les utiliser comme [source de catalogue](../optimizer/setup/catalog-sources.md) pour plusieurs vues de catalogue dans [!DNL Commerce Optimizer].

>[!IMPORTANT]
>
>La modification des paramètres d’exportation déclenche une réindexation complète, ce qui peut prendre beaucoup de temps en fonction de la taille de votre catalogue. Adobe recommande de configurer les étendues de Commerce pour qu’elles soient synchronisées avec [!DNL Commerce Optimizer] avant d’activer l’intégration et de démarrer la synchronisation initiale des données.

Le tableau suivant décrit les données exportées à chaque niveau de l’étendue :

| Portée | Données exportées | Remarques |
| ----- | ------------- | ----- |
| Site web et groupe de clients | Prix et registres des prix | Chaque ensemble de prix est exporté sous la forme d’un [catalogue de prix](../optimizer/setup/pricebooks.md) en utilisant la `&lt;website&gt;::&lt;SHA1 of customer group ID&gt;` de convention d’affectation des noms. Tous les groupes de clients du site web sont inclus. |
| Affichage de la boutique | Produits et attributs de produit | Chaque vue de magasin crée une [source de catalogue](../optimizer/setup/catalog-sources.md) distincte dans [!DNL Commerce Optimizer]. |

![Grille de magasin avec paramètres de synchronisation Commerce Optimizer](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

### Pour modifier les paramètres d’exportation de l’étendue

1. Dans Commerce Admin, accédez à **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Sélectionnez le site web ou la vue de magasin que vous souhaitez configurer.

1. Dans les paramètres de l’exportateur de **, cochez la case pour activer ou désactiver la synchronisation des données si nécessaire.**&#x200B;[!DNL Commerce Optimizer]

   ![Mettre à jour la configuration de la synchronisation des données](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. Enregistrez vos modifications.

### Activer et désactiver le comportement

| Action | Résultat |
| -------- | -------- |
| Désactivation d’une vue de magasin | **La désactivation de la synchronisation supprime les données de catalogue de votre storefront.** La source du catalogue reste en [!DNL Commerce Optimizer], mais toutes les données synchronisées sont supprimées lors de la prochaine exécution cron. |
| Désactiver puis réactiver une vue de magasin | La même source de catalogue est renseignée à nouveau avec une resynchronisation complète des données. |

## Activation de l’intégration [!DNL Commerce Optimizer] {#enable-the-adobe-commerce-optimizer-integration}

Activez l’intégration et lancez la synchronisation des données en exécutant la commande de l’interface de ligne de commande `aco:config:init`. Cette commande effectue les étapes suivantes :

1. Obtient un jeton d’accès IMS à l’aide des informations d’identification fournies en tant qu’arguments de ligne de commande.
1. Appelle le service Commerce Cloud Manager (CCM) à l’adresse `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` pour valider le client et extraire l’URL d’ingestion et l’URL [!DNL Commerce Optimizer] Studio.
1. Enregistre toute la configuration (secret client chiffré) dans `core_config_data`.
1. Planifie la synchronisation complète initiale en invalidant tous les indexeurs de flux [!DNL Commerce Optimizer].

>[!IMPORTANT]
>
>Le traitement de la synchronisation des données démarre en arrière-plan dès que vous avez terminé la configuration. Selon la taille de votre catalogue, le processus de synchronisation des données peut prendre de quelques minutes à plusieurs heures.

### Obtenir les détails de connexion requis

À partir de [&#128279;](https://developer.adobe.com/console), créez un projet activé pour le service d’ingestion [!DNL Commerce Optimizer] et générez des informations d’identification de serveur à serveur OAuth. Pour obtenir des instructions détaillées, voir [Obtention des informations d’identification IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) dans le *Guide du développeur du marchandisage*.

Enregistrez les valeurs suivantes à partir de la page des informations d’identification :

* **Identifiant de l’organisation** (`org_id`)
* **Identifiant client** (`client_id`)
* **Secret client** (`client_secret`)

![Obtention des informations d’identification à partir de la page du projet Adobe Developer Console](./assets/developer-console-project-credentials.png){width="500" zoomable="yes"}

### Obtention des détails de l’instance [!DNL Commerce Optimizer]

Récupérez l’_identifiant du client_ à partir du champ _[!DNL Instance Id]_&#x200B;de l’instance [!DNL Commerce Optimizer] [[!DNL Instance details] page](../optimizer/get-started.md#manage-instances) ou à partir de l’URL utilisée pour accéder à l’instance. Par exemple, dans `https://experience.adobe.com/#/@&lt;your organization&gt;/in:&lt;tenant ID&gt;/commerce-optimizer-studio/home`.

1. Dans l’Administration de Commerce, sélectionnez **[!UICONTROL Adobe Commerce Optimizer]** pour afficher la page de configuration avec les instructions.

   ![[!DNL Commerce Optimizer] page de configuration](./assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. À partir de la ligne de commande, [utilisez SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) pour vous connecter à l’environnement d’évaluation [!DNL Adobe Commerce].

1. Exécutez la commande d’interface de ligne de commande [!DNL Adobe Commerce] suivante pour configurer l’intégration et remplacer les valeurs d’espace réservé par les valeurs de votre projet [!DNL Commerce Optimizer] :

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Vérifiez la connexion en revenant à l’administration Commerce et en sélectionnant l’option [!UICONTROL Adobe Commerce Optimizer] .

   Lorsque vous sélectionnez l’option , elle ouvre l’interface utilisateur de [!DNL Commerce Optimizer] dans un nouvel onglet.

## Vérifier que la synchronisation des données fonctionne {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Étapes suivantes

1. **Configurer [!DNL Commerce Optimizer] vues de catalogue et des politiques**

   Créez des vues et des politiques de catalogue dans l’interface utilisateur de [!DNL Commerce Optimizer]. Notez que les tarifs sont créés automatiquement à partir de groupes de clients [!DNL Adobe Commerce]. Pour obtenir des instructions détaillées, reportez-vous à la documentation [Vues de catalogue](../optimizer/setup/catalog-view.md) et [Politiques](../optimizer/setup/policies.md) du Guide de l’utilisateur *[!DNL Commerce Optimizer].*.

1. **Configuration d’un storefront Commerce sur[!DNL Edge Delivery Services]**

   Suivez la [documentation de configuration de Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/){target="_blank"} pour connecter votre storefront à l’instance [!DNL Commerce Optimizer] et commencer à diffuser des expériences commerciales personnalisées.
