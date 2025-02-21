---
title: Interface de ligne de commande d'exportation de données SaaS
description: Découvrez comment utiliser les commandes de l’interface de ligne de commande pour gérer les flux et les processus pour les services SaaS  [!DNL data export extension] ’Adobe Commerce.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 0%

---

# Référence de l&#39;interface de ligne de commande d&#39;exportation de données SaaS

Les développeurs et les administrateurs système peuvent gérer les opérations de synchronisation pour l’exportation des données SaaS à l’aide de l’outil de ligne de commande [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI). La commande `saas:resync` est incluse dans le package `magento/saas-export`.

Adobe déconseille d&#39;utiliser régulièrement la commande `saas:resync`. Les scénarios classiques d’utilisation de la commande sont les suivants :

- La synchronisation initiale
- L&#39;identifiant [SaaS Data Space](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) a été modifié et vous devez synchroniser les données avec le nouvel espace de données.
- Dépannage

## Synchronisation initiale

>[!NOTE]
>Si vous utilisez Live Search ou Product Recommendations, il n’est pas nécessaire d’exécuter la synchronisation initiale. Le processus est lancé automatiquement après la connexion du service à votre instance Commerce.

Lorsque vous déclenchez une `saas:resync` à partir de la ligne de commande, en fonction de la taille de votre catalogue, la mise à jour des données peut prendre de quelques minutes à quelques heures.

Pour la synchronisation initiale, Adobe recommande d’exécuter les commandes dans l’ordre suivant :

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

## Exemples de commandes

Avant d’utiliser des commandes `saas:resync`, passez en revue les [ descriptions des options ](#command-options).

- Effectuez une resynchronisation complète pour un flux d’entités.

  ```
  bin/magento saas:resync --feed='<FEED_NAME>' 1
  ```

  Les flux qui ont déjà été exportés avec succès ne sont pas resynchronisés.

- resynchroniser complètement les données de flux et de nettoyage spécifiées

  ```
  bin/magento saas:resync --feed='FEED_NAME' --cleanup-feed
  ```

  À utiliser uniquement après l’exécution d’une opération [!DNL Data Space ID Cleanup].

- Pour les flux d’exportation immédiats, renvoyez toutes les données aux services Commerce connectés sans tronquer les données d’index dans la table des flux

  ```
   bin/magento saas:resync --feed='FEED_NAME' --no-reindex
  ```

- Répertoriez les commandes et options disponibles avec leurs descriptions.

  ```
  bin/magento saas:resync --help
  ```

## Options des commandes

Les options suivantes sont disponibles pour gérer les opérations de `saas:resync`.

>[!NOTE]
>
>La commande `saas:resync` prend également en charge des options avancées pour améliorer les commandes d’exportation de données en augmentant la taille du lot et en ajoutant un traitement multithread. Voir [Personnalisation du traitement des exportations](customize-export-processing.md).

### `feed`

Cette option obligatoire spécifie l’entité de flux à resynchroniser, par exemple `products`.

La valeur de l’option `feed` peut inclure l’un des flux d’entités disponibles :

- `products` : flux de données de produit
- `productAttributes` : flux de données des attributs de produit
- `categories` : flux de données des catégories
- `variants` : flux de données de variations de produit configurable
- `prices` : flux de données des prix des produits
- `categoryPermissions` : flux de données des autorisations de catégorie
- `productOverrides` : flux de données des autorisations de produit
- `inventoryStockStatus` : flux de données de statut du stock de stock
- `scopesWebsite` : sites web avec flux de données magasins et vues de magasin
- `scopesCustomerGroup` : flux de données des groupes de clients et clientes
- `orders` : flux de données des commandes client

Selon les [services Commerce](../landing/saas.md) installés, il se peut que vous disposiez d&#39;un ensemble de flux différent pour la commande `saas:resync`.

### `no-reindex`

Cette option envoie à nouveau les données de catalogue existantes à [!DNL Commerce Services] sans réindexation. Si cette option n’est pas spécifiée, la commande exécute une réindexation complète avant de synchroniser les données.

Le comportement de cette option dépend du mode d’exportation du flux : [ancien ou immédiat](data-synchronization.md#synchronization-modes)

- Pour les flux d’exportation hérités, le processus de synchronisation ne tronque pas les données indexées dans la table des flux. Au lieu de cela, il renvoie toutes les données au service Adobe Commerce.
- Pour les flux d’exportation immédiats, cette option est ignorée si elle est spécifiée. Pour ces flux, le processus de resynchronisation ne tronque pas l’index et ne resynchronise que les mises à jour ou les éléments qui ont précédemment échoué.

### `cleanup`

Cette option nettoie la table de l’indexeur de flux avant une synchronisation. Lorsqu’elle est spécifiée, l’exportation des données SaaS exécute une resynchronisation complète pour le flux spécifié et nettoie toutes les données existantes dans la table de flux.

Adobe recommande de n’utiliser cette commande qu’après avoir effectué l’opération [!DNL Data Space ID Cleanup].

>[!WARNING]
>
>**N’utilisez pas cette option régulièrement**. Cela peut entraîner des problèmes de synchronisation des données dans les services Adobe Commerce. Par exemple, le `delete product event` peut ne pas se propager au service Adobe Commerce si l’option `cleanup` est utilisée.

## Dépannage

Si vous ne voyez pas les données attendues dans les services Commerce connectés, résolvez les problèmes en vérifiant les journaux d’erreurs d’exportation des données et en utilisant la commande `saas:resync` avec des variables d’environnement pour passer en revue les payloads et les données de profil. Voir [Vérification des journaux et dépannage](troubleshooting-logging.md).
