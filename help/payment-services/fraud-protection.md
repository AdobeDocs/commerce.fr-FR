---
title: Protection contre la fraude par Signify
description: Activez la protection automatique contre la fraude pour les [!DNL Payment Services] avec Signifyd.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security, Paas, Saas
exl-id: 440296bb-a6ff-408b-8195-3027916e4f84
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '421'
ht-degree: 0%
---
# Protection contre les fraudes signalées

Vous pouvez activer la protection automatique contre la fraude pour les [!DNL Payment Services] avec l’extension [Signifyd](https://commercemarketplace.adobe.com/signifyd-module-connect.html).

Adobe Commerce prend en charge Signifyd versions 5.4.0 et ultérieures. [!DNL Payment Services] prend en charge les flux Signifyd avant et après authentification.

L’intégration Signifyd/[!DNL Payment Services] couvre les cartes de crédit, les cartes de débit, les cartes voûtées, le passage en caisse par l’intermédiaire de l’administrateur et les méthodes de paiement PayPal et Apple Pay. Bien que certains détails des transactions ne soient pas partagés entre les Services de paiement et Signifyd, Signifyd fournit une couverture complète des risques pour tous les modes de paiement, assurant ainsi une protection maximale.

>[!CAUTION]
>
> [Fastlane](payments-options.md#fastlane-button) n’est pas compatible avec Signifyd.

Voir [Documentation Signifyd](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension) pour en savoir plus sur l’installation et la configuration de l’extension.

## Intégration

Vous devez communiquer directement avec Signifyd pour intégrer l’extension à utiliser avec [!DNL Payment Services] ; aucune configuration [!DNL Payment Services] n’est nécessaire. Vous pouvez configurer l’extension Signify dans Admin une fois installée. Toute prise en charge liée à cette extension sera gérée par Signifyd.

Lors de l’intégration à Signifyd, vous devez :

1. Contactez Signify pour configurer un nouveau compte.
1. Par défaut, Signifyd est [placé sur la liste autorisée ](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md) afin de s&#39;assurer qu&#39;il ne déclenche pas d&#39;autres options de paiement qu&#39;il ne prend actuellement pas en charge. Si vous souhaitez interdire un mode de paiement particulier, vous devez apporter des modifications.
1. Confirmez auprès de Signifyd que PayPal ne rejettera pas les commandes, via le paramètre de protection contre la fraude du commerçant dans Paypal, qui pourraient être approuvées par Signifyd.
1. Activez l’extension Signifyd pour qu’elle soit compatible avec [!DNL Payment Services] :
   * Lors de l’utilisation de [!DNL Payment Services] en mode _actif_, Signifyd doit être en mode Production.
   * Lors de l’utilisation de [!DNL Payment Services] en mode _Sandbox_, Signifyd doit être en mode Test.

## Configuration

Étant donné que Signifyd agit sur vos commandes, il est nécessaire de configurer l’extension pour qu’elle se comporte de manière appropriée en fonction de l’action de paiement que vous avez définie pour [!DNL Payment Services].

Ces options de configuration ne sont pas compatibles avec les services de paiement et l’intégration de Signify :

* Lorsque [!DNL Payment Services] est configuré avec l&#39;action de paiement `Authorize` _et_ Signifyd est en mode `PostAuth` avec l&#39;option _[!UICONTROL Decline Guarantees]_définie sur **Créer un avoir**.

  Motif : [!DNL Payment Services] crée une transaction d’autorisation que Signify tente ensuite de rembourser.


* [!DNL Payment Services] est configuré avec l’action de paiement `Authorize and Capture` _et_ Signifyd est en mode `PostAuth` avec l’option _[!UICONTROL Decline Guarantees]_définie sur **Annuler la commande**.

  Motif : [!DNL Payment Services] crée une transaction de capture que Signifyd tente ensuite d’annuler.


Consultez la documentation de Signifyd pour plus d’informations sur [la configuration de l’extension](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension).

Voir la documentation Signifyd pour [en savoir plus sur les workflows de commande](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works).
