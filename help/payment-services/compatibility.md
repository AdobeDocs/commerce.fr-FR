---
title: Compatibilité avec  [!DNL Payment Services]
description: Découvrez si  [!DNL Payment Services]  est disponible dans votre pays et sa compatibilité avec votre version d’Adobe Commerce.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Compatibilité avec [!DNL Payment Services]

[!DNL Payment Services] est disponible pour Adobe Commerce et Magento Open Source. [!DNL Payment Services] est désormais compatible avec les versions 2.4.x d’Adobe Commerce.

## Conditions préalables

Pour utiliser [!DNL Payment Services], vous devez d’abord connecter votre instance Commerce. **Vous ne configurez cette connexion qu’une seule fois**.

1. Si vous ne savez pas si votre instance est connectée, accédez à **Système** > Services > **Connecteur de services Commerce** et affichez les valeurs des clés API publiques et privées dans les sections Clés de sandbox et Clés de production, ainsi que les champs Projet et Espace de données dans la section Identifiant SaaS. Si ces valeurs sont présentes, votre instance est connectée.

1. Si vous devez toujours connecter votre instance, consultez les instructions de la page [Connecteur de services Commerce](../landing/saas.md).

   >[!TIP]
   >
   > Pour plus d’informations, consultez notre tutoriel vidéo [Adobe Commerce Services Connector](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector) .

1. Si vous avez déjà connecté votre instance, accédez à la page [intégration](onboard.md) pour connaître les étapes suivantes.

>[!IMPORTANT]
>
> Tous les commerçants autorisés à [!DNL Payment Services] peuvent utiliser **un espace de données de production** et **deux espaces de données de test**.

## Expérience [!DNL Payment Services] standard ou avancée

[!DNL Payment Services] propose des options de paiement et des flux d’intégration **Standard** (Paiement express) et **Avancé** (entièrement pris en charge), en fonction du pays dans lequel vous opérez.

>[!NOTE]
>
> [!DNL Payment Services] offre des [fonctionnalités de passage en caisse express](../payment-services/payments-options.md) (sous-ensemble d’options de paiement) pour d’autres [pays disponibles lors de l’intégration](../payment-services/production.md#complete-merchant-onboarding).

### Quelle option de [!DNL Payment Services] vous convient le mieux ?

>[!VIDEO](https://video.tv.adobe.com/v/3447920?captions=fre_fr)

Voir [Connect](connect.md) pour plus d’informations sur la configuration de votre extension [!DNL Payment Services].

>[!BEGINTABS]

>[!TAB Standard (Paiement express)]

![check](assets/icon-check.png) Paiement PayPal

![check](assets/icon-check.png) bouton PayPal Débit ou Carte de crédit

![check](assets/icon-check.png) configurations de passage en caisse personnalisées

![check](assets/icon-check.png) Tarification standard

![check](assets/icon-check.png) **Disponible dans XX pays**

[![ en savoir plus ](assets/learn-more-button.svg)](onboard.md)

>[!TAB Avancé (Entièrement Pris En Charge)]

![chèque](assets/icon-check.png) Carte de débit

![chèque](assets/icon-check.png) crédit PayPal

![chèque](assets/icon-check.png) Champs de carte de crédit

![check](assets/icon-check.png) bouton Apple Pay

![check](assets/icon-check.png) bouton Google Pay

![check](assets/icon-check.png) boutons de paiement PayPal

![check](assets/icon-check.png) bouton Venmo

![check](assets/icon-check.png) bouton PayPal Débit ou Carte de crédit

![check](assets/icon-check.png) bouton Payer plus tard

![check](assets/icon-check.png) configurations de passage en caisse personnalisées

![check](assets/icon-check.png) Tarification personnalisée

![check](assets/icon-check.png) (fonctionnalités de tarification L2/L3 - États-Unis uniquement)

![check](assets/icon-check.png) **Disponible uniquement aux États-Unis (US), au Canada (CA), en Australie (AUS). France (FR), Royaume-Uni (UK)**

[![ en savoir plus ](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

Pour plus d’informations sur les versions et les notes de mise à jour[&#128279;](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=fr) consultez les pages Politique de cycle de vie et [[!DNL Payment Services] Notes de mise à jour](release-notes.md).

Pour obtenir les instructions complètes et démarrer le processus d’intégration, reportez-vous à la section [Prise en main d’ [!DNL Payment Services]](onboard.md).

### Cartes de crédit et devises acceptées

[!DNL Payment Services] accepte les devises des pays [dans lesquels il est disponible](#availability). Voir [Configuration de la devise](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=fr) pour plus d’informations sur la configuration des taux de change.

Pour plus d&#39;informations sur les devises et les modes de paiement disponibles avec les produits et services PayPal, consultez les pages suivantes :

* [Documentation sur les devises prises en charge](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [Documentation sur les modes de paiement](https://developer.paypal.com/docs/checkout/payment-methods/).
