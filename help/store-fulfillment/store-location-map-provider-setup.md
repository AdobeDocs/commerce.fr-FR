---
title: Emplacement du magasin et configuration du système de mappage
description: Configurez un fournisseur à distance pour prendre en charge le mappage de l’emplacement du magasin dans l’interface utilisateur de storefront. Les solutions Store Fulfillment nécessitent un fournisseur à distance pour activer la recherche de magasin de vente au détail et d'autres fonctionnalités de mappage et de planification pour le workflow d'exécution de bout en bout.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Integration, Tools and External Services, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Emplacement du magasin et configuration du mappage

Activez les fonctionnalités d&#39;emplacement de magasin et de mappage pour l&#39;exécution de magasin en configurant un [fournisseur à distance](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/distance-priority-algorithm) pour rechercher des emplacements de magasin de vente au détail.

**Conditions requises**

Pendant le processus de configuration, vous fournissez une clé API Google pour la plateforme Google Maps. Si vous n’en avez pas, [générez-en un à partir de la plateforme Google Maps](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/distance-priority-algorithm#configure-google-maps).

Pour configurer le fournisseur à distance :

1. À partir de la configuration **[!UICONTROL Stores > General]** dans Admin, ajoutez l’intégration Google Maps pour le type de contenu Map .

   - Accédez à **[!UICONTROL Stores > Configuration  > General > Content Management]**.

   - Ajoutez votre clé API Google au champ **[!UICONTROL Google Maps API Key]** .

1. Dans la configuration **[!UICONTROL Stores > Inventory]** de l’administrateur, sélectionnez le fournisseur de services à distance pour la Store Fulfillment.

   - Accédez à **[!UICONTROL Stores > Configuration > Catalog > Inventory]**.

   - Développez la section **[!UICONTROL Distance Provider for Distance Based SSA]** .

   - Définissez le **Fournisseur** sur **Mappage Google**.

1. Configurez les paramètres du **[!UICONTROL Google Distance Provider]**.

   - Ajoutez votre clé API **Google**.

   - Définissez **[!UICONTROL Computation Mode]** sur `Driving` et **[!UICONTROL Value]** sur `Distance`
