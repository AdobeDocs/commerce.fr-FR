---
title: Synchronisation des catalogues
description: Découvrez comment exporter des données de produit du serveur  [!DNL Commerce]  vers  [!DNL Commerce Services].
feature: Catalog Management, Data Import/Export, Catalog Service
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Synchronisation des catalogues

>[!NOTE]
>
> Le tableau de bord de synchronisation des catalogues est désormais le tableau de bord de gestion des données. Ce tableau de bord remanié prend désormais en charge les versions [[!DNL Product Recommendations]](../product-recommendations/guide-overview.md) v6.0.0+, [[!DNL Live Search]](../live-search/overview.md) v4.1.0+ et [[!DNL Catalog Service]](../catalog-service/overview.md) v1.17+. Les clients peuvent obtenir le tableau de bord de gestion des données en effectuant une mise à jour vers la dernière version de l’un de ces services. Pour en savoir plus, consultez la documentation du [Tableau de bord de gestion des données](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=fr). Cette rubrique reste ouverte aux utilisateurs qui n’ont pas encore effectué la mise à niveau et qui disposent toujours du tableau de bord de synchronisation des catalogues.

Adobe Commerce utilise des indexeurs pour compiler les données du catalogue dans des tables. Le processus est automatiquement déclenché par des [événements](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/index-management.html?lang=fr#events-that-trigger-full-reindexing) tels qu’une modification du prix d’un produit ou du niveau de stock.

Le service de synchronisation des catalogues déplace régulièrement les données de produit d’une instance [!DNL Adobe Commerce] vers la plateforme [!DNL Commerce Services] afin de maintenir les données à jour. Par exemple, [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) nécessite des informations de catalogue actuelles pour renvoyer avec précision des recommandations avec des noms, des prix et une disponibilité corrects. Utilisez le tableau de bord _Synchronisation des catalogues_ pour observer et gérer le processus de synchronisation ou l’interface de ligne de commande afin de déclencher une synchronisation des catalogues et de réindexer les données de produit pour leur consommation par [!DNL Commerce Services]. Voir [Référence de l’interface de ligne de commande](../data-export/data-export-cli-commands.md) dans le guide _Exportation de données SaaS_.

## Accès au tableau de bord de synchronisation des catalogues

Pour accéder au tableau de bord de synchronisation des catalogues, sélectionnez **Système** > _Transfert de données_ > **Synchronisation des catalogues**.

Avec le tableau de bord **Synchronisation des catalogues** vous pouvez :

- Afficher le statut de la synchronisation (**En cours**, **Succès**, **Échec**)
- Afficher le nombre total de produits synchronisés
- Rechercher des produits synchronisés pour afficher leur état actuel
- Recherchez le catalogue de la boutique par nom, SKU, etc.
- Afficher les détails des produits synchronisés dans JSON pour diagnostiquer une incohérence de synchronisation
- Réinitialiser le processus de synchronisation

### Dernière synchronisation

Indique un statut de synchronisation de :

- **Succès** - Affiche la date et l’heure de réussite de la synchronisation et le nombre de produits mis à jour
- **Échec** - Affiche la date et l’heure de la tentative de synchronisation
- **En cours** - Affiche la date et l’heure de la dernière synchronisation réussie

Le processus de synchronisation du catalogue s’exécute automatiquement toutes les heures. Si vous ne voyez pas les produits attendus sur le storefront, ou si les produits ne reflètent pas les modifications récentes que vous avez effectuées, vous pouvez résoudre [problèmes de synchronisation de catalogue](#resolvesync).

### Produits synchronisés

Affiche le nombre total de produits synchronisés à partir de votre catalogue [!DNL Commerce]. Après la synchronisation initiale, seuls les produits modifiés doivent être synchronisés.

## Resync {#resync}

Si vous devez lancer une resynchronisation de votre catalogue avant que la synchronisation planifiée par heure ne se produise, vous pouvez forcer une resynchronisation.

>[!NOTE]
>
> Forcer une resynchronisation déclenche une resynchronisation de l’ensemble de votre catalogue de produits, ce qui peut augmenter la charge sur les ressources matérielles.

1. Dans le tableau de bord _Synchronisation des catalogues_, sélectionnez **Paramètres**.

   La page _Paramètres de synchronisation des catalogues_ s’affiche.

1. Dans la section _Resynchroniser les données_, cliquez sur [!UICONTROL Resync].

   [!DNL Commerce] synchronise votre catalogue pendant la prochaine fenêtre de synchronisation planifiée. Selon la taille de votre catalogue, cette opération peut prendre beaucoup de temps.

## Produits de catalogue synchronisés

Le tableau **Produits de catalogue synchronisés** affiche les informations suivantes.

| Champ | Description |
|---|---|
| ID | Identifiant unique du produit |
| Nom | Nom de la vitrine du produit |
| Type | Identifie le type de produit, tel que simple, configurable ou téléchargeable |
| Dernière exportation | Date de la dernière exportation réussie du produit depuis votre catalogue |
| Dernière modification | Date de la dernière modification du produit dans votre catalogue |
| SKU | Affiche l&#39;unité de gestion des stocks du produit |
| Prix | Prix du produit |
| Visibilité | Paramètre de visibilité d’un produit tel que défini dans le catalogue [!DNL Commerce] |

## Résolution des problèmes de synchronisation des catalogues {#resolvesync}

Voir [Journaux et dépannage](../data-export/troubleshooting-logging.md#troubleshooting) dans le _Guide d’exportation des données SaaS_.
