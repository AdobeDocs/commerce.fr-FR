---
title: Configuration de ligne de commande
description: Après l’installation, vous pouvez configurer à l [!DNL Payment Services] aide de l’interface de ligne de commande (CLI).
role: Admin, Developer
level: Intermediate
feature: Payments, Checkout, Configuration, Integration
exl-id: bb59bd49-6ecd-4ef1-a6b9-e1e93db04bf6
source-git-commit: 24622b8a20b8cd95e13a68df6e0929206ffbb06b
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Configuration de ligne de commande

Après l’installation de [!DNL Payment Services], vous pouvez facilement le configurer à partir de [à la maison](payments-home.md) ou via l’interface de ligne de commande (CLI).

## Configurer l’export des données

[!DNL Payment Services] combine les données de commande exportées depuis [!DNL Magento Open Source] et [!DNL Adobe Commerce] avec les données de paiement agrégées des fournisseurs de paiement pour créer des rapports utiles. L’extension [!DNL Payment Services] utilise des indexeurs pour collecter efficacement toutes les données nécessaires aux rapports.

Pour en savoir plus sur les données utilisées dans [!DNL Payment Services] reporting, voir [Etat du statut du paiement des commandes](order-payment-status.md#data-used-in-the-report).

### Configuration de cron sur [!DNL Magento Open Source]

Si vous souhaitez utiliser un mode d’index `BY SCHEDULE` sur [!DNL Magento Open Source], vous devez configurer cron. Voir [Configuration et exécution de cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs).

### Définition des indexeurs

Les données de commande sont exportées et conservées dans le service de paiement, à l’aide de l’un des deux modes d’index suivants : `ON SAVE` (par défaut) ou `BY SCHEDULE` (recommandé).

Les index suivants sont pour [!DNL Payment Services] :

| Code | Nom | Description |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | Flux de commande client | Construit l’index des données de commande |
| `sales_order_status_data_exporter` | Flux des statuts de commande client | Construit l&#39;index des données de statut des commandes client |
| `store_data_exporter` | Flux des magasins | Construit l’index des données du magasin |

Pour modifier le mode d’index pour les trois indexeurs, exécutez :

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>Si vous ne spécifiez aucun indexeur dans votre commande, tous les indexeurs sont mis à jour vers la même valeur. Si vous souhaitez modifier un indexeur spécifique, vous devez le répertorier dans votre commande.

Pour en savoir plus sur la modification manuelle du mode d’un indexeur, consultez [Configuration des indexeurs](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"} dans la documentation du développeur. Pour savoir comment le modifier dans l’administration, consultez [Gestion des index](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"} dans le guide d’utilisation principal.

### Réindexation manuelle des données

Vous pouvez réindexer manuellement les données, au lieu d’attendre qu’elles se produisent automatiquement. Pour plus d’informations, consultez [Réindexation](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"} dans [Gestion des indexeurs](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"}.

Lorsque `BY SCHEDULE` mode est défini, le système suit les entités modifiées et la tâche cron met à jour l’index de ces entités selon un planning défini. Voir [Exécuter cron à partir de la ligne de commande](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run) dans [Configurer et exécuter cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)) pour savoir comment déclencher manuellement l’indexation à l’aide de tâches cron.

### Envoyer les données réindexées au service de paiement

Une fois les données indexées, elles sont envoyées automatiquement à [!DNL Payment Services]. Vous pouvez également déclencher manuellement le processus d’envoi des données indexées avec cette commande :

```bash
bin/magento saas:resync --feed [feedName]
```

Utilisez les options de commande suivantes :

| Commande | Description |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | Effectue une réindexation du flux spécifié et l’envoie au service correspondant |
| `bin/magento saas:resync --no-reindex` | Ignore l’indexation et envoie des données non synchronisées depuis les index |

Le paramètre `--feed` vous permet de spécifier le flux à envoyer :

| Flux | Description |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | Flux de commandes en mode Production |
| `paymentServicesOrdersSandbox` | Flux de commandes en mode Sandbox |
| `paymentServicesOrderStatusesProduction` | Statuts des commandes en mode Production |
| `paymentServicesOrderStatusesSandbox` | Statuts de commande en mode Sandbox |
| `paymentServicesStoresProduction` | Magasins en mode Production |
| `paymentServicesStoresSandbox` | Magasins en mode Sandbox |

Toutes les données nécessaires aux rapports sont envoyées automatiquement à [!DNL Payment Services] si cron est configuré et installé. Vous pouvez également déclencher manuellement le processus d’envoi de données cron à [!DNL Payment Services].

```bash
bin/magento cron:run --group payment_services_data_export
```

Pour en savoir plus sur la réindexation et les indexeurs, consultez la rubrique [Gérer les indexeurs](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) dans la documentation destinée aux développeurs.

## Configuration de l’étendue via l’interface de ligne de commande

[!DNL Payment Services] permet aux commerçants d&#39;utiliser [plusieurs comptes PayPal](settings.md#use-multiple-paypal-accounts). Vous pouvez désormais modifier les portées de ces comptes via l’interface de ligne de commande.

Pour définir l’étendue au niveau `website`, exécutez :

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

Pour définir l’étendue au niveau `store`, utilisez :

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> Si vous souhaitez modifier la portée au niveau du magasin, contactez votre représentant commercial [!DNL Payment Services].

Une fois la portée modifiée, videz le cache pour afficher les modifications :

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## Configuration du traitement L2/L3

[!DNL Payment Services] pouvez traiter les données de niveau 2 et de niveau 3 des transactions de paiement par carte afin de fournir des informations supplémentaires aux commerçants.

>[!WARNING]
>
> L&#39;intégration avec le traitement de niveau 2 et de niveau 3 avec PayPal est disponible uniquement pour les commerçants américains. Voir [traitement des paiements](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} dans la documentation destinée aux développeurs PayPal pour plus d’informations.

Si vous souhaitez utiliser des données de traitement L2/L3 pour [!DNL Payment Services], ou si vous avez des questions, contactez votre gestionnaire de compte [!DNL Payment Services].

Pour en savoir plus sur le traitement L2 et L3 utilisé dans [!DNL Payment Services], voir [Traitement de niveau 2 et de niveau 3](levels-card-payment-transactions.md).
