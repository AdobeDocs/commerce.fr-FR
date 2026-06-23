---
title: Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce
description: Découvrez comment utiliser les commandes de l’interface de ligne de commande de Commerce pour gérer les flux et synchroniser les processus pour les services SaaS d [!DNL data export extension] Adobe Commerce.
autotag-review: '2026-06-17T15:08:59.000Z'
exl-id: 1ebee09e-e647-4205-b90c-d0f9d2cac963
TQID: 'https://experienceleague.adobe.com/Vi8hMKOBjTPkSQp0t8DCkjZsJ8s3Q5GSbSXyX2gmWRo'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: ef1a9efc579d8d21c145e6981235489a2e4ea203
workflow-type: tm+mt
source-wordcount: 728
ht-degree: 0%

---

# Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce

La commande `saas:resync` du package `magento/saas-export` permet de gérer la synchronisation des données pour [!DNL Adobe Commerce] services SaaS.

>[!NOTE]
>
>La commande `saas:resync` s’applique également aux flux [!DNL Adobe Commerce Optimizer Connector] tels que `products`, `categories` et `priceBooks`. Consultez [Flux pris en charge](../aco-connector/reference/connector-reference.md#supported-feeds) pour obtenir la liste complète des flux de connecteur et des noms d’indexeur.

Adobe déconseille d&#39;utiliser régulièrement la commande `saas:resync`. Les scénarios classiques d’utilisation de la commande sont les suivants :

- Synchronisation initiale
- Synchronisez les données avec un nouvel espace de données après avoir modifié l’identifiant de l’espace de données [SaaS](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas)
- Dépannage

Surveillez les opérations de synchronisation dans le fichier `var/log/saas-export.log`.

## Synchronisation initiale

>[!NOTE]
>
>La synchronisation initiale s’exécute automatiquement lorsque Live Search ou les recommandations de produits sont activées. Les commandes manuelles ne sont pas nécessaires.
>
>Pour les déploiements [!DNL Adobe Commerce Optimizer Connector], la commande `aco:config:init` planifie la synchronisation complète initiale en invalidant tous les indexeurs de flux du connecteur. Voir [Activation de l’intégration  [!DNL Commerce Optimizer]  &#x200B;](../aco-connector/get-started.md#enable-the-adobe-commerce-optimizer-integration) et [Gestion de la synchronisation vers [!DNL Commerce Optimizer]](../aco-connector/data-sync-manage.md).

Lorsque vous déclenchez une `saas:resync` à partir de la ligne de commande, en fonction de la taille de votre catalogue, la mise à jour des données peut prendre de quelques minutes à quelques heures.

Les synchronisations de flux peuvent être exécutées dans n’importe quel ordre ; il n’existe aucune dépendance matérielle entre elles. La séquence suivante commence par les données de la portée en premier, ce qui est un point de départ logique puisque les portées définissent les vues du magasin auxquelles les autres flux font référence.

```shell
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed productAttributes
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed products
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed productoverrides
```

>[!NOTE]
>
>Votre environnement peut ne pas inclure tous les flux de cette séquence. Voir [Flux pris en charge](reference/feed-table-reference.md#supported-feeds) pour obtenir la liste complète des flux, les noms des flux de l’interface de ligne de commande et les exigences des modules.

## Options des commandes

La commande `saas:resync` prend en charge diverses opérations de synchronisation :

- Synchronisation partielle par SKU
- Reprise des synchronisations interrompues
- Valider les données sans synchronisation

Afficher toutes les options de commande et les indicateurs :

```shell
bin/magento saas:resync --help
```

Consultez les sections suivantes pour obtenir une description des options ainsi que des exemples.

>[!NOTE]
>
>Pour obtenir des options avancées de gestion du traitement des exportations, voir [&#x200B; Personnaliser le traitement des exportations &#x200B;](customize-export-processing.md).

## `--feed`

Obligatoire. Indique l’entité de flux à resynchroniser.

Options de commande et indicateurs des documents `bin/magento saas:resync --help`. Il ne répertorie pas tous les flux disponibles dans votre environnement. Pour obtenir la liste complète des flux avec les noms de flux de l’interface de ligne de commande, les ID d’indexeur et les tableaux de flux, voir [Flux pris en charge](reference/feed-table-reference.md#supported-feeds).

>[!NOTE]
>
>Les modules installés déterminent les flux que vous pouvez resynchroniser. Par exemple, `productOverrides` nécessite une [!DNL Adobe Commerce] sur le cloud, sur site ou Commerce as a Cloud Service, et `orders` nécessite le module Commandes client.

>[!NOTE]
>
>La commande `saas:resync` transmet uniquement les nouveaux éléments, les éléments mis à jour et les éléments dont l’exportation a échoué précédemment. Les éléments dont le hachage du contenu n’a pas changé depuis la dernière exportation sont ignorés.

**Exemple:**

```shell
bin/magento saas:resync --feed products
```

## `--by-ids`

Resynchronisez partiellement des entités spécifiques en fonction de leurs identifiants. Prend en charge les flux `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` et `categoryPermissions`.

Par défaut, lorsque vous utilisez l’option `--by-ids` , vous spécifiez des valeurs à l’aide des valeurs de SKU du produit. Pour utiliser des ID de produit à la place, ajoutez l’option `--id-type=productId` .

>[!NOTE]
>
>Contrairement à une resynchronisation standard, `--by-ids` contourne la vérification de hachage et force les entités spécifiées à être envoyées aux services Commerce connectés, que leur contenu ait ou non changé depuis la dernière exportation.

**Exemples :**

```shell
bin/magento saas:resync --feed products --by-ids='ADB102,ADB111,ADB112'

bin/magento saas:resync --feed products --by-ids='1,2,3' --id-type='productId'
```

## `--cleanup-feed`

Nettoyez la table de l’indexeur de flux avant de réindexer et d’envoyer des données au SaaS. Pris en charge uniquement pour `products`, `productAttributes`, `productOverrides`, `inventoryStockStatus`, `prices`, `variants` et `categoryPermissions`.

Si elle est utilisée avec l’option `--dry-run` , l’opération effectue une opération de resynchronisation d’essai pour tous les éléments.

>[!WARNING]
>
>L’utilisation de la commande resync avec l’option `cleanup-feed` efface l’état d’exportation du flux local et peut entraîner une synchronisation incomplète. Par exemple, les suppressions d’entités dans [!DNL Adobe Commerce] peuvent ne pas être reflétées dans les services Commerce connectés, ou les entités obsolètes peuvent rester dans les index des services Commerce distants même si elles ont été supprimées ou mises à jour dans [!DNL Adobe Commerce]. N’utilisez cette option que pour les reconstructions complètes de l’environnement, par exemple après un nettoyage de l’espace de données SaaS.

**Exemple:**

```shell
bin/magento saas:resync --feed products --cleanup-feed
```

## `--continue-resync`

Reprend une opération de resynchronisation interrompue. Pris en charge uniquement pour les flux `products`, `productAttributes` et `productOverrides`.

**Exemple:**

```shell
bin/magento saas:resync --feed productAttributes --continue-resync
```

## `--dry-run`

Exécute le processus de réindexation des flux sans envoyer le flux à SaaS et sans enregistrer dans la table des flux. Cette option est utile pour identifier les problèmes éventuels liés à votre jeu de données.

Ajoutez la variable d’environnement `EXPORTER_EXTENDED_LOG=1` pour enregistrer la payload dans `var/log/saas-export.log`.

**Exemple:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run
```

### Test d’éléments de flux spécifiques

Testez des éléments de flux spécifiques en ajoutant l’option `--by-ids` avec la collection de journaux étendue pour afficher la payload générée dans le fichier `var/log/saas-export.log`.

**Exemple:**

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed products --dry-run --by-ids='ADB102,ADB111,ADB112'
```

### Tester tous les éléments de flux

Par défaut, le flux envoyé au cours d’une opération de `resync --dry-run` ne comprend que les nouveaux éléments ou les éléments dont l’exportation a échoué précédemment. Pour inclure tous les éléments du flux à traiter, utilisez l’option `--cleanup-feed` .

**Exemple:**

```shell
bin/magento saas:resync --feed products --dry-run --cleanup-feed
```

## `--no-reindex`

Envoie à nouveau les données de catalogue existantes à [!DNL Commerce Services] sans réindexation. Non pris en charge pour les flux liés au produit.

Le comportement varie selon le [mode d’exportation](sync-overview.md#synchronization-modes) :

- Mode hérité : renvoie toutes les données sans les tronquer.
- Mode immédiat : l’option est ignorée et ne synchronise que les mises à jour/échecs.

**Exemple:**

```shell
bin/magento saas:resync --feed productAttributes --no-reindex
```

>[!MORELIKETHIS]
>
> - [Consulter les journaux et résoudre les problèmes](troubleshooting/logging.md) — Diagnostiquer les erreurs d&#39;exportation de données et d&#39;exportation SaaS.
> - [Scénarios de dépannage &#x200B;](troubleshooting/troubleshooting-scenarios.md) — Résolvez les erreurs de configuration et les résultats de synchronisation inattendus.
> - [Fonctionnement de la synchronisation &#x200B;](sync-overview.md) — Découvrez les modes de synchronisation et le comportement des nouvelles tentatives.
