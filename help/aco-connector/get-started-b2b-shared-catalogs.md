---
title: Configurer le connecteur pour B2B Commerce
description: Découvrez comment installer le connecteur B2B, sélectionner des portées Commerce, synchroniser les données de catalogue partagées, vérifier les vues de catalogue et surveiller l’intégrité de la projection.
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
last-update: 2026-10-01T00:00:00.000Z
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%
---

# Configurer le connecteur pour B2B Commerce

Les commerçants qui utilisent [!DNL Adobe Commerce] catalogues partagés B2B peuvent utiliser le [!DNL Adobe Commerce Optimizer Connector for B2B] pour synchroniser les données et la configuration de catalogue partagé personnalisé à [!DNL Adobe Commerce Optimizer].

{{aco-integration-environment-alignment}}

## Conditions requises pour utiliser l’intégration {#requirements-to-use-the-integration}

* Adobe Commerce 2.4.8+ avec [Commerce B2B version 1.5.3+](https://experienceleague.adobe.com/fr/docs/commerce-admin/b2b/install) installé et activé.

* Licence [!DNL Commerce Optimizer] avec instance sandbox configurée.

* [Clés d’authentification](https://experienceleague.adobe.com/fr/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) pour télécharger le package de métadonnées de connecteur à l’aide du compositeur.

* Accès administrateur à une [[!DNL Commerce Optimizer] instance sandbox](../optimizer/get-started.md).

L’utilisateur [!DNL Adobe Commerce] configurant l’intégration doit disposer des éléments suivants :

* Accès de l’administrateur à l’administrateur Commerce.

* [Accès en ligne de commande au serveur  [!DNL Adobe Commerce] ’applications](https://experienceleague.adobe.com/fr/docs/commerce-on-cloud/user-guide/project/user-access).

* Accès des développeurs à l’organisation [IMS](https://experienceleague.adobe.com/fr/docs/core-services/interface/administration/organizations ?) où le projet [!DNL Commerce Optimizer] est configuré.

### Exigences relatives à l’application

* Le cron Commerce et les indexeurs fonctionnent normalement.
* Sites web et vues de magasin requis identifiés pour l’exportation.
* Catalogues partagés, affectations d’entreprise, assortiments et tarification B2B configurés ou prêts à être configurés dans Adobe Commerce.

>[!BEGINSHADEBOX]

## Supprimer les extensions en conflit {#remove-conflicting-extensions}

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## Étapes de configuration {#configuration-steps}

Pour activer le [!DNL Adobe Commerce Optimizer Connector for B2B] et commencer à synchroniser la configuration de catalogue partagé personnalisée de [!DNL Adobe Commerce] à votre instance [!DNL Commerce Optimizer], procédez comme suit.

1. **[Installez le [!DNL Adobe Commerce Optimizer Connector for B2B] package](#install-the-adobe-commerce-optimizer-connector-for-B2B-package)** à l’aide du compositeur pour connecter votre instance [!DNL Adobe Commerce] à [!DNL Commerce Optimizer].

1. **[Personnalisez la configuration d’exportation des portées de Commerce](#data-export-and-scope-mapping)** depuis l’Administration.

1. **[Activez l [!DNL Commerce Optimizer] intégration](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Vérifiez que la synchronisation des données fonctionne](#verify-that-the-data-sync-is-working)**.

## Installation du package [!DNL Adobe Commerce Optimizer Connector for B2B] {#install-the-adobe-commerce-optimizer-connector-for-B2B-package}

Le [!DNL Adobe Commerce Optimizer Connector for B2B] est fourni sous la forme d’un méta-package Compositeur disponible pour tous les commerçants Commerce disposant d’une licence active pour [!DNL Commerce Optimizer].

### Etapes d&#39;installation

1. Ajoutez le module `adobe-commerce/commerce-data-export-aco-adapter-b2b` à l’aide du compositeur :

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter-b2b
   ```

1. Déployez les modifications dans votre environnement d’évaluation [!DNL Adobe Commerce].

   Une fois le déploiement terminé, l’option [!DNL Commerce Optimizer] est disponible dans le menu Commerce Admin . Sélectionnez **[!UICONTROL Commerce Optimizer]** pour ouvrir votre instance [!DNL Commerce Optimizer] directement à partir de l’Administration Commerce.

{{install-extension-links}}

### Exportation des données et mappage de la portée

Sélectionnez les sites web et les vues de magasin à synchroniser, puis vérifiez les flux initiaux. Pour B2B, le connecteur utilise les portées activées lorsqu’il projette des données de catalogue partagées vers [!DNL Commerce Optimizer].

* **Vue de magasin** source → catalogue avec contenu de produit localisé.
* **Site Web et groupe de clients** → catalogue des prix pour le site Web et le groupe de clients
* **Catalogue partagé** → vue de catalogue privé protégée et politique appliquée

Le catalogue partagé définit l’assortiment de produits et chaque vue de magasin activée fournit la source de catalogue localisée. Le site web et le groupe de clients déterminent le catalogue des prix applicable. Le connecteur projette chaque catalogue partagé personnalisé pour chaque vue de magasin activée. Vous n’avez donc pas besoin d’un paramètre de portée distinct pour la projection B2B.

Un catalogue partagé personnalisé peut générer plusieurs vues de catalogue privé protégées, une pour chaque vue de magasin activée. Le catalogue public partagé par défaut n’est pas projeté en tant qu’affichage de catalogue privé B2B. Pour le mappage d’objet détaillé et le flux d’autorisation d’exécution, consultez [projection du catalogue partagé B2B](b2b-shared-catalog-projection.md).

>[!IMPORTANT]
>
>La modification des paramètres d’exportation déclenche une réindexation complète, ce qui peut prendre beaucoup de temps en fonction de la taille de votre catalogue. Configurez les portées de Commerce avant d’activer l’intégration et de démarrer la synchronisation initiale des données.

### Pour modifier les paramètres d’exportation de l’étendue

1. Dans Commerce Admin, accédez à **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Sélectionnez le site web ou la vue de magasin que vous souhaitez configurer.

1. Dans les paramètres de l’exportateur de **, cochez la case pour activer ou désactiver la synchronisation des données si nécessaire.**&#x200B;[!DNL Commerce Optimizer]

   ![Mettre à jour la configuration de la synchronisation des données](./assets/aco-connector-b2b-storeview-list.png){width="500" zoomable="yes"}

1. Enregistrez vos modifications.

### Activer et désactiver le comportement

| Action | Résultat |
| -------- | -------- |
| Désactivation d’une vue de magasin | **La désactivation de la synchronisation supprime les données de catalogue de votre storefront B2B.** La source du catalogue reste en [!DNL Adobe Commerce Optimizer], mais toutes les données synchronisées sont supprimées lors de la prochaine exécution cron. |
| Désactiver puis réactiver une vue de magasin | La même source de catalogue est renseignée à nouveau avec une resynchronisation complète des données. |

### Surveillance des modifications du catalogue partagé B2B

Le connecteur surveille les modifications apportées aux catalogues partagés et aux affectations d’entreprise. Lorsque vous supprimez un catalogue partagé dans l’administration Commerce, le connecteur supprime l’accès à sa vue de catalogue privée après une période de grâce configurable.

>[!NOTE]
>
>La période de grâce de suppression est de sept jours par défaut. Vous pouvez le modifier en mettant à jour la configuration des paramètres de synchronisation des vues du catalogue. Voir [configuration du statut de synchronisation des vues du catalogue](catalog-view-sync-status.md#configure-aco-catalog-view-sync-settings).

## Activation de l’intégration [!DNL Commerce Optimizer] {#enable-the-adobe-commerce-optimizer-integration}

Activez l’intégration et lancez la synchronisation des données en exécutant la commande de l’interface de ligne de commande `aco:config:init`. Cette commande effectue les étapes suivantes :

1. Obtient un jeton d’accès IMS à l’aide des informations d’identification fournies en tant qu’arguments de ligne de commande.
1. Appelle le service Commerce Cloud Manager (CCM) à l’adresse `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` pour valider le client et extraire l’URL d’ingestion et l’URL [!DNL Commerce Optimizer] Studio.
1. Enregistre toute la configuration (secret client chiffré) dans `core_config_data`.
1. Planifie la synchronisation complète initiale en invalidant tous les indexeurs de flux [!DNL Commerce Optimizer].

{{aco-data-sync-processing-note}}

## Obtenir les détails de connexion requis

{{$include /help/_includes/aco-connector/connection-details.md}}

### Obtention des détails de l’instance [!DNL Commerce Optimizer]

{{$include /help/_includes/aco-connector/configure-connection.md}}

## Vérifier que la synchronisation des données fonctionne {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Étapes suivantes

1. **Surveiller la projection de la vue du catalogue B2B**

Après la synchronisation initiale du flux, utilisez [Statut de la synchronisation des vues du catalogue](catalog-view-sync-status.md) pour vérifier les vues de catalogue privées prévues, les politiques, les références au catalogue des prix et la configuration des clés d’accès restreint. Pour le modèle de projection et le flux d’autorisation d’exécution, consultez [projection du catalogue partagé B2B](b2b-shared-catalog-projection.md).

1. **Configuration d’un storefront Commerce sur[!DNL Edge Delivery Services]**

   Pour connecter votre storefront à l’instance [!DNL Commerce Optimizer] et commencer à diffuser des expériences commerciales personnalisées, suivez la [documentation sur la configuration de Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}.
