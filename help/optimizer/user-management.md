---
title: Gestion des utilisateurs et utilisatrices
description: Découvrez comment créer et gérer des utilisateurs et affecter des rôles utilisateur à  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: 36a953d4fb0e1e14c7cb88a80f3b59d6fe8eb49e
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 0%

---

# Gestion des utilisateurs et utilisatrices

Pour autoriser l’accès à [!DNL Adobe Commerce Optimizer], ajoutez des utilisateurs à partir de [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} et assurez-vous qu’ils ont accès au produit Commerce.

Vous pouvez affecter des utilisateurs à l’un des rôles suivants :

- **Utilisateur**— Les utilisateurs ont accès à l’interface utilisateur [!DNL Adobe Commerce Optimizer] pour afficher et gérer les vues de catalogue et les règles de marchandisage, ainsi que pour effectuer le suivi des mesures de performances.

- [**Développeur**](https://helpx.adobe.com/fr/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}— Les développeurs disposent d’autorisations utilisateur et d’un accès au Adobe Developer Console. Cela signifie qu’ils peuvent créer des projets et configurer des informations d’identification pour utiliser des outils de développement tels que les API et les SDK [!DNL Adobe Commerce Optimizer], ainsi que des outils d’extensibilité d’Adobe tels qu’App Builder et le maillage API.

- **Admin** - Il existe trois types différents de rôles d’administrateur :
   - [Administrateurs système](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html){target="_blank"} - L’administrateur système a accès à tous les produits et profils de produits de l’organisation via Adobe Admin Console.
   - [Administrateurs de produit](#add-a-product-admin) - Les administrateurs de produit peuvent [gérer les utilisateurs, les rôles et les autorisations pour le produit](#add-users-and-admins) dans le [!DNL Adobe Admin Console].
   - [Administrateurs de profil de produit](#add-users-developers-and-product-profile-admins) - Les administrateurs de profil de produit peuvent gérer les utilisateurs du produit dans l’[!DNL Adobe Admin Console].

## Ajouter un administrateur de produit

>[!BEGINTABS]

>[!NOTE]
>
>Attribuez le [rôle utilisateur](#add-users) aux administrateurs de produit avant de les ajouter en tant qu’administrateurs de produit. Le rôle Utilisateur est requis pour les autorisations de base de Commerce.

>[!TAB GA (mise en service après le 13 octobre 2025)]

1. Accédez à <https://adminconsole.adobe.com> et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Sélectionnez l’onglet [!UICONTROL **Utilisateurs**].

1. Sélectionnez l’onglet [!UICONTROL **Administrateurs**].

1. Cliquez sur [!UICONTROL **Ajouter un administrateur**].

1. Saisissez le nom d’utilisateur ou l’adresse électronique des utilisateurs que vous souhaitez ajouter en tant qu’administrateurs et cliquez sur [!UICONTROL **Suivant**].

1. Sélectionnez le rôle [!UICONTROL **Administrateur de profils de produit**].

1. Cliquez sur **+** pour ajouter des produits.

1. Sélectionnez l’instance Commerce Optimizer existante à laquelle ajouter l’administrateur. Les instances Commerce Optimizer utilisent le format suivant : `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Sélectionnez le profil de produit.

1. Cliquez sur [!UICONTROL **Appliquer**].

1. Cliquez sur [!UICONTROL **Enregistrer**].

>[!TAB Accès anticipé (fourni avant le 13 octobre 2025)]

1. Accédez à <https://adminconsole.adobe.com> et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![sélectionner un produit](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Sélectionnez l’onglet [!UICONTROL **Administrateurs**].

1. Cliquez sur [!UICONTROL **Ajouter un administrateur**].

1. Saisissez le nom d’utilisateur ou l’adresse électronique des utilisateurs que vous souhaitez ajouter en tant qu’administrateurs et cliquez sur [!UICONTROL **Enregistrer**].

>[!ENDTABS]

## Ajouter des utilisateurs

Les instructions suivantes expliquent comment ajouter des utilisateurs à [!DNL Commerce Cloud Manager] et Commerce Optimizer. L’interface [!DNL Commerce Cloud Manager] vous permet de créer et de gérer vos instances Commerce Optimizer. Ce processus est requis pour tous les utilisateurs, y compris les développeurs et les administrateurs.

>[!NOTE]
>
>Seuls les administrateurs de produit et les administrateurs système peuvent ajouter des utilisateurs et des développeurs au produit Adobe Commerce Optimizer.

>[!BEGINTABS]

>[!TAB GA (mise en service après le 13 octobre 2025)]

1. Accédez à <https://adminconsole.adobe.com> et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Sélectionnez l’onglet [!UICONTROL **Produits**].

1. Sélectionnez le produit [!UICONTROL **Adobe Commerce**].

1. Sélectionnez le produit Commerce Cloud Manager si vous souhaitez ajouter l’utilisateur à l’interface de Cloud Manager, où il peut créer et gérer des instances Commerce Optimizer, ou sélectionnez l’instance Commerce Optimizer existante à laquelle ajouter l’utilisateur. Les instances Commerce Optimizer utilisent le format suivant : `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Sélectionnez l’onglet [!UICONTROL **Utilisateurs**] et cliquez sur [!UICONTROL **Ajouter des utilisateurs**].

1. Saisissez le nom d’utilisateur ou l’adresse e-mail des utilisateurs à ajouter, puis cliquez sur [!UICONTROL **Enregistrer**].

1. Sélectionnez le profil de produit souhaité.

1. Cliquez sur [!UICONTROL **Appliquer**].

1. Cliquez sur [!UICONTROL **Enregistrer**].

>[!TAB Accès anticipé (fourni avant le 13 octobre 2025)]

1. Accédez à <https://adminconsole.adobe.com> et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![sélectionner un produit](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. Cliquez sur le profil de produit [!UICONTROL **Par défaut - Cloud Manager**].

1. Sélectionnez l’onglet [!UICONTROL **Utilisateurs**] et cliquez sur [!UICONTROL **Ajouter des utilisateurs**].

   ![sélectionnez l’onglet](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Saisissez le nom d’utilisateur ou l’adresse e-mail des utilisateurs à ajouter, puis cliquez sur [!UICONTROL **Enregistrer**].

>[!ENDTABS]

### Ajout de développeurs et d’administrateurs de profil de produit

Pour ajouter des développeurs et des administrateurs de profil de produit, répétez le processus [ajouter des utilisateurs](#add-users), mais sélectionnez l’onglet [!UICONTROL **Développeurs**] ou [!UICONTROL **Administrateurs**] au lieu de l’onglet [!UICONTROL **Utilisateurs**].

>[!NOTE]
>
>Attribuez le rôle Utilisateur aux développeurs avant de les ajouter en tant que développeurs. Le rôle Utilisateur est requis pour les autorisations de base de Commerce.

![sélectionnez l’onglet](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## Gestion des utilisateurs en bloc

Vous pouvez ajouter plusieurs utilisateurs plus efficacement par l’une des méthodes suivantes :

- Utilisez la fonction **Ajouter des utilisateurs par fichier CSV** du Adobe Admin Console pour effectuer un [chargement CSV en bloc](https://helpx.adobe.com/fr/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Ajoutez plusieurs utilisateurs et utilisatrices à un rôle en créant un [groupe d’utilisateurs](https://helpx.adobe.com/fr/enterprise/using/user-groups.html){target="_blank"}. Ajoutez ensuite le produit [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] au groupe d’utilisateurs.

