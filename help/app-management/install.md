---
title: Installation et accès [!DNL App Management]
description: Conditions préalables et exigences d’accès pour utiliser  [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: 86c0945bbb0a562de1b66d420dec2a05d4d81e5f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Installation et accès à [!DNL App Management]

[!DNL App Management] est disponible dans Commerce Admin pour les instances de Commerce éligibles. La disponibilité dépend de votre type de déploiement.

## Disponibilité

Une fois les conditions requises suivantes remplies, sélectionnez l’onglet correspondant à votre type de déploiement ci-dessous, pour voir si [!DNL App Management] nécessite une installation ou est déjà disponible sur votre instance.

## Conditions préalables

Avant d’associer une application, vérifiez que vous disposez des éléments suivants :

| Exigence | Description |
|-------------|-------------|
| **Accès administrateur** | Administrateur Commerce avec autorisations [!DNL App Management] |
| **Application déployée** | Application App Builder déployée dans votre organisation et prête à se connecter |
| **Accès à l’organisation** | Accès à l’organisation Adobe sur laquelle l’application est déployée |

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!DNL App Management] est disponible automatiquement sur [!DNL Adobe Commerce as a Cloud Service]. Aucune installation n’est requise. [Activez-le dans Admin](#access-app-management) et commencez à associer des applications.

>[!TAB Adobe Commerce on Cloud (PaaS) et On-premise]

* **Adobe Commerce 2.4.8 et versions ultérieures**—[!DNL App Management] est inclus automatiquement. Aucune installation n’est requise.

* **Adobe Commerce 2.4.5 à 2.4.7**—Installez le [!DNL Admin UI SDK] (qui comprend [!DNL App Management]) à l’aide du compositeur :

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  Exécutez ensuite :

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

Voir [Installer ou mettre à jour Adobe Commerce Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"} pour plus d’informations.

>[!ENDTABS]

## [!DNL App Management] d’accès

1. Connectez-vous à l’administration Commerce.

1. Accédez à **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

La vue [!DNL App Management] s’affiche. Vous pouvez y associer, configurer et gérer des applications App Builder.

## Installation des applications App Builder

Si vous devez installer une application App Builder à partir d’Adobe Exchange (par exemple, une intégration préconfigurée ou une application de marketplace), consultez [Installation d’applications App Builder à partir d’Adobe Exchange](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} pour obtenir des instructions détaillées.

Une fois l’application installée et déployée, utilisez [!DNL App Management] pour l’[associer à votre instance Commerce](manage-app.md#associate-an-app) et configurer ses paramètres.

## Webhooks et applications Commerce

Certaines applications App Builder utilisent des [Webhooks Adobe Commerce](https://developer.adobe.com/commerce/extensibility/webhooks/) afin que Commerce puisse appeler votre application via HTTP lorsque certains événements se produisent (par exemple, après l’enregistrement d’un produit). Les points d’entrée Webhook et la logique d’abonnement sont définis par le **développeur d’applications** lorsque l’application est créée et déployée. Les administrateurs des magasins ne configurent pas les webhooks séparément dans App Management.

Une fois que vous avez [associé l’application](https://experienceleague.adobe.com/en/docs/commerce/app-management/manage-app/manage-app) à votre instance Commerce et suivi les instructions de configuration de l’application, le comportement de webhook suit la mise en œuvre de l’application.

Si [!DNL App Management] ne parvenez pas à déclencher le point d’entrée de validation de l’application (par exemple, l’URL est inatteignable ou la réponse ne répond pas aux exigences), une erreur similaire à celle-ci peut s’afficher dans le tableau de bord [!DNL App Management] :

![Erreur de validation du Webhook](assets/webhook-validation-error.png){width="600" zoomable="yes"}

Contactez le **développeur/développeuse d’applications** pour corriger la configuration ou le déploiement webhook afin que la validation puisse réussir.

**Développeurs d’applications**. Pour mettre en œuvre les abonnements webhook et les réponses des gestionnaires d’App Builder, consultez [Webhooks](https://developer.adobe.com/commerce/extensibility/app-management/installation/webhooks/) dans la documentation Commerce Extensibility destinée aux développeurs et le package [`@adobe/aio-commerce-lib-webhooks`](https://github.com/adobe/aio-commerce-sdk/tree/main/packages/aio-commerce-lib-webhooks) sur GitHub.
