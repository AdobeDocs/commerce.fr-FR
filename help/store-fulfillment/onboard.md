---
title: Présentation de l’intégration des services Store Fulfillment
description: '[!DNL Live Search] le flux d’intégration, la configuration requise, les limites et les limitations.'
role: Admin, Leader
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Présentation de l’intégration pour la Store Fulfillment

Commencez avec [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] en configurant et en activant les composants suivants :

- **Extension Store Fulfillment**-Installez et configurez cette extension tierce sur votre instance Adobe Commerce. Après l’installation, vous pouvez configurer et gérer la solution Store Fulfillment à partir de l’Admin pour prendre en charge les scénarios [!DNL buys online, pickup in store] (BOPIS) dans le storefront Commerce.

  ![[!DNL Store Fulfillment Service] configuration dans la vue Administration ](assets/store-fulfillment-admin-home.png)

- **Compte d’exécution de la boutique**-pendant le processus d’activation, un gestionnaire de compte crée votre compte d’exécution de la boutique et vous fournit les informations de compte et les informations d’identification. Ces informations d’identification sont requises pour activer la connexion entre Adobe Commerce et la solution Store Fulfillment.

- **Application Store Assist** : fournit des magasins associés à un workflow d&#39;exécution de magasin de bout en bout pour gérer les commandes BOPIS à partir d&#39;appareils mobiles. Store Associates peut télécharger et installer le [!DNL Store Assist] de Walmart pour les appareils iOS et Android™. Le processus d’intégration de l’application est géré par le centre client des technologies Walmart de Commerce dans le cadre d’un processus distinct. Cependant, [certains paramètres de configuration d’application](user-setup.md) sont renseignés à partir de l’administration Adobe Commerce.

  | Application d’assistance en magasin - Vue Prise en main | Application d’assistance pour la boutique — Vue Modules |
  |-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
  | Vue ![[!DNL Store Assist App Getting Started] sur un appareil mobile](assets/store-assist-get-started-small.png) | ![[!DNL Store Assist App Orders view] sur un appareil mobile](assets/store-assist-orders-small.png) |

## Étapes d’approvisionnement

- **Inscrivez-vous à l’[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]**-Remplissez le formulaire d’inscription sur [business.adobe.com](https://business.adobe.com/resources/store-fulfillment.html) ou contactez votre gestionnaire de compte Adobe Commerce pour obtenir de l’aide.

- **Lancer la demande de provisioning pour la Store Fulfillment**-Remplissez le formulaire de saisie fourni par votre gestionnaire de compte pour fournir les informations nécessaires au lancement du processus de provisioning.

- **Obtention des informations d’identification du compte d’exécution de la boutique**-Une fois votre compte d’exécution de la boutique créé, vous recevez les informations d’identification requises pour intégrer la solution d’exécution de la boutique à Adobe Commerce.

- **[Téléchargez le code source pour installer l [!DNL Store Fulfillment] extension](install.md)**

## Étapes d’intégration

1. [Installez l’extension Store Fulfillment pour Adobe Commerce](install.md).

1. Depuis l’administration, [activez la solution](enable-general.md).

1. [Configurez l’extension Store Fulfillment à partir de l’administration Adobe Commerce](service-config-settings-overview.md).

1. [Connectez le service à l [!DNL Store Fulfillment] aide des informations d&#39;identification de Store Fulfillment qui vous ont été fournies](connect-set-up-service.md).

1. [Créez des utilisateurs et des rôles pour l’application d’assistance au magasin](user-setup.md).

1. [Téléchargez l [!DNL Store Assist] application de Walmart sur l&#39;appareil de votre choix. L’application est disponible dans les magasins Apple app (iOS) et Google Play (Android™)](app-setup.md).

Une fois l’installation, la configuration et l’intégration terminées, ainsi que l’accès à l’application [!DNL Store Assist], vous pouvez [commencer à créer des commandes et à effectuer des tests](test-and-deploy.md).
