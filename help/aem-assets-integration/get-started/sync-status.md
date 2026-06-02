---
title: Affichage de l’état de synchronisation d’AEM Assets
description: Consultez les ressources synchronisées dans une liste centrée sur les ressources dans l’administration Commerce.
feature: CMS, Media, Integration
source-git-commit: 446739ffad0da97e2e923e6e02be3f8f6b3eb2b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Affichage de l’état de synchronisation d’AEM Assets

La vue **[!UICONTROL Sync Status]** fournit une liste des ressources synchronisées par l’intégration d’AEM Assets en fonction des ressources. Utilisez-le pour rechercher, examiner et résoudre les problèmes liés aux ressources en fonction de leurs propres attributs, au lieu de parcourir le catalogue produit par produit.

![Affichage de l’état de synchronisation ](../assets/aem-assets-sync-status-view.png){width="700" zoomable="yes"}

>[!NOTE]
>
> [!UICONTROL Sync Status] n’est pas disponible pour la [!DNL Adobe Commerce Optimizer].

## Ouvrir le statut de synchronisation

Dans la barre latérale _Admin_, accédez à **[!UICONTROL System]** > **[!UICONTROL AEM Assets]** > **[!UICONTROL Sync Status]**.

![Statut de synchronisation d’AEM Assets dans le menu Système ](../assets/aem-assets-configuration-admin-menu.png){width="600" zoomable="yes"}

## Intégration de l’intégrité de la synchronisation

En haut de la page, la bannière **État de la synchronisation d’** résume l’intégrité du pipeline et le nombre d’événements en attente de traitement. Sélectionnez **[!UICONTROL Refresh]** pour mettre à jour la bannière d’intégrité de la synchronisation.

## Liste des ressources

La grille répertorie les ressources traitées par le pipeline de synchronisation AEM Assets et leur état de synchronisation actuel. Chaque ligne représente une ressource et son état de synchronisation dans Commerce. Il ne représente pas un enregistrement de produit.

| Colonne | Description |
|--------|-------------|
| **ID de ressource** | Identifiant de ressource AEM (par exemple, `urn:aaid:aem:…`). |
| **Statut** | Résultat de la dernière tentative de synchronisation de la ressource. Les valeurs possibles sont **Succès**, **Échec** ou **En attente**. |
| **Traitement** | Date et heure de début du traitement de la ressource. |
| **Distribué** | Date et heure auxquelles l’événement de synchronisation a été distribué. |
| **Erreur** | Message d’erreur lorsque **Status** indique un échec ; vide lorsque la synchronisation a réussi. |

### Filtrage des ressources

1. Sélectionnez **[!UICONTROL Filters]** pour développer le panneau de filtrage.

1. Saisissez un **ID de ressource** ou choisissez une valeur **Statut**.

1. Sélectionnez **[!UICONTROL Apply Filters]** pour mettre à jour la grille ou **[!UICONTROL Cancel]** pour fermer le panneau sans appliquer de modifications.

Les filtres s’appliquent aux données au niveau de la ressource, ce qui vous permet d’isoler les synchronisations ayant échoué ou de suivre une ressource spécifique sans ouvrir de produits individuels.

## Synchronisations ayant échoué

Lorsque le **Statut** indique un échec, consultez la colonne **Erreur** de la grille pour le message renvoyé par le pipeline de synchronisation.

Consultez le message d’erreur complet et les détails de la dernière tentative de synchronisation pour diagnostiquer l’échec.

[!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."} Pour un dépannage supplémentaire, voir [Correspondance automatique par défaut](../synchronize/default-match.md). Les fichiers journaux d’intégration sont disponibles à l’adresse `/var/log/aem-assets-integration.log` et `/var/log/aem-assets-integration-errors.log` sur votre instance Commerce.
