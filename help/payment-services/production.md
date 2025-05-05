---
title: Activer pour  [!DNL Payment Services]  production
description: Terminez le processus d’intégration en activant pour  [!DNL Payment Services]  production.
feature: Payments, Checkout, Configuration, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Activer le [!DNL Payment Services] pour la production

Vous pouvez mettre le service en production et terminer le [processus d’intégration](onboard.md), conformément aux étapes de cette rubrique, après avoir :

* [Installer](install.md) l’extension Payment Services
* [Configuration et connexion](connect.md) votre instance
* [Configurer](sandbox.md) et [tester](test-validate.md) votre sandbox

## Définir [!DNL Payment Services] comme mode de paiement

Après avoir [configuré vos services Commerce](connect.md#configure-commerce-services) et activé [test de sandbox](sandbox.md#enable-sandbox-testing) ou [paiements en direct](#enable-live-payments), vous devez définir [!DNL Payment Services] comme mode de paiement.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Cliquez sur **[!UICONTROL Enable Payment Services]**.

   Cette option est visible si vous n’avez pas encore configuré [!DNL Payment Services] comme mode de paiement pour un ou plusieurs de vos sites web.

   Vous accédez à la zone des paramètres de la vue d’accueil avec les options appropriées développées (**[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Settings]_), où vous pouvez activer les options [!DNL Payment Services] comme [mode de paiement](https://experienceleague.adobe.com/fr/docs/commerce-admin/config/sales/payment-methods/payment-methods){target="_blank"}.

1. Dans _[!UICONTROL General Configuration]_, définissez **[!UICONTROL Enable]**&#x200B;sur `Yes`.
1. Définissez **[!UICONTROL Payment Action]**, pour les _[!UICONTROL Credit Card Fields]_&#x200B;et les&#x200B;_[!UICONTROL PayPal payment buttons]_, sur l’une des options suivantes :

   | Paramètre | Description |
   |---|---|
   | `Authorize` | Valide l&#39;achat et bloque les fonds. Le montant n&#39;est pas retiré tant qu&#39;il n&#39;a pas été « capturé » par le commerçant. |
   | `Authorize and Capture` | Valide l&#39;achat et le commerçant « capture » les fonds. |

   >[!IMPORTANT]
   >
   >[!DNL Payment Services] prend en charge les captures partielles. Un commerçant peut capturer partiellement (facturer) des parties d’une commande. Par exemple, vous pouvez capturer chaque élément individuellement ou un élément maintenant et le reste plus tard.

1. Cliquez sur **[!UICONTROL Save]**.
1. Cliquez sur **[!UICONTROL Go to Payment Services]** pour être redirigé vers la page d’accueil [!DNL Payment Services].
1. [Videz votre cache](https://experienceleague.adobe.com/docs/commerce-admin/systems/tools/cache-management.html?lang=fr).

   L’effacement doit être effectué après chaque modification de la configuration.

Consultez [Configurer les services de paiement](settings.md) pour plus d’informations sur la configuration des champs de carte de crédit et des boutons de paiement PayPal.

## Intégration complète des commerçants

Pour permettre à vos magasins de mettre en ligne les services de paiement, l’étape suivante consiste à terminer l’intégration en direct.

Les services de paiement offrent des options de paiement [**avancées** (entièrement prises en charge) et **standard** (paiement express)](../payment-services/payments-options.md#standard-vs-advanced-payments-experience) ainsi que des flux d’intégration, en fonction du pays dans lequel vous opérez et de votre expérience de paiement préférée.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Cliquez sur **[!UICONTROL Live onboarding]**.

   Cette option est visible si vous n’avez pas encore terminé l’intégration en direct pour [!DNL Payment Services].

1. Dans la boîte de dialogue modale _Sélectionnez votre pays_, sélectionnez le pays à partir duquel vous effectuez vos opérations.

   Payment Services offre actuellement un support complet pour toutes les options de paiement dans [cinq pays](../payment-services/overview.md#availability). Les services de paiement offrent des fonctionnalités de paiement express (un sous-ensemble d’options de paiement) pour tous les autres pays représentés sur la liste des pays.

   Le pays que vous choisissez dans la liste détermine les options de paiement et le flux d’intégration, [avancé](#advanced-onboarding) (entièrement pris en charge) ou [standard](#standard-onboarding) (paiement express), qui vous sont disponibles.

>[!TIP]
>
> Une fois que vous avez choisi et effectué une option d’intégration (Standard ou Avancée), vous devez terminer à nouveau l’intégration pour effectuer une mise à niveau ou une rétrogradation à partir de votre sélection initiale.

### Intégration avancée

Ce flux d’intégration est disponible pour les commerçants dans [pays entièrement pris en charge](../payment-services/overview.md#availability).

Une fois le pays sélectionné :

1. Dans la boîte de dialogue modale qui s’affiche, sélectionnez **Avancé**.

   Pour l’option **Standard**, passez au [Flux d’intégration standard](#standard-onboarding).

1. Cliquez sur **Continuer**.
1. Continuez avec le flux PayPal pour l’intégration avancée entièrement prise en charge, en utilisant les informations d’identification de votre compte PayPal (et non celles de votre compte sandbox) _ou_ inscrivez-vous à un nouveau compte PayPal.

>[!IMPORTANT]
>
>**Intégration avancée** nécessite que les commerçants [demandent des droits de paiement](#request-payments-entitlement-from-adobe) pour activer l’intégration en direct.

### Intégration standard

Ce flux d’intégration standard est disponible pour les commerçants dans les pays disponibles pour lesquels [seule la prise en charge du passage en caisse express](../payment-services/overview.md#availability) est fournie.

Une fois le pays sélectionné :

1. Dans la fenêtre modale _Accord de services de paiement_ qui s’affiche, cliquez sur le lien **Accord de services de paiement** pour afficher l’accord de services de paiement Adobe Commerce.
1. Dans la fenêtre modale _Accord de services de paiement_, cliquez sur **J’accepte**.
1. Continuez avec le flux PayPal pour l&#39;intégration du paiement express, en utilisant les informations d&#39;identification de votre compte PayPal (et non celles de votre compte Sandbox) ou inscrivez-vous à un nouveau compte PayPal.

>[!IMPORTANT]
>
>Les champs [Apple Pay et carte de crédit](../payment-services/payments-options.md) ne sont pas disponibles pour l’**intégration standard**.

## Confirmer l’adresse e-mail

1. Dans la barre latérale d’administration, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**

   Le bouton _[!UICONTROL Live onboarding]_&#x200B;n’est plus visible et une zone de texte « [!UICONTROL Live payments pending] » s’affiche.

   Dans cette zone de texte, vous pouvez également être invité à confirmer votre adresse e-mail auprès de PayPal pour terminer l&#39;intégration.

1. Si vous êtes invité à confirmer votre adresse e-mail, recherchez le message de confirmation envoyé par PayPal dans votre e-mail et cliquez pour confirmer votre adresse e-mail.
1. Dans la barre latérale d’administration, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Actualisez la fenêtre de votre navigateur.

   Lorsque l&#39;intégration de votre marchand PayPal est approuvée, vous devriez voir une notification indiquant que votre système de paiement est en mode sandbox et ne traite pas les paiements en direct.

   >[!IMPORTANT]
   >
   >Si vous révoquez le consentement à [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source] pour le traitement de vos paiements (dans les paramètres de votre compte PayPal), les commandes dans votre boutique ne peuvent pas être traitées par [!DNL Payment Services]. Sur votre page d’accueil des services de paiement, une alerte concernant le consentement révoqué s’affiche.

## Demander des droits de paiement à Adobe

Pour activer vos magasins, demandez les droits de paiement à Adobe (pour [Intégration avancée uniquement](#advanced-onboarding)) :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Cliquez sur **[!UICONTROL Get Live Payments]** dans la page d’accueil [!DNL Payment Services].

   ![Droits de demande](assets/request-entitlements.png){width="500" zoomable="yes"}

1. Remplissez le formulaire.
1. Un membre de l&#39;équipe des ventes vous contactera.

Vous pouvez également demander des droits de paiement à Adobe à l’adresse [business.adobe.com](https://business.adobe.com/resources/payment-services.html).

>[!IMPORTANT]
>
>L’**intégration en direct** n’est pas accessible tant que les droits aux paiements n’ont pas été approuvés.

## Configurer le niveau de tarification

Obtenez votre [!DNL Payment Services] _Identifiant marchand_ :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Dans la vue d’accueil, cliquez sur **[!UICONTROL Settings]**. Voir [Accueil](payments-home.md) pour plus d’informations.
1. Sélectionnez l’_ID de commerçant_ requis et envoyez-le à votre représentant commercial, qui configurera le niveau tarifaire correct.

Voir [Traitement de niveau 2 et de niveau 3](levels-card-payment-transactions.md) pour plus d&#39;informations sur les opérations de paiement.

## Activer les paiements dynamiques

Un _ID de commerçant de production_ est généré automatiquement et renseigné dans la [configuration](configure-admin.md). Ne modifiez pas cet identifiant.

Activer les paiements dynamiques :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Sur l’Accueil, cliquez sur **[!UICONTROL Settings]** en haut à droite de la page. Voir [Accueil](payments-home.md) pour plus d’informations.
1. Dans la section _[!UICONTROL General Configuration]_, définissez **[!UICONTROL Payment mode]**&#x200B;sur `Production`.
1. Cliquez sur **[!UICONTROL Save]**.
1. [Videz votre cache](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/tools/cache-management){target="_blank"}.

   >[!IMPORTANT]
   >
   >Si vous ne videz pas votre cache, les clients ne pourront pas voir les options de paiement PayPal lors du passage en caisse.

Si vous revenez à [!DNL Payment Services] page d’accueil, le message Mode de paiement Sandbox n’apparaît plus, car vous traitez désormais des paiements dynamiques.

Voir [Configurer dans Admin](configure-admin.md) pour connaître les options de configuration héritées.

>[!IMPORTANT]
>
>Si vous révoquez votre consentement à [!DNL Payment Services] pour le traitement de vos paiements (dans les paramètres de votre compte PayPal), les commandes dans votre boutique ne peuvent pas être traitées par [!DNL Payment Services]. Si vous souhaitez réactiver le traitement des paiements, vous devez terminer à nouveau l’intégration. Sur votre page d’accueil des services de paiement, une alerte concernant le consentement révoqué s’affiche.

## Test en production

Il est vivement recommandé de tester Paiements en production, avec des cartes de crédit et des banques réelles, avant de présenter cette fonctionnalité aux acheteurs.

Voir [Tester et valider](test-validate.md) pour plus d’informations.
