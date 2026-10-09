---
title: Suivi de vos envois en [!DNL Payment Services]
description: Personnalisez [!DNL Payment Services] expéditions et les informations de suivi affichées dans le tableau de bord du commerçant Paypal.
feature: Payments, Paas, Saas
exl-id: 17aede1f-56ae-441a-b723-3193e865e469
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '228'
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

Toute extension tierce est compatible avec la fonctionnalité lorsqu’une entité d’expédition est créée via l’API [&#128279;](https://developer.adobe.com/commerce/webapi/rest/attributes/#ShipmentRepositoryInterface){target=_blank}.
