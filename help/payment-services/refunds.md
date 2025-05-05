---
title: Remboursements
description: Créez des remboursements pour  [!DNL Payment Services]  commandes dans l'administrateur dans le cadre du processus d'avoir.
feature: Payments, Checkout
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Remboursements

Les remboursements pour les commandes [!DNL Payment Services] sont créés dans l&#39;Administration dans le cadre du processus d&#39;avoir. Un avoir est un document qui indique le montant dû au client, pour un remboursement complet ou partiel, qui peut être lettré sur un achat ou remboursé directement au client. Les avoirs ne peuvent être émis que pour les commandes [facturées](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#create-an-invoice){target="_blank"}.

Voir [Avoirs](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos){target="_blank"} dans notre guide d&#39;utilisation principal pour plus d&#39;informations et pour savoir comment émettre et imprimer des avoirs.

Pour les commandes traitées avec PayPal ou une carte de crédit, vous pouvez :

* Rembourser la totalité du montant de la commande
* Rembourser un montant partiel d&#39;une commande (ou plusieurs montants partiels)
* Rembourser un montant inférieur à la valeur d&#39;un article de commande spécifique

Voir [ Émission d&#39;un avoir](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create){target="_blank"} dans notre guide d&#39;utilisation principal pour plus d&#39;informations.

>[!NOTE]
>
>Une erreur se produit pour les commandes traitées par PayPal ou par carte de crédit si vous tentez de rembourser partiellement une commande pour un montant supérieur au montant de commande restant (montant d&#39;origine moins le total des remboursements existants), ou si vous effectuez un remboursement pour un montant supérieur au montant total de la commande.

Le paramètre [!UICONTROL Payment Action] de votre configuration [!UICONTROL Payment Settings] (`Authorize` ou `Authorize and Capture`) détermine le [workflow de remboursement de base](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memos#refund-workflow){target="_blank"} pour les commandes.

Pour plus d&#39;informations[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/credit-memos/credit-memo-create#payment-action-setting){target="_blank"} reportez-vous à la section Paramétrage de l&#39;action de paiement de _Émission d&#39;un avoir_.
