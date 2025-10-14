---
title: Installer  [!DNL Payment Services]
description: Installez l’extension des services de paiements.
exl-id: babaa91a-9376-4acb-b934-a89f9df52016
role: Admin
feature: Payments, Checkout, Install, Upgrade, Paas
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 0%

---

# Installer [!DNL Payment Services]

Pour commencer à utiliser les services de paiement pour [!DNL Adobe Commerce] et [!DNL Magento Open Source], vous devez effectuer quelques étapes d’intégration.

>[!INFO]
>
> Consultez notre vidéo [Configurer [!DNL Payment Services] pour Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-payment-services) pour plus d’informations.

Le téléchargement et l’installation de l’extension [!DNL Payment Services] pour [!DNL Adobe Commerce] et [!DNL Magento Open Source] sont des conditions préalables à l’utilisation de [!DNL Payment Services].

## Télécharger l’extension

Vous devez d’abord télécharger l’extension à partir de [Commerce Marketplace](https://experienceleague.adobe.com/docs/commerce-admin/start/resources/commerce-marketplace.html?lang=fr) avant de l’installer.

1. Accédez à l’extension [&#x200B; Services de paiement dans Commerce Marketplace](https://commercemarketplace.adobe.com/magento-payment-services.html).
1. Pour choisir l’édition et la version, faites basculer le **[!UICONTROL Edition]** et le **[!UICONTROL Your store version]** vers vos sélections préférées.
1. Cliquez sur **[!UICONTROL Add to Cart]**.
1. Effectuez le passage en caisse et cliquez sur **[!UICONTROL Place Order]**.
1. Consultez l’e-mail associé à votre téléchargement Marketplace pour obtenir une confirmation de commande et des détails.

>[!NOTE]
>
> Pour Adobe Commerce, la version 2.4.7 ou une version plus récente [!DNL Payment Services] est disponible prête à l’emploi.

## Installation de l’extension

Vous pouvez installer l’extension [!DNL Payment Services] pour les [!DNL Adobe Commerce] sur l’infrastructure cloud et les instances sur site, qui sont liées à votre compte Commerce [mageid](https://developer.adobe.com/commerce/marketplace/guides/sellers/profile-information/#access-keys) fourni lors du processus d’inscription.
[!DNL Magento Open Source] clients utilisent les instructions sur site.

Le compositeur utilise ces clés lors de l’installation initiale d’[!DNL Adobe Commerce] ou dans des situations où les clés du compositeur n’ont pas été enregistrées précédemment dans le fichier `auth.json`.

Voir [Obtenir vos clés d’authentification](https://experienceleague.adobe.com/fr/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) pour plus d’informations sur l’obtention des clés du compositeur.

Consultez [Installation d’une extension](https://experienceleague.adobe.com/fr/docs/commerce-operations/installation-guide/tutorials/extensions) pour plus d’informations sur les éléments à prendre en compte avant de télécharger et d’installer une extension.

### [!DNL Adobe Commerce] sur les infrastructures cloud

Cette méthode est utilisée pour installer l’extension [!DNL Payment Services] pour une instance Commerce Cloud.

1. Mettez à jour votre fichier `composer.json` :

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Mettez à jour les dépendances et installez l’extension :

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilisez la commande `composer update` pour mettre à jour toutes les dépendances racine.

1. Validez et envoyez vos modifications.

### Configurations sur site et autres

Cette méthode est utilisée pour installer l’extension [!DNL Payment Services] pour une instance locale et les clients [!DNL Magento Open Source].

1. Pour obtenir l’extension, exécutez les commandes suivantes :

   ```bash
   composer require magento/payment-services --no-update
   ```

1. Mettez à jour les dépendances et installez l’extension :

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilisez la commande `composer update` pour mettre à jour toutes les dépendances racine.

1. Mettez à niveau votre instance :

   ```bash
   bin/magento setup:upgrade
   ```

1. Effacez le cache :

   ```bash
   bin/magento cache:clean
   ```

1. Validez les modifications.
1. Pour vous assurer que le code validé est déployé, mettez à jour votre instance .

>[!NOTE]
>
> [!DNL Payment Services] 1.6.1 est compatible avec PHP versions 7.x. Cependant, il est vivement recommandé d’effectuer une mise à jour vers la dernière version de [!DNL Payment Services].

## Mettre à niveau l’extension

Lorsqu’une nouvelle version de [!DNL Payment Services] est publiée, vous pouvez facilement mettre à niveau votre extension.

1. Pour obtenir la version la plus récente du package :

   ```bash
   composer update magento/payment-services --with-dependencies
   ```

   Utilisez la commande `composer update` pour mettre à jour toutes les dépendances racine.

1. Après la mise à jour du compositeur, exécutez :

   ```bash
   bin/magento setup:upgrade
   ```

1. Validez et envoyez vos modifications.

## Dépannage

Des erreurs peuvent s’afficher lors de la tentative d’installation de l’extension [!DNL Payment Services]. Utilisez les méthodes de dépannage suivantes pour résoudre les erreurs.

### Liste des référentiels

Vérifiez que `repo.magento.com` est présent dans la liste des référentiels.

### Clés du compositeur incorrectes

Si l’erreur suivante s’affiche indiquant que vous disposez de clés de compositeur incorrectes :

```
Could not find a matching version of package magento/payment-services. Check the package spelling, your version constraint and that the package is available in a stability which matches your minimum-stability (stable).
```

Vérifiez que vos clés de compositeur sont valides et que vous avez accès à d’autres packages Magento.

Pour voir quelles clés du compositeur sont configurées :

1. Recherchez l’emplacement du fichier `auth.json` :

   ```bash
   composer config --global home
   ```

1. Affichez le fichier `auth.json` :

   ```bash
   cat /path/to/auth.json
   ```

1. Voir [quelles clés sont associées à votre compte Commerce `MageID`](https://experienceleague.adobe.com/fr/docs/commerce-operations/installation-guide/prerequisites/authentication-keys).

### Mémoire insuffisante pour PHP

Si vous voyez l&#39;erreur suivante indiquant que vous n&#39;avez pas assez de mémoire pour PHP :

```
Fatal error: Allowed memory size of 2146435072 bytes exhausted (tried to allocate 4096 bytes) in phar:///usr/local/bin/composer/src/Composer/DependencyResolver/RuleWatchGraph.php on line 52
```

[Augmentez la limite de mémoire](https://experienceleague.adobe.com/fr/docs/commerce-cloud-service/user-guide/configure/app/php-settings#increase-php-memory-limit) pour PHP sur votre environnement en `php.ini`.

Vous pouvez également spécifier la limite de mémoire à l’aide de la commande suivante : `php -d memory_limit=-1 [path to composer]/composer require magento/payment-services`.

Par exemple :

```bash
php -d memory_limit=-1 vendor/bin/composer require magento/payment-services
```
