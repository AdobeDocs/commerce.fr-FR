---
title: Installer  [!DNL Data Connection]
description: Découvrez comment installer, mettre à jour et désinstaller l’extension  [!DNL Data Connection]  partir d’Adobe Commerce.
role: Admin, Developer
feature: Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# Installer [!DNL Data Connection]

Avant d’installer l’extension, [consultez les conditions préalables](overview.md#prereqs).

## Installation de l’extension

L’extension [!DNL Data Connection] est disponible sur [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html). Lorsque vous installez cette extension à partir de la ligne de commande du serveur, elle se connecte à votre installation Adobe Commerce en tant que [service](../landing/saas.md). Une fois le processus terminé, **[!DNL Data Connection]** et **Commerce Services Connector** apparaissent dans le menu **Système** sous **Services** dans Commerce _Admin_.

Vue d’administration de l’extension ![[!DNL Data Connection]](assets/epc-adminui.png)

>[!IMPORTANT]
>
>Bien que le nom de l’extension soit passé de connecteur Experience Platform à [!DNL Data Connection], le nom du package reste `experience-platform-connector` pour prendre en charge la rétrocompatibilité.

1. Pour télécharger le package `experience-platform-connector`, exécutez ce qui suit à partir de la ligne de commande :

   ```bash
   composer require magento/experience-platform-connector
   ```

   Ce métapaquet contient les modules et extensions suivants :

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. (Facultatif) Pour inclure des données [!DNL Live Search], qui comprennent des [événements de recherche](events.md#search-events), installez l’extension [[!DNL Live Search]](../live-search/install.md).

1. (Facultatif) Pour inclure des données B2B, qui comprennent des [événements de demande d’approvisionnement](events.md#b2b-events), installez l’extension [B2B](#install-the-b2b-extension).

1. (Facultatif) Si vous êtes un professionnel de la santé, installez l’extension [Data Services HIPAA](#install-the-data-services-hipaa-extension) afin que vos données de back-office [!DNL Commerce] soient conformes à la loi HIPAA.

### Installation de Adobe I/O Events et configuration du module de connecteur client

Après avoir installé l’extension `experience-platform-connector`, vous devez installer Adobe I/O Events pour Adobe Commerce et configurer le module `customers-connector`.

Les étapes suivantes s’appliquent à la fois aux installations sur site et aux infrastructures cloud d’Adobe Commerce.

1. Si vous exécutez Commerce version 2.4.4 ou 2.4.5, utilisez la commande suivante pour charger les modules d’événements :

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6 et versions ultérieures chargent automatiquement ces modules.

1. Mettez à jour les dépendances du projet.

   ```bash
   composer update
   ```

1. Activez les nouveaux modules :

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

Finalisez l’installation en fonction du type de déploiement : Adobe Commerce sur l’infrastructure cloud ou sur site.

#### Sur les infrastructures cloud

Dans Adobe Commerce sur les infrastructures cloud, activez la variable globale `ENABLE_EVENTING` dans `.magento.env.yaml`. [En savoir plus](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html#enable_eventing).

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

Validez et envoyez les fichiers mis à jour dans l’environnement cloud. Lorsque le déploiement est terminé, activez l’envoi d’événements avec la commande suivante :

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### On-premise

Dans les environnements sur site, vous devez activer manuellement la génération de code et les événements Adobe Commerce :

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### Installation de l’extension B2B

Pour les commerçants B2B, installez l’extension suivante pour inclure les données d’événement [liste de demandes](events.md#b2b-events).

Téléchargez l’extension `magento/experience-platform-connector-b2b` en exécutant la commande suivante à partir de la ligne de commande :

```bash
composer require magento/experience-platform-connector-b2b
```

### Installation de l’extension Data Services HIPAA

Pour les commerçants du secteur de la santé, installez l’extension suivante pour vous assurer que les données d’événement back-office sont conformes à la norme HIPAA.

Téléchargez l’extension `magento/module-data-services-hipaa` en exécutant la commande suivante à partir de la ligne de commande :

```bash
composer require magento/module-data-services-hipaa
```

## Mettre à jour l’extension [!DNL Data Connection] {#update}

Pour mettre à jour l’extension [!DNL Data Connection], exécutez la commande suivante à partir de la ligne de commande :

```bash
composer update magento/experience-platform-connector --with-dependencies
```

Ou, pour les commerçants B2B :

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

Pour effectuer une mise à jour vers une version majeure telle que de 2.0.0 à 3.0.0, modifiez le fichier `.json` de [!DNL Composer] racine du projet comme suit :

1. Ouvrez le fichier de `composer.json` racine et recherchez des `magento/experience-platform-connector`.

1. Dans la section `require` , mettez à jour le numéro de version comme suit :

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **Enregistrer** `composer.json`. Exécutez ensuite la commande suivante à partir de la ligne de commande :

   ```bash
   composer update magento/experience-platform-connector –-with-dependencies
   ```

   Ou, pour les commerçants B2B :

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## Désinstaller l’extension [!DNL Data Connection] {#uninstall}

Pour désinstaller l’extension [!DNL Data Connection], consultez la section [désinstallation des modules](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html).
