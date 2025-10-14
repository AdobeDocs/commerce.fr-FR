---
title: Configuration du sandbox de test
description: Utilisez un compte sandbox PayPal à utiliser  [!DNL Payment Services]  mode test.
exl-id: 99c14b4e-e6cf-48f9-9546-5c0d5c71464d
feature: Payments, Checkout, Configuration, Install, Paas, Saas
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 0%

---

# Configuration du sandbox de test

Avant de démarrer l’intégration à la sandbox, vous devez vous inscrire à un compte de développeur PayPal gratuit et créer des comptes de marchand (à utiliser pour l’intégration) et d’acheteur (à utiliser pour tester votre passage en caisse). Vous pouvez créer plusieurs comptes de développeur, si vous le souhaitez.

Un compte sandbox PayPal vous permet d’utiliser [!DNL Payment Services] en mode test. PayPal exige que vous utilisiez un compte de test de sandbox d&#39;entreprise, un e-mail et un mot de passe générés par le portail de développement PayPal pour l&#39;intégration des sandbox. *Ne créez pas de compte supplémentaire pendant le processus d’intégration du sandbox.*

## Intégration des sandbox

Pour terminer l’intégration au sandbox :

1. Accédez à la page [&#x200B; Compte de développeur PayPal &#x200B;](https://developer.paypal.com/developer/accounts/).
1. Cliquez sur **[!UICONTROL Log in to Dashboard]** et connectez-vous avec votre compte de test de sandbox d&#39;entreprise généré par PayPal Developer Portal ou cliquez sur **S&#39;inscrire** pour créer un compte.
1. Créez un compte sandbox PayPal :
   1. Accédez à _[!UICONTROL Testing Tools]_>**[!UICONTROL Sandbox Accounts]**.
   1. Cliquez sur **[!UICONTROL Create account]**.

      Si vous avez créé un compte sandbox PayPal pendant le processus d’intégration de PayPal, vous devez [réinitialiser votre sandbox d’intégration](#reset-your-sandbox-account) car vous ne pouvez pas vérifier votre adresse e-mail.

   1. Sélectionnez **[!UICONTROL Business]** comme type de compte, puis cliquez sur **[!UICONTROL Create]**.
   1. Dans la section _[!UICONTROL Sandbox Accounts]_, cliquez sur les trois points de la colonne&#x200B;_[!UICONTROL Manage accounts]_ pour le compte sandbox que vous avez créé.
   1. Cliquez sur **[!UICONTROL View/edit account]**.

      ![PayPal - Afficher/modifier le compte sandbox](assets/onboarding-viewedit-sandbox.png){width="300" zoomable="yes"}

   1. Copiez et enregistrez l’ID d’e-mail et le mot de passe généré par le système pour une utilisation ultérieure.

1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.
1. Cliquez sur **[!UICONTROL Sandbox onboarding]**.

   Cette option est visible si vous n’avez pas encore terminé l’intégration du sandbox pour [!DNL Payment Services].

   Un ID de vendeur de sandbox est généré automatiquement et renseigné dans [paramètres](configure-admin.md). Ne modifiez pas cet identifiant.

   Un créneau PayPal vous est présenté pour connecter un compte PayPal afin de commencer à accepter les paiements.

1. Saisissez l’adresse e-mail et le mot de passe du compte sandbox PayPal que vous avez généré à l’étape 3 (et non les informations de votre compte professionnel PayPal), ainsi que votre pays ou région.
1. Cliquez sur **[!UICONTROL Next]**.

   ![PayPal - Connecter un compte PayPal pour les paiements](assets/paypal-connectacct.png){width="300" zoomable="yes"}

1. Continuez à suivre le flux PayPal, en utilisant les informations d’identification de votre compte sandbox précédemment enregistré.
1. Dans la barre latérale _Admin_, accédez à **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]**.

   Le bouton **[!UICONTROL Sandbox onboarding]** n’est plus visible et un texte « Paiements Sandbox en attente » s’affiche.

Lorsque l&#39;intégration de votre sandbox PayPal est approuvée, une notification devrait s&#39;afficher indiquant que votre système de paiement est actuellement en mode sandbox et ne traite pas les paiements en direct.

>[!IMPORTANT]
>
>Si vous révoquez le consentement à [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source] pour le traitement de vos paiements (dans les paramètres de votre compte PayPal), les commandes dans votre boutique ne peuvent pas être traitées par [!DNL Payment Services]. Sur la page d’accueil de Payment Services, une alerte concernant le consentement révoqué s’affiche. Pour ignorer l’alerte, cliquez sur **[!UICONTROL Do not show again]**.

### Réinitialiser votre compte sandbox

Si vous avez créé un compte sandbox PayPal pendant le processus d’intégration de PayPal, vous devez réinitialiser votre sandbox d’intégration, car vous ne pouvez pas vérifier votre adresse e-mail.

Pour réinitialiser votre compte sandbox :

1. Cliquez sur **[!UICONTROL Reset sandbox]**. [Créez un compte sandbox professionnel PayPal](https://developer.paypal.com/docs/api-basics/sandbox/accounts/#create-a-business-sandbox-account).
1. Cliquez sur **[!UICONTROL Sandbox onboarding]** et effectuez les étapes suivantes.

## Activer le numéro de téléphone du contact

Le numéro de téléphone de contact vous permet d&#39;obtenir les numéros de téléphone de contact que PayPal collecte auprès de vos clients. PayPal recueille toujours les numéros de téléphone des titulaires de compte PayPal pour aider à confirmer leur identité et à les contacter pour résoudre les problèmes sur leurs comptes ou pour terminer leurs processus d&#39;exécution. Cependant, PayPal décourage l&#39;utilisation des numéros de téléphone de contact directement du marchand car cela peut avoir un impact négatif sur les ventes. Pour plus d’informations, consultez la documentation [PayPal obtenir les numéros de téléphone &#x200B;](https://www.sandbox.paypal.com/businessmanage/preferences/website) contact .

Cette fonctionnalité est `off` par défaut. Lorsque vous l’activez, les administrateurs de magasin peuvent voir les numéros de téléphone lorsqu’un client termine un flux de passage en caisse de marque en dehors de la page de passage en caisse.

>[!IMPORTANT]
>
>Ce paramètre ne s’applique pas aux autres flux de passage en caisse.

## Test dans un environnement sandbox

Il est vivement recommandé d’utiliser des espaces de données de test pour l’intégration et les environnements d’évaluation, et de tester les paiements en production, avec des cartes de crédit et des banques réelles, avant de présenter cette fonctionnalité aux acheteurs.

Voir [Tester et valider](test-validate.md) pour plus d’informations.
