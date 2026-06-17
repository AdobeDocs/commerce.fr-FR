---
title: Pipeline de synchronisation des catalogues
description: Découvrez le fonctionnement du pipeline  [!DNL Adobe Commerce Optimizer Connector]  synchronisation, notamment la transformation des flux, les plannings cron, le contrôle de la portée et la gestion des erreurs.
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
autotag-review: '2026-06-09T16:21:52.214Z'
TQID: 'https://experienceleague.adobe.com/EXUQzAd0I6Hnq4twzhaBZZnv0jLjeGBuTx-QgQz-5MA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 662
ht-degree: 1%

---

# Pipeline de synchronisation du connecteur

Basée sur [[!DNL SaaS Data Export]](https://experienceleague.adobe.com/fr/docs/commerce/saas-data-export/overview), la **[!DNL Adobe Commerce Optimizer Connector]** mappe les données collectées par les indexeurs de [!DNL SaaS Data Export] au format requis par le [!DNL Catalog Data Ingestion API] de [!DNL Adobe Commerce Optimizer] et gère l’authentification, l’envoi par lots et le contrôle de synchronisation basé sur la portée. Les sections ci-dessous décrivent le fonctionnement de cette synchronisation.

Contexte connexe :

- Découvrez la valeur commerciale de l’intégration, ses fonctionnalités clés et son architecture dans la rubrique [[!DNL Commerce Optimizer Connector] présentation](overview.md).

- Pour les noms de package de module, les points d’entrée de l’API de flux et les chemins d’accès aux clés de configuration, consultez la référence [&#x200B; Connector &#x200B;](reference/connector-reference.md)

## Fonctionnement de la synchronisation

Le diagramme suivant montre la synchronisation des données de [!DNL Adobe Commerce] à [!DNL Commerce Optimizer] à travers le [!DNL Adobe I/O Gateway].

![Diagramme de synchronisation de haut niveau du connecteur &#x200B;](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

Lorsque les données du catalogue changent dans [!DNL Adobe Commerce], la synchronisation passe par ces étapes.

1. **Détection des modifications d’entité** — (toutes les 1 min) Une tâche cron (`indexer_reindex_all_invalid`) détecte [!DNL Adobe Commerce] modifications d’entité et déclenche la [!DNL SaaS Data Export], qui assemble les éléments de flux.
1. **Transformation** — Le [!DNL Commerce Optimizer Connector] récupère les flux assemblés, mappe [!DNL Adobe Commerce] entités et les portées aux formats requis par l&#39;API [!DNL Commerce Optimizer] et prépare la payload pour la transmission.
1. **Transmission** — Les données transformées sont envoyées via HTTP POST (`/v1/catalog/<feed name>`) via le [!DNL Adobe I/O Gateway] à [!DNL Commerce Optimizer], qui valide et conserve les flux entrants.
1. **Conserver les résultats** — Conserver le statut de réponse de l’API dans les [tableaux de flux](reference/connector-reference.md#supported-feeds).
1. **Reprise en cas d’échec** (toutes les 5 minutes) — Une tâche cron distincte (`*_resend_failed_items`) détecte tous les éléments de flux ayant échoué et les soumet à nouveau par le biais du même pipeline.

### Traitements cron planifiés

Les tâches cron suivantes automatisent le pipeline selon un planning fixe.

| Groupe cron | Tâche cron | Objectif | Planning |
|-------------------------------------|-------------------------------|------------------------------------------------------------------------------|----------------|
| `index` | `indexer_update_all_views` | Écoute les mises à jour des entités, assemble les éléments de flux et conserve le statut du flux | Toutes les 1 minute |
| `index` | `indexer_reindex_all_invalid` | Effectuer une resynchronisation complète pour les index de flux marqués comme « Réindexation requise » | Toutes les 1 minute |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | Recherche les éléments de flux ayant échoué et les soumet à nouveau à [!DNL Commerce Optimizer] | Toutes les 5 minutes |
| `commerce_data_export` | `cleanup_deleted_feed_items` | Nettoie les éléments de flux supprimés synchronisés après la période de conservation (7 jours) | Tous les jours à 2:00 h |

L’extension **[!DNL SaaS Data Export]** gère la collecte de flux et le suivi des statuts. Le calque de connecteur mappe les entités et les étendues au format requis par l’API [!DNL Commerce Optimizer] et les envoie via `POST /v1/catalog/<feed name>`.

#### Conditions requises

- [Commerce cron doit être en cours d&#39;exécution](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"}.
- Les indexeurs de flux doivent utiliser le mode **[!UICONTROL Update by Schedule]**. Voir [&#x200B; Synchronisation partielle &#x200B;](../data-export/sync-overview.md#partial-sync){target="_blank"}.

## Contrôle de synchronisation basé sur la portée

Le module `CommerceOptimizerScopeMapper` lit les paramètres d’exportation par site web et par magasin et les applique lors de la collecte et de l’envoi des flux.

- **Étendues activées** exportez les données selon la planification delta normale.
- Les **désactivées** sont exclues du pipeline.
Les entités précédemment synchronisées sont supprimées de [!DNL Commerce Optimizer] lors de la prochaine exécution cron.

Si les problèmes de synchronisation n’affectent qu’une seule source de catalogue ou un seul catalogue de prix, consultez [Data not sync](troubleshooting.md#data-not-syncing).

Pour plus d’informations sur la personnalisation de la portée de synchronisation, voir [Personnalisation de la configuration d’exportation des portées Commerce](get-started.md#customize-the-commerce-scopes-export-configuration).

## Calendrier et surveillance

| Scénario | Synchronisation standard |
| -------- | -------------- |
| Mises à jour régulières du catalogue | 1 à 2 cycles de synchronisation delta (~1 à 2 minutes pour l’indexation, plus l’envoi) |
| Échecs transitoires | Reprise toutes les 5 minutes |
| Synchronisation complète pour les catalogues volumineux | De quelques minutes à quelques heures |

Surveillez le statut par flux à partir de la page [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) de l’administration Commerce. Voir [Vérifier que la synchronisation des données fonctionne](./data-sync-manage.md#verify-that-the-data-sync-is-working).

## Envoi du flux et gestion des erreurs

Le processus `FeedSubmitter` gère les appels [!DNL Catalog Data Ingestion API].

1. Sépare les éléments de mise à jour des éléments de suppression (différents points d’entrée de l’API).
1. Les appels mettent à jour et suppriment les points d’entrée indépendamment.
1. Fusionne les résultats de statut par élément en une seule réponse.

### Fusion du code d’état HTTP

Lorsque les appels de mise à jour et de suppression renvoient des codes d’état différents, `FeedSubmitter` combine les résultats comme suit.

| Met à jour le résultat | Supprime le résultat | Résultat final |
| --------------- | --------------- | ------------- |
| 200 | 200 ou aucun | 200 succès |
| 200 | 400 | 200 avec erreurs de suppression |
| 400 | 400 | 400 erreurs fusionnées |
| autres frais | autres frais | RÉESSAYABLE |

| Type d’erreur | Comportement |
| ---------- | -------- |
| **400** | Les éléments répertoriés dans le champ `errors` de réponse apparaissent dans l’administration et nécessitent une attention particulière. Les autres éléments du lot sont repris. |
| **5xx** | Reprise par les tâches cron `*_feed_resend_failed_items` spécifiques au flux dans le groupe `resync_failed_feeds_data_exporter`. |

>[!MORELIKETHIS]
>
> - [Présentation du connecteur](overview.md) — Découvrez le contexte commercial et le mappage de portée
> - [Référence du connecteur](reference/connector-reference.md) — Examiner les modules, les points d’entrée d’API et les clés de configuration
> - [Personnaliser la configuration de l’exportation des portées de Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration) — Configurer les flux par niveau de portée, activer et désactiver le comportement et Étapes d’administration
> - [Dépannage](troubleshooting.md) — Diagnostiquer les échecs de synchronisation
