---
title: Paramètres des services de paiement
description: Après l’installation, vous pouvez configurer  [!DNL Payment Services]  dans l’Accueil.
role: Admin, User
level: Intermediate
exl-id: 108f2b24-39c1-4c87-8deb-d82ee1c24d55
feature: Payments, Checkout, Configuration, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '2420'
ht-degree: 0%

---

# Paramètres

Vous pouvez personnaliser les [!DNL Payment Services] en fonction de vos besoins à l’aide des paramètres utiles dans la page d’accueil [!DNL Payment Services].

Pour configurer [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source] cliquez sur **[!UICONTROL Settings]**. Ces options de configuration s’appliquent uniquement à l’environnement défini dans le champ _[!UICONTROL Payment mode]_&#x200B;des options de configuration[_ Général _](#configure-general-settings).

Pour une configuration multi-magasin ou héritée, voir [Configurer dans l’administration](configure-admin.md).

## Configurer les paramètres généraux

Les paramètres [!UICONTROL General] permettent d’activer ou de désactiver les services de paiement en tant que mode de paiement et d’ajouter des informations aux transactions client pour marquer ou préfixer un site web ou une vue de boutique avec des informations personnalisées.

### Activer les services de paiement

Vous pouvez activer [!DNL Payment Services] pour votre site web et activer les tests de sandbox ou les paiements en direct.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

1. Cliquez sur **[!UICONTROL Settings]**. Voir [Introduction à l’accueil [!DNL Payment Services]  ](payments-home.md) pour plus d’informations.

   ![Vue des paramètres React](assets/react-settings-view.png){width="500" zoomable="yes"}

   La section _[!UICONTROL General]_&#x200B;comprend les paramètres utilisés pour activer [!DNL Payment Services] comme mode de paiement.

1. Dans la section [!DNL Payment Services], pour activer _[!UICONTROL General]_&#x200B;comme mode de paiement pour votre boutique, basculez **[!UICONTROL Enable Payment Services as payment method]**&#x200B;sur `Yes`.

1. Si vous testez toujours [!DNL Payment Services] pour votre boutique, définissez **Mode de paiement** sur `Sandbox`. Si vous êtes prêt à activer les paiements dynamiques, définissez-le sur `Production`.

1. Vos valeurs **[!UICONTROL Payment Services Sandbox ID]** et **[!UICONTROL Payment Services Production ID]** sont automatiquement renseignées une fois que vous avez configuré le [connecteur de services Commerce](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} et que vous avez consulté le tableau de bord [!DNL Payment Services] pour la première fois. Effectuez cette opération pour terminer l’intégration de votre sandbox et/ou de vos environnements de production. Ces valeurs associent votre identifiant SaaS à [!DNL Payment Services].

   >[!WARNING]
   >
   > Si vous réinitialisez vos identifiants [!DNL Payment Services], vous devez procéder à une nouvelle intégration.

1. Cliquez sur **[!UICONTROL Save]**.

   Si vous tentez de quitter cet affichage sans enregistrer vos modifications, une boîte de dialogue modale s’affiche pour vous inviter à ignorer les modifications, à continuer à les modifier ou à les enregistrer.

1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]** et cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

Vous pouvez maintenant procéder à la modification des paramètres par défaut pour [options de paiement](#configure-payment-options) fonctions et affichage storefront.

### Ajouter un descripteur logiciel

Vous pouvez ajouter un [!UICONTROL Soft Descriptor] à la configuration de vos sites web ou de vos vues de magasin individuelles. Les descripteurs soft s’affichent sur les relevés bancaires des transactions client. Si vous disposez de plusieurs magasins/marques/catalogues, par exemple, vous pouvez facilement les délimiter en ajoutant du texte personnalisé au champ [!UICONTROL Soft Descriptor].

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Cliquez sur **[!UICONTROL Settings]**. Voir [Introduction à l’accueil [!DNL Payment Services]  ](payments-home.md) pour plus d’informations.
1. Sélectionnez la vue du site web ou du magasin, dans le menu déroulant **[!UICONTROL Scope]**, pour laquelle vous souhaitez créer un descripteur logiciel. Pour la configuration initiale, laissez ceci comme **[!UICONTROL Default]** pour définir la valeur par défaut.
1. Ajoutez votre texte personnalisé (jusqu’à 22 caractères) dans le champ de texte, en remplaçant `Soft descriptor`.
1. Cliquez sur **[!UICONTROL Save]**.
1. Pour créer un descripteur logiciel autre que la valeur par défaut configurée pour une vue de site web ou de boutique :
   1. Sélectionnez la vue du site web ou du magasin, dans le menu déroulant **[!UICONTROL Scope]**, pour laquelle vous souhaitez créer un descripteur logiciel.
   1. Basculez _désactivé_ **[!UICONTROL Use website]** (ou **[!UICONTROL Use default]**, selon la portée que vous avez sélectionnée).
   1. Ajoutez votre texte personnalisé dans le champ de texte.
   1. Cliquez sur **[!UICONTROL Save]**.
1. Pour activer pour un site web ou un magasin l’affichage du descripteur paramétré par défaut _ou_ le descripteur paramétré utilisé pour le site web parent :
   1. Dans le menu déroulant **[!UICONTROL Scope]**, sélectionnez la vue de site web ou de boutique pour laquelle vous souhaitez activer un descripteur logiciel existant.
   1. Activez _on_ **[!UICONTROL Use website]** (ou **[!UICONTROL Use default]**, selon la portée que vous avez sélectionnée).
   1. Cliquez sur **[!UICONTROL Save]**.

   Si vous tentez de quitter cet affichage sans enregistrer vos modifications, une boîte de dialogue modale s’affiche pour vous inviter à ignorer les modifications, à continuer à les modifier ou à les enregistrer.

### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Enable] | site internet | Activez ou désactivez [!DNL Payment Services] pour votre site web. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Payment mode] | vue magasin | Définissez la méthode, ou l’environnement, de votre magasin. Options : [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | vue magasin | Votre ID de marchand de sandbox, qui est généré automatiquement lors de l’intégration au sandbox. |
| [!UICONTROL Payment Services Production ID] | vue magasin | Votre ID de commerçant de production, qui est généré automatiquement lors de l’intégration de la production (en direct). |
| [!UICONTROL Soft Descriptor] | affichage du site web ou de la boutique | Ajoutez un descripteur à vos sites web et vue(s) de boutique pour ajouter des informations aux transactions client qui délimitent les marques, les boutiques ou les lignes de produits. Le bouton (bascule) [!UICONTROL Use website] applique tout descripteur logiciel ajouté au niveau du site web. Le bouton (bascule) [!UICONTROL Use default] applique tout descripteur logiciel ajouté par défaut. |

## Configurer les options de paiement

Maintenant que vous avez activé [!UICONTROL Payment Services] pour votre site web, vous pouvez modifier les paramètres par défaut des fonctions de paiement et de l’affichage du storefront.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Cliquez sur **[!UICONTROL Settings]**. Voir [Introduction à l’accueil [!DNL Payment Services]  ](payments-home.md) pour plus d’informations.
1. Configurez les options de paiement pour [cartes de crédit](#credit-card-fields), [boutons de paiement](#payment-buttons) et [style de bouton](#button-style), conformément aux sections suivantes.

### Champs de carte de crédit

Les paramètres _[!UICONTROL Credit Card Fields]_&#x200B;offrent une option de paiement simple et sécurisée pour les modes de paiement par carte de crédit ou de débit.

Voir [Options de paiement](payments-options.md#credit-card-fields) pour plus d’informations.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Sélectionnez la vue de magasin, dans le menu déroulant **[!UICONTROL Scope]**, pour laquelle vous souhaitez activer un mode de paiement.
1. Dans la section **[!UICONTROL Credit card fields]** , modifiez la valeur du champ **[!UICONTROL Checkout title]** pour modifier le nom du mode de paiement affiché lors du passage en caisse.
1. Pour [définir l&#39;action de paiement](production.md#set-payment-services-as-payment-method), **[!UICONTROL Payment action]** sur `Authorize` ou `Authorize and Capture`.
1. Pour donner la priorité à un mode de paiement sur la page de passage en caisse, indiquez une valeur de `Numeric Only` dans le champ **[!UICONTROL Sort order]** .
1. Pour activer l’authentification sécurisée [3DS](security.md#3ds) (`Off` par défaut), basculez le sélecteur de **[!UICONTROL 3DS Secure authentication]** sur `Always` ou `When required`.
1. Pour activer ou désactiver les champs de carte de crédit sur la page de passage en caisse, activez le sélecteur de **[!UICONTROL Show on checkout page]**.
1. Pour activer ou désactiver le [coffre de cartes](#card-vaulting), activez le sélecteur de **[!UICONTROL Vault enabled]**.
1. Pour activer ou désactiver les [modes de paiement coffrés dans l’administrateur](#card-vaulting) (pour que les commerçants puissent passer des commandes pour les clients de l’administrateur à l’aide de leur mode de paiement coffré), activez le sélecteur de **[!UICONTROL Show vaulted methods in Admin]**.
1. Pour activer ou désactiver le mode de débogage, activez/désactivez le sélecteur de **[!UICONTROL Debug Mode]**.
1. Cliquez sur **[!UICONTROL Save]**.

   Si vous tentez de quitter cet affichage sans enregistrer vos modifications, une boîte de dialogue modale s’affiche pour vous inviter à ignorer les modifications, à continuer à les modifier ou à les enregistrer.

1. [Videz le cache](#flush-the-cache).

#### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Title] | vue magasin | Ajoutez le texte à afficher comme titre pour cette option de paiement dans la vue Mode de paiement lors du passage en caisse. Options : [!UICONTROL text field] |
| [!UICONTROL Payment Action] | site internet | [action de paiement](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} pour le mode de paiement spécifié. Options : [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | vue magasin | Ordre de tri du mode de paiement spécifié dans la page de passage en caisse. valeur `Numeric Only` |
| [!UICONTROL 3DS Secure authentication] | site internet | Activez ou désactivez l’authentification sécurisée [3DS](security.md#3ds). Options : [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Show on checkout page] | site internet | Activez ou désactivez les champs de carte de crédit à afficher sur la page de passage en caisse. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Vault enabled] | vue magasin | Activez ou désactivez [chambre forte de carte de crédit](vaulting.md). Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show vaulted payment methods in Admin] | vue magasin | Activez ou désactivez la possibilité pour le marchand de passer des commandes pour les clients dans l&#39;Admin [à l&#39;aide d&#39;un mode de paiement en chambre forte](vaulting.md). Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | site internet | Activez ou désactivez le mode de débogage. Options : [!UICONTROL Off] / [!UICONTROL On] |

### Apple Pay

L’option de paiement par bouton [!UICONTROL Apple Pay] vous permet de fournir un bouton de paiement [!UICONTROL Apple Pay] dans le passage en caisse de votre boutique à partir du navigateur Safari (jusqu’à 99 domaines par compte commercial).

Vous ne pouvez utiliser Apple Pay que si vous avez terminé l’auto-inscription à [Apple Pay via Paypal](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) puis [paramétrez Apple Pay](configure-admin.md/#payment-buttons) pour vos magasins.

Voir [Options de paiement](payments-options.md#apple-pay-button) pour plus d’informations.

Vous pouvez activer et configurer l’option de paiement du bouton [!UICONTROL Apple Pay] :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Sélectionnez la vue de magasin, dans le menu déroulant **[!UICONTROL Scope]**, pour laquelle vous souhaitez activer un mode de paiement.
1. Dans la section **[!UICONTROL Apple Pay]** , modifiez la valeur du champ _[!UICONTROL Checkout title]_&#x200B;pour modifier le nom du mode de paiement affiché lors du passage en caisse.
1. Pour [définir l&#39;action de paiement](production.md#set-payment-services-as-payment-method), **[!UICONTROL Payment action]** sur `Authorize` ou `Authorize and Capture`.
1. Pour activer ou désactiver Apple Pay sur la page de passage en caisse, activez/désactivez le sélecteur de **[!UICONTROL Show Apple Pay on checkout page]**.
1. Pour activer ou désactiver Apple Pay dans la page des détails du produit, activez/désactivez le sélecteur de **[!UICONTROL Show Apple Pay on product detail page]**.
1. Pour activer ou désactiver Apple Pay dans l’aperçu du mini panier, activez ou désactivez le sélecteur de **[!UICONTROL Show Apple Pay on the mini cart preview]**.
1. Pour activer ou désactiver Apple Pay dans la page du panier, activez ou désactivez le sélecteur de **[!UICONTROL Show Apple Pay on cart page]**.
1. Pour activer ou désactiver le mode de débogage, activez/désactivez le sélecteur de **[!UICONTROL Debug Mode]**.
1. Cliquez sur **[!UICONTROL Save]**.

   Si vous tentez de quitter cet affichage sans enregistrer vos modifications, une boîte de dialogue modale s’affiche pour vous inviter à ignorer les modifications, à continuer à les modifier ou à les enregistrer.

1. [Videz le cache](#flush-the-cache).

#### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Checkout title] | vue magasin | Ajoutez le texte à afficher comme titre pour cette option de paiement dans la vue Mode de paiement lors du passage en caisse. Options : [!UICONTROL text field] |
| [!UICONTROL Payment Action] | site internet | [action de paiement](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions) pour le mode de paiement spécifié. Options : [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | site internet | Activez ou désactivez le bouton Apple Pay à afficher sur la page de passage en caisse. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on checkout page] | site internet | Activez ou désactivez le bouton Apple Pay à afficher sur la page des détails du produit. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on mini cart preview] | site internet | Activez ou désactivez le bouton Apple Pay à afficher en prévisualisation de mini panier. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show on cart page] | site internet | Activez ou désactivez le bouton Apple Pay à afficher sur la page du panier. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | site internet | Activez ou désactivez le mode de débogage. Options : [!UICONTROL Off] / [!UICONTROL On] |

### Boutons de paiement

Les options de paiement [!DNL PayPal payment buttons] offrent un processus de paiement simple, rapide et sécurisé pour votre client. Voir [Options de paiement](payments-options.md#paypal-smart-buttons) pour plus d’informations.

Vous pouvez activer et configurer les options de paiement des boutons de paiement PayPal :

1. Sélectionnez la vue de magasin, dans le menu déroulant **[!UICONTROL Scope]**, pour laquelle vous souhaitez activer un mode de paiement.
1. Pour modifier le nom du mode de paiement tel qu&#39;il s&#39;affiche lors du passage en caisse, modifiez la valeur dans le champ **[!UICONTROL Checkout Title]**.
1. Pour [définir l&#39;action de paiement](production.md#set-payment-services-as-payment-method), **[!UICONTROL Payment action]** sur `Authorize` ou `Authorize and Capture`.
1. Pour donner la priorité à un mode de paiement sur la page de passage en caisse, indiquez une valeur de `Numeric Only` dans le champ **[!UICONTROL Sort order]** .
1. Utilisez les sélecteurs de bascule pour activer ou désactiver [!DNL PayPal smart button] fonctionnalités d’affichage :

   - **[!UICONTROL Show PayPal buttons on product checkout page]**
   - **[!UICONTROL Show PayPal buttons on product detail page]**
   - **[!UICONTROL Show PayPal buttons in mini-cart preview]**
   - **[!UICONTROL Show PayPal buttons on cart page]**
   - **[!UICONTROL Show PayPal Pay Later button]**
   - **[!UICONTROL Show PayPal Pay Later message]**
   - **[!UICONTROL Show Venmo button]**
   - **[!UICONTROL Show Apple Pay button]**
   - **[!UICONTROL Show PayPal Credit and Debit Card button]**

     >[!NOTE]
     >
     > Pour utiliser Apple Pay, vous [devez disposer d’un compte de testeur de sandbox Apple](https://developer.apple.com/apple-pay/sandbox-testing/#create-a-sandbox-tester-account) (comportant une fausse carte de crédit et des informations de facturation) pour le tester. Lorsque vous êtes prêt à utiliser Apple Pay en mode sandbox _ou_ production, après avoir terminé les [tests et validation](test-validate.md#test-in-sandbox-environment), effectuez l’auto-enregistrement [avec [!DNL Apple Pay]](https://developer.paypal.com/docs/checkout/apm/apple-pay/#register-your-live-domain) (_Enregistrement de votre domaine actif_ section uniquement) et configurez-le pour vos magasins en [!DNL Payment Services].

     Lorsque vous activez/désactivez la visibilité des boutons de paiement ou du message PayPal Pay Later, un aperçu visuel de cette configuration s’affiche au bas de la page Paramètres.

1. Pour activer le mode de débogage, activez le sélecteur de **[!UICONTROL Debug Mode]**.
1. Cliquez sur **[!UICONTROL Save]**.

   Si vous tentez de quitter cet affichage sans enregistrer vos modifications, une boîte de dialogue modale s’affiche pour vous inviter à ignorer les modifications, à continuer à les modifier ou à les enregistrer.

1. [Videz le cache](#flush-the-cache).

#### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Title] | vue magasin | Ajoutez le texte à afficher comme titre pour cette option de paiement dans la vue Mode de paiement lors du passage en caisse. Options : champ de texte |
| [!UICONTROL Payment Action] | site internet | [action de paiement](https://experienceleague.adobe.com/en/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} pour le mode de paiement spécifié. Options : [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | vue magasin | Ordre de tri du mode de paiement spécifié dans la page de passage en caisse. valeur `Numeric Only` |
| [!UICONTROL Show PayPal buttons on checkout page] | vue magasin | Activez ou désactivez [!DNL PayPal payment buttons] sur la page de passage en caisse. Options : [!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons on product detail page] | vue magasin | Activez ou désactivez [!DNL PayPal payment buttons] dans la page des détails du produit. Options : [!UICONTROL &#x200B; Yes] / [!UICONTROL No] |
| [!UICONTROL Show PayPal buttons in mini-cart preview] | vue magasin | Activez ou désactivez l’[!DNL PayPal payment buttons] dans l’aperçu du mini-panier. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal buttons on cart page] | vue magasin | Activez ou désactivez l’[!DNL PayPal payment buttons] sur la page du panier. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later button] | vue magasin | Activez ou désactivez l&#39;apparence de l&#39;option de paiement différé lorsque des boutons de paiement sont affichés. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Pay Later Message] | site internet | Activez ou désactivez le message Payer plus tard dans le panier, la page produit, le mini-panier et pendant le flux de passage en caisse. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Venmo button] | vue magasin | Activez ou désactivez l&#39;option de paiement Venmo où les boutons de paiement sont affichés. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show Apple Pay button] | vue magasin | Activez ou désactivez l’option de paiement Apple Pay dans laquelle les boutons de paiement sont affichés. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Show PayPal Credit and Debit card button] | vue magasin | Activez ou désactivez l’option de paiement par carte de crédit et de débit où s’affichent les boutons de paiement. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Debug Mode] | site internet | Activez ou désactivez le mode de débogage. Options : [!UICONTROL Off] / [!UICONTROL On] |

### Style de bouton

Vous pouvez également configurer les options de _[!UICONTROL Button style]_&#x200B;des boutons de paiement :

1. Pour modifier le **[!UICONTROL Layout]**, sélectionnez `Vertical` ou `Horizontal`.

   >[!NOTE]
   >
   > Si le style de bouton est configuré comme `Horizontal` et que votre boutique est configurée pour afficher plusieurs boutons de paiement, vous pouvez uniquement voir deux boutons affichés sur la page du produit, la page de passage en caisse et le mini-panier, ainsi qu’un bouton affiché dans le panier.

1. Pour activer le sélecteur de balises dans une disposition horizontale, activez/désactivez le sélecteur de **[!UICONTROL Show tagline]**.
1. Pour modifier la **[!UICONTROL Color]**, sélectionnez l’option de couleur de votre choix.
1. Pour modifier le **[!UICONTROL Shape]**, sélectionnez `Pill` ou `Rectangle`.
1. Pour activer le sélecteur de hauteur de bouton, activez le sélecteur de **[!UICONTROL Responsive button height]**.
1. Pour modifier le **[!UICONTROL Label]**, sélectionnez l’option de libellé de votre choix.

   Lorsque vous modifiez les options de configuration de la disposition, de la couleur, de la forme, de la hauteur et de l’étiquette, un aperçu visuel de cette configuration s’affiche au bas de la page Paramètres. Dans l’image ci-dessous, la **[!UICONTROL Shape]** est définie sur _Rectangle_ et la **[!UICONTROL Label]** sur _PayPal (recommandé)_.

   ![[!DNL PayPal payment buttons] options](assets/payment-buttons.png){width="400" zoomable="yes"}

1. Cliquez sur **[!UICONTROL Save]**.

   Si vous tentez de quitter cet affichage sans enregistrer vos modifications, une boîte de dialogue modale s’affiche pour vous inviter à ignorer les modifications, à continuer à les modifier ou à les enregistrer.

1. [Videz le cache](#flush-the-cache).

Vous pouvez configurer le style du bouton de paiement [dans la configuration héritée dans Admin](configure-admin.md#configure-paypal-smart-buttons) ou ici dans [!DNL Payment Services Home]. Pour plus d&#39;informations sur le style des boutons de paiement PayPal[ consultez le ](https://developer.paypal.com/docs/checkout/standard/customize/buttons-style-guide/)Guide de style des boutons PayPal.

#### Options de configuration

| Champ | Portée | Description |
|--- |--- |--- |
| [!UICONTROL Layout] | Affichage de la boutique | Définissez le style de disposition des boutons de paiement. Options : [!UICONTROL Vertical] / [!UICONTROL Horizontal] |
| [!UICONTROL Tagline] | Affichage de la boutique | Activez/désactivez le slogan. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Color] | Affichage de la boutique | Définissez la couleur des boutons de paiement. Options : [!UICONTROL Blue] / [!UICONTROL Gold] / [!UICONTROL Silver] / [!UICONTROL White] / [!UICONTROL Black] |
| [!UICONTROL Shape] | Affichage de la boutique | Définissez la forme des boutons de paiement. Options : [!UICONTROL Rectangular] / [!UICONTROL Pill] |
| [!UICONTROL Responsive Button Height] | Affichage de la boutique | Définit si les boutons de paiement utilisent une hauteur par défaut. Options : [!UICONTROL Off] / [!UICONTROL On] |
| [!UICONTROL Height] | Affichage de la boutique | Définissez la hauteur des boutons de paiement. Valeur par défaut : aucune |
| [!UICONTROL Label] | Affichage de la boutique | Définissez le libellé qui s’affiche dans les boutons de paiement. Options : [!UICONTROL PayPal] / [!UICONTROL Checkout] / [!UICONTROL Buynow] / [!UICONTROL Pay] / [!UICONTROL Installment] |

## Configuration des rôles

Pour que les utilisateurs administrateurs puissent créer et gérer des commandes dans Commerce Admin, activez les ressources spécifiques aux [!DNL Payment Services] pour les rôles utilisateur.

Voir [Rôles utilisateur](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions-user-roles.html) pour savoir comment gérer les rôles.

Lors de l’affectation de ressources au rôle, vous devez sélectionner les éléments suivants :

- **Payer avec[!DNL Payment Services]** : cette ressource permet de s’assurer que, lorsque vous créez une commande dans l’administrateur, [!DNL Payment Services] cartes de crédit sont disponibles comme mode de paiement. Si vous sélectionnez la ressource parent **Actions**, cette ressource sera également sélectionnée.
- **[!DNL Payment Services]** : cette ressource comprend les ressources **Tableau de bord** et **Proxy de services SaaS**, qui doivent également être sélectionnées. Elles permettent de s’assurer que [!DNL Payment Services] apparaît dans le menu _Ventes_.

  ![Ressources Payment Services](assets/roles-payments.png){width="400" zoomable="yes"}

## Vider le cache

Si vous modifiez la configuration dans _Paramètres_, par exemple en appuyant sur les boutons Apple Pay, Venmo ou PayPal PayLater, videz manuellement le cache afin que votre boutique affiche les dernières configurations.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**.
1. Cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

Si un type de cache de la table Gestion du cache a un statut `INVALIDATED`, votre boutique risque de ne pas afficher la configuration la plus récente pour cet élément. Videz le cache pour mettre à jour votre magasin afin d’afficher la configuration la plus récente.

Pour vous assurer que votre magasin affiche la configuration correcte, videz régulièrement [le cache](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cache-management).

## Coffre de cartes

Vous pouvez activer la fonctionnalité permettant à vos clients de mettre en chambre forte (ou « enregistrer ») leurs informations de carte de crédit dans leur compte Mon compte pour les achats futurs.

Vous pouvez également utiliser le stockage des cartes dans l’administrateur pour terminer les commandes suivantes pour les clients existants.

Activez ou désactivez le coffre de cartes dans les [Paramètres des champs de carte de crédit](#credit-card-fields).

Pour plus d’informations, consultez [chambre forte de carte de crédit](vaulting.md).

## 3DS

3DS protège les clients et les commerçants contre les activités frauduleuses dans leurs magasins et permet de se conformer aux normes de l&#39;Union européenne (UE).

Activez ou désactivez 3DS dans les paramètres de champ [Carte de crédit](#credit-card-fields).

Voir [3DS dans Sécurité](security.md#3ds) pour plus d’informations.

## Utiliser plusieurs comptes PayPal

En [!UICONTROL Payment Services], vous pouvez utiliser plusieurs comptes PayPal dans **un** compte marchand au niveau du site web. Par exemple, si vous exploitez vos magasins dans plusieurs pays (qui utilisent différentes [devises](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/site-store/currency/currency)) ou si vous souhaitez utiliser Adobe Commerce pour certaines parties de votre entreprise, mais pas _toutes_, vous pouvez configurer votre compte commercial pour utiliser plusieurs comptes PayPal.

Consultez [Site, magasin et portée d’affichage](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) pour plus d’informations sur la hiérarchie des sites web, des magasins et des vues de magasin.

Consultez [Configuration de ligne de commande](configure-cli.md#configure-scope-via-cli) pour plus d’informations sur la configuration des portées de plusieurs comptes PayPal via l’interface de ligne de commande.

Votre représentant commercial peut créer une nouvelle [portée](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) pour votre compte marchand et intégrer le site supplémentaire avec PayPal afin que tous les boutons PayPal que vous configurez pour apparaître s&#39;affichent sur votre site. Contactez votre représentant commercial pour obtenir de l’aide sur l’utilisation de plusieurs comptes PayPal pour vos sites web.
