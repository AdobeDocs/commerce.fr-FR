---
title: Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce
description: Découvrez comment utiliser les commandes de l’interface de ligne de commande pour gérer les flux et les processus pour les services SaaS  [!DNL data export extension] ’Adobe Commerce.
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
source-git-commit: 086a571b69e8ad76a912c339895409b0037642b9
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---

# Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce

La commande `saas:resync` du package `magento/saas-export` permet de gérer la synchronisation des données pour les services SaaS Adobe Commerce.

Adobe déconseille d&#39;utiliser régulièrement la commande `saas:resync`. Les scénarios classiques d’utilisation de la commande sont les suivants :

- Synchronisation initiale
- Synchronisez les données avec le nouvel espace de données après avoir modifié l’identifiant [SaaS Data Space](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Dépannage

Surveillez les opérations de synchronisation dans le fichier `var/log/saas-export.log`.

## Synchronisation initiale

>[!NOTE]
>
>La synchronisation initiale s’exécute automatiquement lorsque Live Search ou les recommandations de produits sont activées. Les commandes manuelles ne sont pas nécessaires.

Lorsque vous déclenchez une `saas:resync` à partir de la ligne de commande, en fonction de la taille de votre catalogue, la mise à jour des données peut prendre de quelques minutes à quelques heures.

Pour la synchronisation initiale, Adobe recommande d’exécuter les commandes dans l’ordre suivant :

```shell
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

## Synchronisation à l’aide des commandes de l’interface de ligne de commande

La commande `saas:resync` prend en charge diverses opérations de synchronisation :

- Synchronisation partielle par SKU
- Reprise des synchronisations interrompues
- Valider les données sans synchronisation

Afficher toutes les options disponibles :

```shell
bin/magento saas:resync --help
```

Consultez les sections suivantes pour obtenir une description des options ainsi que des exemples.


>[!NOTE]
>
>Pour obtenir des options avancées de gestion du traitement des exportations, voir [ Personnaliser le traitement des exportations ](customize-export-processing.md).

## `--by-ids`

Resynchronisez partiellement des entités spécifiques en fonction de leurs identifiants. Prend en charge les flux `products`, `productAttributes` et `productOverrides`.

Par défaut, les entités sont spécifiées par SKU du produit. Utilisez `--id-type=ProductID` pour utiliser à la place les ID de produit.

**Exemples :**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<SKU-1>,<SKU-2>,<SKU-3>'

bin/magento saas:resync --feed='<FEED_NAME>' --by-ids='<ID-1>,<ID-2>,<ID-3>' --id-type='productId'
```

## `--cleanup-feed`

Nettoie la table de l’indexeur de flux avant de réindexer et d’envoyer des données au SaaS. Pris en charge uniquement pour les flux `products`, `productOverrides` et `prices`.

>[!IMPORTANT]
>
>À utiliser uniquement après le nettoyage de l’environnement. Peut entraîner des problèmes de synchronisation des données dans les services Commerce.

**Exemple:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --cleanup-feed
```

## `--continue-resync`

Reprend une opération de resynchronisation interrompue. Pris en charge uniquement pour les flux `products`, `productAttributes` et `productOverrides`.

**Exemple:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --continue-resync
```

## `--dry-run`

Exécute le processus de réindexation des flux sans effectuer d’envoi en SaaS ni enregistrer dans la table des flux. Permet de valider les données.

Ajoutez la variable d’environnement `EXPORTER_EXTENDED_LOG=1` pour enregistrer la payload dans `var/log/saas-export.log`.

**Exemple:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed='<FEED_NAME>' --dry-run
```

## `--feed`

Obligatoire. Indique l’entité de flux à resynchroniser.

Flux disponibles :

- `categories`
- `categoryPermissions`
- `inventoryStockStatus`
- `orders`
- `prices`
- `products`
- `productAttributes`
- `productOverrides`
- `scopesWebsite`
- `scopesCustomerGroup`
- `variants`

**Exemple:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>'
```

## `--no-reindex`

Envoie à nouveau les données de catalogue existantes à [!DNL Commerce Services] sans réindexation. Non pris en charge pour les flux liés au produit.

Le comportement varie selon le [mode d’exportation](data-synchronization.md#synchronization-modes) :

- Mode hérité : renvoie toutes les données sans les tronquer.
- Mode immédiat : l’option est ignorée et ne synchronise que les mises à jour/échecs.

**Exemple:**

```shell
bin/magento saas:resync --feed='<FEED_NAME>' --no-reindex
```

## Dépannage

Si vous ne voyez pas les données attendues dans les services Commerce connectés, résolvez les problèmes en vérifiant les journaux d’erreurs d’exportation des données et en utilisant la commande `saas:resync` avec des variables d’environnement pour passer en revue les payloads et les données de profil. Voir [Vérification des journaux et dépannage](troubleshooting-logging.md).
