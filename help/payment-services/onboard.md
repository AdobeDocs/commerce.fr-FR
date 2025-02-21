---
title: Intégration  [!DNL Payment Services]
description: Connectez votre instance aux fonctionnalités  [!DNL Payment Services]  en effectuant quelques étapes d’intégration.
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# [!DNL Payment Services] intégré

Pour commencer à utiliser [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source], vous devez effectuer quelques étapes d’intégration pour connecter votre instance à la fonctionnalité de paiements.

## Flux d’intégration

Ce diagramme de flux présente le processus général d’intégration des [!DNL Payment Services].

![Flux d’intégration](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> Pour les versions 2.4.7 ou ultérieures d’Adobe Commerce, vous pouvez ignorer l’étape Extension de Marketplace, car [!DNL Payment Services] est disponible et prêt à l’emploi.

Une fois l’intégration terminée pour les paiements sandbox ou dynamiques, les rapports financiers sont accessibles depuis [!DNL Payment Services] dans l’Administration.

Si les paiements sandbox et dynamiques sont intégrés et activés, vous pouvez facilement basculer entre ces modes à partir de l’Accueil [!DNL Payment Services].

## Conditions préalables

Pour utiliser [!DNL Payment Services], tous les modules dépendants doivent être activés et les éléments suivants doivent être disponibles pour votre instance :

* Module Services Connector
* Module Services ID
* Clés API

Les modules Connecteur de services et ID de services sont automatiquement installés lors de l’[installation de  [!DNL Payment Services]](install.md).

Une fois l’installation terminée, une nouvelle section s’affiche dans les paramètres de configuration (**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**) si vous développez **[!UICONTROL Services]**—**[!UICONTROL Commerce Services Connector]**.

Pour savoir comment créer vos clés API ou y accéder, voir [Informations d’identification de l’API](#obtain-api-credentials).

## Étapes d’intégration

1. [Installez l [!DNL Payment Services] extension](install.md#get-payment-services).
1. [Obtention des informations d’identification d’API](connect.md#obtain-api-credentials).
1. [Connectez votre instance](connect.md#configure-commerce-services) aux services Commerce. Cette connexion ne doit être établie qu’une seule fois par instance Commerce.
1. [Configurez le service sandbox](sandbox.md#enable-sandbox-testing) (ou passez à l’[activation des paiements dynamiques](sandbox.md#enable-live-payments) si vous avez testé la fonctionnalité dans un autre environnement) avec un compte de traitement des paiements PayPal de test.
1. [Définissez [!DNL Payment Services] comme mode de paiement](production.md#set-payment-services-as-payment-method), en mode sandbox, pour commencer à traiter les paiements de test.
1. [Demander des droits de paiement](production.md#request-payments-entitlement-from-adobe) pour activer l’intégration en direct.
1. [Intégration complète des commerçants](production.md#complete-merchant-onboarding) pour activer les paiements en direct pour vos sites web Commerce.
1. [Obtenez votre [!DNL Payment Services] ID de commerçant](production.md#configure-pricing-tier) et remettez-le au service des ventes pour configurer le niveau tarifaire approprié.
1. [Activer [!DNL Payment Services] en mode réel](production.md#enable-live-payments) pour commencer à traiter les paiements dynamiques.
1. Testez les paiements dans les environnements [sandbox](sandbox.md#test-in-sandbox-environment) et [production](production.md#test-in-production).

>[!NOTE]
>
>Si vous ne configurez pas vos services Commerce dans l’administration (étape 3), vous ne pouvez pas configurer de sandbox ou de paiements dynamiques.

## Dépannage

* [Dépannage [!DNL Payment Services] installation](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
* [Compte sandbox PayPal non vérifié](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
* [Données  [!DNL Payment Services]  rapport différées](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
* [Le test de la carte de crédit échoue avec PayPal lors du traitement des paiements dans un environnement Sandbox](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
