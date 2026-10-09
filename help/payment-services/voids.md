---
title: Vides
description: Les annulations vous permettent de libérer les fonds d'un compte de carte de crédit ou de débit qui sont bloqués ou mis de côté par une autorisation pour le montant d'un achat.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
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
source-wordcount: '244'
ht-degree: 0%
---
# Vides

[!DNL Payment Services] prend en charge les fonctionnalités existantes de Commerce pour annuler les transactions. Une annulation libère des fonds sur un compte de carte de crédit ou de débit détenus par une autorisation pour le montant de l’achat. Les transactions ne peuvent être annulées que si le paiement n&#39;a pas encore été saisi.

* Si votre boutique est [configurée](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} pour autoriser uniquement (et non pour capturer) des fonds au point de vente, un achat auprès de votre boutique entraîne une commande avec un statut `Processing` dans l’administrateur Commerce.

* Vous pouvez également [annuler une commande](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} qui n&#39;est pas facturée. Toute autorisation non capturée est également annulée dans le cadre de ce processus d’annulation.

>[!NOTE]
>
>L&#39;annulation d&#39;une commande entraîne également une annulation, mais l&#39;annulation d&#39;une commande ne déclenche pas une annulation.

Pour en savoir plus sur les étapes de base d’une commande, voir la rubrique [Workflow de commande](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} dans le guide d’utilisation principal.

Pour en savoir plus sur la fonctionnalité d&#39;annulation et sur la façon d&#39;annuler une transaction de commande, consultez [Traitement d&#39;une commande](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} dans le guide d&#39;utilisation principal.
