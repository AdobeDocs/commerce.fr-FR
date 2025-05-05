---
title: Utilisation de Adobe Journey Optimizer pour envoyer un e-mail de panier abandonné
description: Découvrez comment utiliser Adobe Journey Optimizer pour envoyer un e-mail de panier abandonné.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---

# Utilisation de Adobe Journey Optimizer pour envoyer un e-mail de panier abandonné

Découvrez comment diffuser un e-mail de réengagement personnalisé ou une notification si une session de panier ou de navigateur a été abandonnée. Dans cet article, vous utilisez des données générées à partir de clients qui ont consulté un certain nombre de produits et de catégories, qui ont utilisé un produit ou qui ont passé du temps sur une page.

## Quelles données dois-je envisager d’utiliser ?

Créez un panier abandonné, parcourez les e-mails ou les notifications à l’aide des données issues des événements de storefront et de back-office.

| Types de données | Données Storefront (Événements Comportementaux) | Données de back-office (événements côté serveur) |
|---|---|---|
| **Définition** | Clics ou actions des clients sur votre site. | Informations sur le cycle de vie et détails de chaque commande (passée et actuelle). |
| **Événements capturés par Adobe Commerce** | [pageView](https://experienceleague.adobe.com/fr/docs/commerce/data-connection/event-forwarding/events#pageview)<br>[productPageView](https://experienceleague.adobe.com/fr/docs/commerce/data-connection/event-forwarding/events)<br>[addToCart](https://experienceleague.adobe.com/fr/docs/commerce/data-connection/event-forwarding/events#addtocart)<br>[openCart](https://experienceleague.adobe.com/fr/docs/commerce/data-connection/event-forwarding/events#opencart)<br>[startCheckout](https://experienceleague.adobe.com/fr/docs/commerce/data-connection/event-forwarding/events#startcheckout)<br>[completeCheckout](https://experienceleague.adobe.com/fr/docs/commerce/data-connection/event-forwarding/events#completecheckout) | [orderPlaced](https://experienceleague.adobe.com/fr/docs/commerce/data-connection/event-forwarding/events-backoffice#orderplaced)<br>[Order history](https://experienceleague.adobe.com/fr/docs/commerce/data-connection/fundamentals/connect-data#send-historical-order-data) |

### Qu’ont accompli les autres clients ?

Les clients Adobe [!DNL Commerce] ont obtenu un impact commercial significatif en mettant en œuvre des campagnes d’abandon personnalisées à l’aide d’Adobe [!DNL Commerce], d’Adobe [!DNL Journey Optimizer] et d’Adobe [!DNL Real-Time CDP].

Un détaillant mondial de vêtements multi-marques a réalisé :

- Conversion 1.9x en cas de clic à partir de nouvelles campagnes
- Augmentation de 57 % des revenus provenant des parcours d&#39;abandon omnicanal
- Augmentation de 41 % du taux de conversion des campagnes de réengagement
- Plus de 1 000 nouveaux acheteurs engagés par semaine

Une entreprise mondiale de boissons a obtenu :

- Taux d’ouverture des e-mails de réengagement de 36 %
- Augmentation de 21 % des taux de clics
- Augmentation de 8,5 % du taux de conversion
- 89 % des personnes abandonnées réengagées se convertissent

## Commençons

Ce cas d’utilisation particulier se concentre sur la création d’un e-mail de panier abandonné à l’aide des données de votre instance [!DNL Commerce] et leur envoi à Adobe [!DNL Journey Optimizer].

### Qu’est-ce que Adobe Journey Optimizer ?

[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html?lang=fr) vous aide à personnaliser l’expérience commerciale pour vos acheteurs. Par exemple, vous pouvez utiliser Journey Optimizer pour créer et diffuser des campagnes marketing planifiées, telles que des promotions hebdomadaires pour un magasin de vente au détail, ou pour générer un e-mail de panier abandonné si un client a ajouté un produit à un panier, mais n’a pas terminé le processus de passage en caisse.

Dans cette rubrique, vous apprendrez à créer un e-mail de panier abandonné en écoutant un événement `checkout` généré à partir de votre instance [!DNL Commerce] et en répondant à cet événement dans Journey Optimizer.

>[!IMPORTANT]
>
>À des fins de démonstration, utilisez votre environnement sandbox [!DNL Commerce] afin de ne pas diluer vos données d’événement de production avec les données d’événement storefront et back-office que vous envoyez à Experience Platform.

### Conditions préalables

Avant de commencer ces étapes, assurez-vous des points suivants :

- Les privilèges d’accès vous ont été attribués pour utiliser Adobe [!DNL Journey Optimizer]. En cas de doute, contactez l’intégrateur système ou l’équipe de développement qui gère les projets et les environnements.
- Vous avez [installé](install.md) et [configuré](connect-data.md) l’extension [!DNL Data Connection] dans [!DNL Commerce].
- Vous avez [confirmé](connect-data.md#confirm-that-event-data-is-collected) que vos données d’événement [!DNL Commerce] arrivent à Experience Platform Edge.

## Étape 1 : créer un utilisateur dans votre environnement sandbox [!DNL Commerce]

Créez un utilisateur dans votre environnement sandbox et vérifiez que les informations de ce compte d’utilisateur apparaissent dans Experience Platform. Assurez-vous que l’e-mail que vous avez spécifié est valide, car il est utilisé ultérieurement dans cette section pour envoyer l’e-mail de panier abandonné.

1. Connectez-vous ou créez un compte dans votre environnement sandbox [!DNL Commerce].

   ![Connexion à votre compte de test](assets/sign-in-account.png){width="700" zoomable="yes"}

   Une fois l’extension [!DNL Data Connection] installée et configurée, ces informations de compte sont envoyées à Experience Platform en tant que profil.

1. Vérifiez que les informations de votre compte d’utilisateur s’affichent dans la section **[!UICONTROL Profile]** d’Experience Platform.

   Accédez à **[!UICONTROL Profiles]** dans le Adobe Experience Platform. Cliquez sur **[!UICONTROL Detail]** dans le profil pour afficher le profil que vous avez créé.

   ![Confirmer le profil](assets/check-event-profile.png){width="700" zoomable="yes"}

## Étape 2 : affichage des événements dans Journey Optimizer

Dans votre environnement de sandbox [!DNL Commerce], déclenchez des événements sur votre storefront en affichant les pages de produits, en ajoutant des articles à un panier et en effectuant diverses autres activités qu’un acheteur effectuerait. Vérifiez ensuite que ces événements sont transmis à Journey Optimizer.

1. Lancer [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=fr).
1. Sélectionnez **[!UICONTROL Profiles]**.
1. Définissez **[!UICONTROL Identity namespace]** sur `Email`.
1. Définissez la **[!UICONTROL Identity value]** sur votre adresse e-mail.
1. Sélectionnez votre profil, puis sélectionnez l’onglet **[!UICONTROL Events]** .

   ![Vérifier les détails de l’événement](assets/check-event-details.png){width="700" zoomable="yes"}

   Recherchez l&#39;événement `commerce.checkouts` et examinez la payload de l&#39;événement :

   ```json
   "personID": "84281643067178465783746543501073369488", 
   "eventType": "commerce.checkouts", 
   "_id": "4b41703f-e42e-485b-8d63-7001e3580856-0", 
   "commerce": { 
       "cart": {}, 
       "checkouts": { 
           "value": 1 
       } 
   ```

   Comme vous pouvez le constater, la payload d&#39;événement complète contient des données d&#39;événement riches. Dans la section suivante, vous allez configurer des événements dans Journey Optimizer pour écouter l’événement `commerce.checkouts` généré à partir de votre storefront [!DNL Commerce] et y répondre.

## Étape 3 : configuration des événements dans Journey Optimizer

Configurez deux événements dans Journey Optimizer : un événement écoute l’événement `commerce.checkouts` depuis Commerce et l’autre est un événement de temporisation de base qui attend qu’un temps spécifique se passe avant de déclencher un e-mail de panier abandonné.

### Créer un événement de listener

1. Lancer [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html?lang=fr).

1. Cliquez sur **[!UICONTROL Configurations]** dans la section **[!UICONTROL Administration]** du volet de gauche.

1. Dans la mosaïque **[!UICONTROL Events]**, cliquez sur **[!UICONTROL Manage]**.

   ![Configuration D’Événement Journey Optimizer](assets/ajo-config.png){width="700" zoomable="yes"}

1. Sur la page **[!UICONTROL Events]**, cliquez sur **[!UICONTROL Create Event]**.

1. Dans le volet de navigation de droite, configurez l’événement comme suit :

   1. Définissez la **[!UICONTROL Name]** sur : `firstname_lastname_checkout`.
   1. Définissez **[!UICONTROL Type]** sur **[!UICONTROL Unitary]**.
   1. Définissez **[!UICONTROL Event id typ]e** sur **[!UICONTROL Rule based]**.
   1. **[!UICONTROL Schema]** à votre [!DNL Commerce] [schéma](update-xdm.md).
   1. Sélectionnez **[!UICONTROL Fields]** pour ouvrir la page **[!UICONTROL Fields]**. Sélectionnez ensuite les champs utiles à cet événement. Par exemple, sélectionnez tous les champs sous les **[!UICONTROL Product list items]**, **[!UICONTROL Commerce]**, **[!UICONTROL eventType]** et **[!UICONTROL Web]**.
   1. Cliquez sur **[!UICONTROL OK]** pour enregistrer les champs sélectionnés.
   1. Cliquez dans le champ **[!UICONTROL Event id condition]** . Créez ensuite une condition : `eventType` est égal à `commerce.checkouts` ET `personalEmail.address` est égal à l’adresse e-mail que vous avez utilisée lors de la création du profil dans la section précédente.

      ![Condition d&#39;ensemble Journey Optimizer](assets/ajo-set-condition.png){width="700" zoomable="yes"}

   1. Cliquez sur **[!UICONTROL OK]**.
   1. Cliquez sur **[!UICONTROL Save]** pour enregistrer l’événement.

### Créer un événement de temporisation

1. Créez un événement dans Journey Optimizer comme vous l’avez fait auparavant.

1. Dans le volet de navigation de droite, configurez l’événement comme suit :

   1. Définissez la **[!UICONTROL Name]** sur : `firstname_lastname_timeout`.
   1. Définissez **[!UICONTROL Type]** sur **[!UICONTROL Unitary]**.
   1. Définissez **[!UICONTROL Event id type]** sur **[!UICONTROL Rule based]**.
   1. **[!UICONTROL Schema]** à votre [!DNL Commerce] [schéma](update-xdm.md).
   1. Définissez les **[!UICONTROL Schema]**, **[!UICONTROL Fields]** et **[!UICONTROL Event id condition]** sur la même valeur que ci-dessus.
   1. Cliquez sur **[!UICONTROL Save]** pour enregistrer l’événement.

Une fois ces deux événements configurés, créez un parcours qui envoie un e-mail de panier abandonné.

## Étape 4 : créer un parcours de passage en caisse

Créez un parcours qui écoute l’événement `commerce.checkouts`, puis envoie un e-mail de panier abandonné après un délai spécifié.

1. Dans Journey Optimizer, sélectionnez **[!UICONTROL Journeys]** sous **J[!UICONTROL OURNEY MANAGEMENT]**.
1. Cliquez sur **[!UICONTROL Create Journey]**.
1. Indiquez le nom de votre parcours.
1. Cliquez sur **[!UICONTROL OK]** pour enregistrer le parcours.
1. Dans le volet de navigation de gauche de la section **[!UICONTROL EVENTS]**, recherchez l’événement de passage en caisse que vous avez précédemment créé : `firstname_lastname_checkout`, puis faites-le glisser et déposez-le sur la zone de travail.

   >[!TIP]
   >
   >Double-cliquez sur l’événement pour l’ajouter automatiquement à la zone de travail.

1. Recherchez l’événement de temporisation et ajoutez-le à la zone de travail.
1. Double-cliquez sur l’événement de temporisation.

   1. Dans la section **[!UICONTROL Timeout]** , cochez la case **[!UICONTROL Define the event time]** .
   1. Dans le champ **[!UICONTROL Wait for]** , saisissez `1` et `Minute`.
   1. Cochez la case **[!UICONTROL Set a timeout path]** .

   Avec cette configuration de temporisation, un acheteur qui effectue un passage en caisse mais ne termine pas la commande dans la minute qui suit déclenche cette branche de temporisation. Dans un environnement de production réel, vous pouvez définir ce paramètre sur une période plus longue, de l’ordre de 24 heures.

1. Dans le volet de navigation de gauche, sous **[!UICONTROL ACTIONS]**, ajoutez l’action **[!UICONTROL Email]** à la branche Temporisation . Votre parcours doit se présenter comme suit :

   ![Zone De Travail Journey Optimizer](assets/ajo-canvas.png){width="700" zoomable="yes"}

### Créer un e-mail de panier abandonné

Créez un e-mail de panier abandonné envoyé lorsqu’un panier abandonné est détecté.

1. Dans le parcours que vous avez créé ci-dessus, double-cliquez sur l’icône **[!UICONTROL Email]** dans la zone de travail.

1. Suivez les [étapes](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/personalization/personalization-use-cases/personalization-use-case-helper-functions.html?lang=fr#configure-email) du guide Journey Optimizer pour créer l’e-mail de panier abandonné.

Vous disposez désormais d’un parcours dans Journey Optimizer qui écoute l’événement `commerce.checkouts` de votre boutique [!DNL Commerce] et d’un e-mail de panier abandonné qui est envoyé après un certain temps. La section suivante vous explique comment tester le parcours.

## Étape 5 : déclencher l’événement de passage en caisse en temps réel

Dans cette section, vous testez l’événement en temps réel.

1. Dans Journey Optimizer, activez le mode Test .

   ![Activer le mode test](assets/ajo-enable-test.png){width="700" zoomable="yes"}

1. Pour tester ce parcours en temps réel, ouvrez un autre onglet du navigateur et accédez au site web [!DNL Commerce] dans votre environnement sandbox.

   1. Ajoutez un produit à votre panier.
   1. Accédez à la page de passage en caisse.
   1. Sur la page de passage en caisse, abandonnez le panier en revenant à la page principale ou en fermant votre onglet.

      Le parcours est maintenant déclenché. Pour confirmer, ouvrez l’onglet qui contient votre parcours dans Journey Optimizer. Vous devriez voir une flèche verte qui indique le chemin parcouru par votre utilisateur.

1. Vérifiez votre boîte de réception pour l’e-mail.
