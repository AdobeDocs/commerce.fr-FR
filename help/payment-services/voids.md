---
title: Vides
description: Les annulations vous permettent de libérer les fonds d'un compte de carte de crédit ou de débit qui sont bloqués ou mis de côté par une autorisation pour le montant d'un achat.
exl-id: 029a7038-2812-46ce-b188-929a7a758d89
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# Vides

[!DNL Payment Services] prend en charge les fonctionnalités existantes de Commerce pour annuler les transactions. Une annulation libère des fonds sur un compte de carte de crédit ou de débit détenus par une autorisation pour le montant de l’achat. Les transactions ne peuvent être annulées que si le paiement n&#39;a pas encore été saisi.

* Si votre boutique est [configurée](https://experienceleague.adobe.com/fr/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} pour autoriser uniquement (et non pour capturer) des fonds au point de vente, un achat auprès de votre boutique entraîne une commande avec un statut `Processing` dans l’administrateur Commerce.

* Vous pouvez également [annuler une commande](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order){target="_blank"} qui n&#39;est pas facturée. Toute autorisation non capturée est également annulée dans le cadre de ce processus d’annulation.

>[!NOTE]
>
>L&#39;annulation d&#39;une commande entraîne également une annulation, mais l&#39;annulation d&#39;une commande ne déclenche pas une annulation.

Pour en savoir plus sur les étapes de base d’une commande, voir la rubrique [Workflow de commande](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/order-management/orders/order-processing){target="_blank"} dans le guide d’utilisation principal.

Pour en savoir plus sur la fonctionnalité d&#39;annulation et sur la façon d&#39;annuler une transaction de commande, consultez [Traitement d&#39;une commande](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/order-management/orders/order-processing#process-an-order){target="_blank"} dans le guide d&#39;utilisation principal.
