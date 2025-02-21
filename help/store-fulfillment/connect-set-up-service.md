---
title: Connecter la solution Store Fulfillment
description: Établir les connexions entre Adobe Commerce et la solution Store Fulfillment. Créez et autorisez une intégration Adobe Commerce, puis ajoutez les informations d’identification du compte Store Fulfillment à la configuration du service Adobe Commerce.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install, Configuration, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Connecter la solution Store Fulfillment

Connectez Store Fulfillment Services à Adobe Commerce en ajoutant les informations d’authentification et les données de connexion requises à l’administrateur Adobe Commerce.

- **[Configurer [!DNL Commerce integration settings]](#create-an-adobe-commerce-integration)**-Créez une intégration Adobe Commerce pour les services Store Fulfillment et générez les jetons d’accès pour authentifier les demandes entrantes provenant des serveurs Store Fulfillment.

- **[Configurer les informations d&#39;identification de compte pour les services Store Fulfillment](#configure-store-fulfillment-account-credentials)**-Ajoutez vos informations d&#39;identification pour connecter Adobe Commerce à votre compte Store Fulfillment.

>[!NOTE]
>
>Terminez la configuration de la connexion et validez-la avant de commencer le test.

## Création d’une intégration Adobe Commerce

Pour intégrer Adobe Commerce aux services Store Fulfillment, créez une intégration Commerce et générez des jetons d’accès qui peuvent être utilisés pour authentifier les demandes provenant des serveurs Store Fulfillment. Vous devez également mettre à jour les options de [!UICONTROL Consumer Settings] d’Adobe Commerce afin d’éviter les erreurs de réponse `The consumer isn't authorized to access %resources.` sur les demandes d’Adobe Commerce aux services [!DNL Store Fulfillment].

1. À partir de l’administrateur, créez l’intégration pour la Store Fulfillment.

   - Nommer l’extension
   - Saisissez votre adresse e-mail
   - Entrez le mot de passe de votre compte d’administrateur

1. Configurez les autorisations d&#39;accès aux ressources API pour l&#39;intégration avec les éléments suivants :

   - Ventes > BOPIS Mise à jour de commande
   - Système > Autorisations de l&#39;application Store Fulfillment

1. Générez les jetons d’accès pour l’authentification en enregistrant et en activant l’intégration.

1. Copiez et enregistrez les jetons d’accès dans un emplacement sécurisé et chiffré.

1. Contactez votre gestionnaire de compte pour terminer la configuration du côté Traitement des commandes en magasin et pour autoriser l’intégration.

1. Activez l’option [!UICONTROL Consumer Settings] Adobe Commerce à [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens].

   - Depuis l’administration, accédez à **[!UICONTROL Stores]** > [!UICONTROL Configuration] > **[!UICONTROL Services]** > **[!UICONTROL OAuth]** > **[!UICONTROL Consumer Settings]**

   - Définissez l’option [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens] sur **[!UICONTROL Yes]**.

>[!IMPORTANT]
>
> Le jeton d’intégration est spécifique à l’environnement. Si vous restaurez la base de données pour un environnement avec les données sources d’un autre environnement, par exemple en restaurant les données de production d’un environnement d’évaluation, excluez la table `oauth_token` de l’exportation de la base de données afin que les détails du jeton d’intégration ne soient pas remplacés pendant l’opération de restauration.


## Configurer les informations d&#39;identification du compte Store Fulfillment

Une fois que vous avez rempli le formulaire de réception, un compte d&#39;exécution de magasin Walmart est créé pour vous. Vous recevez les informations d’identification suivantes lorsqu’elles sont disponibles :

- [!DNL Merchant ID]
- [!DNL Consumer ID]
- [!DNL Consumer Secret]
- [!DNL API Server URL]
- [!DNL Token Auth Server URL] (généralement la même configuration que ci-dessus)

Ces informations d&#39;identification sont requises pour configurer et utiliser le traitement des commandes en magasin.

>[!NOTE]
>
>Le processus de création du compte peut prendre un certain temps. Pendant que vous attendez les informations d’identification, [vérifiez et configurez d’autres paramètres pour la solution Store Fulfillment](service-config-settings-overview.md).

### Ajouter des informations d’identification pour vous connecter à la Store Fulfillment

1. Configurez les [informations d’identification de compte](enable-general.md) pour les environnements de production et de sandbox.

1. Depuis l’administrateur, accédez à **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**

1. Saisissez les informations d’identification de compte fournies pour le **[!UICONTROL Production environment]**. Tous les champs sont obligatoires.

1. Sélectionnez **[!UICONTROL Save Config]**.

1. Testez la connexion en sélectionnant **[!UICONTROL Validate Credentials]**.

>[!NOTE]
>
>Si les informations d’identification ne sont pas valides, vérifiez que vous avez saisi les valeurs correctes pour chaque environnement et validez à nouveau. Contactez votre représentant de compte si vous rencontrez toujours des problèmes de connexion.
