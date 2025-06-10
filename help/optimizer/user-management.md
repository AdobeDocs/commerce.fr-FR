---
title: Gestion des utilisateurs et utilisatrices
description: Découvrez comment gérer les utilisateurs dans  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 1427db02c65fd45777f69eac3d10417d6e6177a1
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Gestion des utilisateurs et utilisatrices

>[!NOTE]
>
>Cette documentation de gestion des utilisateurs s’adresse aux participants en accès anticipé et contient des instructions d’intégration pour gérer et configurer [!DNL Adobe Commerce Optimizer] utilisateurs au sein de leur organisation Adobe. Si vous ne disposez pas de ces instructions, contactez votre représentant de compte pour obtenir de l’aide sur la gestion des utilisateurs. Pendant le programme d’accès anticipé, la configuration des utilisateurs pour [!DNL Adobe Commerce Optimizer] est gérée en affectant des utilisateurs à la solution de produit **[!UICONTROL Adobe Commerce as a Cloud Service - backend]**.

Pour autoriser l’accès à [!DNL Adobe Commerce Optimizer], ajoutez des utilisateurs à partir de [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} et assurez-vous qu’ils ont accès au produit Commerce.

Vous pouvez affecter des utilisateurs à l’un des rôles suivants :

* **Utilisateur** - Les utilisateurs ont accès à l’interface utilisateur de [!DNL Adobe Commerce Optimizer] pour afficher et gérer les vues de catalogue et les règles de marchandisage, ainsi que pour effectuer le suivi des mesures de performances.

* [**Développeur**](https://helpx.adobe.com/fr/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Les développeurs disposent d’autorisations utilisateur et d’un accès au Adobe Developer Console. Cela signifie qu’ils peuvent créer des projets et configurer des informations d’identification pour utiliser des outils de développement tels que les API et les SDK [!DNL Adobe Commerce Optimizer], ainsi que des outils d’extensibilité d’Adobe tels qu’App Builder et le maillage API.

* **Admin** - Il existe trois types différents de rôles d’administrateur :
   * [Administrateurs système](https://helpx.adobe.com/fr/enterprise/using/admin-roles.html){target="_blank"} - L’administrateur système a accès à tous les produits et profils de produits de l’organisation via Adobe Admin Console.
   * [Administrateurs de produit](#add-a-product-admin) - Les administrateurs de produit peuvent [gérer les utilisateurs, les rôles et les autorisations pour le produit](#add-users-and-admins) dans le [!DNL Adobe Admin Console].
   * [Administrateurs de profil de produit](#add-users-developers-and-product-profile-admins) - Les administrateurs de profil de produit peuvent gérer les utilisateurs du produit dans l’[!DNL Adobe Admin Console].

## Ajouter un administrateur de produit

1. Accédez à l’[Admin Console](https://adminconsole.adobe.com) et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Commerce as a Cloud Service - Serveur principal**].

   ![sélectionner un produit](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Sélectionnez l’onglet [!UICONTROL **Administrateurs**].

1. Cliquez sur [!UICONTROL **Ajouter un administrateur**].

1. Saisissez le nom d’utilisateur ou l’adresse électronique des utilisateurs que vous souhaitez ajouter en tant qu’administrateurs et cliquez sur [!UICONTROL **Enregistrer**].

## Ajouter des utilisateurs, des développeurs et des administrateurs de profil de produit

>[!BEGINSHADEBOX « Conditions préalables »]
>
>La mise en service suivante est requise pour User Management :

* Organisation IMS configurée pour [!DNL Adobe Commerce Optimizer]
* Un compte Adobe Experience Cloud dans la même organisation IMS avec le rôle d’administrateur système ou de produit.

>[!ENDSHADEBOX]

Suivez les instructions ci-dessous pour ajouter des utilisateurs et des développeurs au [!DNL Commerce Cloud Manager], où vous gérez vos instances Commerce.

1. Accédez à https://adminconsole.adobe.com et connectez-vous avec votre Adobe ID.

1. Sélectionnez votre organisation.

1. Dans l’onglet [!UICONTROL **Produits**], sous [!UICONTROL **Produits et services**], sélectionnez le produit [!UICONTROL **Adobe Commerce as a Cloud Service - Serveur principal**].

   ![sélectionner un produit](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Cliquez sur le profil de produit [!UICONTROL **Par défaut - Cloud Manager**].

1. Sélectionnez l’onglet [!UICONTROL **Utilisateurs**], [!UICONTROL **Développeurs**] ou [!UICONTROL **Administrateurs**] et cliquez sur [!UICONTROL **Ajouter des utilisateurs**] ou [!UICONTROL **Ajouter des développeurs**] ou [!UICONTROL **Ajouter des administrateurs**].

   Les administrateurs ajoutés à partir de cet écran sont affectés au groupe [administrateurs de profil de produit](#understanding-roles).

   ![sélectionnez l’onglet](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Saisissez le nom d’utilisateur ou l’adresse électronique des utilisateurs que vous souhaitez ajouter en tant qu’administrateurs et cliquez sur [!UICONTROL **Enregistrer**].

## Gestion des utilisateurs en bloc

Vous pouvez ajouter plusieurs utilisateurs plus efficacement par l’une des méthodes suivantes :

* Utilisez la fonction **Ajouter des utilisateurs par fichier CSV** du Adobe Admin Console pour effectuer un [chargement CSV en bloc](https://helpx.adobe.com/fr/enterprise/using/bulk-upload-users.html){target="_blank"}.
* Ajoutez plusieurs utilisateurs et utilisatrices à un rôle en créant un [groupe d’utilisateurs](https://helpx.adobe.com/fr/enterprise/using/user-groups.html){target="_blank"}. Ajoutez ensuite le produit [!UICONTROL **Adobe Commerce as a Cloud Service - Serveur principal**] au groupe d’utilisateurs.

