---
title: Configurer les autorisations utilisateur IMS pour l’intégration d’AEM Assets
description: Découvrez comment l’identité IMS et les profils Admin Console activent l’accès à la diffusion AEM Assets, le sélecteur de ressources et les champs de configuration Commerce automatiquement renseignés.
feature: CMS, Media, Configuration
source-git-commit: 0fd98bf86555c914f7a5b1e177c31c37764dbf84
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Autorisations utilisateur et IMS

**IMS** (système Adobe Identity Management) est la couche d’authentification. Pour Adobe Commerce as a Cloud Service, l’authentification IMS est activée par défaut dans l’Administration. Pour Adobe Commerce sur le cloud ou sur site, l’IMS est facultatif ; l’[activation d’IMS pour Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=fr){target=_blank} fournit une interface utilisateur de configuration améliorée (sélecteur de ressources, listes déroulantes auto-renseignées), mais vous pouvez configurer l’intégration sans IMS en saisissant manuellement **ID de programme** et **ID d’environnement**.

L’intégration AEM Assets nécessite également des profils de produit **Adobe Admin Console spécifiques** lors de l’utilisation d’IMS. Les utilisateurs qui configurent l’intégration dans Commerce Admin ont besoin du profil de produit **Utilisateurs de l’OpenAPI AEM Assets DM - diffusion** ou **auteur** comme solution de secours. Elle est contrôlée par les profils de produit Admin Console dans l’organisation IMS de l’utilisateur et permet :

* Le **sélecteur de ressources** permet de sélectionner des images à partir d’AEM Assets lors de la gestion des images de catégorie ou du contenu Page Builder.
* **Champs de configuration automatiquement renseignés** tels que les listes déroulantes **ID de programme**, **ID d’environnement** et **Mappage de domaine** qui extraient des valeurs de la session IMS de l’utilisateur en fonction de ses profils de produit Admin Console (diffusion ou auteur).

Sans les autorisations appropriées, le sélecteur de ressources n’est pas disponible et ces champs semblent vides ou nécessitent une saisie manuelle.
>[!BEGINSHADEBOX]

**Comment IMS et les autorisations fonctionnent ensemble**

Adobe IMS fournit l’identité de l’utilisateur et le contexte de l’organisation, tandis que le Adobe Admin Console définit les **profils de produit**(autorisations) dont il dispose. L’intégration d’AEM Assets utilise les détails IMS ainsi que le profil attribué pour déterminer si elle peut renseigner automatiquement les champs de configuration et activer le sélecteur de ressources.

>[!ENDSHADEBOX]

## Pourquoi des profils de produit sont-ils requis ?

L&#39;intégration ne peut charger que des domaines mappés à un profil. Par conséquent, les utilisateurs peuvent avoir les profils de produit suivants :

* **Profil de produit de diffusion AEM**. Obligatoire pour le sélecteur de ressources et l’interface utilisateur de configuration lorsque l’utilisateur dispose à la fois de profils de création et de diffusion. L’intégration utilise le profil de produit de diffusion AEM lorsqu’il est disponible.

* **Créer un profil de produit**. Obligatoire pour accéder à l’interface utilisateur d’AEM Assets. Il sert également de solution de secours pour le sélecteur de ressources et l’interface utilisateur de configuration lorsque l’utilisateur ne dispose pas du profil de produit de diffusion AEM dans son Admin Console.

Les domaines (y compris l’ID de programme, l’ID d’environnement et le mappage de domaine) sont affectés au profil de produit de diffusion AEM. L’intégration charge les domaines à partir du profil de produit de diffusion **AEM** lorsqu’il est disponible, ou revient au profil de produit **auteur** lorsque le profil de produit de diffusion AEM ne figure pas dans l’Admin Console de l’utilisateur. Les utilisateurs ont besoin de l’un de ces profils pour :

* Renseignez les listes déroulantes **ID de programme**, **ID d’environnement** et **Mappage de domaine** dans la configuration Commerce Admin.
* Utilisez le sélecteur de ressources pour parcourir et sélectionner des ressources à partir d’AEM Assets.

Si aucun des profils n’est configuré, les utilisateurs peuvent saisir manuellement les **ID de programme** et **ID d’environnement**, mais le sélecteur de ressources ne sera pas disponible.

## Octroi des autorisations par type de déploiement

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE SaaS uniquement]{type=Positive tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."}

L’authentification IMS est activée par défaut. Ajoutez l’utilisateur au profil de produit **Utilisateurs OpenAPI AEM Assets DM - diffusion** dans le [Adobe Admin Console](https://adminconsole.adobe.com/) ou au profil de produit **auteur** (par exemple, `<environment-name> - author - <program-id> - <environment-id>`) comme solution de secours lorsque l’utilisateur n’a pas le profil de produit de diffusion AEM dans son Admin Console.

>[!NOTE]
>
> Les utilisateurs doivent également être ajoutés à Commerce et AEM Assets. Voir [Ajout d’un utilisateur à AEM Assets ou Visuels de produit](https://experienceleague.adobe.com/fr/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} dans le guide _Utilisateur et Identity Management_ pour une configuration complète.

![Profil de produit Admin Console pour la diffusion AEM Assets](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB Adobe Commerce sur le cloud ou sur site]

[!BADGE PaaS uniquement]{type=Informative tooltip="S’applique uniquement à Adobe Commerce sur les projets cloud (infrastructure PaaS gérée par Adobe)."}

L’**ID client IMS** est requis pour que PaaS active le sélecteur de ressources. Voir [Configurer le projet AEM Assets](configure-aem.md#prerequisites) pour connaître les conditions préalables, notamment la manière d’obtenir l’identifiant du client IMS lors de l’activation de Dynamic Media avec OpenAPI.

Pour utiliser le sélecteur de ressources et les champs de configuration automatiquement renseignés (ID de programme, ID d’environnement, mappage de domaine) :

1. [Activez l’IMS d’Adobe pour Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=fr){target=_blank} de sorte que l’administrateur Commerce utilise l’authentification IMS et puisse lire les profils de produits Admin Console de l’utilisateur.

1. [Ouvrez un ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) pour demander un identifiant client IMS personnalisé pour le sélecteur de ressources.

1. À partir du [Adobe Admin Console](https://adminconsole.adobe.com/), ajoutez l’utilisateur au profil de produit **Utilisateurs OpenAPI AEM Assets DM - diffusion** ou au profil de produit **auteur** (par exemple, `<environment-name> - author - <program-id> - <environment-id>`) comme solution de secours lorsque l’utilisateur n’a pas le profil de produit de diffusion AEM dans son Admin Console.

Sans IMS, vous pouvez toujours configurer l’intégration en saisissant manuellement l’ID de programme et l’ID d’environnement dans l’Administration de Commerce.

>[!ENDTABS]

## Documentation connexe

* [Configurer les autorisations utilisateur IMS pour l’intégration d’AEM Assets](setup-synchronization.md) : connectez Commerce à AEM Assets et configurez les règles correspondantes.
* [Sélection manuelle des ressources](../synchronize/asset-selector-integration.md) : utilisez le sélecteur de ressources pour les images de catégorie et le générateur de page.
* [Ajout d’un utilisateur à AEM Assets ou à Product Visuals](https://experienceleague.adobe.com/fr/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} : pour ACCS, ajoutez d’abord des utilisateurs à Commerce et AEM Cloud Manager (propriétaire de l’entreprise, responsable de déploiement). Le profil **Utilisateurs de l’OpenAPI AEM Assets DM - diffusion** (ou profil **auteur** comme profil de secours) est une exigence supplémentaire pour le sélecteur de ressources et le remplissage automatique des fonctionnalités.
* [Affectez des membres de l’équipe à la couche de diffusion AEM](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}. Documentation AEM pour l’accès aux diffusions.
