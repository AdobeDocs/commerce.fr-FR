---
title: Prise en main de  [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez comment commencer à utiliser  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer, User
exl-id: 58d98b9e-b41d-44db-9666-c924a5b005b3
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 9c3f5d1d5e7fd57d2306502d654a854bc5c66c71
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Prise en main

{{accs-early-access}}

[!DNL Adobe Commerce as a Cloud Service] fournit la plupart des configurations prêtes à l’emploi. Après avoir terminé quelques processus de configuration de base, votre boutique sera opérationnelle en un rien de temps. Ce guide vous guide tout au long de la création et de l’utilisation d’une instance.

Cliquez sur les onglets ci-dessous pour afficher des vues d’ensemble générales des workflows pour les types d’utilisateurs suivants :

* Administrateurs
* Marchands
* Développeur

>[!BEGINTABS]

>[!TAB Workflow administrateur et commerçant]

Ce diagramme présente de manière générale la manière dont les administrateurs et les commerçants accèdent aux instances [!DNL Adobe Commerce as a Cloud Service] et les gèrent. Voir le [Guide Adobe Admin Console](https://helpx.adobe.com/enterprise/admin-guide.html) pour plus d&#39;informations sur les workflows d&#39;administration.

![[!DNL Adobe Commerce as a Cloud Service] diagramme de flux des commerçants](./assets/merchant-flow.svg){zoomable="yes"}

>[!TAB Workflow du développeur]

Ce diagramme présente de manière générale la manière dont les développeurs créent des intégrations pour les [!DNL Adobe Commerce as a Cloud Service] à l’aide d’App Builder. Pour plus d’informations, consultez la [documentation de l’API](https://developer.adobe.com/commerce/webapi/rest/).

![[!DNL Adobe Commerce as a Cloud Service] le diagramme de flux du développeur](./assets/developer-flow.svg){zoomable="yes"}

>[!ENDTABS]

## Création d’une instance

>[!NOTE]
>
>Avant de pouvoir créer une instance, l’administrateur produit ou l’administrateur système de votre organisation doit vous ajouter en tant qu’utilisateur du produit [!DNL Adobe Commerce as a Cloud Service]. Voir [ Ajout d’utilisateurs et d’administrateurs ](./user-management.md#add-users-and-admins) pour plus d’informations.

[!DNL Adobe Commerce as a Cloud Service] instances utilisent un système basé sur les crédits. Vous pouvez créer plusieurs instances, mais chaque instance nécessite un montant relatif de crédits. Le montant des crédits dont vous disposez au départ dépend de votre abonnement.

1. Connectez-vous à votre compte [Adobe Experience Cloud](https://experience.adobe.com/).

1. Sous [!UICONTROL Quick access], cliquez sur [!UICONTROL **Commerce**] pour ouvrir le [!UICONTROL Commerce Cloud Manager].

   La [!UICONTROL Commerce Cloud Manager] affiche une liste des instances de [!DNL Adobe Commerce as a Cloud Service] disponibles dans votre organisation Adobe IMS.

1. Cliquez sur [!UICONTROL **Ajouter une instance**] dans le coin supérieur droit de l’écran.

   ![Créer une instance](./assets/create-instance.png){width="50%" align="center" zoomable="yes"}

1. Sélectionnez [!UICONTROL **Commerce as a Cloud Service**].

1. Saisissez un **Nom** et un **Description** pour votre instance.

1. Sélectionnez la région dans laquelle vous souhaitez que votre instance soit hébergée.

   >[!NOTE]
   >
   >Une fois votre instance créée, vous ne pourrez plus modifier la région.

1. Sélectionnez le [!UICONTROL **type d’environnement**] de votre instance. Vous pouvez choisir entre les options suivantes :

   * [!UICONTROL **Sandbox**] - Idéal pour la conception et les tests. Commencez votre parcours de [!DNL Adobe Commerce as a Cloud Service] à l’aide de l’environnement Sandbox.
   * [!UICONTROL **Production**] - Pour les magasins en ligne et les sites orientés clients.

   >[!NOTE]
   >
   >Les instances Sandbox sont actuellement limitées à la région Amérique du Nord.

1. _(Facultatif)_ Si vous souhaitez inclure des exemples de données de produit à des fins de test et d’apprentissage, sélectionnez [!UICONTROL **Adobe Store**] dans le menu déroulant [!UICONTROL **Tester les données**].

   Vous pouvez ignorer cette option, mais votre storefront n&#39;aura aucun produit si vous le faites. Vous devrez [importer votre catalogue](#import-your-catalog) pour afficher l’expérience storefront complète.

1. Cliquez sur [!UICONTROL **Ajouter une instance**].

## Accès à une instance

Après avoir créé une instance, vous pouvez y accéder à partir du [!UICONTROL Commerce Cloud Manager] .

1. Connectez-vous à votre compte [Adobe Experience Cloud](https://experience.adobe.com/).

1. Sous [!UICONTROL Quick access], cliquez sur [!UICONTROL **Commerce**] pour ouvrir le [!UICONTROL Commerce Cloud Manager].

   La [!UICONTROL Commerce Cloud Manager] affiche une liste des instances disponibles dans votre organisation Adobe IMS.

1. Pour ouvrir le [!UICONTROL Commerce Admin] d’une instance, cliquez sur son nom.

>[!TIP]
>
>Pour afficher des informations sur votre instance, notamment les points d’entrée REST et GraphQL ainsi que l’URL d’administration, cliquez sur l’icône d’information en regard du nom de l’instance.

## Importer votre catalogue

Par défaut, les instances de [!DNL Adobe Commerce as a Cloud Service] n’incluent aucune donnée de produit. Vous avez la possibilité d’inclure des exemples de données de produit lorsque vous créez une instance à des fins de test et d’apprentissage avant d’importer votre propre catalogue.

Pour importer votre catalogue dans [!DNL Adobe Commerce as a Cloud Service], deux méthodes sont possibles :

* [**Commerce Admin**](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/import/data-import) - Une interface conviviale qui vous permet d&#39;importer vos données de catalogue en quelques clics.
* [**Importer l’API JSON**](https://developer.adobe.com/commerce/webapi/rest/modules/import/#import-json-api) - Une API REST qui vous permet d’importer les données de votre catalogue par programmation.

<!-- TODO

- Add guidance about how to choose which method to use
- Add guidance for new vs existing customers (cross-reference OR and _include file for migration content)

-->

## Configurer le storefront

Maintenant que vous avez créé une instance , vous êtes prêt à poursuivre [la configuration](storefront.md) votre storefront Commerce optimisé par Edge Delivery Services.
