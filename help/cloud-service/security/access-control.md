---
title: Gestion des identités et accès
description: Découvrez les fonctionnalités de gestion des identités et des accès d’Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---


# Gestion des identités et des accès

[!DNL Adobe Commerce as a Cloud Service] exploite l’infrastructure d’identité de niveau entreprise d’Adobe pour garantir un contrôle d’accès sécurisé, évolutif et centralisé dans tous les environnements. La gestion des identités et des accès (IAM) dans [!DNL Adobe Commerce as a Cloud Service] est conçue pour simplifier l’approvisionnement des utilisateurs, appliquer l’accès avec les privilèges d’accès les plus faibles et assurer la conformité aux normes de sécurité internationales.

- **[!DNL Adobe Identity Management Services (IMS)]** : [!DNL Adobe Commerce as a Cloud Service] utilise [Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview) pour authentifier les utilisateurs et gérer les droits. Cela inclut la prise en charge des fournisseurs d’identité fédérée et du [contrôle d’accès en fonction du rôle](../user-management.md).

- **Gouvernance d’Admin Console** : les administrateurs gèrent l’accès au storefront et au serveur principal via [!DNL Adobe Admin Console]. Les autorisations peuvent être limitées à des fonctionnalités et rôles spécifiques, garantissant ainsi un accès avec les privilèges les plus faibles.

## Adobe Identity Management Services (IMS)

[!DNL Adobe Commerce as a Cloud Service] utilise [!DNL Adobe Identity Management Services (IMS)] pour authentifier les utilisateurs et gérer les droits sur la plateforme. IMS fournit les éléments suivants :

- **Prise en charge des identités fédérées** : intégrez-la aux fournisseurs d’identité d’entreprise, tels qu’Azure AD et Okta, à l’aide de SAML ou OIDC.
- **Authentification unique (SSO)** : accès transparent à [!DNL Adobe Commerce] et à d’autres produits [!DNL Adobe Experience Cloud].
- **Multi-Factor Authentication (MFA)** : appliquée au niveau de l’organisation pour une sécurité renforcée.
- **Redondance globale** : les données d’identité sont stockées dans une infrastructure cloud multi-région et à charge équilibrée.

## Contrôle d’accès Admin Console

Le [!DNL Adobe Admin Console] est le hub central pour gérer l’accès des utilisateurs aux [!DNL Adobe Commerce as a Cloud Service] :

- **Contrôle d’accès en fonction du rôle (RBAC)** : attribuez des autorisations granulaires aux utilisateurs en fonction de leurs rôles, tels que Développeur, Administrateur et Analyste.
- **Profils de produit** : définissez des portées d’accès pour différents environnements, tels que l’évaluation et la production.
- **Administration déléguée** : les administrateurs système et les administrateurs de produit peuvent gérer l’accès des utilisateurs sans intervention du service informatique.

Pour plus d’informations, voir [gestion des utilisateurs](https://experienceleague.adobe.com/fr/docs/commerce/cloud-service/user-management).

## Sécurité de l’authentification et de l’intégration des API

L’authentification de l’API REST de [!DNL Adobe Commerce as a Cloud Service] est gérée via Adobe [!DNL Adobe Identity Management Services (IMS)] à l’aide de protocoles OAuth 2 normalisés. Ce système d’authentification prend en charge à la fois les workflows interactifs basés sur l’utilisateur et les intégrations automatisées serveur à serveur, assurant ainsi un accès sécurisé et approprié pour différents cas d’utilisation.

>[!NOTE]
>
>Les méthodes de génération de jeton d’administration et d’intégration dans les versions PaaS de [!DNL Adobe Commerce] ne sont pas prises en charge dans les environnements SaaS. Vous devez plutôt obtenir un jeton d’administration IMS par le biais de l’authentification OAuth.

- **Prise en charge d’OAuth 2.0** : authentification sécurisée basée sur les jetons pour les intégrations et les services tiers.
- **Accès à l’API étendue** : limitez l’accès à l’API à des ressources et opérations spécifiques.
- **Journalisation d’audit** : suivez les événements d’authentification et les modifications d’accès pour la conformité et le dépannage.

Voir [Authentification REST](https://developer.adobe.com/commerce/webapi/rest/authentication/) pour plus d’informations.
