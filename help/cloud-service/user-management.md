---
title: Gestion des utilisateurs et utilisatrices
description: Découvrez comment gérer les utilisateurs dans  [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 34057c1e55ff117ea7aab4407f31548ce826691b
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Gestion des utilisateurs et utilisatrices

{{accs-early-access}}

Si vous souhaitez que les utilisateurs accèdent à l’administrateur dans [!DNL Adobe Commerce as a Cloud Service], vous devez les ajouter en tant qu’utilisateurs de votre organisation et vous assurer qu’ils ont accès au produit Cloud Service dans [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Ce processus nécessite une organisation IMS ayant accès à [!DNL Adobe Commerce as a Cloud Service]. Seul un administrateur système ou un administrateur produit de l’organisation peut effectuer ces processus.

>[!TIP]
>
>Pour ajouter plusieurs utilisateurs simultanément, vous pouvez effectuer un [chargement CSV en bloc](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> Vous pouvez également ajouter plusieurs utilisateurs et utilisatrices à un rôle en créant un [groupe d’utilisateurs](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. Vous pouvez ensuite ajouter le produit [!UICONTROL **Adobe Commerce as a Cloud Service - Serveur principal**] au groupe d’utilisateurs.

## Compréhension des rôles

Les rôles suivants sont disponibles pour [!DNL Adobe Commerce as a Cloud Service]. Pour afficher ou modifier ces rôles, dans l’administrateur Commerce, accédez à **Système** > **Autorisations** > **Rôles utilisateur**.

* **Utilisateurs** - Les utilisateurs disposent d’un accès administrateur à l’administration Commerce, mais ne peuvent pas gérer l’accès au niveau du produit dans Admin Console. Les utilisateurs peuvent également utiliser des crédits pour [créer des instances](./getting-started.md#create-an-instance) dans le [!DNL Commerce Cloud Manager].

* [**Développeurs**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Les développeurs disposent d’autorisations utilisateur et sont ajoutés à l’instance Commerce en tant qu’utilisateur développeur. Cela signifie qu’ils peuvent utiliser [Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [configurer des événements](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} et [créer des Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Administrateurs - Il existe trois types d’administrateurs différents :
   * [Administrateurs système](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"} - L’administrateur système a accès à tous les produits et profils de produits de l’organisation via Admin Console.
   * [Administrateurs de produit](#add-a-product-admin) - Les administrateurs de produit peuvent [gérer les utilisateurs, les rôles et les autorisations pour le produit](#add-users-and-admins) dans l’[!DNL Adobe Admin Console] et [gérer les utilisateurs dans l’administrateur Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Administrateurs de profil de produit](#add-users-developers-and-product-profile-admins) - Les administrateurs de profil de produit n’ont pas accès à l’administrateur Adobe Commerce, mais peuvent gérer les utilisateurs du produit dans l’[!DNL Adobe Admin Console].

Pour plus d’informations sur les autorisations accordées à chaque rôle dans Adobe Commerce, voir [autorisations utilisateur](#user-permissions).

## Ajouter un administrateur de produit

1. Accédez à https://adminconsole.adobe.com et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Commerce as a Cloud Service - Serveur principal**].

   ![sélectionner un produit](./assets/backend.png){width="600" zoomable="yes"}

1. Sélectionnez l’onglet [!UICONTROL **Administrateurs**].

1. Cliquez sur [!UICONTROL **Ajouter un administrateur**].

1. Saisissez le nom d’utilisateur ou l’adresse électronique des utilisateurs que vous souhaitez ajouter en tant qu’administrateurs et cliquez sur [!UICONTROL **Enregistrer**].

## Ajouter des utilisateurs, des développeurs et des administrateurs de profil de produit

Les instructions suivantes fournissent des informations sur la manière d’ajouter des utilisateurs et des développeurs à l’[!DNL Commerce Cloud Manager] et à l’administrateur Commerce. L’interface [!DNL Commerce Cloud Manager] vous permet de créer et de gérer vos instances Commerce.

>[!NOTE]
>
>Seuls les administrateurs de produit et les administrateurs système peuvent ajouter des utilisateurs et des développeurs au produit Adobe Commerce as a Cloud Service.

1. Accédez à https://adminconsole.adobe.com et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Commerce as a Cloud Service - Serveur principal**].

   ![sélectionner un produit](./assets/backend.png){width="600" zoomable="yes"}

1. Cliquez sur le profil de produit [!UICONTROL **Par défaut - Cloud Manager**].

1. Sélectionnez l’onglet [!UICONTROL **Utilisateurs**], [!UICONTROL **Développeurs**] ou [!UICONTROL **Administrateurs**] et cliquez sur [!UICONTROL **Ajouter des utilisateurs**] ou [!UICONTROL **Ajouter des développeurs**] ou [!UICONTROL **Ajouter des administrateurs**].

   >[!NOTE]
   >
   >Les administrateurs ajoutés à partir de cet écran sont des [administrateurs de profil de produit](#understanding-roles) et n’ont pas accès à l’administrateur Commerce.

   ![sélectionnez l’onglet](./assets/tab-select.png){width=600 zoomable="yes"}

1. Saisissez le nom d’utilisateur ou l’adresse électronique des utilisateurs que vous souhaitez ajouter en tant qu’administrateurs et cliquez sur [!UICONTROL **Enregistrer**].

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
