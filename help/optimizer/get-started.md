---
title: Prise en main
description: Découvrez comment commencer à utiliser  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Prise en main

Cet article vous explique comment vous familiariser avec [!DNL Adobe Commerce Optimizer]. Bien que ce guide se concentre sur les rôles de marchandiseur et d’administrateur, il inclut toutefois de brèves tâches générales qu’un développeur pourrait effectuer. Voir la [documentation pour les développeurs](https://developer-stage.adobe.com/commerce/services/composable-catalog/) pour obtenir un contenu détaillé spécifique au développeur.

## Quel est votre rôle ?

La configuration réussie d’[!DNL Adobe Commerce Optimizer] implique généralement les membres d’équipe suivants :

- Administrateur
- Développeur
- Marchandiseur

Chaque membre de l’équipe possède son propre ensemble de rôles et de responsabilités, comme décrit dans le tableau suivant :

| Rôle(s) | Tâche |
|---|---|
| Administrateur | Utilisez Admin Console pour créer des administrateurs, des groupes d’utilisateurs, des utilisateurs et des développeurs&#x200B;. |
|  | Créez une instance [!DNL Adobe Commerce Optimizer] dans Commerce Cloud Manager&#x200B; |
|  | Configurez vos politiques et vues de catalogue. |
| Développeur | Utilisez Developer Console pour créer un projet, accorder aux développeurs l’accès à l’API et installer les applications et personnalisations requises. |
|  | Connectez-vous à votre système de back-office (panier, passage en caisse) à l’aide du maillage API et d’App Builder&#x200B;. |
|  | Ingérez les données du catalogue à partir de vos solutions de commerce existantes à l’aide de l’API Merchandising Services Data Ingestion&#x200B; |
|  | Configurer votre storefront |
| Marchandiseur | Configurer la découverte de produits&#x200B;. |
|  | Configurez les recommandations de produits. |

Chaque rôle fait partie intégrante de l’intégration et du lancement réussis de votre environnement de [!DNL Adobe Commerce Optimizer]. Le diagramme suivant montre un workflow de début à fin général pour chaque rôle de votre organisation :

![Workflow de haut niveau](./assets/high-level-workflow.png){zoomable="yes"}

### Administrateur

Les administrateurs sont chargés de configurer les instances, de gérer les utilisateurs, les groupes et les droits de votre organisation.

- **[Accéder à Adobe Admin Console](https://helpx.adobe.com/fr/enterprise/admin-guide.html)** - Gérez les droits Adobe dans l’ensemble de votre organisation. Voir [gestion des utilisateurs](./user-management.md) pour savoir comment vous, l’administrateur produit de votre entreprise ou l’administrateur système pouvez ajouter des utilisateurs au produit [!DNL Adobe Commerce Optimizer].

- **Créer une instance** - [!DNL Adobe Commerce Optimizer] instances utilisent un système basé sur les crédits. Vous pouvez créer plusieurs instances Sandbox et de Production, chaque instance nécessitant un crédit correspondant. Le montant des crédits dont vous disposez au départ dépend de votre abonnement. [En savoir plus](#create-an-instance).

- **Accéder à une instance** - Après avoir créé une instance, vous pouvez y accéder à partir du [!UICONTROL Commerce Cloud Manager]. [En savoir plus](#access-an-instance).

- **Configurer des vues et des politiques de catalogue** - Découvrez comment [définir vos vues et politiques de catalogue](./setup/catalog-view.md). Le catalogue contient non seulement vos données de produit, mais il vous aide également à définir la structure de votre entreprise.

### Développeur

L’équipe de développement crée des projets et des informations d’identification, installe des extensions, ingère des données de catalogue et effectue des tâches générales d’architecture de Platform. Voir la [documentation pour les développeurs](https://developer-stage.adobe.com/commerce/services/composable-catalog/) pour obtenir un contenu détaillé spécifique au développeur.

- **Accéder à Developer Console** - Accédez au [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) pour créer un projet à [!DNL Adobe Commerce Optimizer], générer des jetons d’accès et installer les applications et personnalisations requises.

- **Ingérer des données de catalogue** - Consultez la documentation de l’[API d’ingestion de données](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) pour savoir comment importer des données de catalogue dans [!DNL Adobe Commerce Optimizer].

  Les données de catalogue ingérées sont visibles dans la page [synchronisation des données](./setup/data-sync.md).

- **Configuration du storefront** - Avant de configurer le storefront, vous devez d’abord créer une instance , qui est une tâche généralement effectuée par l’[administrateur](#administrator) de votre organisation. Une fois votre instance créée, vous êtes prêt à poursuivre la [configuration](./storefront.md) de votre storefront Commerce optimisé par Edge Delivery Services.

### Marchandiseur

Le marchandiseur utilise les données et les analyses des acheteurs pour prendre des décisions stratégiques sur le placement, les prix et les promotions des produits sur le storefront, tout en optimisant les expériences d’achat grâce à la découverte et aux recommandations de produits.

- **Configurer la découverte de produits et les recommandations** - Découvrez comment [créer des expériences personnalisées](./merchandising/overview.md) pour vos acheteurs grâce à la découverte de produits et aux recommandations.

## Création d’une instance

1. Connectez-vous à votre compte [Adobe Experience Cloud](https://experience.adobe.com/).

1. Sous [!UICONTROL Quick access], cliquez sur [!UICONTROL **Commerce**] pour ouvrir le [!UICONTROL Commerce Cloud Manager].

   La [!UICONTROL Commerce Cloud Manager] affiche une liste des instances [!DNL Adobe Commerce] disponibles dans votre organisation Adobe IMS, y compris les deux instances configurées pour [!DNL Adobe Commerce Optimizer] et [!DNL Adobe Commerce as a Cloud Service].

1. Cliquez sur [!UICONTROL **Ajouter une instance**] dans le coin supérieur droit de l’écran.

   ![Créer une instance](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. Sélectionnez [!UICONTROL **Commerce Optimizer**].

1. Saisissez un **Nom** et un **Description** pour votre instance.

1. Sélectionnez la région dans laquelle vous souhaitez que votre instance soit hébergée.

   >[!NOTE]
   >
   >Après avoir créé une instance, vous ne pouvez pas modifier la région.

1. Sélectionnez l’un des [!UICONTROL **type d’environnement**] suivants pour votre instance :

   - [!UICONTROL **Sandbox**] - Idéal pour la conception et les tests. Commencez votre parcours de [!DNL Adobe Commerce Optimizer] à l’aide de l’environnement Sandbox.
   - [!UICONTROL **Production**] - Pour les magasins en ligne et les sites orientés clients.

   >[!NOTE]
   >
   >Les instances Sandbox sont actuellement limitées à la région Amérique du Nord.

1. Cliquez sur [!UICONTROL **Ajouter une instance**].

   La nouvelle instance est désormais disponible dans Cloud Manager.

1. Pour afficher les détails de l’instance, notamment les points d’entrée GraphQL et Catalog Service, l’URL d’accès à l’application Adobe Commerce Optimizer et l’ID d’instance (ID de client), cliquez sur l’icône d’information en regard du nom de l’instance.

   ![Créer une instance](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## Accès à une instance

1. Connectez-vous à votre compte [Adobe Experience Cloud](https://experience.adobe.com/).

1. Sous [!UICONTROL Quick access], cliquez sur [!UICONTROL **Commerce**] pour ouvrir le [!UICONTROL Commerce Cloud Manager].

   La [!UICONTROL Commerce Cloud Manager] affiche une liste des instances disponibles dans votre organisation Adobe IMS.

1. Pour ouvrir l’application [!UICONTROL Commerce Optimizer] associée à une instance, cliquez sur le nom de l’instance.


