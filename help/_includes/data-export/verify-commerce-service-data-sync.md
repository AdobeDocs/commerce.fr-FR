---
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---
# Vérifier la synchronisation des données du service Commerce

Pour vérifier que la synchronisation des données fonctionne, vérifiez que les données ont bien été exportées depuis [!DNL Adobe Commerce] et que les données ont bien été diffusées au service Commerce connecté. Utilisez les tableaux de bord pour votre déploiement afin de vérifier les deux étapes.

Commencez par l’exportation, puis confirmez la diffusion.

1. Vérifiez le statut de synchronisation dans l’administration Commerce.

   Accédez à **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Page État de synchronisation des flux de données avec rapport sur l’état des éléments de flux](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   Lorsque la synchronisation est en cours, les données de flux affichent les enregistrements envoyés avec succès. Sélectionnez un flux pour afficher les détails ou résoudre les problèmes de synchronisation.

1. Vérifiez que les données ont été diffusées aux services Commerce connectés.

   Dans l’administration Commerce, accédez à **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**.

   ![Tableau de bord de la gestion des données affichant les données de catalogue synchronisées dans les services Commerce connectés](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   Vérifiez que les produits, prix et attributs attendus s’affichent.

>[!TIP]
>
>Si vous rencontrez d’autres problèmes avec la synchronisation des données, voir [Vérifier les journaux et résoudre les problèmes](/help/data-export/troubleshooting/logging.md).

