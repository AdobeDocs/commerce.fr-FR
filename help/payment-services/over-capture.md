---
title: Surcapturer
description: Découvrez les exigences et la configuration de la surcapture de l’extension Payment Services.
role: Admin, User
level: Intermediate
feature: Payments, Paas
source-git-commit: d2bcc58f34af50f26d4a4f082e5b3fc30089ab58
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%
---
# Surcapturer

La surcapture permet aux commerçants éligibles ayant un accord de surcapture PayPal de capturer plus que le montant autorisé à l&#39;origine lors de la facturation d&#39;une commande. Par exemple, le montant final pourrait augmenter en raison de rajustements en fonction du poids ou de changements dans les coûts des matières entre l&#39;autorisation et l&#39;exécution.

PayPal détermine la limite de surcapture pour chaque compte marchand. L&#39;activation de la surcapture dans [!DNL Payment Services] n&#39;établit pas d&#39;accord ni n&#39;augmente la limite approuvée par PayPal.

>[!NOTE]
>
>Cette rubrique décrit la surcapture dans l’extension [!DNL Payment Services]. Pour [!DNL Adobe Commerce as a Cloud Service] d’informations, voir [Quantités de capture personnalisées](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) pour connaître les différentes exigences en matière de disponibilité et d’activation.

## Conditions préalables

Avant d’activer la surcapture :

* La surcapture n’est disponible que dans [!DNL Payment Services] 2.17.0 ou une version ultérieure.
* La surcapture n&#39;est possible que pour les entreprises américaines. Les [exigences de surcapture de PayPal (PSD2)](https://www.paypal.com/us/cshelp/article/overcapture-requirements-psd2-help954) s&#39;appliquent également aux commerçants basés aux États-Unis qui vendent aux acheteurs PayPal dans l&#39;Espace économique européen (EEE).
* La surcapture n&#39;est pas disponible pour les modes de paiement alternatifs (APM).
* Obtenez un accord de surcapture avec PayPal et confirmez la limite approuvée pour votre compte marchand avec votre gestionnaire de compte PayPal.
* Définissez la **[!UICONTROL Payment Action]** du mode de paiement sur `Authorize`. La surcapture s’applique aux commandes autorisées capturées ultérieurement lors de la facturation, et non aux commandes automatiquement capturées avec `Authorize and Capture`. Voir [Définir [!DNL Payment Services] comme mode de paiement](production.md#set-payment-services-as-payment-method).

## Activer la surcapture

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Dans le panneau de gauche, développez **[!UICONTROL Sales]** et choisissez **[!UICONTROL Payment Methods]**.
1. Sélectionnez le site web à configurer à l’aide du sélecteur de portée du magasin.
1. Développez la section _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Dans la section _[!UICONTROL Payment Services]_, développez la section&#x200B;_[!UICONTROL General Configuration]_ .
1. Définissez **[!UICONTROL Over Capture Enabled]** sur `Yes`.
1. Cliquez sur **[!UICONTROL Save Config]** pour enregistrer vos modifications.
1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, puis cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

## Capturer un paiement autorisé

La surcapture a lieu lors de la facturation dans l’administrateur. Le montant de la capture demandée doit être compris dans la limite approuvée par PayPal pour votre compte marchand. Voir [Créer une facture](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice) pour le workflow de facturation standard.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Orders]**.
1. Ouvrez une commande avec un paiement autorisé qui n&#39;a pas encore été saisi.
1. Cliquez sur **[!UICONTROL Invoice]**.
1. Dans le champ Montant de capture personnalisé, saisissez le montant total à capturer. Par exemple, si le montant autorisé est USD 100 et que les frais définitifs convenus sont USD 110, saisissez `110`, et non `10`. Le montant demandé doit être compris dans votre limite approuvée par PayPal.
1. Sélectionnez la capture en ligne de la facture pour demander le paiement via le fournisseur de paiement.
1. Vérifiez la facture et cliquez sur **[!UICONTROL Submit Invoice]**.

### Capture à l’aide de l’API Invoice

Utilisez le point d’entrée standard [Créer une facture](https://developer.adobe.com/commerce/webapi/rest/tutorials/orders/order-create-invoice) :

```http
POST /rest/<store_code>/V1/order/<orderId>/invoice
```

Utilisez le code magasin pour la commande et l’identifiant interne de la commande. Authentifiez-vous avec un jeton d’administration ou d’intégration autorisé et définissez `Content-Type: application/json`.

L’exemple de payload suivant demande une facture complète avec capture en ligne d’USD 110 pour une commande autorisée pour USD 100, à condition que le contrat PayPal du commerçant autorise ce montant :

```json
{
  "capture": true,
  "notify": false,
  "arguments": {
    "extension_attributes": {
      "custom_capture_amount": 110
    }
  }
}
```

Dans cet exemple :

1. `capture` demande une capture en ligne.
1. `notify` contrôle si Commerce envoie l’e-mail de notification de facture.
1. `custom_capture_amount` est le montant final à saisir, et non l’augmentation par rapport au montant autorisé.

## Résolution des problèmes liés à une capture rejetée

Si PayPal rejette une demande de surcapture :

* Vérifiez qu&#39;un accord de surcapture est actif pour le compte marchand PayPal utilisé pour le paiement.
* Vérifiez que le montant demandé est dans la limite approuvée. S&#39;il dépasse la limite, demandez un montant inférieur ou contactez votre gestionnaire de compte PayPal pour discuter d&#39;une augmentation.
