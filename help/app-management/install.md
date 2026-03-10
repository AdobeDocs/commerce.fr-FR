---
title: Installation et accès [!DNL App Management]
description: Conditions préalables et exigences d’accès pour utiliser Adobe Commerce [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

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

Si vous devez installer une application App Builder à partir d’Adobe Exchange (par exemple, une intégration préconfigurée ou une application de marketplace), consultez [Installation d’applications App Builder à partir d’Adobe Exchange](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} pour obtenir des instructions détaillées.

Une fois l’application installée et déployée, utilisez [!DNL App Management] pour l’[associer à votre instance Commerce](manage-app.md#associate-an-app) et configurer ses paramètres.
