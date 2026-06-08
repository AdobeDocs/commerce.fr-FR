---
title: Prise en main
description: Découvrez comment commencer à utiliser  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
TQID: https://experienceleague.adobe.com/1dcKMjOut1GtiOevvGJECsaU7URFmYg-mQ-m9wi7n4Y
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: dba482e5-29a8-4127-afa2-c4b913512ef8id: df401a2a-327d-468c-a5e4-b7b7ccd071a0id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 48b94b1b5f38560d5a7be6c5f5431007685202fa
workflow-type: tm+mt
source-wordcount: 1349
ht-degree: 0%

---

# Prise en main

Ce guide vous guide tout au long de la configuration de [!DNL Adobe Commerce Optimizer], du début à la fin. Bien que ce guide couvre tous les rôles, consultez la [documentation destinée aux développeurs](https://developer.adobe.com/commerce/services/optimizer/) pour obtenir du contenu détaillé spécifique aux développeurs.

## Types d’instances et isolation d’environnement

Adobe Commerce Optimizer utilise des instances distinctes pour différents environnements, tels que **sandbox** et **production**. Chaque instance possède son propre ID d’instance et ses propres données isolées, y compris les vues de catalogue, les politiques, la configuration de recherche et les recommandations de produits.

Lors de l’intégration à Adobe Commerce as a Cloud Service, à des plateformes commerciales tierces ou à des vitrines Edge Delivery Services, les environnements correspondent toujours :

- Connectez les **instances Sandbox Optimizer** aux environnements de commerce et de storefront hors production.
- Connectez les **instances de production Optimizer** aux environnements de production, de commerce et de storefront.

Le mélange des environnements Sandbox avec les environnements de production entraîne des données de catalogue incohérentes, un comportement inattendu de recherche et de marchandisage, ainsi que des mesures non fiables. Utilisez le type et l’ID d’instance dans Commerce Cloud Manager comme source de vérité lors de la configuration des intégrations.

## Conditions préalables

Avant de commencer, vérifiez que vous disposez des éléments suivants :

- Compte **** avec droits [!DNL Adobe Commerce Optimizer]
- **Accès administrateur de l’organisation** pour créer des instances et gérer les utilisateurs
- **Compte GitHub** pour le chargement de données d’exemple et le développement du storefront
- **Compréhension de base** des concepts du commerce électronique

## Guide de démarrage rapide

Pour que votre environnement [!DNL Adobe Commerce Optimizer] fonctionne, procédez comme suit :

### Étape 1. Création d’une instance

1. Connectez-vous à [](https://experience.adobe.com/).
1. Accédez à **** > **Commerce Cloud Manager**.
1. Cliquez sur **Ajouter une instance** > **Commerce Optimizer**.

   ![Écran Ajouter une instance d’Adobe Commerce Cloud Manager pour la création d’un environnement Commerce Optimizer](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

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
1. Configurez l’accès des utilisateurs et utilisatrices à l’aide du [ Guide de gestion des utilisateurs ](./user-management.md).

### Étape 3. Ajouter des données d’exemple (facultatif)

Pour les tests et l’apprentissage, suivez les instructions [Charger des données d’exemple](#add-sample-data).

## Workflows basés sur les rôles

La configuration et la gestion des [!DNL Adobe Commerce Optimizer] reposent sur trois rôles clés. Chaque rôle comporte des tâches et des responsabilités spécifiques :

![Workflow basé sur les rôles pour la configuration des [!DNL Adobe Commerce Optimizer] présentant les tâches de l’administrateur, du développeur et des utilisateurs](./assets/high-level-workflow.png){zoomable="yes"}

### Tâches de l’administrateur

Les administrateurs gèrent les instances, les utilisateurs et les paramètres organisationnels.

| Tâche | Description | Lien |
|---|---|---|
| **Gérer les utilisateurs** | Ajouter des utilisateurs, des développeurs et des administrateurs | [Gestion des utilisateurs](./user-management.md) |
| **Créer des instances** | Configurer des environnements de sandbox et de production | [Créer une instance](#step-1-create-an-instance) |
| **Gérer les instances** | Vérifiez le statut, mettez à jour le nom et la description de l’instance et obtenez les URL clés pour l’accès aux applications et aux API | [Gérer les instances](#manage-instances) |
| **Configurer l’accès** | Configurer des vues et des politiques de catalogue | [Vues du catalogue](./setup/catalog-view.md) |

### Tâches du développeur

Les développeurs gèrent l’implémentation technique et l’intégration des données, y compris les tâches d’architecture de plateforme.

| Tâche | Description | Lien |
|---|---|---|
| **Accéder à Developer Console** | Créer des projets et générer des informations d’identification | [](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Ingérer des données de catalogue** | Importer les données de produit des systèmes existants | Pour ingérer des données directement dans Adobe Commerce Optimizer, consultez la section [API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}.<br><br>Pour ingérer des données à partir de Commerce dans des environnements cloud ou on-premise ou d’autres systèmes tiers, consultez la section [Intégrations](./integrations/integrations-overview.md){target="_blank"}. |
| **Configuration du storefront** | Configuration du storefront Edge Delivery Services | [Configuration de Storefront](./storefront.md) |

### Tâches du marchandiseur

Les marchandiseurs optimisent et personnalisent l’expérience d’achat par le biais de la découverte et des recommandations de produits. Elles utilisent également les données et les analyses des acheteurs pour prendre des décisions stratégiques concernant le placement, les prix et les promotions des produits sur le storefront.

| Tâche | Description | Lien |
|---|---|---|
| **Découverte de produits** | Configuration de la recherche et du filtrage | [Présentation du marchandisage](./merchandising/overview.md) |
| **Paramètres de recherche** | Gestion de la recherche sémantique (activée par défaut) et du réglage facultatif | [Paramètres — Recherche avancée](./settings.md#advanced-search) et [Recherche sémantique](./setup/semantic-search.md) |
| **Recommandations** | Configurer des recommandations de produits optimisées par l’IA | [Recommandations de produits](./merchandising/recommendations/overview.md) |
| **Suivi des performances** | Surveiller les mesures de succès | [Mesures de succès](./manage-results/success-metrics.md) |

## Gestion des instances

Gérez les instances à partir du gestionnaire Commerce Cloud.

>[!NOTE]
>
>Tous les utilisateurs [!DNL Adobe Commerce Optimizer] n’ont pas accès à Cloud Manager. L’accès dépend du rôle et des autorisations attribués au compte d’utilisateur.

1. Connectez-vous à [](https://experience.adobe.com/).

1. Ouvrez Commerce Cloud Manager :

   - Sous **Accès rapide**, cliquez sur **Commerce**.
   - Affichez les instances disponibles.

### Rechercher et filtrer des instances

Après vous être connecté, le tableau de bord affiche toutes les instances de produit Commerce disponibles dans l’organisation.
La colonne Produit indique pour quelle application Commerce l’instance est configurée.

![Tableau de bord présentant les options de recherche et de filtrage pour les instances de produit Adobe Commerce Cloud](./assets/search-filter-instances.png){zoomable="yes"}

Utilisez les outils de filtrage et de recherche pour rechercher rapidement des instances spécifiques par date de création, région, créateur, type de produit, environnement ou statut.

### Accéder à l’interface d’administration [!DNL Adobe Commerce Optimizer Studio]

Une fois l’application ouverte, basculez facilement entre des environnements tels que le sandbox et la production pour afficher les données et les paramètres de chacun sans revenir au gestionnaire Commerce Cloud.

1. Dans Commerce Cloud Manager, cliquez sur le nom de l’instance pour l’ouvrir [!DNL Adobe Commerce Optimizer Studio].

1. Basculez entre les instances [!DNL Adobe Commerce Optimizer] sans quitter l’application.

   - Cliquez sur la liste déroulante des instances pour afficher toutes les instances d’Optimizer disponibles dans l’organisation.

     ![Liste déroulante du sélecteur d’instances pour sélectionner [!DNL Adobe Commerce Optimizer] environnements](./assets/context-switcher.png){zoomable="yes"}

- Sélectionnez l’instance à afficher.

>[!NOTE]
>
>Pour revenir au Gestionnaire Commerce Cloud afin d’afficher les détails de l’instance ou de gérer les instances, cliquez sur l’icône ![Icône d’ouverture des applications Experience Cloud](./assets/apps-icon.png) (Applications) dans le coin supérieur gauche du volet de navigation supérieur de Commerce Optimizer.

### Obtenir les détails de l’instance

Affichez les détails de l’instance en cliquant sur l’icône d’information en regard de son nom.

![[!DNL Adobe Commerce Optimizer] panneau Détails de l’instance affichant les points d’entrée et l’ID d’instance](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

Notez les informations clés suivantes :

- **Point d’entrée GraphQL** point d’entrée GraphQL utilisé par votre storefront pour interroger les données de catalogue et de marchandisage de cette instance à l’aide de l’API [Merchandising Service](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/){target=« _blank}
- Point d’entrée **catalogue** point d’entrée de l’API REST que vous utilisez pour ingérer des produits et des prix dans Adobe Commerce Optimizer à partir de votre système Commerce ou PIM. Voir [API Data Ingestion](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- **URL** ouvre l’interface utilisateur d’administration de [Adobe Commerce Optimizer Studio](overview.md) pour configurer et gérer les vues de catalogue, les politiques et le marchandisage.
- **ID d’instance** : identifiant unique (ID de client) de cette instance Adobe Commerce Optimizer, utilisé par les storefronts, les API et les outils pour se connecter à l’environnement approprié.

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
   - Configurer le storefront [](./storefront.md)
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
- **Ressources Storefront** : [documentation du storefront Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/)
- **Tutoriels** : [tutoriels Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview)
- **Assistance** : [Ressources d’assistance Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)
