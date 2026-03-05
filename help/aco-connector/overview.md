---
title: Connecteur Adobe Commerce Optimizer
description: Découvrez comment connecter vos données de votre projet cloud ou local Commerce à Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 11bb5df2488a017065db44504f35612fe54e284c
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 0%

---


# Connecteur Adobe Commerce Optimizer

Le connecteur Adobe Commerce Optimizer est le pont d’intégration qui synchronise les données de catalogue et de tarification entre une Adobe Commerce sur l’infrastructure cloud ou un déploiement et une [!DNL Adobe Commerce Optimizer] sur site. La synchronisation des données avec Adobe Commerce Optimizer offre des fonctionnalités telles que la Recherche optimisée par l&#39;IA dynamique, les recommandations, l’optimisation des sites et les storefronts découplés à chargement rapide, y compris les storefronts Adobe Commerce sur Edge Delivery Services, ainsi que l’analyse des performances en temps réel.

## Architecture et expérience

Le connecteur Adobe Commerce Optimizer fonctionne en mappant les sites web Commerce et les vues de magasin à un projet Commerce Optimizer, comme illustré dans la figure suivante :

![Mappage des données Commerce à Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="700" zoomable="yes"}

Lorsque des données sont exportées de Commerce vers Commerce Optimizer :

* Les vues du magasin Commerce sont mappées aux sources de catalogue
* Les sites web sont mappés aux livres de prix

Les données de catalogue et de prix associées sont exportées et utilisées ultérieurement pour créer des vues de catalogue et éventuellement définir des politiques pour filtrer les données de catalogue et de prix pour des cas d’utilisation professionnels spécifiques.

Lorsque le connecteur est activé, vous pouvez également configurer et gérer des règles de marchandisage pour la découverte de produits et des règles pour les recommandations à l’aide des [[!DNL Adobe Commerce Optimizer] outils de marchandisage](../optimizer/overview.md#quick-tour) L’instance Adobe Commerce devient la source de données des données de catalogue et de prix. Lorsque les données sont mises à jour dans Commerce, les mises à jour sont synchronisées avec l’instance [!DNL Adobe Commerce Optimizer].

## Workflows

Le connecteur permet plusieurs workflows clés :

* **Exporter les données du catalogue Commerce vers[!DNL Adobe Commerce Optimizer]** : les données de prix et de catalogue sont exportées au niveau du site web et du groupe de clients. Les données de produit et d’attribut de produit sont exportées au niveau du `store view`. Par défaut, la synchronisation des données de catalogue est activée pour toutes les portées de Commerce (sites web et vues de magasin).

  Pour activer ce workflow, installez l’extension PHP `adobe-commerce/commerce-data-export-aco-adapter`, vérifiez la configuration de l’exportateur, puis activez l’intégration entre Commerce et Commerce Optimizer à partir de l’administration Commerce. Pour obtenir des instructions détaillées, voir [Prise en main](#get-started).

* **Mapper le site web Commerce et stocker les données de vue à exporter vers[!DNL Adobe Commerce Optimizer]**

  Vous pouvez éventuellement personnaliser les paramètres d’exportation pour synchroniser les données uniquement pour des sites web ou des vues de boutique spécifiques. Par exemple, vous pouvez choisir d’exporter des données de catalogue pour une seule vue de magasin à utiliser pour un cas d’utilisation spécifique, comme l’optimisation de l’expérience de recherche pour un marché ou une région spécifique.

* **Configuration et gestion des règles de marchandisage**

  Lorsque le connecteur est activé, les règles de marchandisage pour la découverte de produits et les recommandations sont définies et gérées à partir de l’interface utilisateur de [!DNL Adobe Commerce Optimizer], et non à partir des pages [!UICONTROL Live Search] et [!UICONTROL Product Recommendations] de l’administration Commerce.

* **Déploiement de votre storefront Commerce sur Edge Delivery Services**

  Après avoir configuré l’intégration avec [!DNL Adobe Commerce Optimizer], vous pouvez déployer un storefront Commerce sur Edge Delivery Services. Vous bénéficiez ainsi de performances ultrarapides, d’une évolutivité, d’une création de contenu transparente et d’une personnalisation intégrée à l’aide d’une architecture composable pilotée par API.

Pour plus d’informations sur la configuration de l’intégration et l’activation de ces workflows, voir [Prise en main](get-started.md).
