---
title: Gestion des identités et accès
description: Découvrez les fonctionnalités de gestion des identités et des accès d’Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
autotag-review: '2026-06-18T16:14:06.699Z'
TQID: 'https://experienceleague.adobe.com/lbI3nsLtafel6GtquXnkZmXD2Z3b-rRGPOyr8EqzrjE'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
role_v2:
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 419
ht-degree: 0%

---


# Gestion des identités et des accès

[!DNL Adobe Commerce as a Cloud Service] exploite l’infrastructure d’identité de niveau entreprise d’Adobe pour garantir un contrôle d’accès sécurisé, évolutif et centralisé dans tous les environnements. La gestion des identités et des accès (IAM) dans [!DNL Adobe Commerce as a Cloud Service] est conçue pour simplifier l’approvisionnement des utilisateurs, appliquer l’accès avec les privilèges d’accès les plus faibles et assurer la conformité aux normes de sécurité internationales.

- **[!DNL Adobe Identity Management Services (IMS)]** : [!DNL Adobe Commerce as a Cloud Service] utilise [Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview) pour authentifier les utilisateurs et gérer les droits. Cela inclut la prise en charge des fournisseurs d’identité fédérée et du [contrôle d’accès en fonction du rôle](../user-management.md).

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

Pour plus d’informations, voir [gestion des utilisateurs](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management).

## Sécurité de l’authentification et de l’intégration des API

L’authentification de l’API REST de [!DNL Adobe Commerce as a Cloud Service] est gérée via Adobe [!DNL Adobe Identity Management Services (IMS)] à l’aide de protocoles OAuth 2 normalisés. Ce système d’authentification prend en charge à la fois les workflows interactifs basés sur l’utilisateur et les intégrations automatisées serveur à serveur, assurant ainsi un accès sécurisé et approprié pour différents cas d’utilisation.

>[!NOTE]
>
>Les méthodes de génération de jeton d’administration et d’intégration dans les versions PaaS de [!DNL Adobe Commerce] ne sont pas prises en charge dans les environnements SaaS. Vous devez plutôt obtenir un jeton d’administration IMS par le biais de l’authentification OAuth.

- **Prise en charge d’OAuth 2.0** : authentification sécurisée basée sur les jetons pour les intégrations et les services tiers.
- **Accès à l’API étendue** : limitez l’accès à l’API à des ressources et opérations spécifiques.
- **Journalisation d’audit** : suivez les événements d’authentification et les modifications d’accès pour la conformité et le dépannage.

Voir [Authentification REST](https://developer.adobe.com/commerce/webapi/rest/authentication/) pour plus d’informations.
