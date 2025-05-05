---
title: Suivi de vos expéditions dans  [!DNL Payment Services]
description: Personnaliser [!DNL Payment Services] les expéditions et les informations de suivi affichées dans le tableau de bord marchand Paypal.
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Suivi de vos envois en [!DNL Payment Services]

[!DNL Payment Services] permet aux commerçants de voir les informations de suivi d&#39;une expédition dans leur tableau de bord de commerçants PayPal.

Voir la rubrique [expéditions](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/order-management/shipments){target=_blank} pour plus d’informations sur la grille des expéditions pour Adobe Commerce.

## Fonctionnement du suivi de votre expédition

Cette fonctionnalité dépend de la facturation de la commande, car PayPal doit recevoir un `capture_id` pour traiter les informations de suivi. Si un marchand expédie ses produits avant la capture, les informations de suivi ne sont pas envoyées à PayPal.

>[!NOTE]
>
> Il est recommandé de créer une expédition par numéro de suivi, en associant les articles corrects à l&#39;expédition.

## Ajouter le numéro de tracking

Les instructions suivantes vous guideront tout au long du processus de création d’une expédition dans Adobe Commerce avec [!DNL Payment Services] :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.

1. Dans la colonne **[!UICONTROL Action]** de l&#39;ordre sélectionné, cliquez sur **[!UICONTROL View]**.

1. Cliquez sur **[!UICONTROL Ship]**.

1. Faites défiler jusqu’au bloc **[!UICONTROL Payment & Shipping Method]** et cliquez sur **[!UICONTROL Add Tracking Number]** dans **[!UICONTROL Shipping Information]**.

1. Définissez la **[!UICONTROL Carrier]**.

1. Pour suivre l&#39;expédition, saisissez les **[!UICONTROL Title]** et **[!UICONTROL Number]** .

1. Cliquez sur **[!UICONTROL Submit Shipment]**.

>[!NOTE]
>
> Vous pouvez également utiliser un module d’expédition pour saisir les informations sur le numéro de suivi. Assurez-vous que le module d’expédition enregistre les informations du numéro de suivi dans le champ `tracking_number` .

### Compatibilité avec les tiers

Toute extension tierce est compatible avec la fonctionnalité lorsqu’une entité d’expédition est créée via l’API [Commerce](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}.
