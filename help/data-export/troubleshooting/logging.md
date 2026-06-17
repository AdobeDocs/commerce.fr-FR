---
title: Consulter les journaux et résoudre les problèmes
description: Découvrez comment résoudre les erreurs  [!DNL data export]  l’aide des journaux data-export et saas-export .
autotag-review: '2026-06-17T15:08:59.000Z'
feature: Services
exl-id: d022756f-6e75-4c2a-9601-31958698dc43
TQID: https://experienceleague.adobe.com/PkV4L0RpfA-jeja0Fd6JCDriE6wwjd25Qou0JhG5o8E
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 1007
ht-degree: 0%

---

# Consulter les journaux et résoudre les problèmes

L’extension [!DNL data export] fournit des journaux pour suivre les processus de collecte de données et de synchronisation.

>[!NOTE]
>
>Vous pouvez également suivre l’intégrité et les performances des flux d’exportation de données pour les données de produit et de catégorie à partir du tableau de bord [Statut de synchronisation des flux de données](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) dans Admin.

## Logs

Les journaux sont disponibles dans le répertoire `var/log` du serveur d’applications Commerce.

| nom du journal | nom de fichier | description |
|-----------------| ----------| -------------|
| Log d&#39;export de données SaaS | `commerce-data-export.log` | Fournit des informations sur les activités d’exportation de données, telles que les événements d’entité et les déclencheurs de resynchronisation complète.  Chaque enregistrement de journal possède une structure spécifique et fournit des informations sur le flux, l’opération, le statut, le temps écoulé, l’ID de processus et l’appelant. |
| Journal des erreurs d&#39;export des données SaaS | `data-export-errors.log` | Fournit des messages d’erreur et des traces de pile pour les erreurs qui se produisent pendant le processus de synchronisation des données. |
| Log d&#39;export SaaS | `saas-export.log` | Fournit des informations sur les données envoyées aux services SaaS de Commerce. |
| Journal des erreurs d&#39;export SaaS | `saas-export-errors.log` | Fournit des informations sur les erreurs qui se produisent lors de l’envoi de données aux services SaaS Commerce. |

Si vous ne voyez pas les données attendues pour un service Adobe Commerce, utilisez les journaux d’erreurs de l’extension d’exportation des données pour déterminer où le problème s’est produit. Vous pouvez également étendre les journaux avec des données supplémentaires pour le suivi et le dépannage. Voir [Journalisation étendue](#extended-logging).

### Format du log

Chaque enregistrement de journal présente la structure suivante.

```text
[<log record datetime>] report.<log level>:
{
   "feed": "<feed name>",
   "operation": "<executed operation>",
   "status": "<status of operation>",
   "elapsed": "<time elapsed from script run>",
   "pid": "<process id that executed `operation`>",
   "caller": "<who called this `operation`>"
} [] []
```

>[!NOTE]
>
>La chaîne basée sur JSON est enrichie pour une meilleure lisibilité.

Le tableau suivant décrit les types d’opérations qui peuvent être enregistrés dans les journaux.

| Fonctionnement | Description | Exemple d’appelant |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|
| synchronisation complète | Collecte et envoie toutes les données au SaaS pour un flux donné. | `bin/magento saas:resync --feed=products` |
| réindexation partielle | Collecte et envoie des données au SaaS pour les entités mises à jour uniquement dans un flux donné. Ce journal est présent uniquement s’il existe des entités mises à jour. | `bin/magento cron:run --group=index` |
| réessayer les éléments ayant échoué | Renvoyez les éléments d’un flux donné à SaaS si l’opération de synchronisation précédente a échoué en raison d’une erreur de serveur ou d’application Commerce. Ce journal n’est présent que si des éléments ayant échoué existent. | `bin/magento cron:run --group=saas_data_exporter` (tout groupe cron « *_data_exportateur ») |
| synchronisation complète (héritée) | Collecte et envoie toutes les données au SaaS pour un flux donné en mode d’exportation hérité. | `bin/magento saas:resync --feed=categories` |
| réindexation partielle (héritée) | Envoie les entités mises à jour au SaaS pour un flux donné en mode d’exportation hérité. Ce journal est présent uniquement s’il existe des entités mises à jour. | `bin/magento cron:run --group=index` |
| synchronisation partielle (héritée) | Envoie les entités mises à jour au SaaS pour un flux donné en mode d’exportation hérité. Ce journal est présent uniquement s’il existe des entités mises à jour. | `bin/magento cron:run --group=saas_data_exporter` (tout groupe cron « *_data_exportateur ») |


### Exemples de journalisation

Lors d’une resynchronisation complète, la progression est suivie et consignée toutes les 30 secondes par défaut. Voici un exemple d’entrée de journal.

```json
{
   "feed": "prices",
   "operation": "full sync",
   "status": "Progress: 2/5, processed: 200, synced: 100",
   "elapsed": "00:00:00 190 ms",
   "pid": "12824",
   "caller": "bin/magento saas:resync --feed=products"
}
```

Dans cet exemple, les valeurs `status` fournissent des informations sur l’opération de synchronisation :

- **`"Progress 2/5"`** indique que 2 itérations sur 5 ont été terminées. Le nombre d’itérations dépend du nombre d’entités exportées.
- **`"processed: 200"`** indique que 200 éléments ont été traités.
- **`"synced: 100"`** indique que 100 articles ont été envoyés à SaaS. On s’attend à ce que `"synced"` ne soit pas égal à `"processed"`. Voici un exemple :
   - **`"synced" < "processed"`** signifie que la table de flux n’a détecté aucune modification dans l’élément, par rapport à la version synchronisée précédemment. Ces éléments sont ignorés pendant l’opération de synchronisation.
   - **`"synced" > "processed"`** même id d’entité (par exemple, `Product ID`) peut avoir plusieurs valeurs dans différentes portées. Par exemple, un produit peut être attribué à cinq sites web. Dans ce cas, il se peut que vous ayez « 1 élément traité » et « 5 éléments synchronisés ».

+++ **Exemple : journal de resynchronisation complet pour le flux de prix**

```text
Price feed full resync:

[2024-03-05T21:00:51.754687+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Initialize","elapsed":"383 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.803178+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Creating batch table `catalog_data_exporter_product_prices_index_batches`. Start position: 30515","elapsed":"434 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.851878+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Batch table `catalog_data_exporter_product_prices_index_batches` created. Total Items: 500, batches: ~1","elapsed":"482 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:51.852548+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"start processing `500` items in `1` threads with `500` batch size","elapsed":"483 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:52.288369+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 0","elapsed":"919 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.994249+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Progress 1\/1, processed 500, synced 100","elapsed":"00:00:02 625 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
[2024-03-05T21:00:53.995168+00:00] report.INFO: {"feed":"prices","operation":"full sync","status":"Complete","elapsed":"00:00:02 626 ms","pid":"14469","caller":"bin\/magento saas:resync --feed=prices"} [] []
```

+++

## Affichage et résolution des problèmes liés aux journaux avec New Relic

Si vous stockez les journaux Adobe Commerce dans le New Relic, vous pouvez ajouter des règles d’analyse pour améliorer la lisibilité et l’expérience des requêtes.

1. Connectez-vous à New Relic.

1. Accédez à `Logs => Parsing`.

1. Cliquez sur `Create parsing rule`.

1. Configurez la règle d’analyse en ajoutant les valeurs suivantes.

   - **Filtrer les journaux en fonction de NRQL**

     `filePath LIKE '%commerce-data-export%.log'`

   - **Règle d&#39;analyse**

     `\[%{DATA:timestamp}\] report.%{DATA:logLevel}: %{GREEDYDATA:feed:json}`

Cet exemple ajoute une règle qui vous permet d’interroger les journaux New Relic par type de flux spécifique, opération, etc.

**Exemple de chaîne de requête**—`feed.feed:"products" and feed.status:"Complete"`

## Dépannage

Si des données sont manquantes ou incorrectes dans les services Commerce, recherchez dans les journaux les messages d’erreur relatifs à la synchronisation entre Adobe Commerce et la plateforme des services Commerce. Si nécessaire, utilisez la journalisation étendue pour ajouter des informations supplémentaires aux journaux à des fins de dépannage.

- Le journal des erreurs d’exportation des données (`commerce-data-export-errors.log`) capture les erreurs qui se produisent pendant la phase de collecte.
- Le journal des erreurs d’exportation SaaS (`saas-export-errors.log`) capture les erreurs qui se produisent pendant la phase de transmission.

Si vous rencontrez des erreurs non liées à la configuration ou aux extensions tierces, envoyez un [ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) avec autant d’informations que possible.

### Résolution des problèmes de synchronisation des catalogues {#resolvesync}

Pour la résolution des problèmes de synchronisation de catalogue (notamment les incohérences des données, la synchronisation non exécutée et le statut de synchronisation en échec), consultez la section [Dépannage des scénarios](troubleshooting-scenarios.md).

## Journalisation étendue

Utilisez des variables d’environnement pour étendre les journaux avec des données supplémentaires à des fins de suivi et de dépannage. Ajoutez la variable d’environnement à la ligne de commande lorsque vous exécutez les commandes de l’interface de ligne de commande d’exportation des données, comme illustré dans les exemples suivants.

### Vérifier la payload du flux

Incluez la payload du flux dans le journal d’exportation SaaS en ajoutant la variable d’environnement `EXPORTER_EXTENDED_LOG=1` lorsque vous resynchronisez le flux.

```shell
EXPORTER_EXTENDED_LOG=1 bin/magento saas:resync --feed=products
```

Une fois l’opération terminée, la payload de flux peut être consultée dans le journal d’exportation SaaS (`var/.log/saas-export.log`).

### Conserver la payload dans la table d’index de flux

Pour l’extension d’exportation de données SaaS Commerce (`magento/module-data-exporter`) 103.3.0 et versions ultérieures, les flux d’exportation immédiats conservent uniquement les données minimales requises dans la table d’index. Les flux comprennent tous les flux de statut du stock de catalogue et d’inventaire.

La conservation des données de payload dans la table d’index n’est pas recommandée dans les environnements de production, mais elle peut s’avérer utile dans un environnement de développement. Incluez la payload du flux dans l’index en ajoutant la variable d’environnement `PERSIST_EXPORTED_FEED=1` lorsque vous resynchronisez le flux.

```shell
PERSIST_EXPORTED_FEED=1 bin/magento saas:resync --feed=products
```

### Exécutez le profileur pour résoudre les problèmes de performances lentes.

Si le processus de réindexation d’un flux spécifique prend un temps déraisonnable, exécutez le profileur pour collecter des données supplémentaires qui peuvent être utiles à l’équipe d’assistance.

Exécutez le profileur en ajoutant la variable d’environnement `EXPORTER_PROFILER=1` lorsque vous exécutez la commande de réindexation.

```shell
EXPORTER_PROFILER=1 bin/magento indexer:reindex catalog_data_exporter_products
```

Les données du profileur sont stockées dans le journal d’exportation des données (`var/log/commerce-data-export.log`) au format suivant :

```text
<Provider class name>, <# of processed entities>, <execution time im ms>, <memory consumption in Mb>
```

>[!MORELIKETHIS]
>
> - [Scénarios de dépannage &#x200B;](troubleshooting-scenarios.md) — Résolvez les problèmes de synchronisation des catalogues et les incohérences entre les données.
> - [Référence des codes journaux](log-codes-reference.md) — Recherchez les codes journaux d&#39;exportation.
> - [Synchroniser les flux à l’aide de l’interface de ligne de commande Commerce](../data-export-cli-commands.md) — Exécuter les resynchronisations des flux ciblés.
