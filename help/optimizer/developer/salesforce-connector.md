---
title: Connecteur Salesforce Commerce
description: Découvrez le  [!DNL Commerce Optimizer SFCC Connector]  qui fournit un point de départ pour l’intégration de Salesforce Commerce B2C à afin de synchroniser les données de catalogue et d [!DNL Adobe Commerce Optimizer] implémenter et de personnaliser le connecteur pour prendre en charge les opérations commerciales.
role: Admin, Developer
source-git-commit: fc6f8566a1932e830a37bcfa32cd1c4168c67c68
workflow-type: tm+mt
source-wordcount: '1115'
ht-degree: 0%

---

# Connecteur Salesforce Commerce pour Adobe Commerce Optimizer

Basée sur la technologie Adobe App Builder, la [!DNL Commerce Optimizer Salesforce Commerce Connector] permet un transfert et une gestion transparents des données de catalogue de Salesforce Commerce Cloud B2C vers [!DNL Adobe Commerce Optimizer]. Il relie les deux plateformes, en conservant les informations sur les produits, les prix et les mises à jour synchronisés, sans reconfiguration de la plateforme.

Le connecteur prêt à l’emploi offre des fonctionnalités de synchronisation des données fiables et la possibilité de personnaliser les workflows en fonction des besoins de votre entreprise.

Pour une série complète de tutoriels vidéo, consultez [En savoir plus sur le kit de démarrage cloud de Salesforce Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/sfcc-starter-kit/overview).

## Fonctionnalités clés

* **Synchronisation des données de catalogue :** transmettez les données sur les produits (y compris les variantes, les tarifs et les structures) de Salesforce Commerce B2C vers Adobe Commerce Optimizer pour maintenir à jour les vitrines et les applications basées sur l’expérience.
* **Synchronisation des prix :** importez et gérez les données de prix directement à partir de Salesforce Commerce B2C.
* **Prend en charge plusieurs types de données** Synchronisez les produits, les structures de prix et de catalogue pour refléter des configurations de marchandisage complexes.

* **Workflows de synchronisation flexibles**
   * **Synchronisations planifiées :** automatisez les mises à jour à l’aide de la planification des tâches cron, sans effort manuel.
   * **Mises à jour à la demande :** déclenchez instantanément des mises à jour au niveau des SKU pour des modifications, des corrections ou des lancements de produits urgents.

* **Conçu pour l’extensibilité**
   * Utilise des points d’entrée SCAPI (Salesforce B2C API[ ](https://developer.salesforce.com/docs/commerce/commerce-api/guide/get-started.html)Commerce personnalisés pour garantir la compatibilité et une adaptation facile à des cas d’utilisation uniques ou avancés.
   * Évolue en fonction de la phase de démarrage de votre entreprise avec la synchronisation des catalogues et des prix, puis étend les workflows pour prendre en charge des intégrations supplémentaires ou la logique commerciale.
   * Configurez et faites évoluer les workflows sans reconstruire les intégrations principales.

>[!NOTE]
>
>Le connecteur est spécialement conçu pour Salesforce Commerce Cloud B2C. Il ne prend pas en charge les produits Salesforce B2B ou D2C, qui reposent sur différentes piles technologiques.

## Qui bénéficie du connecteur Salesforce ?

L&#39;[!DNL Salesforce Commerce Connector] est idéal pour :

* **Clients Salesforce Commerce Cloud B2C existants** amélioration des fonctionnalités de storefront
* **Entreprises multi-marques** nécessitant des fonctionnalités avancées de marchandisage et de personnalisation sur plusieurs storefronts
* **Entreprises à la recherche d’améliorations des performances** via Adobe Edge Delivery Services pour des expériences storefront plus rapides
* **Sociétés avec des structures de tarification complexes** synchronisant des tarifs sophistiqués et une tarification spécifique aux paramètres régionaux
* **Clients AEM** gestion des catalogues de produits à partir de Salesforce Commerce B2C lors de l’utilisation du storefront Adobe Commerce avec Edge Delivery Services
* **Détaillants avec des exigences multi-locales** synchroniser les informations localisées sur les produits sur les marchés et dans les langues

## Cas d’utilisation

Le connecteur prend en charge plusieurs cas d’utilisation clés :

### Ingestion des données de catalogue et affichage du storefront

Ce cas d’utilisation principal illustre l’ensemble du flux de données du B2C Salesforce Commerce vers le storefront Adobe Commerce :

1. **Ingestion initiale du catalogue :** chargez en masse l’ensemble de votre catalogue Salesforce Commerce, y compris les produits simples avec des variantes, des catalogues de prix et des informations de prix.
1. **Mises à jour delta automatisées :** synchroniser automatiquement les mises à jour de produit à partir de l’interface utilisateur de la gestion de catalogue de Salesforce Commerce vers [!DNL Commerce Optimizer].
1. **Intégration de Storefront :** permet d’afficher des données de catalogue synchronisées sur votre storefront de service Adobe Commerce Edge Delivery à l’aide des API de storefront [!DNL Commerce Optimizer].
1. **Mises à jour en temps réel :** affichez les informations mises à jour sur les produits (noms, prix et descriptions) immédiatement sur votre storefront après avoir apporté des modifications dans Salesforce.

### Gestion de produits à plusieurs paramètres régionaux

Tirez parti des fonctionnalités de localisation B2C de Salesforce Commerce :

* Synchronisez les versions localisées des champs de texte de produit (noms, descriptions) à partir de Salesforce Commerce B2C pour différents paramètres régionaux.
* Mappez les paramètres régionaux Salesforce 1:1 avec les paramètres régionaux [!DNL Commerce Optimizer].
* Prise en charge de plusieurs cycles d’ingestion de produit pour différentes localisations.
* Maintenir la cohérence entre les catalogues de produits globaux.

## Architecture et composants

Le [!DNL SFCC Connector] fournit une couche d’intégration robuste entre une instance Salesforce Commerce B2C et [!DNL Commerce Optimizer]. Le connecteur fonctionne par le biais d’une série d’actions de synchronisation qui transfèrent les données de votre catalogue, les tarifs et les informations sur les produits.

1. **Extraction de données** : authentifiez-vous avec votre instance Salesforce Commerce B2C et extrayez les données de catalogue à l’aide d’API SCAPI personnalisées.
1. **Transformation des données** : transformez les données de produit pour répondre aux exigences du schéma et du modèle de données [!DNL Commerce Optimizer].
1. **Ingestion de données** : transmettez en toute sécurité les données transformées aux [!DNL Commerce Optimizer] à l’aide du SDK TypeScript ACO.
1. **Intégration Storefront** : les données synchronisées sont disponibles via les API [!DNL Commerce Optimizer] pour les expériences de storefront.

Le diagramme suivant illustre le flux de données de haut niveau pour l’intégration :

![Architecture du connecteur Commerce de Salesforce](../assets/sfcc_starter_kit.png){zoomable="yes"}

### Composants clés

Le [!DNL Commerce Optimizer SFCC Connector] se compose de plusieurs composants clés :

* **Application App Builder ACO SFCC Starter Kit**-fournit des fonctions sans serveur qui gèrent la synchronisation des données entre SFCC et Adobe Commerce Optimizer.
* **Cartouche SFCC personnalisée** - Cartouche requise qui étend votre instance Salesforce Commerce Cloud avec les API nécessaires à l’extraction des données.
* **Interface utilisateur de gestion** : interface web permettant de surveiller le statut de synchronisation et de gérer les opérations du connecteur.

### Processus de synchronisation

Le connecteur prend en charge plusieurs modes de synchronisation.

| Mode de synchronisation | Description |
|-----------|-------------|
| **synchronisation complète du site** | Effectue une synchronisation complète de tous les produits, tarifs et prix pour votre site Salesforce Commerce Cloud et vos paramètres régionaux configurés. Cela inclut : <ul><li>métadonnées et attributs du produit</li><li>structure et catégories du catalogue</li><li>catalogue des prix</li><li>information sur les prix</li><li>données de produit multi-paramètres régionaux</li></ul> |
| **Synchronisation delta** | Récupère et synchronise uniquement les modifications apportées aux données de prix et de produit Salesforce depuis la dernière synchronisation, assurant ainsi des mises à jour efficaces et opportunes.<br>La synchronisation Delta s’exécute automatiquement selon un calendrier (par défaut : toutes les heures) pour maintenir l’actualisation des données. |
| **Options de synchronisation ciblées** | Fournit des fonctionnalités de synchronisation granulaire : <ul><li>**Synchronisation du catalogue des prix** synchronise uniquement les informations sur le catalogue des prix</li><li>**Synchronisation des métadonnées** met à jour les métadonnées de produit et les définitions d’attributs</li><li>**Synchronisation de produit spécifique** synchronise les produits individuels par SKU</li></ul> |

## Considérations importantes

Lors de la planification de votre implémentation, tenez compte des facteurs clés suivants :

### Mappage des données et attributs

* **Attributs pouvant faire l’objet de recherches :** Salesforce Commerce B2C définit les attributs pouvant faire l’objet de recherches via l’interface utilisateur, ce que l’API n’expose pas. Utilisez l’[[!DNL Catalog Data Ingestion metadata APIs]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata) pour configurer manuellement ces attributs pouvant faire l’objet de recherches dans Adobe Commerce Optimizer.
* **Mappage des attributs :** planifiez le mappage des attributs de produit B2C Salesforce Commerce aux métadonnées [!DNL Commerce Optimizer] en fonction des besoins de votre entreprise.
* **Champs pouvant faire l’objet d’une recherche par défaut :** le connecteur rend automatiquement les attributs principaux (`name`, `description`, `ID`) consultables par défaut.

### Portée de la synchronisation

* **Sélection de sites :** Salesforce Commerce B2C présente un concept de sites auxquels les catalogues se rattachent. Lors de la synchronisation complète, sélectionnez le site Salesforce à synchroniser.
* **Gestion des paramètres régionaux :** chaque paramètre régional de Salesforce Commerce entraîne un cycle d’ingestion de produit distinct dans [!DNL Commerce Optimizer].
* **Volume des données :** tenez compte de la taille du catalogue et de la fréquence de synchronisation lors de la planification de l’implémentation.

## Surveillance et gestion

Une fois installé et configuré, le [!DNL Commerce Optimizer SFCC Connector] fournit des fonctionnalités complètes de surveillance et de gestion à partir du [!DNL SFCC to ACO Sync Panel] :

![Interface utilisateur de gestion du connecteur Commerce de Salesforce](../assets/sfcc_management_ui.png){width="700" zoomable="yes"}

L’URL de cette interface est fournie après le déploiement du [!DNL Commerce Optimizer SFCC Connector Starter Kit] dans le projet App Builder.

Les principales fonctionnalités sont les suivantes :

* **Suivi de l’état de synchronisation :** surveiller le statut et l’horodatage de toutes les opérations de synchronisation.
* **Validation de la connectivité :** testez les connexions à Salesforce Commerce Cloud et Adobe Commerce Optimizer.
* **Validation des données de produit :** vérifiez que les données de produit synchronisées apparaissent correctement dans le storefront.
* **Journalisation et dépannage des erreurs :** journaux d’erreurs à des fins de dépannage sont accessibles via l’interface de ligne de commande App Builder.
* **Gestion des états :** suivez la progression de la synchronisation et évitez les conflits avec la gestion des états intégrée.

## Code Source et ressources de développement

Le [!DNL Commerce Optimizer SFCC Connector] est en open source et disponible pour personnalisation. Les référentiels principaux sont les suivants :

* **[Kit de démarrage ACO SFCC](https://github.com/adobe-commerce/aco-sfcc-starter-kit)** - Application et documentation du connecteur principal.
* **[Cartouches ACO SFCC](https://github.com/adobe-commerce/aco-sfcc-cartridges)** - Cartouche SFCC requise pour l’intégration de l’API.
* **[ACO TypeScript SDK](https://github.com/adobe-commerce/aco-ts-sdk)** - Intégration de SDK for Adobe Commerce Optimizer.

Ces référentiels fournissent un code source complet, une documentation détaillée ainsi que des exemples d’implémentation et de personnalisation du connecteur.

## Étapes suivantes

Vous êtes prêt à intégrer vos données Salesforce Commerce Cloud à Adobe Commerce Optimizer ? Commencez par consulter le guide de mise en œuvre détaillé dans le référentiel [ACO SFCC Starter Kit](https://github.com/adobe-commerce/aco-sfcc-starter-kit) et assurez-vous que les conditions préalables nécessaires sont en place.
