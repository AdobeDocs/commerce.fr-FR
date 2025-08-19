---
title: Configuration [!DNL Payment Services]
description: Après l’installation, vous pouvez effectuer la configuration  [!DNL Payment Services]  dans l’Administration au niveau de la configuration du magasin.
role: Admin, User
level: Intermediate
exl-id: e1a3269d-bdf9-4b0f-972f-e8a0ef469503
feature: Payments, Checkout, Configuration
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '2568'
ht-degree: 0%

---

# Configuration [!DNL Payment Services]

Vous pouvez personnaliser des [!DNL Payment Services] en fonction de vos besoins à l’aide des options de configuration utiles dans l’Administration.

Lorsque vous configurez [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source] dans l’Administration, ces configurations s’appliquent uniquement à l’environnement défini dans le champ _[!UICONTROL Method]_&#x200B;de&#x200B;_[!UICONTROL General Configuration]_. Toute modification apportée aux champs de configuration est indépendante du changement de la sélection _[!UICONTROL Method]_; si vous changez de méthode, vos sélections ne sont pas réinitialisées.

## Configuration générale

Vous pouvez activer les [!DNL Payment Services] pour votre boutique et votre _[!UICONTROL Merchant Location]_, ainsi que les tests de sandbox ou les paiements en direct dans la section&#x200B;_[!UICONTROL General Configuration]_ .

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Dans le panneau de gauche, développez **[!UICONTROL Sales]** et choisissez **[!UICONTROL Payment Methods]**.
1. Définissez le champ _[!UICONTROL Merchant Country]_&#x200B;dans le&#x200B;_[!UICONTROL Merchant Location]_. Si aucun _[!UICONTROL Merchant Country]_&#x200B;n’est spécifié, le&#x200B;_[!UICONTROL Default Country]_ de la configuration générale est utilisé.
1. Développez la section _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_&#x200B;pour accéder à la section&#x200B;_[!UICONTROL [!DNL Payment Services]]_ .
1. Dans la section _[!UICONTROL [!DNL Payment Services]]_, développez la section&#x200B;_[!UICONTROL General Configuration]_ .
1. Pour **Activer**, définissez-le sur `Yes` afin d’activer le [!DNL Payment Services] pour votre boutique.
1. Pour **Méthode**, définissez-la sur `Sandbox` si vous testez toujours [!DNL Payment Services] pour votre magasin ou sur `Production` si vous êtes prêt à activer les paiements dynamiques.
1. Vos valeurs **[!UICONTROL Payment Services Sandbox ID]** et **[!UICONTROL Payment Services Production ID]** sont automatiquement renseignées une fois que vous avez configuré le [connecteur de services Commerce](https://experienceleague.adobe.com/fr/docs/commerce-merchant-services/user-guides/integration-services/saas){target=_blank} et que vous avez consulté le tableau de bord [!DNL Payment Services] pour la première fois. Effectuez cette opération pour terminer l’intégration de votre sandbox et/ou de vos environnements de production. Ces valeurs associent votre identifiant SaaS à [!DNL Payment Services].

   >[!WARNING]
   >
   > Si vous devez modifier l’ID de votre espace de données dans le connecteur de services Commerce, vous devez réinitialiser votre ID de [!DNL Payment Services]. Cliquez sur **Réinitialiser l’ID des services de paiement** pour réinitialiser votre ID de sandbox. Si vous avez réinitialisé votre ID de sandbox [!DNL Payment Services], vous devez procéder à une nouvelle intégration.

1. Vos valeurs **[!UICONTROL PayPal Merchant ID]** et **[!UICONTROL PayPal Merchant Status]** sont automatiquement fournies par PayPal lorsque vous consultez le tableau de bord [!DNL Payment Services] pour la première fois.
1. Pour **Descripteur soft** (valeurs personnalisées qui s’affichent sur les relevés bancaires de transaction client pour délimiter les magasins/marques/catalogues), ajoutez votre texte personnalisé (jusqu’à 22 caractères) dans le champ de texte, en remplaçant `Soft descriptor` ou la valeur existante.
1. Cliquez sur **[!UICONTROL Save Config]** pour enregistrer vos modifications.
1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, puis cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

![Vue de la solution Adobe présentée](assets/config-view-all.png){width="700" zoomable="yes"}

### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Enable] | site internet | Activez ou désactivez [!DNL Payment Services] pour votre site web. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Method] | vue magasin | Définissez la méthode, ou l’environnement, de votre magasin. Options : [!UICONTROL Sandbox] / [!UICONTROL Production] |
| [!UICONTROL Payment Services Sandbox ID] | vue magasin | Votre ID de marchand de sandbox, qui est généré automatiquement lors de l’intégration au sandbox. |
| [!UICONTROL Payment Services Production ID] | vue magasin | Votre ID de commerçant de production, qui est généré automatiquement lors de l’intégration de la production (en direct). |
| [!UICONTROL PayPal Merchant ID] | vue magasin | Identifiant unique de votre compte PayPal Merchant, généré lors de la création de votre compte PayPal. |
| [!UICONTROL PayPal Merchant Status] | vue magasin | Statut de votre ID de vendeur PayPal. |
| [!UICONTROL Soft Descriptor] | affichage du site web ou de la boutique | Ajoutez un descripteur à vos sites web et vue(s) de boutique pour ajouter des informations aux transactions client qui délimitent les marques, les boutiques ou les lignes de produits. |

## [!UICONTROL Credit Card Fields]

Les options de paiement [!UICONTROL Credit Card Fields] offrent un passage en caisse simple et sécurisé pour les modes de paiement par carte de crédit ou de débit.

Voir [Options de paiement](payments-options.md#paypal-smart-buttons) pour plus d’informations.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Dans le panneau de gauche, développez **[!UICONTROL Sales]** et choisissez **[!UICONTROL Payment Methods]**.
1. Développez la section _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Dans la section _[!UICONTROL Payment Services]_, développez la section&#x200B;_[!UICONTROL Credit Card Fields]_ .
1. Par **[!UICONTROL Title]**, saisissez du texte (si nécessaire) pour modifier le nom du mode de paiement, comme indiqué lors du passage en caisse.
1. Pour [définir l&#39;action de paiement](production.md#set-payment-services-as-payment-method), sélectionnez **[!UICONTROL Authorize]** ou **Autoriser et capturer**.
1. Pour donner la priorité à un mode de paiement sur la page de passage en caisse, indiquez une valeur de `Numeric Only` dans le champ **[!UICONTROL Sort order]** .
1. Par **[!UICONTROL Show on checkout page]**, choisissez `Yes` pour activer les champs de carte de crédit sur la page de passage en caisse.
1. Par **[!UICONTROL Vault Enabled]**, choisissez `Yes` pour activer le stockage en chambre forte des cartes de crédit pour le passage en caisse.
1. Par **[!UICONTROL Vault Enabled in Admin]**, choisissez `Yes` pour permettre au commerçant de créer des commandes pour les clients à l’aide de leur carte de crédit voûtée.
1. Pour activer **[!UICONTROL 3D Secure authentication]** (`Off` par défaut), choisissez `Always` ou `When required`.
1. Par **[!UICONTROL Debug Mode]**, choisissez `Yes` pour activer le mode de débogage ou `No` pour le désactiver.
1. Cliquez sur **[!UICONTROL Save Config]** pour enregistrer vos modifications.
1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, puis cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Title] | vue magasin | Ajoutez le texte à afficher en tant que titre pour cette option de paiement dans la vue Mode de paiement lors du passage en caisse. Options : [!UICONTROL text field] |
| [!UICONTROL Payment Action] | site internet | [action de paiement](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=fr) pour le mode de paiement spécifié. Options : [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | vue magasin | Ordre de tri du mode de paiement spécifié dans la page de passage en caisse. valeur `Numeric Only` |
| [!UICONTROL Show on checkout page] | site internet | Activez ou désactivez les champs de carte de crédit sur la page de passage en caisse. Options : [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled] | vue magasin | Activez ou désactivez [chambre forte de carte de crédit](vaulting.md). Options : [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL Vault enabled in Admin] | vue magasin | Activez ou désactivez la possibilité pour le [commerçant de passer des commandes pour les clients dans l’administrateur](vaulting.md) à l’aide d’un mode de paiement en chambre forte. Options : [!UICONTROL Yes] / [!UICONTROL No] |
| [!UICONTROL 3D Secure authentication] | site internet | Activez ou désactivez l’authentification sécurisée [3DS](security.md#3ds). Options : [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | site internet | Activez ou désactivez le mode de débogage. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Fastlane]

[[!DNL Fastlane by PayPal]](https://www.paypal.com/us/cshelp/article/what-is-fastlane-by-paypal-help1096) est un moyen rapide et facile de payer en ligne en toute sécurité. Lors d&#39;un passage en caisse **Invité**, vous pouvez stocker en toute sécurité votre carte et les informations d&#39;expédition pour des achats encore plus rapides à l&#39;avenir.

Voir [Options de paiement](payments-options.md#fastlane-button) pour plus d’informations.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Dans le panneau de gauche, développez **[!UICONTROL Sales]** et choisissez **[!UICONTROL Payment Methods]**.
1. Développez la section _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Dans la section _[!UICONTROL Payment Services]_, développez la section&#x200B;_[!UICONTROL Fastlane]_ .
1. Pour l’activer, sélectionnez `Yes` pour la **[!UICONTROL Enable Fastlane]** (`No` la désactive).

   >[!NOTE]
   >
   > Si [!UICONTROL Fastlane] est activé, l’option de paiement [!UICONTROL Credit Card Fields] est désactivée.

1. Par **[!UICONTROL Title]**, saisissez du texte (si nécessaire) pour modifier le nom du mode de paiement, comme indiqué lors du passage en caisse. Le titre par défaut est `Credit Card (via Fastlane)`
1. Pour [définir l&#39;action de paiement](production.md#set-payment-services-as-payment-method), sélectionnez **[!UICONTROL Authorize]** ou **Autoriser et capturer**.
1. Pour donner la priorité à un mode de paiement sur la page de passage en caisse, indiquez une valeur de `Numeric Only` dans le champ **[!UICONTROL Sort order]** .
1. Indiquez si le branding [!UICONTROL Fastlane] est activé lors de l’extraction dans Adobe Commerce en définissant le champ **[!UICONTROL Enable messaging]** sur `Yes`.
1. Cliquez sur **[!UICONTROL Save Config]** pour enregistrer vos modifications.
1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, puis cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Enable Fastlane] | vue magasin | Activez ou désactivez [!DNL Fastlane] sur la page de passage en caisse. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Title] | vue magasin | Ajoutez le texte à afficher en tant que titre pour cette option de paiement dans la vue Mode de paiement lors du passage en caisse. La valeur par défaut est `Credit Card (via Fastlane)`. Options : [!UICONTROL text field] |
| [!UICONTROL Payment Action] | site internet | [action de paiement](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=fr) pour le mode de paiement spécifié. Options : [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Sort order] | vue magasin | Ordre de tri du mode de paiement spécifié dans la page de passage en caisse. valeur `Numeric Only` |
| [!UICONTROL Enable messaging] | vue magasin | Indiquez si le branding [!UICONTROL Fastlane] est activé lors de l’extraction dans Adobe Commerce. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |

### Facultatif. Paramètres de style avancés

Ces paramètres facultatifs peuvent personnaliser l’affichage de [!UICONTROL Fastlane] sur votre site web.

>[!TIP]
>
>Les styles qui ne respectent pas les directives d’accessibilité reviennent aux paramètres par défaut.

1. Dans la section _[!UICONTROL Payment Services]_, accédez à la section&#x200B;_[!UICONTROL Fastlane]_ .
1. Développez la section _[!UICONTROL Advanced Style Settings (optional)]_.
1. Modifiez les paramètres selon les besoins.
1. Cliquez sur **[!UICONTROL Save Config]** pour enregistrer vos modifications.

Consultez [Documentation pour les développeurs PayPal](https://developer.paypal.com/limited-release/accelerated-checkout-bt/) pour plus d’informations sur la personnalisation.

#### Root Settings

Ces paramètres facultatifs modifient le composant de passage en caisse [!UICONTROL Fastlane] global.

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Background Color] | vue magasin | Définit la couleur d’arrière-plan du composant. Valeurs `RGB` uniquement |
| [!UICONTROL Border Color] | vue magasin | Définit la couleur de bordure du composant. Valeurs `RGB` uniquement |
| [!UICONTROL Font Family] | vue magasin | Définit la police du composant. Seules les polices disponibles dans votre thème s’affichent |
| [!UICONTROL Font Size Base] | vue magasin | Définit la taille de la police. Uniquement `px` valeurs (pixels) |
| [!UICONTROL Padding] | vue magasin | Définit la marge intérieure dans le composant. Uniquement `px` valeurs (pixels) |
| [!UICONTROL Primary Color] | vue magasin | Définit la couleur principale du composant. Valeurs `RGB` uniquement |
| [!UICONTROL Text Color] | vue magasin | Définit la couleur principale du texte dans le composant. Valeurs `RGB` uniquement |

#### Paramètres d’entrée

Ces paramètres facultatifs s’appliquent aux champs de saisie client de votre composant [!UICONTROL Fastlane].

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Background Color] | vue magasin | Définit la couleur d’arrière-plan du composant. Valeurs `RGB` uniquement |
| [!UICONTROL Border Color] | vue magasin | Définit la couleur de bordure du composant. Valeurs `RGB` uniquement |
| [!UICONTROL Border Radius] | vue magasin | Définit le rayon de la bordure. Uniquement `px` valeurs (pixels) |
| [!UICONTROL Border Width] | vue magasin | Définit la largeur de la bordure. Uniquement `px` valeurs (pixels) |
| [!UICONTROL Focus Border Color] | vue magasin | Définit la couleur de la bordure de mise au point du composant. Valeurs `RGB` uniquement |
| [!UICONTROL Text Color Base] | vue magasin | Définit la couleur principale du texte dans le composant. Valeurs `RGB` uniquement |

## [!UICONTROL Apple Pay]

Grâce à [!DNL Apple Pay], les commerçants peuvent offrir une expérience de passage en caisse sécurisée, rapide et transparente dans Safari, prenant en charge jusqu’à 99 domaines par compte de commerçant. Le bouton [!DNL Apple Pay] renseigne automatiquement les informations de paiement, de contact et d’expédition à partir de l’appareil iOS ou macOS du client, ce qui permet des achats rapides et en une pression qui peuvent améliorer les taux de conversion.

Voir [Options de paiement](payments-options.md#apple-pay-button) pour plus d’informations.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Dans le panneau de gauche, développez **[!UICONTROL Sales]** et choisissez **[!UICONTROL Payment Methods]**.
1. Développez la section _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Dans la section _[!UICONTROL Payment Services]_, développez la section&#x200B;_[!UICONTROL Apple Pay]_ .
1. Par **[!UICONTROL Title]**, saisissez du texte (si nécessaire) pour modifier le nom du mode de paiement, comme indiqué lors du passage en caisse.
1. Pour [définir l&#39;action de paiement](production.md#set-payment-services-as-payment-method), sélectionnez **[!UICONTROL Authorize]** ou **[!UICONTROL Authorize and Capture]**.
1. Indiquez où l’option [!DNL Apple Pay] est activée dans Adobe Commerce en la sélectionnant `Yes` dans les options suivantes selon vos besoins :
   * **[!UICONTROL Show Apple Pay on checkout page]**
   * **[!UICONTROL Show Apple Pay on product detail page]**
   * **[!UICONTROL Show Apple Pay in mini cart preview]**
   * **[!UICONTROL Show Apple Pay on cart page]**
1. Pour activer le mode de débogage, sélectionnez `Yes` pour le **[!UICONTROL Debug Mode]** (`No` le désactive).
1. Pour enregistrer vos modifications, cliquez sur **[!UICONTROL Save Config]** .
1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, puis cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Title] | vue magasin | Ajoutez le texte à afficher en tant que titre pour cette option de paiement dans la vue Mode de paiement lors du passage en caisse. Options : [!UICONTROL text field] |
| [!UICONTROL Payment Action] | site internet | [action de paiement](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=fr) pour le mode de paiement spécifié. Options : [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Show on checkout page] | site internet | Activez ou désactivez [!DNL Apple Pay] sur la page de passage en caisse. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | vue magasin | Ordre de tri du mode de paiement spécifié dans la page de passage en caisse. valeur `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | vue magasin | Activez ou désactivez [!DNL Apple Pay] dans la page des détails du produit. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | vue magasin | Activez ou désactivez l’[!DNL Apple Pay] dans l’aperçu du mini-panier. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | vue magasin | Activez ou désactivez l’[!DNL Apple Pay] dans la page du panier. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | site internet | Activez ou désactivez le mode de débogage. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## [!UICONTROL Google Pay]

L&#39;option de paiement [!UICONTROL Google Pay] permet au commerçant d&#39;offrir Google Pay à ses acheteurs, qui peuvent utiliser le Google Wallet sur leurs appareils pour effectuer des achats.

Voir [Options de paiement](payments-options.md#google-pay-button) pour plus d’informations.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Dans le panneau de gauche, développez **[!UICONTROL Sales]** et choisissez **[!UICONTROL Payment Methods]**.
1. Développez la section _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Dans la section _[!UICONTROL Payment Services]_, développez la section&#x200B;_[!UICONTROL Google Pay]_ .
1. (Facultatif) Modifiez le nom du mode de paiement affiché lors du passage en caisse en saisissant le nouveau nom dans le champ **[!UICONTROL Title]**.
1. [Définissez l&#39;action de paiement](production.md#set-payment-services-as-payment-method) en sélectionnant **[!UICONTROL Authorize]** ou **[!UICONTROL Authorize and Capture]**.
1. Indiquez où l’option [!DNL Google Pay] est activée dans Adobe Commerce en la sélectionnant `Yes` dans les options suivantes selon vos besoins :
   * **[!UICONTROL Show Google Pay on checkout page]**
   * **[!UICONTROL Show Google Pay on product detail page]**
   * **[!UICONTROL Show Google Pay in mini cart preview]**
   * **[!UICONTROL Show Google Pay on cart page]**
1. Pour activer **[!UICONTROL 3D Secure authentication]** (`Off` par défaut), choisissez `Always` ou `When required`.
1. Pour activer le mode de débogage, sélectionnez `Yes` pour le **[!UICONTROL Debug Mode]** (`No` le désactive).
1. Configurez l’aspect du bouton _[!UICONTROL Google Pay]_&#x200B;en sélectionnant les **[!UICONTROL Button Color]**, les **[!UICONTROL Button Type]**&#x200B;et les **[!UICONTROL Button Style]**&#x200B;selon vos besoins.
1. Pour définir la hauteur, utilise la valeur par défaut de la hauteur définie dans **[!UICONTROL Button Style]**.
1. Pour enregistrer vos modifications, cliquez sur **[!UICONTROL Save Config]** .
1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, puis cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Title] | vue magasin | Spécifie le libellé de texte qui s&#39;affiche pour cette option de paiement dans la vue Mode de paiement lors du passage en caisse. Options : `[!UICONTROL text field]` |
| [!UICONTROL Payment Action] | site internet | [action de paiement](https://experienceleague.adobe.com/docs/commerce-admin/config/sales/payment-methods/payment-methods.html?lang=fr) pour le mode de paiement spécifié. Options : `[!UICONTROL Authorize]` / `[!UICONTROL Authorize and Capture]` |
| [!UICONTROL Show on checkout page] | site internet | Activez ou désactivez [!DNL Google Pay] sur la page de passage en caisse. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Sort order] | vue magasin | Ordre de tri du mode de paiement spécifié dans la page de passage en caisse. valeur `Numeric Only` |
| [!UICONTROL Show buttons on product detail page] | vue magasin | Activez ou désactivez [!DNL Google Pay] dans la page des détails du produit. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | vue magasin | Activez ou désactivez l’[!DNL Google Pay] dans l’aperçu du mini-panier. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | vue magasin | Activez ou désactivez l’[!DNL Google Pay] sur la page du panier. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL 3D Secure authentication] | vue magasin | Activez ou désactivez l’authentification sécurisée [3D](security.md#3ds). Options : [!UICONTROL Always] / [!UICONTROL When Required] / [!UICONTROL Off] |
| [!UICONTROL Debug Mode] | site internet | Activez ou désactivez le mode de débogage. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Button Color] | Affichage de la boutique | Définissez la couleur du bouton [!DNL Google Pay]. Options : `[!UICONTROL Default]` / `[!UICONTROL Black]` / `[!UICONTROL White]` |
| [!UICONTROL Button Type] | Affichage de la boutique | Définissez le type du bouton [!DNL Google Pay]. Options : `[!UICONTROL buy]` / `[!UICONTROL checkout]` / `[!UICONTROL order]` / `[!UICONTROL pay]` / `[!UICONTROL plain]` |

Pour plus d’informations[ consultez la documentation Options d’objet de requête de l’API Google Pay ](https://developers.google.com/pay/api/web/reference/request-objects).

## [!DNL PayPal Payment Buttons]

Les options de paiement [!DNL PayPal payment buttons] offrent un processus de paiement simple, rapide et sécurisé pour votre client.

Voir [Options de paiement](payments-options.md#paypal-smart-buttons) pour plus d’informations.

Configurer [!DNL PayPal payment buttons]

Vous pouvez activer et configurer les options de paiement des boutons de paiement PayPal dans l’administrateur :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Dans le panneau de gauche, développez **[!UICONTROL Sales]** et choisissez **[!UICONTROL Payment Methods]**.
1. Développez la section _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Dans la section _[!UICONTROL Payment Services]_, développez la section&#x200B;_[!UICONTROL PayPal payment buttons]_ .
1. Pour modifier le nom du mode de paiement tel qu&#39;il s&#39;affiche lors du passage en caisse, modifiez le champ _[!UICONTROL Title]_.
1. Pour [définir l&#39;action de paiement](production.md#set-payment-services-as-payment-method), sélectionnez **[!UICONTROL Authorize]** ou **[!UICONTROL Authorize and Capture]**.
1. Pour donner la priorité à un mode de paiement sur la page de passage en caisse, indiquez une valeur de `Numeric Only` dans le champ **[!UICONTROL Sort order]** .
1. Pour activer/désactiver la [messagerie à paiement différé](payments-options.md#pay-later-button), sélectionnez `Yes`/`No` pour **[!UICONTROL Display Pay Later Message]**.

   * Si vous activez le [message Payer plus tard](payments-options.md#pay-later-button), un bouton modal **[!UICONTROL Configure Messaging]** s’affiche pour vous permettre de définir les styles du **[!UICONTROL PayPal Pay Later messaging]**.

1. Indiquez où les boutons de paiement PayPal sont activés dans Adobe Commerce en sélectionnant `Yes` dans les options suivantes, le cas échéant :
   * **[!UICONTROL Show buttons on checkout page]**
   * **[!UICONTROL Show buttons on product detail page]**
   * **[!UICONTROL Show buttons in mini cart preview]**
   * **[!UICONTROL Show buttons on cart page]**
1. Pour activer Venmo en tant qu&#39;option de paiement, sélectionnez `Yes` pour **[!UICONTROL Venmo Enabled]**.
1. Pour activer les cartes de crédit et de débit comme option de paiement (bouton PayPal Smart), sélectionnez `Yes` pour **[!UICONTROL Credit and Debit Card Enabled]**.
1. Pour activer/désactiver l&#39;option de paiement [PayPal Pay Later](payments-options.md#pay-later-button), sélectionnez `Yes`/`No` pour **[!UICONTROL PayPal Pay Later Enabled]**.
1. Pour activer le mode de débogage, sélectionnez `Yes` pour le **[!UICONTROL Debug Mode]** (`No` le désactive).
1. Pour enregistrer vos modifications, cliquez sur **[!UICONTROL Save Config]** .
1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, puis cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

### Options de configuration

| Champ | Portée | Description |
|---|---|---|
| [!UICONTROL Title] | vue magasin | Ajoutez le texte à afficher comme titre pour cette option de paiement dans la vue Mode de paiement lors du passage en caisse. Options : champ de texte |
| [!UICONTROL Payment Action] | site internet | [action de paiement](https://experienceleague.adobe.com/fr/docs/commerce-admin/config/sales/payment-methods/payment-methods#payment-actions){target="_blank"} pour le mode de paiement spécifié. Options : [!UICONTROL Authorize] / [!UICONTROL Authorize and Capture] |
| [!UICONTROL Display Pay Later Message] | site internet | Activez ou désactivez la messagerie PayPal Pay Later dans le panier, la page produit, le mini-panier et pendant le flux de passage en caisse. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Configure Messaging] | vue magasin | Modifiez les styles de messagerie PayPal Pay Later. Options : `[!UICONTROL Product page]` / `[!UICONTROL Cart]` |
| [!UICONTROL Show buttons on checkout page] | vue magasin | Activez ou désactivez [!DNL PayPal payment buttons] sur la page de passage en caisse. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on product detail page] | vue magasin | Activez ou désactivez [!DNL PayPal payment buttons] dans la page des détails du produit. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons in mini-cart preview] | vue magasin | Activez ou désactivez l’[!DNL PayPal payment buttons] dans l’aperçu du mini-panier. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Show buttons on cart page] | vue magasin | Activez ou désactivez l’[!DNL PayPal payment buttons] dans la page du panier. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Venmo Enabled] | vue magasin | Activez ou désactivez l&#39;option de paiement Venmo où les boutons de paiement sont affichés. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Credit and Debit Card Enabled] | vue magasin | Activez ou désactivez les options des cartes de crédit et de débit où s’affichent les boutons de paiement. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL PayPal Pay Later Enabled] | vue magasin | Activez ou désactivez l&#39;apparence de l&#39;option de paiement PayPal Pay Later lorsque les boutons de paiement sont affichés. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Debug Mode] | site internet | Activez ou désactivez le mode de débogage. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Style de bouton

Vous pouvez également configurer les options de _[!UICONTROL Button style]_&#x200B;des boutons de paiement :

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. Dans le panneau de gauche, développez **[!UICONTROL Sales]** et choisissez **[!UICONTROL Payment Methods]**.
1. Développez la section _[!UICONTROL FEATURED ADOBE PAYMENT SOLUTION]_.
1. Dans la section _[!UICONTROL [!DNL Payment Services]]_, développez la section&#x200B;_[!UICONTROL PayPal Smart Button Styling]_ .
1. Pour définir la disposition, sélectionnez `Vertical` ou `Horizontal` pour **[!UICONTROL Layout]**
1. Pour définir la couleur, sélectionnez l’une des couleurs disponibles dans **[!UICONTROL Color]**.
1. Pour définir la forme, sélectionnez `Rectangular` ou `Pill` pour **[!UICONTROL Shape]**.
1. Pour utiliser la hauteur par défaut, sélectionnez `Yes` ou `No` pour **[!UICONTROL Use Default Height]**.
1. Pour définir la hauteur personnalisée, ajoutez la hauteur en pixels souhaitée pour **[!UICONTROL Height]**.
1. Pour définir le slogan, sélectionnez `Yes` ou `No` pour **[!UICONTROL Tagline]**.
1. Pour enregistrer vos modifications, cliquez sur **[!UICONTROL Save Config]** .
1. Accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**, puis cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

### Options de configuration

| Champ | Portée | Description |
|--- |--- |--- |
| [!UICONTROL Layout] | Affichage de la boutique | Définissez le style de disposition des boutons de paiement Paypal. Options : `[!UICONTROL Vertical]` / `[!UICONTROL Horizontal]` |
| [!UICONTROL Color] | Affichage de la boutique | Définissez la couleur des boutons de paiement Paypal. Options : [!UICONTROL Blue] / `[!UICONTROL Gold]` / `[!UICONTROL Silver]` / `[!UICONTROL White]` / `[!UICONTROL Black]` |
| [!UICONTROL Shape] | Affichage de la boutique | Définissez la forme des boutons de paiement Paypal. Options : `[!UICONTROL Rectangular]` / `[!UICONTROL Pill]` |
| [!UICONTROL Use Default Height] | Affichage de la boutique | Définit si les boutons de paiement PayPal utilisent une hauteur par défaut. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |
| [!UICONTROL Height] | Affichage de la boutique | Définissez la hauteur des boutons de paiement PayPal. Valeur par défaut : aucune |
| [!UICONTROL Label] | Affichage de la boutique | Définissez le libellé qui apparaît sur les boutons de paiement PayPal. Options : `[!UICONTROL PayPal]` / `[!UICONTROL Checkout]` / `[!UICONTROL Buynow]` / `[!UICONTROL Pay]` / `[!UICONTROL Installment]` |
| [!UICONTROL Tagline] | Affichage de la boutique | Active le slogan. Options : `[!UICONTROL Yes]` / `[!UICONTROL No]` |

## Vider le cache

Si vous modifiez la configuration dans _Paramètres_, par exemple en appuyant sur les boutons Apple Pay, Venmo ou PayPal PayLater, videz manuellement le cache afin que votre boutique affiche les dernières configurations.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL System]** > **[!UICONTROL Cache Management]**.
1. Cliquez sur **[!UICONTROL Flush Cache]** pour actualiser tous les caches non valides.

Si un type de cache de la table Gestion du cache a un statut `INVALIDATED`, votre boutique risque de ne pas afficher la configuration la plus récente pour cet élément. Videz le cache pour mettre à jour votre magasin afin d’afficher la configuration la plus récente.

Pour vous assurer que votre magasin affiche la configuration correcte, videz régulièrement [le cache](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/tools/cache-management).

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

En [!UICONTROL Payment Services], vous pouvez utiliser plusieurs comptes PayPal dans **un** compte marchand au niveau du site web. Par exemple, si vous exploitez vos magasins dans plusieurs pays (qui utilisent différentes [devises](https://experienceleague.adobe.com/fr/docs/commerce-admin/stores-sales/site-store/currency/currency)) ou si vous souhaitez utiliser Adobe Commerce pour certaines parties de votre entreprise, mais pas _toutes_, vous pouvez configurer votre compte commercial pour utiliser plusieurs comptes PayPal.

Consultez [Site, magasin et portée d’affichage](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=fr) pour plus d’informations sur la hiérarchie des sites web, des magasins et des vues de magasin.

Consultez [Configuration de ligne de commande](configure-cli.md#configure-scope-via-cli) pour plus d’informations sur la configuration des portées de plusieurs comptes PayPal via l’interface de ligne de commande.

Votre représentant commercial peut créer une nouvelle [portée](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html?lang=fr#scope-settings) pour votre compte marchand et intégrer le site supplémentaire avec PayPal afin que tous les boutons PayPal que vous configurez pour apparaître s&#39;affichent sur votre site. Contactez votre équipe commerciale
représentant pour obtenir de l’aide sur l’utilisation de plusieurs comptes PayPal pour vos sites web.
