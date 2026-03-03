---
title: Connecteur Adobe Commerce Optimizer
description: Découvrez comment connecter vos données de votre projet cloud ou local Commerce à Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 380d2c91a17a3e6b84d435774de1b05ada7d3a52
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---


# Connecteur Adobe Commerce Optimizer

Le connecteur Adobe Commerce Optimizer est le pont d’intégration qui synchronise les données de catalogue et de tarification entre une Adobe Commerce sur l’infrastructure cloud ou un déploiement et une [!DNL Adobe Commerce Optimizer] sur site. La synchronisation des données avec Adobe Commerce Optimizer permet d’accéder à des fonctionnalités telles que la Recherche optimisée par l&#39;IA dynamique, les recommandations, les storefronts découplés à chargement rapide, y compris les storefronts Adobe Commerce sur Edge Delivery Services, et l’analyse des performances en temps réel.

## Architecture et expérience

Le connecteur Adobe Commerce Optimizer fonctionne en mappant les sites web Commerce et les vues de magasin à un projet Commerce Optimizer, comme illustré dans la figure suivante :

![Mappage des données Commerce à Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.svg){width="600" zoomable="yes"}

Lorsque des données sont exportées de Commerce vers Commerce Optimizer :

* Les vues du magasin Commerce sont mappées aux sources de catalogue
* Les sites web sont mappés aux livres de prix

Les données de catalogue et de prix associées sont exportées et utilisées ultérieurement pour créer des vues de catalogue et éventuellement définir une politique pour filtrer les données de catalogue et de prix pour des cas d’utilisation professionnels spécifiques.

Au lieu de configurer et de gérer les services Commerce (recherche en direct et recommandations de produits) à partir de l’administration Commerce, vous utilisez des [[!DNL Adobe Commerce Optimizer] outils de marchandisage](../optimizer/merchandising/overview.md) pour gérer la découverte de produits (recherche en direct) et la configuration des règles Recommendations (recommandations de produits). L’instance Adobe Commerce devient la source de données des données de catalogue et de prix. Lorsque les données sont mises à jour dans Commerce, les mises à jour sont synchronisées avec l’instance [!DNL Adobe Commerce Optimizer].

## Workflows

Le connecteur permet plusieurs workflows clés :

* **Exporter les données du catalogue Commerce vers[!DNL Adobe Commerce Optimizer]** : les données de prix et de catalogue sont exportées au niveau du site web et du groupe de clients. Les données de produit et d’attribut de produit sont exportées au niveau du `store view`. Par défaut, la synchronisation des données de catalogue est activée pour toutes les portées de Commerce (sites web et vues de magasin).

  Pour activer ce workflow, installez l’extension PHP `adobe-commerce/commerce-data-export-aco-adapter`, vérifiez la configuration de l’exportateur, puis activez l’intégration entre Commerce et Commerce Optimizer à partir de l’administration Commerce. Pour obtenir des instructions détaillées, voir [Prise en main](#get-started).

* **Mapper le site web Commerce et stocker les données de vue à exporter vers[!DNL Adobe Commerce Optimizer]**

  Vous pouvez éventuellement personnaliser les paramètres d’exportation pour synchroniser les données uniquement pour des sites web ou des vues de boutique spécifiques. Par exemple, vous pouvez choisir d’exporter des données de catalogue pour une seule vue de magasin à utiliser pour un cas d’utilisation spécifique, comme l’optimisation de l’expérience de recherche pour un marché ou une région spécifique.

* **Configuration et gestion des règles de marchandisage**

  Lorsque le connecteur est activé, les règles de marchandisage pour la découverte de produits et les recommandations sont définies et gérées à partir de l’interface utilisateur de [!DNL Adobe Commerce Optimizer], et non à partir des pages [!UICONTROL Live Search] et [!UICONTROL Product Recommendations] de l’administration Commerce.

* **Déploiement de votre storefront Commerce sur Edge Delivery Services**

  Après avoir configuré l’intégration avec [!DNL Adobe Commerce Optimizer], vous pouvez configurer et déployer un storefront Commerce sur Edge Delivery Services pour offrir des performances ultrarapides, une évolutivité, une création de contenu transparente, une personnalisation intégrée et des coûts d’exploitation réduits à l’aide de l’architecture composable pilotée par API et des composants modulaires disponibles avec [!DNL Adobe Commerce Optimizer].

Pour plus d’informations sur la configuration de l’intégration et l’activation de ces workflows, voir [Prise en main](get-started.md).
