---
title: Compatibilité avec  [!DNL Payment Services]
description: Découvrez si  [!DNL Payment Services]  est disponible dans votre pays et sa compatibilité avec votre version d’Adobe Commerce.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
exl-id: 4bef8429-5053-424d-806a-9e8b96295b1b
TQID: https://experienceleague.adobe.com/UUD0IiEiwh0sZKMkclOJtoC2bKYcmDN3WAWD16mfad4
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
source-git-commit: 4235bf48bb5f24a076621ee5985e9e7316fcb1cc
workflow-type: tm+mt
source-wordcount: 498
ht-degree: 0%

---

# Compatibilité avec [!DNL Payment Services]

[!DNL Payment Services] est disponible pour [!DNL Adobe Commerce as a Cloud Service], toutes les versions prises en charge d’[!DNL Adobe Commerce on Cloud] et sur site, ainsi que pour Magento Open Source. Voir la page [Politique de cycle de vie](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/lifecycle-policy) pour obtenir des informations spécifiques à la version.

## Conditions préalables

Pour utiliser [!DNL Payment Services], vous devez d’abord connecter votre instance Commerce. **Vous n’effectuez cette connexion qu’une seule fois**.

1. Si vous ne savez pas si votre instance est connectée, accédez à **Système** > Services > **Connecteur des services Commerce** pour afficher vos clés API et les détails de votre identifiant SaaS. Si ces valeurs sont présentes, votre instance est connectée.

1. Si vous devez toujours connecter votre instance, consultez les instructions de la page [Connecteur de services &#x200B;](../landing/saas.md).

   >[!TIP]
   >
   > Pour plus d’informations, consultez notre tutoriel vidéo [Adobe Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector) .

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

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

Voir [Connect](connect.md) pour plus d’informations sur la configuration de votre extension [!DNL Payment Services].

>[!BEGINTABS]

>[!TAB Standard (Paiement express)]

![check](assets/icon-check.png) Paiement PayPal

![check](assets/icon-check.png) bouton PayPal Débit ou Carte de crédit

![check](assets/icon-check.png) configurations de passage en caisse personnalisées

![check](assets/icon-check.png) Tarification standard

![check](assets/icon-check.png) **Disponible dans plus de 200 pays**

[![&#x200B; en savoir plus &#x200B;](assets/learn-more-button.svg)](onboard.md)

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

![check](assets/icon-check.png) Disponible dans 37 pays. Allemagne, Australie, Autriche, Belgique, Bulgarie, Canada, Chine, Chypre, Danemark, Espagne, Estonie, États-Unis, Finlande, France, Grèce, Hong Kong, Hongrie, Irlande, Italie, Japon, Lettonie, Liechtenstein, Lituanie, Luxembourg, Malte, Mexique, Norvège, Pays-Bas, Pologne, Portugal, République tchèque, Roumanie, Royaume-Uni, Singapour, Slovaquie, Slovénie, Suède. **Tarifs négociés disponibles aux États-Unis (US), au Canada (CA), en Australie (AU), en France (FR), au Royaume-Uni (GB), en Italie (IT), aux Pays-Bas (NL), en Allemagne (DE)**

[![&#x200B; en savoir plus &#x200B;](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

Pour plus d’informations sur les versions et les notes de mise à jour[&#128279;](https://experienceleague.adobe.com/en/docs/commerce-operations/release/planning/lifecycle-policy) consultez les pages Politique de cycle de vie et [[!DNL Payment Services] Notes de mise à jour](release-notes.md).

Pour obtenir les instructions complètes et démarrer le processus d’intégration, reportez-vous à la section [Prise en main d’ [!DNL Payment Services]](onboard.md).

### Cartes de crédit et devises acceptées

[!DNL Payment Services] accepte les devises des pays dans lesquels il est disponible. Voir [Configuration de la devise](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration) pour plus d’informations sur la configuration des taux de change.

Pour plus d&#39;informations sur les devises et les modes de paiement disponibles avec les produits et services PayPal, consultez les pages suivantes :

* [Documentation sur les devises prises en charge](https://developer.paypal.com/reports/reference/supported-currencies).

* [Documentation sur les modes de paiement](https://developer.paypal.com/payment-methods).
