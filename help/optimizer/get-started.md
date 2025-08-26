---
title: Prise en main
description: Découvrez comment commencer à utiliser  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: 89099811cd04b92a56fd3c1bda98c586e988f878
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 0%

---

# Prise en main

Ce guide vous guide tout au long de la configuration de [!DNL Adobe Commerce Optimizer], du début à la fin. Bien que ce guide couvre tous les rôles, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/) pour obtenir du contenu détaillé spécifique aux développeurs.

## Conditions préalables

Avant de commencer, vérifiez que vous disposez des éléments suivants :

- Compte **Adobe Experience Cloud** avec droits [!DNL Adobe Commerce Optimizer]
- **Accès administrateur de l’organisation** pour créer des instances et gérer les utilisateurs
- **Compte GitHub** pour le chargement de données d’exemple et le développement du storefront
- **Compréhension de base** des concepts du commerce électronique

## Guide de démarrage rapide

Pour que votre environnement [!DNL Adobe Commerce Optimizer] fonctionne, procédez comme suit :

### Étape 1. Création d’une instance

1. Connectez-vous à [Adobe Experience Cloud](https://experience.adobe.com/).
1. Accédez à **Commerce** > **Commerce Cloud Manager**.
1. Cliquez sur **Ajouter une instance** > **Commerce Optimizer**.

   ![Créer une instance](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Configurez les paramètres des instances :
   - **Nom de l’instance** : nom explicite (par exemple, « Mon entreprise - Sandbox »)
   - **Description** : brève description de l’objectif
   - **Type d’environnement** : commencez par un environnement **Sandbox** pour les tests
   - **Région** : sélectionnez la région de votre choix

1. Cliquez sur **Ajouter une instance**.

   Le Cloud Manager se met à jour pour inclure votre nouvelle instance. Pour plus d’informations sur son accès et sa gestion, voir [Gestion d’une instance](#manage-instances).

>[!NOTE]
>
>Vous ne pouvez créer des environnements Sandbox qu’en Amérique du Nord. Une fois une instance créée, vous ne pouvez pas modifier la région.

### Étape 2. Configuration de votre environnement

Après avoir créé votre instance :

1. [Gérez votre instance](#manage-instances) à partir de Commerce Cloud Manager.
1. Configurez l’accès des utilisateurs et utilisatrices à l’aide du [ guide de gestion des utilisateurs ](./user-management.md).

### Étape 3. Ajouter des données d’exemple (facultatif)

Pour les tests et l’apprentissage, suivez les instructions [Charger des données d’exemple](#add-sample-data).

## Workflows basés sur les rôles

La configuration et la gestion des [!DNL Adobe Commerce Optimizer] reposent sur trois rôles clés. Chaque rôle comporte des tâches et des responsabilités spécifiques :

![Workflow de haut niveau](./assets/high-level-workflow.png){zoomable="yes"}

### Tâches de l’administrateur

Les administrateurs gèrent les instances, les utilisateurs et les paramètres organisationnels.

| Tâche | Description | Lien |
|---|---|---|
| **Gérer les utilisateurs** | Ajouter des utilisateurs, des développeurs et des administrateurs | [Gestion des utilisateurs](./user-management.md) |
| **Créer des instances** | Configurer des environnements de sandbox et de production | [Créer une instance](#create-an-instance) |
| **Gérer les instances** | Vérifiez le statut, mettez à jour le nom et la description de l’instance et obtenez les URL clés pour l’accès aux applications et aux API | [Gérer les instances](#manage-instances) |
| **Configurer l’accès** | Configurer des vues et des politiques de catalogue | [Vues du catalogue](./setup/catalog-view.md) |

### Tâches du développeur

Les développeurs gèrent l’implémentation technique et l’intégration des données, y compris les tâches d’architecture de plateforme.

| Tâche | Description | Lien |
|---|---|---|
| **Accéder à Developer Console** | Créer des projets et générer des informations d’identification | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Ingérer des données de catalogue** | Importer les données de produit des systèmes existants | [API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) |
| **Configuration du storefront** | Configuration du storefront Edge Delivery Services | [Configuration de Storefront](./storefront.md) |

### Tâches du marchandiseur

Les marchandiseurs optimisent et personnalisent l’expérience d’achat par le biais de la découverte et des recommandations de produits. Elles utilisent également les données et les analyses des acheteurs pour prendre des décisions stratégiques concernant le placement, les prix et les promotions des produits sur le storefront.

| Tâche | Description | Lien |
|---|---|---|
| **Découverte de produits** | Configuration de la recherche et du filtrage | [Présentation du marchandisage](./merchandising/overview.md) |
| **Recommandations** | Configurer des recommandations de produits optimisées par l’IA | [Recommandations de produits](./merchandising/recommendations/overview.md) |
| **Suivi des performances** | Surveiller les mesures de succès | [Mesures de succès](./manage-results/success-metrics.md) |

## Gestion des instances

Gérez les instances à partir du gestionnaire Commerce Cloud.

>[!NOTE]
>
>Tous les utilisateurs de Adobe Commerce Optimizer n’ont pas accès à Cloud Manager. L’accès dépend du rôle et des autorisations attribués au compte d’utilisateur.

1. Connectez-vous à [Adobe Experience Cloud](https://experience.adobe.com/).

1. Ouvrez Commerce Cloud Manager :

   - Sous **Accès rapide**, cliquez sur **Commerce**.
   - Affichez les instances disponibles.

### Rechercher et filtrer des instances

Après vous être connecté, le tableau de bord affiche toutes les instances de produit Commerce disponibles dans l’organisation.
La colonne Produit indique pour quelle application Commerce l’instance est configurée.

![Recherche et filtrage d’instances](./assets/search-filter-instances.png){zoomable="yes"}

Utilisez les outils de filtrage et de recherche pour rechercher rapidement des instances spécifiques par date de création, région, créateur, type de produit, environnement ou statut.

### Accès à l’application [!DNL Adobe Commerce Optimizer]

Une fois l’application ouverte, basculez facilement entre des environnements tels que le sandbox et la production pour afficher les données et les paramètres de chacun sans revenir au gestionnaire Commerce Cloud.

1. Dans Commerce Cloud Manager, cliquez sur le nom de l’instance pour ouvrir l’application [!DNL Adobe Commerce Optimizer].

1. Basculez entre les instances [!DNL Adobe Commerce Optimizer] sans quitter l’application.

   La liste déroulante Instance répertorie toutes les instances d’Optimizer disponibles dans l’organisation. Sélectionnez l’instance à afficher.

   ![Sélecteur d’instances](./assets/context-switcher.png){zoomable="yes"}

### Obtenir les détails de l’instance

Affichez les détails de l’instance en cliquant sur l’icône d’information en regard de son nom.

![Détails de l’instance](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

Notez les informations clés suivantes :

- Point d’entrée **GraphQL** pour récupérer les données du catalogue Commerce à l’aide de l’API de marchandisage.
- **Point d’entrée du service de catalogue** pour l’ingestion de données à l’aide de l’API REST
- **URL Commerce Optimizer** pour accéder à l&#39;application [!DNL Adobe Commerce Optimizer]
- **ID de l’instance** identifiant client unique qui identifie l’instance

Si vous êtes développeur, vous avez besoin de ces informations pour configurer votre environnement de développement et vous connecter aux API [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Pour accéder aux détails de l’instance, vous devez disposer des autorisations nécessaires dans votre organisation Adobe IMS. Si les détails de l’instance ne s’affichent pas ou si vous ne pouvez pas accéder à l’application, contactez l’administrateur ou l’administratrice de votre organisation.

### Modifier le nom et la description de l’instance

Mettez à jour le nom et la description de l’instance si nécessaire.

1. Cliquez sur l’icône **Modifier** en regard d’un nom d’instance.
1. Mettez à jour le **nom de l’instance** et le **description** selon les besoins.
1. Cliquez sur **Enregistrer**.

## Ajout de données d’exemple

Adobe fournit un référentiel GitHub avec des exemples de données et d’outils pour vous aider à apprendre et à tester les fonctionnalités de [!DNL Adobe Commerce Optimizer].
Les données d’exemple sont basées sur le [scénario commercial Carvelo](./use-case/admin-use-case.md) et incluent :

- Catalogue de produits avec pièces automobiles
- Plusieurs tarifs et scénarios de tarification
- Vues et stratégies de catalogue pour différents revendeurs
- Exemples complets de workflows de bout en bout

**Chargez les exemples de données :**

1. Accédez au référentiel GitHub [ingestion de données de catalogue d’exemples](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion).

1. Suivez les instructions de configuration du fichier LISEZ-MOI du référentiel pour effectuer les tâches suivantes :

   - Configuration de votre environnement
   - Terminer le processus d’ingestion des données
   - Créer des vues de catalogue et des politiques à l’aide des données d’exemple
   - Vérifiez l’ingestion des données en vérifiant les données du service de catalogue sur la page [ Synchronisation des données ](./setup/data-sync.md)

## Étapes suivantes

Une fois la configuration terminée :

1. Configurez votre storefront :
   - Configurer le storefront [Edge Delivery Services](./storefront.md)
   - Connexion aux données de votre catalogue

1. Explorez le cas d’utilisation de Carvelo :
   - Suivez le [workflow de bout en bout](./use-case/admin-use-case.md)
   - Pratique avec des scénarios réels

1. Configurez le marchandisage :
   - Configurer [découverte de produits](./merchandising/overview.md)
   - Créer des [recommandations](./merchandising/recommendations/overview.md)

1. Surveillance des performances :
   - Suivi [mesures de succès](./manage-results/success-metrics.md)
   - Analyse [performances de recherche](./manage-results/search-performance.md)

## Dépannage

### Problèmes courants

| Problème | Solution |
|---|---|
| **Impossible de créer une instance** | Vérifiez que vous disposez des droits d’[!DNL Adobe Commerce Optimizer] et des autorisations d’administrateur. |
| **L’instance n’apparaît pas** | Vérifiez votre organisation Adobe IMS et actualisez la page. |
| **Impossible d’accéder à l’instance** | Assurez-vous d’être ajouté en tant qu’utilisateur dans Admin Console. |
| **Les exemples de données ne se chargent pas** | Vérifiez les informations d’identification de votre instance et les points d’entrée de l’API. |

### Obtenir de l’aide

- **Ressources pour les développeurs** : [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/)
- **Ressources Storefront** : [documentation du storefront Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr)
- **Tutoriels** : [tutoriels Commerce Optimizer](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview)
- **Assistance** : [Ressources d’assistance Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/overview)
