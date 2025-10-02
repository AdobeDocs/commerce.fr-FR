---
title: Gestion des utilisateurs et utilisatrices
description: Découvrez comment gérer les utilisateurs dans  [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Admin
source-git-commit: 00d31ca7e4e81ecbc34373ce95b1256a7ae012db
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# Gestion des utilisateurs et utilisatrices

Si vous souhaitez que les utilisateurs accèdent à l’administrateur dans [!DNL Adobe Commerce as a Cloud Service], vous devez les ajouter en tant qu’utilisateurs de votre organisation et vous assurer qu’ils ont accès au produit Cloud Service dans [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Ce processus nécessite une organisation IMS ayant accès à [!DNL Adobe Commerce as a Cloud Service]. Seul un administrateur système ou un administrateur produit de l’organisation peut effectuer ces processus.

>[!TIP]
>
>Pour ajouter plusieurs utilisateurs simultanément, vous pouvez effectuer un [chargement CSV en bloc](https://helpx.adobe.com/fr/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> Vous pouvez également ajouter plusieurs utilisateurs et utilisatrices à un rôle en créant un [groupe d’utilisateurs](https://helpx.adobe.com/fr/enterprise/using/user-groups.html){target="_blank"}. Vous pouvez ensuite ajouter le produit [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] au groupe d’utilisateurs.

## Compréhension des rôles

Les rôles suivants sont disponibles pour [!DNL Adobe Commerce as a Cloud Service]. Pour afficher ou modifier ces rôles, dans l’administrateur Commerce, accédez à **Système** > **Autorisations** > **Rôles utilisateur**.

* **Utilisateurs** - Les utilisateurs disposent d’un accès administrateur à l’administration Commerce, mais ne peuvent pas gérer l’accès au niveau du produit dans Admin Console. Les utilisateurs peuvent également utiliser des crédits pour [créer des instances](./getting-started.md#create-an-instance) dans le [!DNL Commerce Cloud Manager].

  >[!NOTE]
  >
  >Le rôle d’utilisateur doit également être attribué à tous les utilisateurs et utilisatrices de Commerce, y compris les développeurs et les administrateurs et administratrices. Il est nécessaire pour les autorisations de base de Commerce.

* [**Développeurs**](https://helpx.adobe.com/fr/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Les développeurs disposent d’autorisations utilisateur et sont ajoutés à l’instance Commerce en tant qu’utilisateur développeur. Cela signifie qu’ils peuvent utiliser [Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [configurer des événements](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} et [créer des Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Administrateurs - Il existe trois types d’administrateurs différents :
   * [Administrateurs système](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html){target="_blank"} - L’administrateur système a accès à tous les produits et profils de produits de l’organisation via Admin Console.
   * [Administrateurs de produit](#add-a-product-admin) - Les administrateurs de produit peuvent [gérer les utilisateurs, les rôles et les autorisations pour le produit](#add-users) dans l’[!DNL Adobe Admin Console] et [gérer les utilisateurs dans l’administrateur Commerce](https://experienceleague.adobe.com/fr/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Administrateurs de profil de produit](#add-developers-and-product-profile-admins) - Les administrateurs de profil de produit n’ont pas accès à l’administrateur Adobe Commerce, mais peuvent gérer les utilisateurs du produit dans l’[!DNL Adobe Admin Console].

Pour plus d’informations sur les autorisations accordées à chaque rôle dans Adobe Commerce, voir [autorisations utilisateur](#user-permissions).

## Ajouter un administrateur de produit

>[!NOTE]
>
>Attribuez le [rôle utilisateur](#add-users) aux administrateurs de produit avant de les ajouter en tant qu’administrateurs de produit. Le rôle Utilisateur est requis pour les autorisations de base de Commerce.

1. Accédez à https://adminconsole.adobe.com et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![sélectionner un produit](./assets/backend.png){width="600" zoomable="yes"}

1. Sélectionnez l’onglet [!UICONTROL **Administrateurs**].

1. Cliquez sur [!UICONTROL **Ajouter un administrateur**].

1. Saisissez le nom d’utilisateur ou l’adresse électronique des utilisateurs que vous souhaitez ajouter en tant qu’administrateurs et cliquez sur [!UICONTROL **Enregistrer**].

## Ajouter des utilisateurs

Les instructions suivantes expliquent comment ajouter des utilisateurs à l’[!DNL Commerce Cloud Manager] et à l’administrateur Commerce. L’interface [!DNL Commerce Cloud Manager] vous permet de créer et de gérer vos instances Commerce. Ce processus est requis pour tous les utilisateurs, y compris les développeurs et les administrateurs.

>[!NOTE]
>
>Seuls les administrateurs de produit et les administrateurs système peuvent ajouter des utilisateurs et des développeurs au produit Adobe Commerce as a Cloud Service.

1. Accédez à https://adminconsole.adobe.com et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![sélectionner un produit](./assets/backend.png){width="600" zoomable="yes"}

1. Cliquez sur le profil de produit [!UICONTROL **Par défaut - Cloud Manager**].

1. Sélectionnez l’onglet [!UICONTROL **Utilisateurs**] et cliquez sur [!UICONTROL **Ajouter des utilisateurs**].

   ![sélectionnez l’onglet](./assets/tab-select.png){width=600 zoomable="yes"}

1. Saisissez le nom d’utilisateur ou l’adresse électronique des utilisateurs que vous souhaitez ajouter en tant qu’administrateurs et cliquez sur [!UICONTROL **Enregistrer**].

### Ajout de développeurs et d’administrateurs de profil de produit

Pour ajouter des développeurs et des administrateurs de profil de produit, répétez le processus [ajouter des utilisateurs](#add-users), mais sélectionnez l’onglet [!UICONTROL **Développeurs**] ou [!UICONTROL **Administrateurs**] au lieu de l’onglet [!UICONTROL **Utilisateurs**].

>[!NOTE]
>
>Les administrateurs de profil de produit n’ont pas accès à l’administrateur Commerce. Pour plus d’informations, voir [Présentation des rôles](#understanding-roles).
>
>Attribuez le rôle Utilisateur aux développeurs avant de les ajouter en tant que développeurs. Le rôle Utilisateur est requis pour les autorisations de base de Commerce.

![sélectionnez l’onglet](./assets/tab-select.png){width=600 zoomable="yes"}

## Ressources des rôles

La liste suivante décrit les ressources auxquelles les rôles par défaut ont l’autorisation d’accéder dans Adobe Commerce Admin. Pour modifier les autorisations par défaut pour chaque rôle, accédez à **Système** > **Autorisations** > **Rôles utilisateur** dans Commerce Admin.

**Utilisateurs**

* Catalogue
   * Inventaire
      * Produits
         * Lire le prix du produit

**Développeurs**

* Catalogue
   * Inventaire
      * Produits
         * Lire le prix du produit
* Système
   * Transfert de données
      * Importer l&#39;historique
* Configuration des événements IO Adobe
   * Vérification de la configuration
   * Créer un fournisseur d’événements
   * Mise à jour de la configuration
   * Synchroniser les événements
   * Obtenir la liste des fournisseurs d&#39;événements
* Structure d’événement
   * Liste des événements
   * Tester la connexion aux événements
   * S’abonner à un événement
   * Désabonnement d’un événement
   * Statut de l’événement
   * API pour obtenir des abonnements aux événements
   * Afficher l’interface utilisateur d’administration des abonnements aux événements
   * Interface utilisateur d’administration de la création d’abonnements aux événements
   * Demander une nouvelle interface utilisateur d’administration des événements
* Webhooks
   * Signature numérique Webhooks
      * Paramètres de signature numérique des Webhooks
      * Clés de génération de signature numérique Webhooks
   * Gestion des Webhooks
      * Grille Webhooks
      * Webhooks Modifier
      * Tester les Webhooks
      * Abonnement de l’API au webhook
      * Désabonnement de l’API à partir du webhook
      * Liste des Webhooks
      * Demander un nouveau Webhook
      * Journaux des Webhooks
      * Obtenir la liste des Webhooks

**Administrateurs**

Les administrateurs ont accès à toutes les autorisations.

## Ajout d’un utilisateur à AEM Assets ou à Product Visuals

La configuration suivante est requise pour les utilisateurs [!DNL Adobe Experience Manager Assets] et [!DNL Product Visuals powered by AEM Assets].

Si votre compte a accès à [Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service) et que vous souhaitez autoriser un utilisateur à accéder aux fonctionnalités avancées de [AEM Assets](https://experienceleague.adobe.com/fr/docs/commerce/aem-assets-integration/overview){target="_blank"} avec [!DNL Adobe Commerce as a Cloud Service], procédez comme suit :

>[!NOTE]
>
>Les utilisateurs ne disposant pas des autorisations de ressources appropriées ne pourront pas accéder aux fonctionnalités avancées de [!DNL AEM Assets], telles que la génération d’images [AI](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/generative-ai/generative-ai-in-aem){target="_blank"}, les variations générées par [IA](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/generative-ai/generate-variations-integrated-editor){target="_blank"} etc.

>[!TIP]
>
>Pour ajouter plusieurs utilisateurs simultanément, vous pouvez effectuer un [chargement CSV en bloc](https://helpx.adobe.com/fr/enterprise/using/bulk-upload-users.html){target="_blank"}.
>
>Vous pouvez également ajouter plusieurs utilisateurs et utilisatrices à un rôle en créant un [groupe d’utilisateurs](https://helpx.adobe.com/fr/enterprise/using/user-groups.html){target="_blank"}. Vous pouvez ensuite ajouter le produit [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] au groupe d’utilisateurs.

1. Accédez à https://adminconsole.adobe.com et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**].

   ![sélectionner un produit](./assets/backend-aem.png){width="600" zoomable="yes"}

1. Sélectionnez l’onglet [!UICONTROL **Utilisateurs**].

1. Cliquez sur [!UICONTROL **Ajouter un utilisateur**].

1. Saisissez le nom d’utilisateur ou l’adresse e-mail des utilisateurs que vous souhaitez ajouter.

1. Cliquez sur [!UICONTROL **Ajouter un produit**].

1. Sélectionnez les profils de produit suivants, qui sont nécessaires pour intégrer AEM Assets à Commerce :

   * Propriétaire de l’entreprise - Obligatoire pour créer et gérer des programmes.
   * Responsable de déploiement - Obligatoire pour déployer le code de vos référentiels vers AEM.

   Si vous ajoutez un développeur ou une développeuse qui n’a pas besoin d’accéder aux interfaces Cloud Manager ou Experience Manager, vous pouvez plutôt lui attribuer le rôle de développeur.

   >[!NOTE]
   >
   >Pour plus d’informations sur la manière dont ces autorisations affectent votre accès à AEM Assets, reportez-vous à [Profils de produit Cloud Manager](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles#cloud-manager-product-profiles){target="_blank"}.

1. Cliquez sur [!UICONTROL **Appliquer**].

1. Cliquez sur [!UICONTROL **Enregistrer**].

Pour confirmer que l’utilisateur a accès, cliquez sur son nom pour ouvrir sa page de profil. Dans la section [!UICONTROL **Products**], il doit être indiqué [!UICONTROL **Completed**] sous le produit [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]. Quelques secondes peuvent être nécessaires après l’ajout de l’utilisateur pour voir le statut mis à jour sur son profil. Actualisez la page pour afficher le statut mis à jour.

![accès au produit](./assets/product-access.png){width="600" zoomable="yes"}

## Accès à l’interface d’Experience Manager

Après avoir ajouté un utilisateur à AEM Assets, il peut accéder à l’interface [!DNL Experience Manager] en accédant à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}.

1. Dans la section [!UICONTROL **Accès rapide**], cliquez sur [!UICONTROL **Experience Manager**] ou sur [!UICONTROL **Afficher tout**] si vous ne voyez pas [!UICONTROL **Experience Manager**]. Cliquez ensuite sur [!UICONTROL **Cloud Manager**] ou accédez directement à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}.

1. Dans la page [!UICONTROL **Cloud Manager**], cliquez sur [!UICONTROL **Ajouter un programme**] pour commencer.

1. [Créer un nouveau programme](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/onboarding/journey/create-program){target="_blank"}.

1. [Créer un environnement](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/creating-an-environment){target="_blank"}.

1. Après avoir créé l’environnement, revenez à [Admin Console](https://adminconsole.adobe.com){target="_blank"} puis sélectionnez [!UICONTROL **Adobe Experience Manager as a Cloud Service**].

1. Vous devriez maintenant voir les nouveaux profils de produit. Sélectionnez qui contient des `- author -`. Par exemple, `<environment-name> - author - <program-id> - <environment-id>`.

1. [Ajoutez des utilisateurs au profil de produit](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-manager/content/requirements/users-and-roles){target="_blank"}.

* [Configuration d’AEM Assets pour la prise en charge des métadonnées Commerce](https://experienceleague.adobe.com/fr/docs/commerce/aem-assets-integration/get-started/configure-aem)
* [Intégrer AEM Assets à Commerce pour la synchronisation des ressources](https://experienceleague.adobe.com/fr/docs/commerce/aem-assets-integration/get-started/setup-synchronization)
