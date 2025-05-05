---
title: Options de paiement
description: Définissez les options de paiement afin de personnaliser les méthodes disponibles pour les clients de votre boutique.
feature: Payments, Checkout, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1174'
ht-degree: 0%

---

# Options de paiement

Avec [!DNL Adobe Commerce] et [!DNL Magento Open Source] [!DNL Payment Services], vous disposez de plusieurs options de paiement.

Vous pouvez configurer ces options de paiement dans [Paramètres du domicile](payments-home.md) ou [Configuration du magasin](configure-admin.md) (recommandé pour les options de paiement héritées ou une configuration multi-magasin).

Il existe différents comportements pour chaque mode de paiement en fonction de l’étape du processus de passage en caisse :

* Page de produit : page de produit d&#39;un article
* Mini panier : disponible lorsqu&#39;un produit a été ajouté au panier et que vous cliquez sur l&#39;icône du panier.
* Panier : disponible lorsque vous cliquez sur _Afficher et modifier le panier_ à partir du mini-panier.
* Vue de passage en caisse : disponible lorsque vous cliquez sur _Passer en caisse_ à partir d&#39;un mini-panier ou d&#39;un panier

>[!IMPORTANT]
>
>[!DNL Payment Services] intégration doit être terminée avant que les paiements puissent être traités.

## Expérience de paiements standard ou avancés

[!DNL Payment Services] offre des options de paiement et des flux d’intégration **avancés** (entièrement pris en charge) et **standard** (paiement express), en fonction du pays dans lequel vous opérez.

* **Avancé** - Toutes les [options de paiement](../payment-services/payments-options.md) sont disponibles pour les [pays actuellement entièrement pris en charge](../payment-services/overview.md#availability). Lors de l’intégration pour activer les paiements en direct, sélectionnez l’option [ Intégration avancée ](../payment-services/production.md#advanced-onboarding).
* **Standard** - Un sous-ensemble d’options de paiement (paiement express), à savoir les cartes de crédit et de débit PayPal, est disponible pour les autres pays pris en charge. [Les champs de carte de crédit](#credit-card-fields) et [Apple Pay](#apple-pay-button) ne sont pas disponibles pour cette option d’intégration. Lors de l’intégration pour activer les paiements en direct, sélectionnez l’option [ Intégration standard ](../payment-services/production.md#standard-onboarding).

Consultez [Activer [!DNL Payment Services] pour la production](../payment-services/production.md#complete-merchant-onboarding) pour plus d’informations sur l’intégration avancée et standard.

## [!UICONTROL Credit Card Fields]

[!UICONTROL Credit Card Fields] offre un passage en caisse simple et sécurisé pour les méthodes de paiement par carte de crédit ou de débit. Lorsqu’un acheteur passe en caisse à l’aide des champs de carte de crédit, il saisit son nom, son adresse de facturation et ses informations de carte de crédit ou de débit pour passer sa commande. Leurs informations client sont utilisées en toute sécurité pendant la session d’achat afin de les guider en toute simplicité tout au long du flux de passage en caisse.

![Champs de carte de crédit dans le passage en caisse](assets/credit-card-fields.png){width="500" zoomable="yes"}

Activez [ chambre forte de carte de crédit](#vaulting) pour vos magasins afin de permettre aux acheteurs de mettre en chambre forte (enregistrer) leurs informations de carte de crédit pour un passage en caisse rapide ultérieurement.

Vous pouvez configurer [!UICONTROL Credit Card Fields] dans la configuration du magasin ou l’Accueil [!DNL Payment Services]. Voir [Paramètres](settings.md#credit-card-fields) pour plus d’informations.

Vous pouvez également modifier la disposition, la largeur, la hauteur et le style extérieur des champs de carte de crédit. Voir [Documentation PayPal](https://developer.paypal.com/docs/checkout/advanced/customize/card-field-style/) pour plus d’informations.

## bouton [!DNL Apple Pay]

Les clients peuvent utiliser [[!DNL Apple Pay]](https://www.apple.com/apple-pay/), qui utilise des informations d’identification de paiement par carte de crédit et de débit stockées sur un appareil iOS ou macOS, pour effectuer des achats.

[!DNL Apple Pay] n’est disponible que dans le navigateur Safari. Les commerçants peuvent ajouter jusqu’à 99 domaines par compte de commerçant.

![Bouton Apple Pay dans le mini-graphique](assets/applepay-button.png){width="500" zoomable="yes"}

Le bouton [!DNL Apple Pay] est visible à partir de la page produit, du mini-panier, du panier et des vues de passage en caisse.

Pour utiliser [!DNL Apple Pay] pour vos magasins, complétez le [auto-enregistrement avec [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) (_Enregistrement de votre domaine actif_ section uniquement) et [configurez-le pour vos magasins dans [!DNL Payment Services]](settings.md#payment-buttons).

>[!NOTE]
>
> Consultez la section [Passage en caisse avancé](https://www.paypal.com/us/cshelp/article/what-is-paypal-advanced-checkout-and-how-do-i-get-started-help953){target=_blank} de la documentation PayPal destinée aux développeurs pour savoir comment permettre aux acheteurs de payer avec Apple Pay sur votre site.

Vous pouvez configurer [!UICONTROL Apple Pay] dans la configuration de la boutique ou sur la page de départ Services de paiement. Voir [Paramètres](settings.md#apple-pay) pour plus d’informations.

## bouton [!DNL Google Pay]

Les clients peuvent utiliser [[!DNL Google Pay]](https://pay.google.com/about/) en ajoutant des informations de paiement à leur compte Google, où elles sont stockées en toute sécurité pour une expérience de passage en caisse transparente.

[!DNL Google Pay] n’est disponible que dans certains pays ou régions et sur certains appareils. Voir [[!DNL Google Pay] documentation](https://developer.paypal.com/docs/checkout/apm/google-pay/#link-googlepayintegration) pour plus d’informations.

![Bouton Google Pay dans le passage en caisse](assets/google-pay-button.png){width="500" zoomable="yes"}

Le bouton [!DNL Google Pay] est visible à partir de la page produit, du mini-panier, du panier et des vues de passage en caisse.

Vous pouvez configurer [!UICONTROL Google Pay] dans la configuration de la boutique ou sur la page de départ Services de paiement. Voir [Paramètres](configure-admin.md) pour plus d’informations.

>[!NOTE]
>
> L’API [!DNL Google Pay] ne peut être utilisée que sur des sites web dans un contexte sécurisé. Voir la documentation [Dépannage](https://developers.google.com/pay/api/web/support/troubleshooting) pour plus d’informations.

## [!DNL PayPal Payment Buttons]

[!DNL PayPal payment buttons], qui utilise PayPal pour effectuer un achat, stocke l&#39;adresse d&#39;expédition de votre acheteur, les adresses de facturation et les détails de paiement pour une utilisation ultérieure. Les acheteurs peuvent utiliser n&#39;importe quel mode de paiement précédemment stocké ou proposé par PayPal.

![bouton PayPal](assets/paypal-button.png){width="350" zoomable="yes"}

Vous pouvez configurer [!UICONTROL PayPal payment buttons] dans la configuration du magasin ou l’Accueil [!DNL Payment Services]. Voir [Paramètres](settings.md#payment-buttons) pour plus d’informations.

Découvrez les modes de paiement disponibles par pays dans la [documentation relative aux modes de paiement](https://developer.paypal.com/docs/checkout/payment-methods/) de PayPal.

### bouton [!DNL PayPal]

Les clients peuvent quitter facilement et en toute confiance en utilisant le bouton PayPal.

Le bouton [!DNL PayPal] est visible à partir de la page produit, du mini-panier, du panier et des vues de passage en caisse.

### bouton [!DNL Venmo]

Les clients peuvent passer en caisse à l’aide du bouton [Venmo](https://venmo.com/).

Le bouton [!DNL Venmo] est visible à partir de la page produit, du mini-panier, du panier et des vues de passage en caisse.

### Bouton de carte de débit ou de crédit PayPal

Les clients peuvent passer en caisse à l&#39;aide du bouton PayPal Débit ou Carte de crédit.

Le bouton PayPal Débit ou Carte de crédit est visible depuis la page de passage en caisse.

Cette option peut être utilisée pour présenter une option de paiement par carte de débit ou de crédit à vos acheteurs à l&#39;aide d&#39;un bouton hébergé par PayPal comme alternative à une intégration par carte de crédit.

### bouton [!DNL Pay Later]

Offrez à vos clients des paiements à court terme sans intérêt et d&#39;autres options de financement afin qu&#39;ils puissent acheter maintenant et payer plus tard avec le bouton [!DNL Pay Later].

Le bouton [!DNL Pay Later] est visible à partir de la page produit, du mini-panier, du panier et des vues de passage en caisse.

Consultez les informations sur les offres Pay Later dans [Documentation sur les offres Pay Later de PayPal](https://developer.paypal.com/docs/checkout/pay-later/us/). Utilisez le menu déroulant **Pays ou région** pour sélectionner une région d’intérêt.

Découvrez comment désactiver ou activer la messagerie [!DNL Pay Later] en mettant à jour la configuration [Paramètres](settings.md#payment-buttons).

## Utiliser uniquement les boutons de paiement PayPal

Pour mettre rapidement votre boutique en mode production, vous pouvez configurer _uniquement_ les boutons de paiement PayPal (Venmo, PayPal, etc.)... au lieu d&#39;utiliser également l&#39;option de paiement par carte de crédit PayPal.

Cela vous permet d’effectuer les opérations suivantes :

* Proposez différentes options de paiement à vos clients, y compris des boutons de paiement Venmo et PayPal, avec la possibilité de désactiver les champs de carte hébergée PayPal et d&#39;utiliser un fournisseur de carte de crédit existant.
* Utilisez votre fournisseur de carte de crédit existant pour les paiements par carte de crédit, tout en utilisant les autres options de paiement de PayPal.
* Utilisez les boutons de paiement PayPal dans les régions où PayPal ne prend pas en charge les cartes de crédit comme option de paiement.

Pour **capturer les paiements avec _uniquement_ les boutons de paiement PayPal (_pas_ l’option de paiement par carte de crédit PayPal)** :

1. Assurez-vous que votre boutique est [en mode production](settings.md#enable-payment-services).
1. [Configurez les boutons de paiement PayPal souhaités](settings.md#payment-buttons) dans Paramètres.
1. Désactivez _off_ l’option **[[!UICONTROL Show PayPal Credit and Debit card button]](settings.md#payment-buttons)** dans la section _[!UICONTROL Payment buttons]_.

Pour **capturer des paiements avec votre fournisseur de carte de crédit existant _et_ les boutons de paiement PayPal** :

1. Assurez-vous que votre boutique est [en mode production](settings.md#enable-payment-services).
1. [Configurez les boutons de paiement PayPal souhaités](settings.md#payment-buttons).
1. Désactivez _off_ l’option **[[!UICONTROL PayPal Show Credit and Debit card button]](settings.md#payment-buttons)** dans la section _[!UICONTROL Payment buttons]_.
1. Désactivez _Désactiver_ l’option **[[!UICONTROL Show on checkout page]](settings.md#credit-card-fields)** dans la section _[!UICONTROL Credit card fields]_&#x200B;et utilisez votre [compte de fournisseur de carte de crédit existant](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/payments/payments.html?lang=fr#payments).

## Recalcul de commande

Lorsqu’un client accède au flux de passage en caisse à partir du mini-panier, du panier ou de la page produit, il est redirigé vers une page de révision de commande où il peut voir l’adresse de livraison sélectionnée dans une fenêtre contextuelle PayPal. Une fois que le client a sélectionné le mode d’expédition, le montant de la commande est recalculé de manière appropriée et il peut consulter les coûts d’expédition et les taxes.

Lorsqu’un client accède au flux de passage en caisse à partir de la page de passage en caisse, le système connaît déjà l’adresse de livraison et le montant calculé final, et les totaux sont correctement représentés.

Les congés fiscaux, les frais d&#39;expédition et les taxes de vente peuvent varier considérablement d&#39;un endroit à l&#39;autre. Une fois que [!DNL Payment Services] a reçu l’adresse et le tarif de livraison, il recalcule rapidement tous les coûts applicables et les affiche correctement au cours des dernières étapes de la commande.

## Chambre forte de carte de crédit

Les acheteurs peuvent mettre en coffre (ou « enregistrer ») leurs informations de carte de crédit pour leurs achats futurs au niveau du site web (n’importe quel magasin situé dans le compte du même commerçant).

Pour plus d’informations, consultez [chambre forte de carte de crédit](vaulting.md).

## Sécurité

Pour plus d’informations, consultez [Conformité PCI](security.md#pci-compliance).
