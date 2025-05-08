---
title: Chambre forte de carte de crédit
description: Les acheteurs peuvent mettre en chambre forte (enregistrer) leurs informations de carte de crédit pour leurs achats futurs.
exl-id: b4060307-ffcd-41cb-9b9d-a2fef02f23bd
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# Chambre forte de carte de crédit

Convertissez les clients occasionnels en clients fidèles avec la chambre forte de carte de crédit. Les clients connectés peuvent enregistrer (ou « mettre en coffre ») leurs informations d’identification de carte de crédit pour les utiliser lors d’un achat ultérieur pour le même magasin ou un autre dans le même compte commercial.

## Activer la mise en chambre forte

Les commerçants peuvent activer le coffre par carte de crédit pour leurs magasins dans le [!DNL Payment Services] [Paramètres](settings.md#card-vaulting).

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

1. Cliquez sur **[!UICONTROL Settings]**.

1. Activez/désactivez le sélecteur de **[!UICONTROL Vault enabled]**. Voir [Activer [!DNL Payment Services]](settings.md#enable-payment-services) pour plus d’informations.

## Mise en chambre forte sans achat

Les clients connectés peuvent archiver un mode de paiement dans le tableau de bord **Mon compte** en procédant comme suit :

1. Se connecter à leur **Mon compte** sur le storefront.

1. Accédez à **[!UICONTROL Stored Payment Methods]** dans le volet de navigation de gauche pour afficher tous les modes de paiement stockés.

   Voir [Modes de paiement stockés](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/stored-payment-methods) pour plus d’informations.

1. Le client clique sur **[!UICONTROL Add New Card]** pour stocker une nouvelle carte.

   ![Ajouter une nouvelle carte](assets/add-new-card.png){width="400" zoomable="yes"}

   Le client doit fournir tous les détails requis, tels que les informations de carte et de facturation, pour sauvegarder le mode de paiement.
Tous les modes de paiement voûtés utilisent l&#39;adresse de facturation définie lors de la voûte de la carte, qui se trouve dans le compte PayPal de l&#39;acheteur. Le client peut voir une adresse de facturation différente de celle affichée dans Commerce.

1. Clic **[!UICONTROL Save New Card]**

   ![Modes de paiement stockés dans Mon compte](assets/stored-payment-methods.png){width="400" zoomable="yes"}

Les cartes stockées peuvent être utilisées lors d’une commande :

![Utiliser les informations d’identification stockées pour un achat ultérieur](assets/use-stored-card.png){width="400" zoomable="yes"}

### Supprimer un mode de paiement stocké

Les clients peuvent facilement supprimer les cartes de crédit en chambre forte du **Modes de paiement stockés** dans le **Mon compte** en cliquant sur **Supprimer** pour une carte spécifique.

## Mise en chambre forte d’un mode de paiement lors du passage en caisse

Les clients connectés peuvent enregistrer une carte de crédit lors du passage en caisse pour l’utiliser lors d’achats ultérieurs dans le magasin actuel ou dans d’autres magasins du même compte commercial :

![Mettez leur carte de crédit en chambre forte pour une utilisation ultérieure](assets/save-card-for-later.png){width="400" zoomable="yes"}

Commerce stocke un jeton qui permet aux clients de passer en caisse à l’avenir en récupérant leurs informations de carte de crédit enregistrées. La mise en chambre forte d’une carte du compte client ou lors du passage en caisse entraîne différents jetons de paiement.

>[!WARNING]
>
> PayPal peut actuellement stocker un maximum de cinq cartes voûtées.

## Utiliser le stockage en chambre forte dans l’administrateur

Si un client possède une carte de crédit précédemment enregistrée, un commerçant peut créer une commande ultérieure pour ce client dans l’administrateur à l’aide de l’un de ces modes de paiement enregistrés.

Vous ne pouvez utiliser des cartes voûtées dans l&#39;Admin que si le client dispose à la fois d&#39;un compte existant et d&#39;un jeton valide stocké dans le système à partir d&#39;un paiement déjà effectué.

Pour créer une commande dans l’Administration pour un client à l’aide de sa carte de crédit voûtée :

1. [Créer une commande et ajouter des produits](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order.html).
1. Dans _[!UICONTROL Payment & Shipping Information]_, sélectionnez **[!UICONTROL Stored Cards]**comme mode de paiement.
1. Sélectionnez le mode de paiement par carte de crédit en chambre forte souhaité.
1. Après avoir effectué toutes les autres étapes nécessaires pour la commande, [envoyez-la](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/point-of-purchase/assist/customer-account-create-order.html?lang=en#step-3%3A-submit-the-order).

   ![Utilisez une carte de crédit voûtée dans Admin pour le client](assets/admin-vaultedcard.png){width="600" zoomable="yes"}

## Sécurité

Les informations de carte de crédit sont partagées avec l’acheteur de manière minimale ; il ne voit que les quatre derniers chiffres, la date d’expiration et la marque de sa carte de crédit en chambre forte. Les informations de carte de crédit sont stockées avec le fournisseur de paiement pour satisfaire aux normes de conformité [PCI](security.md#PCI-compliance).
