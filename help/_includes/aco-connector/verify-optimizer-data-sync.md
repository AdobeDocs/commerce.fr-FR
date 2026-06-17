---
source-git-commit: 3d05a7307e58ea2758ac4b6f2b70d24b8ea7a5ac
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---
# Vérifier la synchronisation des données de l’optimiseur

Vérifiez que les données ont bien été exportées à partir de l’administration Commerce et que les données ont bien été diffusées à [!DNL Commerce Optimizer]. Démarrez avec l’export dans l’administration Commerce, puis confirmez la diffusion en [!DNL Commerce Optimizer].

1. **Vérification du statut de synchronisation dans l’administration Commerce :**

   Accédez à **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Page État de synchronisation des flux de données avec rapport sur l’état des éléments de flux](/help/aco-connector/assets/data-feed-sync-status.png){width="700" zoomable="yes"}

   Lorsque la synchronisation est en cours, les données de flux affichent les enregistrements envoyés avec succès. Sélectionnez un flux pour afficher les détails ou résoudre les problèmes de synchronisation.

1. **Confirmer que les données ont été diffusées à [!DNL Commerce Optimizer]:**

   Dans le menu [!DNL Commerce Optimizer], sélectionnez **[!UICONTROL Data Sync]**.

   ![Page de synchronisation des données dans Adobe Commerce Optimizer affichant les données de catalogue synchronisées](/help/aco-connector/assets/data-sync.png){width="700" zoomable="yes"}

   Vérifiez que les produits, prix et attributs attendus s’affichent.

Lorsque la synchronisation fonctionne comme prévu :

- **[!UICONTROL Data Feed Sync Status]** affiche les enregistrements envoyés avec succès pour les flux du connecteur, sans erreurs au niveau de l’élément non résolues.
- **[!UICONTROL Data Sync]** dans [!DNL Commerce Optimizer] répertorie les sources de catalogue, les produits, les prix et les attributs attendus.

>[!TIP]
>
>Si vous rencontrez des problèmes avec la synchronisation des données, consultez le guide [Dépannage](/help/aco-connector/troubleshooting.md).
