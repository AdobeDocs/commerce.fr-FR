---
title: Prise en main de  [!DNL Live Search]
description: Découvrez la configuration requise et les étapes d’installation pour  [!DNL Live Search]  à partir d’Adobe Commerce.
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 69258b150bab98e680ab682aba593cdb2e2b7f04
workflow-type: tm+mt
source-wordcount: '2512'
ht-degree: 0%

---

# Configuration pour la réussite avec [!DNL Live Search]

Adobe Commerce [!DNL Live Search] et [[!DNL Catalog Service]](../catalog-service/guide-overview.md) fonctionnent ensemble pour fournir une solution de recherche performante, pertinente et intuitive permettant à vos clients de trouver exactement ce dont ils ont besoin, rapidement. Plus précisément, [!DNL Catalog Service] affiche vos données de catalogue pour les services SaaS, comme les [!DNL Live Search] à utiliser.

Cet article fournit des instructions détaillées sur l’implémentation de [!DNL Live Search] avec le [!DNL Catalog Service].

## Audience

Cet article est destiné au développeur ou à l’intégrateur système de votre équipe chargé de l’installation et de la configuration de votre instance Adobe Commerce.

## Conditions requises

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8.1, 8.2 ou 8.3
- [!DNL Composer]
- Exécution des tâches cron et des indexeurs

>[!IMPORTANT]
>
>Avant d’implémenter [!DNL Live Search], consultez la section [ Limites et limites ](boundaries-limits.md) pour vous assurer que [!DNL Live Search] correspond aux besoins de votre entreprise.

## Mises à jour importantes

- Depuis [!DNL Live Search] 3.0.2, l’extension [!DNL Catalog Service] est fournie avec l’installation .

## Plateformes prises en charge

- Adobe Commerce on Cloud (ECE) : 2.4.4+
- Adobe Commerce on-prem (EE) : 2.4.4+

## Présentation des workflows

À un niveau élevé, la [!DNL Live Search] d’intégration nécessite que vous :

1. [Installer](#1-install-the-live-search-extension) l’extension [!DNL Live Search]
1. [Configurer](#2-configure-api-keys) les clés API
1. [Synchroniser](#3-sync-your-catalog-data) les données de votre catalogue
1. [Vérifier](#4-verify-that-the-data-was-exported) que les données du catalogue ont été exportées
1. [Configurer](#5-configure-the-data) les données
1. [Tester](#6-test-the-connection) la connexion
1. [Valider](#7-verify-that-events-are-capturing-data) vérifier que les événements capturent des données
1. [Personnaliser](#8-customize-for-your-storefront) votre storefront

## &#x200B;1. Installer l’extension [!DNL Live Search]

[!DNL Live Search] est installé en tant qu’extension depuis [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) via [Composer](https://getcomposer.org/). Une fois que vous avez installé et configuré [!DNL Live Search], Adobe [!DNL Commerce] commence à partager des données de recherche et de catalogue avec les services SaaS. À ce stade, les utilisateurs *administrateurs* peuvent configurer, personnaliser et gérer les facettes de recherche, les synonymes et les règles de marchandisage.

>[!BEGINTABS]

>[!TAB Nouvelle instance Commerce]

Suivez ces instructions si vous installez [!DNL Live Search] sur une nouvelle instance Commerce.

1. Vérifiez que les [tâches cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) et [indexeurs](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) sont en cours d’exécution.

1. Utilisez le compositeur pour ajouter le module Live Search à votre projet :

   ```bash
   composer require magento/live-search --no-update
   ```

1. Mettez à jour les dépendances et installez l’extension :

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Désactivez les modules [!DNL OpenSearch] et associés, puis installez-les [!DNL Live Search].

   ```bash
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch8 Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   [!DNL Elasticsearch] continue de gérer les requêtes de recherche du storefront pendant que le service [!DNL Live Search] synchronise les données de catalogue et indexe les produits en arrière-plan.

1. Installez les mises à jour.

   ```bash
   bin/magento setup:upgrade
   ```

1. Vérifiez que les [indexeurs](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) suivants sont définis sur « Mettre à jour selon le calendrier » :

   - Flux de produit
   - Flux de variante de produit
   - Flux d’attributs de catalogue
   - Flux des prix des produits
   - Étendue Du Flux De Données Du Site Web
   - Étendue du flux de données des groupes de clients
   - Flux de catégories
   - Flux d’autorisations des catégories

Après avoir vérifié les indexeurs, l’étape suivante consiste à [configurer les clés API](#2-configure-api-keys).

>[!TAB Instance Commerce existante]

Suivez ces instructions si vous installez [!DNL Live Search] sur une instance Commerce existante.

1. Vérifiez que les [tâches cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) et [indexeurs](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) sont en cours d’exécution.

1. Utilisez le compositeur pour ajouter le module Live Search à votre projet :

   ```bash
   composer require magento/live-search --no-update
   ```

1. Mettez à jour les dépendances et installez l’extension :

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Désactivez les modules [!DNL Live Search] qui servent aux résultats de recherche storefront.

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing
   ```

   [!DNL Elasticsearch] continue de gérer les requêtes de recherche du storefront pendant que le service [!DNL Live Search] synchronise les données de catalogue et indexe les produits en arrière-plan.

1. Installez les mises à jour.

   ```bash
   bin/magento setup:upgrade
   ```

1. Vérifiez que les [indexeurs](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) suivants sont définis sur « Mettre à jour selon le calendrier » :

   - Flux de produit
   - Flux de variante de produit
   - Flux d’attributs de catalogue
   - Flux des prix des produits
   - Étendue Du Flux De Données Du Site Web
   - Étendue du flux de données des groupes de clients
   - Flux de catégories
   - Flux d’autorisations des catégories

1. Activez l’extension [!DNL Live Search] et désactivez [!DNL OpenSearch] (modules Magento Elasticsearch et OpenSearch).

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing
   ```

   ```
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_Elasticsearch8 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   >[!NOTE]
   >
   >La commande disable inclut la liste des modules Commerce qui prennent en charge OpenSearch. Si aucun module n’est installé sur votre instance Commerce, une erreur `module does not exist` s’affiche.

1. Installez les mises à jour.

   ```bash
   bin/magento setup:upgrade
   ```

Après avoir vérifié les indexeurs, l’étape suivante consiste à [configurer les clés API](#2-configure-api-keys).

>[!ENDTABS]

## &#x200B;2. Configuration des clés API

La clé API Adobe Commerce et sa clé privée associée sont nécessaires pour [!DNL Live Search] connecter à une installation d’Adobe Commerce. La clé API est générée et conservée dans le compte du titulaire de la licence [!DNL Commerce], qui peut la partager avec le développeur ou l’intégrateur système. Le développeur peut ensuite créer et gérer les espaces de données SaaS pour le compte du titulaire de la licence. Si vous disposez déjà d’un ensemble de clés API, vous n’avez pas besoin de les régénérer.

Découvrez comment configurer vos clés API dans l’article [Connecteur de services Commerce](../landing/saas.md).

## &#x200B;3. Synchroniser les données de votre catalogue

[!DNL Live Search] déplace les données de catalogue vers l’infrastructure SaaS d’Adobe. Les données sont indexées et les résultats de la recherche sont directement transmis au storefront à partir de cet index. En fonction de la taille et de la complexité, l’indexation peut prendre de 30 minutes à quelques heures.

Pour commencer la synchronisation initiale des données de catalogue avec les services SaaS, exécutez les commandes suivantes dans l’ordre suivant :

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

Lorsque vous exécutez ces commandes, la synchronisation initiale des données de votre catalogue avec les services SaaS commence.

>[!WARNING]
>
>Les opérations de recherche et de navigation par catégorie ne sont pas disponibles lors de la synchronisation. Le processus peut prendre 1+ heures selon la taille du catalogue.

### Surveillance de la progression de la synchronisation

Utilisez le [tableau de bord de gestion des données](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) pour surveiller la progression de la synchronisation. Ce tableau de bord fournit des informations précieuses sur la disponibilité des données de produit sur votre storefront, afin qu’elles puissent être rapidement affichées pour les clients.

![Tableau de bord de gestion des données](assets/data-management-dashboard.png)

Vous pouvez également exécuter des commandes de synchronisation et résoudre les problèmes de synchronisation à l’aide de l’[interface de ligne de commande Commerce](../data-export/data-export-cli-commands.md#troubleshooting) et des journaux d’extension d’exportation de données.

#### Futures mises à jour des produits

Après la synchronisation initiale, il peut s’écouler jusqu’à 15 minutes avant que les mises à jour incrémentielles des produits ne soient disponibles pour la recherche storefront. Pour en savoir plus, consultez [Diffusion de mises à jour de produit](indexing.md) dans la documentation sur l’indexation.

## &#x200B;4. Vérifier que les données ont été exportées

Pour vérifier si vos données de catalogue ont été exportées à partir d’Adobe Commerce et synchronisées avec [!DNL Live Search], vous disposez de quelques options :

- Recherchez des entrées dans les tableaux suivants :

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >Si vous obtenez une erreur `table does not exist`, recherchez les entrées dans les tableaux `catalog_data_exporter_products` et `catalog_data_exporter_product_attributes`. Ces noms de table sont utilisés dans les versions [!DNL Live Search] antérieures à la version 4.2.1.

- Utilisez le [terrain de jeu GraphQL](https://experienceleague.adobe.com/en/docs/commerce/live-search/live-search-admin/graphql) avec la requête par défaut (voir [Référence de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) pour plus de détails) pour vérifier les éléments suivants :

   - Le nombre de produits renvoyés est proche de ce que vous attendiez pour la vue du magasin.
   - Les facettes sont renvoyées.

Pour obtenir de l’aide supplémentaire, consultez [[!DNL Live Search] catalogue non synchronisé](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) dans la base de connaissances du support.

## &#x200B;5. Configuration des données

La configuration correcte des données de produit garantit de bons résultats de recherche pour vos clients. Dans cette section, vous activez les widgets de liste de produits et attribuez des catégories.

### Activer les widgets de liste de produits

Lorsque vous installez [!DNL Live Search] version 4.0.0 ou ultérieure, les widgets de liste de produits sont activés par défaut. Lorsque les widgets sont activés, un autre composant d’interface utilisateur est utilisé pour les résultats de la recherche et pour parcourir les catégories dans les pages de liste de produits. Ce composant de l’interface utilisateur effectue des appels directs à l’[API Catalog Service](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/), ce qui accélère les temps de réponse.

Si vous disposez d’une version de [!DNL Live Search] antérieure à 4.0.0 ou ultérieure, vous devez activer manuellement le widget Liste des produits.

1. Dans *Admin*, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Sous **[!UICONTROL Live Search]**, sélectionnez **[!UICONTROL Storefront Features]**.
1. Définissez **[!UICONTROL Enable Product Listing Widgets]** sur `Yes`.

   ![Activer les widgets de liste de produits](assets/ls-admin-enable-widget.png)

Lorsque vous modifiez cette configuration, le message `Page cache is invalidated` s’affiche. Vous devez vider le cache du Magento pour enregistrer votre modification.

1. Accédez à la page [Gestion du cache](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management) en effectuant l’une des opérations suivantes :

   - Cliquez sur le lien **[!UICONTROL Cache Management]** dans le message au-dessus de l’espace de travail.
   - Dans la barre latérale _Admin_, accédez à **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**.

1. Sélectionnez le **** Configuration[!UICONTROL Cache Type] et cliquez sur **[!UICONTROL Flush Magento Cache]**.

   Les modifications apportées au storefront sont immédiates après avoir vidé le cache.

### Attribuer des catégories

Les produits renvoyés dans [!DNL Live Search] doivent être affectés à une [catégorie](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/categories). Dans Luma, par exemple, les produits sont classés dans des catégories telles que « Hommes », « Femmes » et « Équipement ». Des sous-catégories sont également définies pour les « Tops », les « Bottoms » et les « Watches ». Ces affectations de catégorie améliorent la granularité lors du filtrage.

## &#x200B;6. Tester la connexion

Maintenant que vos données de catalogue sont en SaaS, testez-les pour vous assurer que les données de produit sont renvoyées dans les scénarios suivants :

- La zone de [!UICONTROL Search] renvoie correctement les résultats
- L’exploration des catégories renvoie correctement les résultats
- Les facettes sont disponibles en tant que filtres dans les pages de résultats de recherche

Si tout fonctionne correctement, [!DNL Live Search] est installé, connecté et prêt à l’emploi.

Si vous rencontrez des problèmes au niveau du storefront, vérifiez dans le fichier `var/log/system.log` les échecs ou les erreurs de communication de l’API côté services.

Pour autoriser le [!DNL Live Search] à travers un pare-feu, ajoutez des `commerce.adobe.io` à la liste autorisée.

## &#x200B;7. Vérifiez que les événements capturent des données

Assurez-vous que les événements storefront déployés sur votre site fonctionnent. Ce contrôle est particulièrement important pour les implémentations découplées.

- Passez en revue les [événements](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search) requis pour la [!DNL Live Search].
- Assurez-vous que le [tableau de bord de la recherche en direct](performance.md) affiche les données de vos environnements hors production.
- [Vérifier la collecte des événements](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/).

## &#x200B;8. Personnaliser pour votre storefront

Vous avez installé l’extension [!DNL Live Search], synchronisé, validé et configuré vos données. L’étape suivante consiste à s’assurer que les widgets [!DNL Live Search] sont conformes à l’aspect de votre boutique.

Vous pouvez mettre en forme les widgets de fenêtre contextuelle et de liste déroulante en définissant des règles CSS personnalisées selon vos besoins. Voir [Mise en forme des éléments de fenêtre contextuelle](storefront-popover.md#styling-popover-example) et [widget de page de liste de produits](plp-styling.md#styling-example).

Si vous souhaitez étendre les fonctionnalités des widgets, le code source de chacun d’eux est disponible dans un référentiel public.
Dans ce scénario, vous pouvez personnaliser le JavaScript selon vos propres besoins, puis héberger votre code personnalisé sur votre réseau CDN. Ce script personnalisé communique avec le service [!DNL Live Search] et renvoie les résultats comme d’habitude, ce qui vous permet de contrôler la fonctionnalité du widget.

- [référentiel de widgets PLP](https://github.com/adobe/storefront-product-listing-page)
- [Référentiel de barre de recherche](https://github.com/adobe/storefront-search-as-you-type)

## Mise à jour des [!DNL Live Search]

Avant de mettre à jour [!DNL Live Search], vérifiez la version de [!DNL Live Search] installée à l’aide du compositeur.

```bash
composer show magento/module-live-search | grep version
```

Pour mettre à jour [!DNL Live Search], exécutez la commande suivante à partir de la ligne de commande :

```bash
composer update magento/live-search --with-dependencies
```

Pour effectuer une mise à jour vers une version majeure telle que de 3.1.1 à 4.0.0, modifiez le fichier [!DNL Composer] de `.json` racine du projet comme suit :

1. Si la version `magento/live-search` actuellement installée est `3.1.1` ou inférieure et que vous effectuez une mise à niveau vers la version `4.0.0` ou supérieure, exécutez la commande suivante avant la mise à niveau :

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   Pour plus d’informations sur la version `magento/live-search` actuellement installée, exécutez la commande suivante :

   ```bash
   composer show magento/live-search
   ```

1. Ouvrez le fichier de `composer.json` racine et recherchez des `magento/live-search`.

1. Dans la section `require` , mettez à jour le numéro de version comme suit :

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. Enregistrez `composer.json`. Exécutez ensuite la commande suivante à partir de la ligne de commande :

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## Désinstallation de [!DNL Live Search]

Pour désinstaller [!DNL Live Search], voir [Désinstaller les modules](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## packages [!DNL Live Search]

L’extension [!DNL Live Search] se compose des packages suivants :

| Package | Description |
|--- |--- |
| `module-live-search` | Permet aux commerçants de configurer leurs paramètres de recherche pour les facettes, les synonymes, les règles de requête, etc., et donne accès à un terrain de jeu GraphQL en lecture seule pour tester les requêtes provenant de l’*Administrateur*. |
| `module-live-search-adapter` | Achemine les requêtes de recherche du storefront vers le service [!DNL Live Search] et effectue le rendu des résultats dans le storefront. <br />- Navigation par catégorie - Achemine les requêtes du storefront [navigation supérieure](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation-top) vers le service de recherche.<br />- Recherche globale - Achemine les requêtes du champ [recherche rapide](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search) vers le service [!DNL Live Search]. Le champ de recherche rapide se trouve dans le coin supérieur droit de la page du storefront. |
| `module-live-search-storefront-popover` | Une fenêtre contextuelle « rechercher en cours de frappe » remplace la recherche rapide standard et renvoie les données et les miniatures des meilleurs résultats de recherche. |

## [!DNL Live Search] dépendances

Le métapaquet [!DNL Composer] pour installer l’extension [!DNL Live Search] comprend les dépendances de module suivantes.

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## Concepts avancés

Les sections suivantes contiennent des rubriques plus détaillées lorsque vous utilisez [!DNL Live Search] et [!DNL Catalog Service].

### Point d’entrée

[!DNL Live Search] communique via le point d’entrée à l’adresse `https://catalog-service.adobe.io/graphql`.

Comme [!DNL Live Search] n’a pas accès à la base de données complète des produits, les API [!DNL Live Search] GraphQL et Commerce core GraphQL n’ont pas une parité totale.

Adobe recommande d’appeler directement les API SaaS, en particulier le point d’entrée du service de catalogue.

- Amélioration des performances et réduction de la charge du processeur en contournant le processus Commerce database/Graphql.
- Tirez parti de la fédération [!DNL Catalog Service] pour appeler [!DNL Live Search], [!DNL Catalog Service] et [!DNL Product Recommendations] à partir d’un seul point d’entrée.

Pour certains cas d’utilisation, il peut être préférable d’appeler [!DNL Catalog Service] pour obtenir des détails sur le produit et des cas similaires. Voir [refineProduct](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) pour plus d’informations.

Si vous disposez d’une implémentation découplée personnalisée, consultez les implémentations de référence [!DNL Live Search] :

- [Widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [[!DNL Live Search] champ](https://github.com/adobe/storefront-search-as-you-type)

La collecte automatique des données d’interaction utilisateur ne fonctionne pas par défaut si vous n’utilisez pas les composants standard tels que l’adaptateur de recherche, les widgets Luma ou les widgets AEM CIF. Adobe Sensei utilise ces données collectées pour le marchandisage intelligent et le suivi des performances. Pour résoudre ce problème, vous devez développer une solution personnalisée pour implémenter cette collecte de données en mode découplé.

La dernière version de [!DNL Live Search] utilise déjà [!DNL Catalog Service].

### Prise en charge linguistique

Les widgets [!DNL Live Search] prennent en charge les langues suivantes :

|  |  |  |  |
|--- |--- |--- |--- |
| Langue | Région | Code de langue | Magento Locale |
| Bulgare | Bulgarie | bg_BG | bg_BG |
| Catalan | Espagne | ca_ES | ca_ES |
| Tchèque | République tchèque | cs_CZ | cs_CZ |
| Danois | Danemark | da_DK | da_DK |
| Allemand | Allemagne | de_DE | de_DE |
| Grec | Grèce | el_GR | el_GR |
| Anglais | Royaume-Uni | en_GB | en_GB |
| Anglais | États-Unis | en_US | en_US |
| Espagnol | Espagne | es_ES | es_ES |
| Estonien | Estonie | et_EE | et_EE |
| Basque | Espagne | eu_ES | eu_ES |
| Perse | Iran | fa_IR | fa_IR |
| Finlandais | Finlande | fi_FI | fi_FI |
| Français | France | fr_FR | fr_FR |
| Galicien | Espagne | gl_ES | gl_ES |
| Hindi | Inde | hi_IN | hi_IN |
| Hongrois | Hongrie | hu_HU | hu_HU |
| Indonésien | Indonésie | id_ID | id_ID |
| Italien | Italie | it_IT | it_IT |
| Coréen | Corée du Sud | ko_KR | ko_KR |
| Lituanien | Lituanie | lt_LT | lt_LT |
| Letton | Lettonie | lv_LV | lv_LV |
| Norvégien | Norvège - Bokmal | nb_NO | nb_NO |
| Néerlandais | Pays-Bas | nl_NL | nl_NL |
| Polonais | Pologne | pl_PL | pl_PL |
| Portugais | Brésil | pt_BR | pt_BR |
| Portugais | Portugal | pt_PT | pt_PT |
| Roumain | Roumanie | ro_RO | ro_RO |
| Russe | Russie | ru_RU | ru_RU |
| Suédois | Suède | sv_SE | sv_SE |
| Thaïlandais | Thaïlande | th_TH | th_TH |
| Turc | Turquie | tr_TR | tr_TR |
| Chinois | Chine | zh_CN | zh_Hans_CN |
| Chinois | Taïwan | zh_TW | zh_Hant_TW |

Si le widget détecte que le paramètre Langue d’administration de Commerce correspond à une langue prise en charge, il utilise cette langue par défaut. Dans le cas contraire, le widget est défini par défaut sur Anglais. Dans Admin, le paramètre de langue est configuré en accédant à _[!UICONTROL Stores]_> [!UICONTROL Settings] >_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options].

Les administrateurs peuvent également définir la langue de l’[index de recherche](settings.md#language) pour garantir de meilleurs résultats de recherche.

### Référentiel de code de widget

Le code du widget de page de liste de produits et du widget de champ de [!DNL Live Search] peut être téléchargé à partir de GitHub.

Les développeurs qui ont accès au code peuvent entièrement personnaliser son fonctionnement et son aspect. Ils hébergent le code sur leurs propres serveurs, mais utilisent toujours le service [!DNL Live Search].

- [Widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [ Barre de recherche ](https://github.com/adobe/storefront-search-as-you-type)

### Extension Data Export

Une fois [!DNL Live Search] activé, l’extension d’exportation de données synchronise les données Commerce entre l’application Commerce et [!DNL Live Search]. Ce processus garantit que les données Commerce les plus récentes sont disponibles sur le storefront. Dans l’Administration, vous pouvez vérifier l’état de synchronisation à l’aide du tableau de bord Data Management. Vous pouvez gérer et résoudre les problèmes du processus d’exportation des données à l’aide de l’interface de ligne de commande et des journaux Commerce. Pour plus d’informations, consultez le [ Guide d’exportation de données ](../data-export/overview.md).

### Inventory management

[!DNL Live Search] prend en charge les fonctionnalités [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) dans Commerce (anciennement appelé Multi-Source Inventory, ou MSI). Pour activer la prise en charge complète, vous devez [mettre à jour](install.md#updating-live-search) le module de dépendance `commerce-data-export` à la version 102.2.0+.

[!DNL Live Search] renvoie une valeur de type boolean qui indique si un produit est disponible dans Inventory management, mais ne contient aucune information sur la source qui possède le stock.

### Indexeur de prix

[!DNL Live Search] clients peuvent utiliser l&#39;indexeur de prix [SaaS](../price-index/price-indexing.md), qui offre des mises à jour de changement de prix et une synchronisation plus rapides.

### Prise en charge des prix

Les widgets [!DNL Live Search] prennent en charge la plupart des types de prix pris en charge par Adobe Commerce, mais pas tous.

Actuellement, les prix de base sont soutenus. Les prix avancés non pris en charge sont les suivants :

- Coût
- Prix minimum annoncé

Examinez le [maillage API](../catalog-service/mesh.md) pour des calculs de prix plus complexes.

Le format des prix prend en charge le paramètre de configuration des paramètres régionaux dans l’instance Commerce : *Magasins* > Paramètres > *Configuration* > Général > *Général* > Options locales > Paramètres régionaux.

### Prise en charge du storefront découplé

Vous devrez peut-être installer le module `module-data-services-graphql` qui étend la couverture GraphQL existante de l’application pour inclure les champs requis pour la collecte de données comportementales en storefront.

```bash
composer require magento/module-data-services-graphql
```

Ce module ajoute des contextes supplémentaires aux requêtes GraphQL :

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### Prise en charge B2B

[!DNL Live Search] prend en charge la fonctionnalité [B2B](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview) avec des [limitations](boundaries-limits.md#b2b-and-category-permissions) supplémentaires.

### Prise en charge de PWA

[!DNL Live Search] fonctionne avec PWA Studio, mais les utilisateurs peuvent voir de légères différences par rapport aux autres implémentations de Commerce. Les fonctionnalités de base telles que la recherche et la page de liste de produits fonctionnent dans Venia, mais certaines permutations de Graphql peuvent ne pas fonctionner correctement. Il peut également y avoir des différences de performances.

- L’implémentation PWA actuelle de [!DNL Live Search] nécessite davantage de temps de traitement pour renvoyer les résultats de la recherche qu’une [!DNL Live Search] avec le storefront Commerce natif.
- [!DNL Live Search] dans PWA ne prend pas en charge [la gestion des événements](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Par conséquent, les rapports de recherche et le marchandisage intelligent ne fonctionnent pas sur les vitrines PWA.
- Lors de l&#39;utilisation de [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/), GraphQL ne prend pas en charge le filtrage directement sur `description`, `name`, `short_description`, mais ces champs peuvent être renvoyés avec un filtre plus général.

Pour utiliser [!DNL Live Search] avec PWA Studio, les intégrateurs doivent également :

1. Installez [livesearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
1. Définissez la `environmentId` dans l’objet `storeDetails`.

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### Cookies

[!DNL Live Search] collecte les données d’interaction utilisateur pour améliorer les fonctionnalités de recherche et stocke ces informations dans des cookies de navigateur. Cette collecte de données nécessite le consentement de l’utilisateur lorsque les restrictions de cookie sont activées. [!DNL Live Search] et [!DNL Product Recommendations] partagent le même mécanisme de collecte de données et de gestion des cookies. Pour plus d’informations sur les restrictions relatives aux cookies et la conformité en matière de confidentialité, consultez [Gestion des restrictions sur les cookies](../product-recommendations/setting-cookie.md).
