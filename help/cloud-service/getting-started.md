---
title: Prise en main de  [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez comment commencer à utiliser  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud, Integration
role: Admin, Developer, User
level: Beginner
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: f71795ab6a10a28e6352d7adfcffd11a40e8ef67
workflow-type: tm+mt
source-wordcount: '1261'
ht-degree: 0%

---

# Prise en main

[!DNL Adobe Commerce as a Cloud Service] fournit la plupart des configurations prêtes à l’emploi. Après avoir terminé quelques processus de configuration de base, votre boutique est opérationnelle en un rien de temps. Ce guide vous guide tout au long de la création et de l’utilisation d’une instance et vous aide à configurer votre organisation pour réussir. Cela permet à vos équipes d’avoir un accès approprié aux [!DNL Adobe Commerce as a Cloud Service] et aux outils dont vous avez besoin pour commencer.

[!DNL Adobe Commerce as a Cloud Service] est une plateforme commerciale native au cloud qui offre flexibilité, évolutivité et efficacité pour la diffusion d’expériences commerciales numériques. Cette offre SaaS est une plateforme entièrement gérée et sans version qui offre une expérience de mise à niveau transparente sans intervention manuelle.

## Composants clés

[!DNL Adobe Commerce as a Cloud Service] comprend les composants suivants :

* **[[!DNL Adobe Experience Cloud]](https://experience.adobe.com/)** : point d’entrée central pour tous les produits [!DNL Adobe Commerce] sur [experience.adobe.com](https://experience.adobe.com/).
   * Cliquez sur [!UICONTROL **Commerce**] sous [!UICONTROL **Accès rapide**] pour ouvrir Commerce Cloud Manager
* **[[!DNL Commerce Cloud Manager]](https://experience.adobe.com/#/commerce/cloud-service)** - Créez et gérez des instances, accédez aux URL d’API et à votre administrateur Commerce
* **[[!DNL Adobe Admin Console]](https://adminconsole.adobe.com/)** - Gestion des utilisateurs et des rôles
* **Administrateur Commerce** - Gérer les produits, les commandes, les clients et la configuration de la boutique
* **[Storefront optimisé par [!DNL Edge Delivery Services]](./storefront.md)** - Créez et personnalisez un storefront orienté client à l’aide d’un système composable et haute performance qui offre une vitesse, un référencement et une expérience utilisateur exceptionnels pour les commerçants et les développeurs
* **[[!DNL Adobe Developer App Builder]](https://developer.adobe.com/app-builder/)** - Créez des intégrations personnalisées à l’aide de [!DNL App Builder], ainsi que d’autres outils d’extensibilité tels que le [ kit de démarrage d’intégration ](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) et [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/)

## Configuration et gestion

Dans le cadre du processus de configuration des [!DNL Adobe Commerce as a Cloud Service], l’administrateur système, les commerçants et les développeurs configurent l’accès et les ressources de votre organisation, y compris l’approvisionnement des ressources cloud et l’affectation des utilisateurs aux rôles appropriés en fonction de leurs responsabilités.

### Workflow d’installation et de gestion

En tant que groupe, l’administrateur système, le commerçant et le développeur doivent suivre les étapes essentielles suivantes pour que votre instance Commerce soit opérationnelle :

1. **Tous les utilisateurs** : [créer une instance](#create-an-instance)
1. **Administrateur système** : [Ajouter des utilisateurs et affecter des rôles](user-management.md#add-users-and-admins)
1. **Commerçants** : [accédez à l’administration Commerce](#access-an-instance) et [importez votre catalogue](#import-your-catalog)
1. **Développeurs** : [Configurez votre storefront](storefront.md) et explorez la [plateforme de développement](overview.md#developer-platform)

#### Workflow des visualisations d’AEM Assets et de produit

Les étapes suivantes sont nécessaires pour intégrer [!DNL Adobe Experience Manager Assets] ou [!DNL Product Visuals powered by AEM Assets] à [!DNL Adobe Commerce as a Cloud Service] :

1. **Administrateur système** : [Ajouter des utilisateurs au profil  [!DNL AEM Assets]  produit et  [!DNL Product Visuals]  produit](user-management.md#add-a-user-to-aem-assets-or-product-visuals)
1. **Développeurs** : [intégrer [!DNL AEM Assets] et [!DNL Product Visuals]](../aem-assets-integration/overview.md)
1. **Commerçants** : [Accédez à votre [!DNL AEM Assets] et [!DNL Product Visuals]](./user-management.md#access-the-experience-manager-interface)

### Tâches de configuration et de gestion basées sur les rôles

Sélectionnez un onglet ci-dessous pour afficher les graphiques de workflow de haut niveau pour le rôle correspondant :

>[!BEGINTABS]

>[!TAB Workflow de l’administrateur système et du commerçant]

Ce diagramme présente de manière générale la manière dont les administrateurs système et les commerçants accèdent aux instances [!DNL Adobe Commerce as a Cloud Service] et les gèrent. Voir le [Guide Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html) pour plus d&#39;informations sur les workflows d&#39;administration.

![Diagramme de workflow de l’administrateur système et du commerçant pour Adobe Commerce as a Cloud Service](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Workflow du développeur]

Ce diagramme présente de manière générale la manière dont les développeurs créent des intégrations pour les [!DNL Adobe Commerce as a Cloud Service] à l’aide d’App Builder. Pour plus d’informations, consultez la [documentation de l’API](https://developer.adobe.com/commerce/webapi/rest/).

![Diagramme de workflow du développeur pour la création d’intégrations avec Adobe Commerce as a Cloud Service](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

Sélectionnez votre rôle pour trouver des ressources afin de commencer votre processus de configuration :

>[!BEGINTABS]

>[!TAB  Administrateur système ]

En tant qu’administrateur système, vous êtes chargé de configurer l’organisation et de gérer l’accès des utilisateurs.

| Tâche | Description | Ressource |
|------|-------------|----------|
| Comprendre la plateforme | En savoir plus sur l’architecture et les avantages d’Adobe Commerce as a Cloud Service | [Aperçu](overview.md) |
| Comparer les fonctionnalités | Comprendre les différences entre Cloud Service et les autres offres Adobe Commerce | [Comparaison des fonctionnalités](feature-comparison.md) |
| Création d’une instance | Configuration des environnements de sandbox et de production | [Créer une instance](#create-an-instance) |
| Configurer User Management | Ajouter des utilisateurs, attribuer des rôles et gérer les autorisations | [Gestion des utilisateurs](user-management.md) |
| Configuration de [!DNL AEM Assets] et [!DNL Product Visuals] (facultatif) | Ajouter des utilisateurs, attribuer des rôles et gérer les autorisations | [Gestion des utilisateurs](user-management.md#add-a-user-to-aem-assets-or-product-visuals) |

>[!TAB Marchand]

En tant que commerçant, vous vous concentrez sur la gestion des produits, des commandes et du contenu du storefront.

| Tâche | Description | Ressource |
|------|-------------|----------|
| Accès à votre instance | Connectez-vous à l’administrateur Commerce pour gérer votre boutique | [Accéder à une instance](#access-an-instance) |
| Explorer les cas d’utilisation | Découvrir les scénarios et les workflows opérationnels pratiques | [Cas d’utilisation](./use-cases.md) |
| Importer le catalogue | Découvrez comment importer vos données de produit dans la plateforme | [Importer votre catalogue](#import-your-catalog) |
| [!DNL AEM Assets] et [!DNL Product Visuals] d’accès (facultatif) | Accédez à Experience Manager pour commencer à utiliser [!DNL AEM Assets] et [!DNL Product Visuals] | [Accéder à l’interface d’Experience Manager](./user-management.md#access-the-experience-manager-interface) |

>[!TAB Développeur]

En tant que développeur, vous devez savoir comment créer des intégrations personnalisées et étendre les fonctionnalités de la plateforme.

| Tâche | Description | Ressource |
|------|-------------|----------|
| Présentation de l’architecture | En savoir plus sur l’extensibilité et les API de la plateforme | [Présentation - Plateforme du développeur](overview.md#developer-platform) |
| Configuration d’un environnement de développement | Créer une instance sandbox pour le développement et les tests | [Créer une instance](#create-an-instance) |
| Créer un storefront | Découvrez comment configurer et personnaliser le storefront Commerce | [Configuration de Storefront](./storefront.md) |
| Configuration de votre storefront | Découvrez comment configurer votre storefront | [Configuration de Storefront](./storefront.md) |
| Explorer les options d’intégration | Découvrez App Builder, le maillage API et d’autres outils d’extensibilité auxquels vous avez accès | [Présentation - Plateforme du développeur](overview.md#developer-platform) |
| Intégrer [!DNL AEM Assets] et [!DNL Product Visuals] (facultatif) | Découvrez comment intégrer [!DNL AEM Assets] et [!DNL Product Visuals] à [!DNL Adobe Commerce] | [Intégration AEM Assets](../aem-assets-integration/overview.md) |

>[!ENDTABS]

### Étapes suivantes

Après avoir effectué les tâches de configuration spécifiques à votre rôle :

* **Administrateurs système** : consultez les instructions relatives à la [responsabilité partagée](shared-responsibility.md)
* **Commerçants** : explorez les [cas d’utilisation](use-cases.md) pour les scénarios d’entreprise courants
* **Développeurs** : consultez la [documentation Adobe Commerce destinée aux développeurs](https://developer.adobe.com/commerce/docs)

## Principes de base d’Adobe Commerce as a Cloud Service

Les sections suivantes décrivent les processus de base à effectuer pour que votre instance Commerce soit opérationnelle.

### Création d’une instance

>[!NOTE]
>
>Avant de pouvoir créer une instance, l’administrateur produit ou l’administrateur système de votre organisation doit vous ajouter en tant qu’utilisateur du produit [!DNL Adobe Commerce as a Cloud Service]. Voir [ Ajout d’utilisateurs et d’administrateurs ](./user-management.md#add-users-and-admins) pour plus d’informations.

[!DNL Adobe Commerce as a Cloud Service] instances utilisent un système basé sur les crédits. Vous pouvez créer plusieurs instances, mais chaque instance nécessite des crédits disponibles. Le nombre de crédits dont vous disposez au départ dépend de votre abonnement.

1. Connectez-vous à votre compte [[!DNL Adobe Experience Cloud]](https://experience.adobe.com/).

1. Sous [!UICONTROL Quick access], cliquez sur [!UICONTROL **Commerce**] pour ouvrir le [!UICONTROL Commerce Cloud Manager].

   La [!UICONTROL Commerce Cloud Manager] affiche une liste des instances de [!DNL Adobe Commerce as a Cloud Service] disponibles dans votre organisation Adobe IMS.

1. Cliquez sur [!UICONTROL **Ajouter une instance**] dans le coin supérieur droit de l’écran.

   ![Bouton Créer une instance et champ de nom d’instance dans Commerce Cloud Manager](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Sélectionnez [!UICONTROL **Commerce as a Cloud Service**].

1. Saisissez un **Nom** et un **Description** pour votre instance.

1. Sélectionnez le [!UICONTROL **type d’environnement**] de votre instance. Vous pouvez choisir entre les options suivantes :

   * [!UICONTROL **Sandbox**] - À des fins de conception et de test uniquement. Commencez votre parcours de [!DNL Adobe Commerce as a Cloud Service] à l’aide de l’environnement Sandbox.

   >[!NOTE]
   >
   > Les instances Sandbox sont uniquement destinées à des fins de conception et de test. Vous ne devez pas utiliser de données de production dans un environnement sandbox.
   >
   >Les instances Sandbox sont limitées à la région Amérique du Nord.

   * [!UICONTROL **Production**] - Pour les magasins en ligne et les sites orientés clients.

   >[!NOTE]
   >
   >L’infrastructure Adobe Commerce as a Cloud Service est disponible dans le monde entier. Pour plus d’informations sur les environnements de production de votre région, contactez votre représentant du service client.

1. Sélectionnez la région dans laquelle vous souhaitez que votre instance soit hébergée.

   >[!NOTE]
   >
   >Une fois votre instance créée, vous ne pourrez plus modifier la région.

1. Cliquez sur [!UICONTROL **Ajouter une instance**].

{{aem-assets-instance-mapping}}

### Accès à une instance

Après avoir créé une instance, vous pouvez y accéder à partir du [!UICONTROL Commerce Cloud Manager] .

1. Connectez-vous à votre compte [Adobe Experience Cloud](https://experience.adobe.com/).

1. Sous [!UICONTROL Quick access], cliquez sur [!UICONTROL **Commerce**] pour ouvrir le [!UICONTROL Commerce Cloud Manager].

   La [!UICONTROL Commerce Cloud Manager] affiche une liste des instances disponibles dans votre organisation Adobe IMS.

1. Pour ouvrir le [!UICONTROL Commerce Admin] d’une instance, cliquez sur son nom.

>[!TIP]
>
>Pour afficher des informations sur votre instance, notamment les points d’entrée REST et GraphQL ainsi que l’URL d’administration, cliquez sur l’icône d’information en regard du nom de l’instance.

Les URL de base de votre administrateur et de vos points d’entrée diffèrent en fonction de la région et de l’environnement, selon le modèle suivant :

* Admin
   * Administrateur de production pour l&#39;Amérique du Nord : `https://na1.admin.commerce.adobe.com`
   * Administrateur sandbox pour l’Amérique du Nord : `https://na1-sandbox.admin.commerce.adobe.com`
   * Administrateur de production pour l&#39;Europe : `https://eu1.admin.commerce.adobe.com`
* REST et GraphQL
   * GraphQL de production nord-américaine : `https://na1.api.commerce.adobe.com`
   * GraphQL Sandbox Amérique du Nord : `https://na1-sandbox.api.commerce.adobe.com`
   * GraphQL de production en Europe : `https://eu1.api.commerce.adobe.com`

### Importer votre catalogue

Par défaut, les instances de [!DNL Adobe Commerce as a Cloud Service] n’incluent aucune donnée de produit. Vous avez la possibilité d’inclure des exemples de données de produit lorsque vous créez une instance à des fins de test et d’apprentissage avant d’importer votre propre catalogue.

Pour importer votre catalogue dans [!DNL Adobe Commerce as a Cloud Service], deux méthodes sont possibles :

* [**Commerce Admin**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) - Une interface conviviale qui vous permet d&#39;importer vos données de catalogue en quelques clics.
* [**Importer l’API JSON**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - Une API REST qui vous permet d’importer les données de votre catalogue par programmation.

### Configurer le storefront

Maintenant que vous avez créé une instance , vous êtes prêt à [configurer votre storefront](storefront.md) optimisé par [!DNL Edge Delivery Services].

## Ressources supplémentaires

* [Notes de mise à jour](release-notes.md)
* [Guide de migration](migration/overview.md)
* [Documentation de Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/)
