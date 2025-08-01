---
title: Amélioration des performances d’exportation des données SaaS
description: Découvrez comment améliorer les performances d’exportation des données SaaS pour les services Commerce à l’aide d’un mode d’exportation de données multithread.
role: Admin, Developer
exl-id: 7151118c-5e30-44d0-b515-5801a73e44ec
source-git-commit: 9b28da0bf861a266e9d679ba59470f46d9a89c1c
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 0%

---

# Amélioration des performances d’exportation des données SaaS

Le **mode d’exportation de données multithread** accélère le processus d’exportation en divisant les données de flux en lots et en les traitant simultanément.

Les développeurs ou les intégrateurs système peuvent améliorer les performances en utilisant le mode d’exportation de données multithread au lieu du mode par défaut à thread unique. En mode thread unique, il n’existe aucune parallélisation du processus d’envoi des flux. En outre, en raison des limites par défaut définies, tous les clients sont limités à l’utilisation d’un seul thread. Dans la plupart des cas, il n’est pas nécessaire de personnaliser la configuration.

## Considérations relatives à l’utilisation du mode multithread

Lorsque vous utilisez des services d’exportation de données, vous souhaitez optimiser les performances tout en assurant une synchronisation précise.
Adobe recommande d’utiliser la configuration par défaut pour l’ingestion de données, qui répond généralement aux exigences de synchronisation pour les commerçants Commerce. Cependant, il existe des scénarios où la personnalisation peut accélérer le temps de traitement.

Tenez compte des facteurs clés suivants lorsque vous décidez de personnaliser la configuration de l’exportation des données :

- **Synchronisation initiale**-Évaluez le nombre de produits et [estimez le volume de données et la durée de transmission](estimate-data-volume-sync-time.md) en fonction de la configuration par défaut. Demandez-vous ceci : pouvez-vous attendre cette synchronisation initiale des données après l’intégration d’un service Commerce ?

- **Ajout de nouvelles vues de boutique ou de nouveaux sites web**-Si vous prévoyez d’ajouter des vues de boutique ou des sites web avec le même nombre de produits après la mise en ligne, estimez le volume de données et le temps de transmission. Déterminez si l’heure de synchronisation est acceptable avec la configuration par défaut ou si un traitement multithread est nécessaire.

- **Importations régulières**-Anticipez les importations régulières, telles que les mises à jour de prix ou les changements de statut des stocks. Évaluez si ces mises à jour peuvent être appliquées dans un délai acceptable ou si un traitement plus rapide est nécessaire.

- **Poids du produit**-Déterminez si vos produits sont légers ou lourds. Ajustez la taille du lot en conséquence si les descriptions ou les attributs du produit gonflent la taille du produit.

N’oubliez pas qu’une planification minutieuse, y compris l’estimation du volume de données et de la durée de synchronisation, peut souvent éliminer le besoin de personnalisation. Planifiez les opérations d’ingestion de flux en fonction de ces estimations pour obtenir des résultats optimaux.

>[!NOTE]
>
>Adobe recommande de faire preuve de prudence lors de l’utilisation du traitement multithread. Si vous configurez le multithread pour des performances plus rapides, vous pouvez déclencher les mécanismes de sécurisation des services Adobe Commerce inclus pour éviter toute utilisation abusive du système lors de l’ingestion des données. Ces mécanismes de sécurisation empêchent également les utilisateurs de déclencher des modifications de synchronisation susceptibles de surcharger le système. Lorsque les mécanismes de sécurisation sont déclenchés, les requêtes sont bloquées et le système renvoie des erreurs 429. Si vous rencontrez ces erreurs, ajustez votre configuration et envoyez un ticket d’assistance pour obtenir de l’aide.

## Configuration du multithread

Le mode multithread est pris en charge pour toutes les [méthodes de synchronisation](data-synchronization.md#synchronization-process) : synchronisation complète, synchronisation partielle et synchronisation des éléments en échec. Pour configurer le multithread, vous spécifiez le nombre de threads et la taille du lot à utiliser pendant la synchronisation.

- `thread-count` correspond au nombre de threads activés pour traiter les entités. La `thread-count` par défaut est `1`.
- `batch-size` est le nombre d&#39;entités qui sont traitées dans une seule itération. La `batch-size` par défaut est `100` enregistrements pour tous les flux, à l’exception du flux de prix. Pour le flux de prix, la valeur par défaut est `500` enregistrements.

Vous pouvez configurer le multithread en tant qu’option temporaire lors de l’exécution d’une commande de resynchronisation ou en ajoutant la configuration multithread à la configuration de l’application Adobe Commerce.

>[!NOTE]
>
>Veillez à aligner les performances de l’exportation des données SaaS avec la limite de débit définie pour un client du côté client.

### Configurer le multithread au moment de l’exécution

Lorsque vous exécutez une commande de synchronisation complète à partir de la ligne de commande, spécifiez le traitement multithread en ajoutant les options `thread-count` et `batch-size` à la commande de l’interface de ligne de commande.

```
bin/magento saas:resync --feed=products --thread-count=2 --batch-size=200
```

Les options spécifiées sur la ligne de commande remplacent la configuration d’exportation des données spécifiée dans le fichier de `config.php` de l’application Adobe Commerce.

### Ajout du multithread à la configuration Commerce

Pour traiter toutes les opérations d’exportation de données à l’aide du multithread, les intégrateurs système ou les développeurs peuvent modifier le nombre de threads et la taille du lot pour chaque flux dans la configuration de l’application Commerce.

Ces modifications peuvent être appliquées en ajoutant des valeurs personnalisées à la [section système](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/files/config-reference-configphp#system) du fichier de configuration, `app/etc/config.php`.

**Exemple : configuration du multithreading pour les produits et les prix**

```php
<?php
return [
    'system' => [
        'default' => [
            'commerce_data_export' => [
                'feeds' => [
                    'products' => [
                        'batch_size' => 100,
                        'thread_count' => 2,
                    ],
                    'prices' => [
                        'batch_size' => 400,
                        'thread_count' => 4,
                    ]
                ]
            ],
//   ...
```
