---
title: Synchroniser les données avec l'export de données SaaS
description: Découvrez comment le collecte et synchronise  [!DNL SaaS Data Export]  données entre les instances Adobe Commerce et les services SaaS connectés.
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: ae672ed3f2693e2f14e8c7f379e59ef117a34fc3
workflow-type: tm+mt
source-wordcount: '880'
ht-degree: 0%

---

# Synchroniser les données avec l&#39;export de données SaaS

Lorsque vous installez un service Commerce qui nécessite l’exportation de données, tel que Catalog Service, Live Search ou Product Recommendations, une collection de modules d’exportation de données Saas est installée pour gérer le processus de collecte de données et de synchronisation.

L’exportation des données SaaS déplace régulièrement les données de produit d’une instance Adobe Commerce vers la plateforme Commerce Services afin de maintenir les données à jour. Par exemple, Recommandations de produits nécessite des informations de catalogue actuelles pour renvoyer avec précision des recommandations aux noms, prix et disponibilité corrects. Utilisez le tableau de bord [Data Management](https://experienceleague.adobe.com/fr/docs/commerce/user-guides/data-services/catalog-sync) pour observer et gérer le processus de synchronisation ou l’interface de ligne de commande pour déclencher une synchronisation et réindexer les données de produit pour leur consommation par les services Commerce.

Le diagramme suivant illustre le flux d’exportation des données SaaS.

![Collecte de données d&#39;export SaaS et flux de synchronisation pour Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

Les principaux composants du flux d&#39;exportation de données SaaS sont les suivants :

- Modules d’exportation de données SaaS qui collectent les données pour les flux d’Adobe Commerce, assemblent les éléments des flux, écoutent les mises à jour et conservent le statut des flux.
- Les modules SaaS exportent les données, configurent le routage et publient les flux vers les services connectés.
- Le service Adobe Commerce gère le processus d’ingestion des données pour valider les flux entrants et conserver les mises à jour des services connectés.

>[!NOTE]
>
>Pour garantir une planification fluide et éviter toute perturbation du fonctionnement du site, Adobe recommande d’estimer le volume de données et l’heure de synchronisation avant de démarrer la synchronisation des flux de données. Cette estimation est importante lors de la planification de synchronisations initiales ou de mises à jour de catalogue à grande échelle, telles que des modifications de prix en masse. Pour plus d’informations, voir [&#x200B; Estimation du volume de données et de la durée de transmission pour la synchronisation des données](estimate-data-volume-sync-time.md)

## Modes de synchronisation

L’exportation des données SaaS comporte deux modes de traitement des flux d’entités :

- **Mode d’exportation immédiat** : dans ce mode, les données sont collectées et envoyées immédiatement au service Commerce en une seule itération. Ce mode accélère la diffusion des mises à jour d’entités au service Commerce et réduit la taille de stockage des tables de flux.

- **Mode d’exportation hérité** : dans ce mode, les données sont collectées dans un seul processus. Ensuite, une tâche cron envoie les données collectées aux services commerciaux connectés. Dans les entrées du journal d’exportation de données, les flux qui utilisent le mode hérité sont étiquetés `(legacy)`.

## Types de synchronisation

L&#39;exportation de données SaaS prend en charge trois types de synchronisation : synchronisation complète, synchronisation partielle et synchronisation des éléments ayant échoué à une nouvelle tentative.

### Synchronisation complète

Après la connexion d’une instance Adobe Commerce au service Commerce, effectuez une synchronisation complète pour envoyer des données de flux d’entités d’Adobe Commerce au service connecté.

>[!NOTE]
>
>La synchronisation complète est principalement destinée à la phase d’intégration. Évitez de l’utiliser régulièrement pour éviter la surcharge de la base de données. Après la synchronisation initiale, les modifications en cours sont automatiquement synchronisées à l’aide d’une synchronisation partielle.

### Synchronisation partielle

Avec une synchronisation partielle, l’exportation de données SaaS envoie automatiquement des mises à jour depuis l’application Commerce, telles que des modifications de nom de produit ou de prix, aux services commerciaux connectés.

Le processus d’exportation des données utilise les tâches cron suivantes pour automatiser l’opération de synchronisation partielle.

- tâches de groupe cron « index » :
   - La tâche `indexer_reindex_all_invalid` réindexe tous les flux non valides. Il s’agit d’une tâche cron Adobe Commerce standard.
   - La tâche `saas_data_exporter` concerne les flux d’exportation hérités.
   - La tâche `sales_data_exporter` est spécifique au flux d’exportation des données de vente.

Ces tâches s’exécutent toutes les minutes.

Pour que la synchronisation partielle fonctionne, l’application Commerce nécessite la configuration suivante :

- [La planification des tâches est activée via les tâches cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=fr)

- Tous les indexeurs d&#39;export de données SaaS sont configurés en mode `Update by Schedule`.

  Dans la version 103.1.0 et les versions ultérieures de l’exportation des données SaaS, le mode `Update by Schedule` est activé par défaut. Vous pouvez vérifier la configuration de l’index sur le serveur à l’aide de la commande Commerce CLI, `bin/magento indexer:show-mode | grep -i feed`

### Réessayer la synchronisation des éléments ayant échoué

La synchronisation des éléments en échec de la reprise utilise un processus distinct pour renvoyer les éléments qui n’ont pas pu être synchronisés en raison d’erreurs lors du processus de synchronisation, par exemple une erreur d’application, une interruption de réseau ou une erreur de service SaaS. L’implémentation de cette synchronisation repose également sur les tâches cron.

- `resync_failed_feeds_data_exporter` tâches du groupe cron :
   - La tâche `<feed name>_feed_resend_failed_feeds_items` renvoie les éléments dont la synchronisation a échoué, par exemple `products_feed_resend_failed_items`.

### Afficher et gérer le processus de synchronisation

La plupart des activités de synchronisation sont traitées automatiquement en fonction de la configuration de l’application. Cependant, l’exportation de données SaaS fournit également des outils pour gérer le processus.

- Les utilisateurs administrateurs peuvent afficher et suivre la progression de la synchronisation et obtenir des informations sur les données à partir du tableau de bord [Data Management](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard).

- Les développeurs, les intégrateurs système ou les administrateurs ayant accès au serveur d’applications Commerce peuvent gérer le processus de synchronisation et les flux de données à l’aide de l’outil de ligne de commande (CLI) Adobe Commerce. Voir [&#x200B; Gérer les opérations de synchronisation à l’aide de l’interface de ligne de commande Commerce](data-export-cli-commands.md).

### Vérification de la configuration de l’application Commerce

La synchronisation partielle et la synchronisation des éléments ayant échoué une nouvelle tentative ne fonctionnent que si l’instance Commerce a été correctement configurée. En règle générale, la configuration est effectuée lors de la configuration du service Commerce. Si l’exportation des données ne fonctionne pas correctement, vérifiez la configuration suivante.

- [Vérifiez que les tâches cron sont en cours d’exécution](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- Vérifiez que les indexeurs s’exécutent à partir de l’[Admin](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/tools/index-management) ou à l’aide de la `bin/magento indexer:info` de commande de l’interface de ligne de commande Commerce.

- Vérifiez que les indexeurs des flux suivants sont définis sur `Update by Schedule` : Attributs de catalogue, Produit, Remplacements de produit et Variante de produit. Vous pouvez vérifier les indexeurs à partir de [Gestion des index](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/tools/index-management) dans l’interface administrateur ou à l’aide de l’interface de ligne de commande (`bin/magento indexer:show-mode | grep -i feed`).

### Notifications du gestionnaire d’événements pour la journalisation du transfert de données

Dans les versions 103.3.4 et ultérieures, l’exportation de données SaaS distribue l’événement `data_sent_outside` lorsque des données sont envoyées de l’instance Commerce aux services Adobe Commerce.

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>Pour plus d’informations sur les événements et sur la manière de s’y abonner, consultez [Événements et observateurs](https://developer.adobe.com/commerce/php/development/components/events-and-observers) dans la documentation destinée aux développeurs Adobe Commerce.
