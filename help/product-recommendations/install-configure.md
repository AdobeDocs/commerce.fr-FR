---
title: Installation et configuration
description: Découvrez comment installer, mettre à jour et désinstaller [!DNL Product Recommendations].
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 7d5e3faeef2fb16779d1558027a0b76ff3fe3a38
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# Installation et configuration

Pour déployer [!DNL Product Recommendations] sur votre storefront et votre administrateur, vous devez installer le module et configurer le [connecteur de services Commerce](../landing/saas.md). Au fur et à mesure que des mises à jour sont publiées, vous pouvez facilement mettre à jour l’installation avec la dernière version.

- [Installer](#install)
- [Configuration](#configure)
- [Mise à jour](#update)
- [Désinstaller](#uninstall)

## Installer [!DNL Product Recommendations] {#install}

Le module [!DNL Product Recommendations] étant un métapaquet autonome, les mises à jour sont publiées plus fréquemment qu’Adobe Commerce. Pour vous assurer que vous disposez des derniers correctifs et fonctionnalités, reportez-vous aux [notes de mise à jour](release-notes.md).

>[!IMPORTANT]
>
>Vérifiez que vous disposez des [droits](../landing/saas.md#credentials) appropriés pour utiliser les recommandations de produits.

Installez le module `magento/product-recommendations` avec le compositeur :

```bash
composer require magento/product-recommendations
```

### Ajout de la prise en charge de Page Builder {#pbsupport}

[!DNL Product Recommendations] pour Page Builder est un module facultatif qui est installé séparément. Pour utiliser [!DNL Product Recommendations] avec Page Builder, installez le module en exécutant la commande suivante :

```bash
composer require magento/module-page-builder-product-recommendations
```

En activant [!DNL Product Recommendations] dans Page Builder, vous pouvez ajouter une [unité de recommandation](https://experienceleague.adobe.com/fr/docs/commerce-admin/page-builder/add-content/recommendations) active à tout contenu créé dans Page Builder, tel que des pages, des blocs et des blocs dynamiques.

Voir [Utilisation  [!DNL Product Recommendations]  contenu Page Builder](page-builder.md) pour plus d’instructions.

### Ajouter un type de recommandation de similarité visuelle {#vissimsupport}

Le type de recommandation _Similarité visuelle_ vous permet de déployer une unité de recommandation sur la page des détails du produit. Cette unité affiche des produits [visuellement similaires](type.md#visualsim) au produit affiché. Ce type de recommandation est particulièrement utile lorsque les images et les aspects visuels des produits constituent des parties importantes de l’expérience d’achat. Installez le type de recommandation _Similarité visuelle_ en exécutant la commande suivante :

```bash
composer require magento/module-visual-product-recommendations
```

## Configurer [!DNL Product Recommendations] {#configure}

1. Après avoir installé le module `magento/product-recommendations`, configurez le [connecteur de services Commerce](../landing/saas.md) en spécifiant les clés API et en sélectionnant un espace de données SaaS.

   La configuration de cette connexion permet la synchronisation des données et la communication entre l’instance Commerce, le service de catalogue et d’autres services annexes. La synchronisation des données est gérée par l’extension [Exportation de données SaaS](../data-export/overview.md).

1. Pour vous assurer que l’exportation du catalogue peut s’exécuter correctement, vérifiez que les tâches [cron](https://experienceleague.adobe.com/fr/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) et les [indexeurs](https://experienceleague.adobe.com/fr/docs/commerce-operations/configuration-guide/cli/manage-indexers) sont en cours d’exécution et que l’indexeur de `Product Feed` est défini sur `Update by Schedule`.

Une fois que vous avez réussi à lier l’application Commerce aux services Commerce et que vous avez spécifié l’espace de données [SaaS](../landing/saas.md#saas-configuration), la synchronisation du catalogue commence. Vous pouvez ensuite [vérifier](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) que les données comportementales sont envoyées à votre storefront.

## Surveillance et dépannage de la synchronisation des données

Dans l’administration Commerce, vous pouvez surveiller le processus de synchronisation à l’aide du tableau de bord [Data Management Dashboard](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-dashboard). Utilisez l’[interface de ligne de commande Commerce](../data-export/data-export-cli-commands.md#troubleshooting) et les journaux pour gérer et résoudre les problèmes liés au processus.

Vous pouvez ensuite [vérifier](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) que les données comportementales sont envoyées à votre storefront.

## Mise à jour de l’installation [!DNL Product Recommendations] {#update}

Comme tout Adobe Commerce, [!DNL Product Recommendations] utilise le compositeur pour l’installation et les mises à jour. Pour mettre à jour le module `magento/product-recommendations`, exécutez les opérations suivantes :

```bash
composer update magento/product-recommendations --with-dependencies
```

Pour effectuer une mise à jour vers une version majeure, par exemple de la version 5.0 à la version 6.0, vous devez modifier le fichier `composer.json` racine de votre projet. (Voir les [notes de mise à jour](release-notes.md) pour plus d’informations sur la dernière version.) Par exemple, nous allons ouvrir le fichier `composer.json` principal et rechercher le module `magento/product-recommendations` :

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

Passons la version majeure de `5.0` à `6.0` :

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

Enregistrez le fichier `composer.json` et exécutez :

```bash
composer update magento/product-recommendations --with-dependencies
```

Ou si vous avez installé les modules `magento/module-visual-product-recommendations` et `magento/module-page-builder-product-recommendations` :

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> Dans les versions 3.x.x de Product Recommendations, vous n’aviez besoin que d’une seule clé API. Dans les versions 4.x.x et ultérieures, vous devez fournir des clés d’API publiques et privées pour les environnements de sandbox et de production. Si vous ne fournissez pas les deux paires de clés API, vous ne pouvez pas accéder à la fonctionnalité de recommandations de produits dans l’Administration. Cependant, la collecte de données se poursuit sur votre storefront et les recommandations existantes continuent d’être présentées à vos clientes et clients.

## Pare-feux

Pour autoriser Product Recommendations à passer par un pare-feu, ajoutez des `commerce.adobe.io` à la liste autorisée.

## Désinstaller [!DNL Product Recommendations] {#uninstall}

Si nécessaire, vous pouvez [désinstaller](https://experienceleague.adobe.com/fr/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) le module de recommandations de produits.
