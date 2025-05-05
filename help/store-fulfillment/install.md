---
title: Installation
description: Installez  [!DNL Store Fulfillment solution]  pour un storefront Adobe Commerce à l’aide du compositeur pour PHP.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---


# Installation

Terminez l’installation initiale de l’extension [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] dans un environnement hors production avec le gestionnaire de file d’attente en cours d’exécution et la mise en cache configurée pour permettre la gestion des exceptions. Assurez-vous que votre environnement de développement comprend des outils de développement afin de garantir l’application des bonnes pratiques relatives au fonctionnement et à la maintenance de votre instance Adobe Commerce.

>[!TIP]
>
>Mettez à niveau l’extension Store Fulfillment pour Adobe Commerce on-premise en suivant les [ instructions de mise à niveau ](https://experienceleague.adobe.com/docs/commerce-operations/upgrade-guide/modules/upgrade.html?lang=fr) dans le _Guide de mise à niveau d’Adobe Commerce_. Pour Adobe Commerce sur les infrastructures cloud, consultez la section [Mettre à niveau une extension](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure-store/extensions.html?lang=fr#upgrade-an-extension) dans le guide *Commerce sur les infrastructures cloud*.

## Conditions préalables

Passez en revue les [conditions requises](solution-requirements.md) de la solution Store Fulfillment et collectez les informations requises avant d’installer ou de mettre à niveau l’extension [!DNL Store Fulfillment] pour Adobe Commerce.

Si vous avez installé une version préliminaire ou la version bêta de l’extension Store Fulfillment for Adobe Commerce, utilisez la commande suivante pour la supprimer avant d’installer la version actuelle.

```bash
rm -rf composer.lock vendor/walmart &&
composer require walmart/magento-bopis-metapackage:1.0.0
```

## Configuration requise pour l’installation

- **Accès à l’archive logicielle Store Fulfillment by Walmart Commerce Technologies (fichier .zip)**—Pendant le processus d’intégration et d’activation, contactez votre gestionnaire de compte pour obtenir l’accès au fichier d’installation de l’extension Store Fulfillment.

- **Informations sur le compte Adobe Commerce**-L’installation de la solution [!DNL Store Fulfillment] nécessite un [[!DNL Commerce] compte](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/commerce-account/commerce-account-create){target="_blank"}. Vous avez besoin d’un identifiant de compte et d’informations d’identification avec un accès Propriétaire ou Administrateur au projet [!DNL Adobe Commerce].

- Pour les [!DNL Adobe Commerce] sur les projets d’infrastructure cloud, les installateurs de logiciels doivent disposer d’un accès administrateur au projet cloud. Voir [Gérer l’accès des utilisateurs](https://experienceleague.adobe.com/fr/docs/commerce-cloud-service/user-guide/project/user-access).

- **Expérience d’utilisation du compositeur et de l’[!DNL Commerce CLI]** : consultez [Installation de l’interface de ligne de commande générale](https://experienceleague.adobe.com/fr/docs/commerce-operations/installation-guide/tutorials/extensions){target="_blank"} pour plus d’informations sur l’utilisation de ces outils pour installer et gérer des extensions sur la plateforme [!DNL Adobe Commerce].

- **Expérience d’installation d’extensions tierces sur Adobe Commerce** : pour référence, consultez la documentation d’Adobe Commerce.

   - [Installez une extension pour une instance Adobe Commerce sur une infrastructure cloud](https://experienceleague.adobe.com/fr/docs/commerce-cloud-service/user-guide/configure-store/extensions#install-an-extension).

   - [Installez une extension pour une instance Adobe Commerce sur site](https://experienceleague.adobe.com/fr/docs/commerce-operations/installation-guide/tutorials/extensions).

### Étape 1 : télécharger le lot d’extension

Suivez les instructions fournies par les représentants de votre compte pour télécharger le fichier d’archive contenant les packages du compositeur pour installer l’extension Store Fulfillment Services.

### Étape 2 : extraire des artefacts d’extension dans votre application

Extrayez le fichier d’archive contenant le lot d’intégration pour installer l’extension Store Fulfillment Services.

1. Créez un répertoire cible pour les fichiers extraits.

   - Sur la ligne de commande, accédez au répertoire racine doc du serveur web.

   - Créez un répertoire `artifacts`.

1. Extrayez le fichier d’archive dans le nouveau répertoire.

1. Vérifiez que les fichiers ont bien été extraits en consultant la liste des fichiers.

   ```
   ../var/www/html/artifacts]$ ls -a
   .
   ..
   bopis-sdk.zip
   module-magento-bopis-alternate-pickup-contact-admin-ui.zip
   module-magento-bopis-alternate-pickup-contact-api.zip
   ```

### Étape 3 : configurer votre application à l’aide du compositeur

Utilisez le compositeur pour configurer le répertoire source pour l’installation et installer l’extension Store Fulfillment Services.

1. Configurez le référentiel source pour l’installation du compositeur.

   ```bash
   composer config repositories.artifacts artifact artifacts/
   ```

1. Ajoutez l&#39;extension Store Fulfillment Services à `composer.json`.

   ```bash
   composer require walmart/magento-bopis-metapackage:1.0.0
   ```

>[!NOTE]
>
>Pour de meilleures performances sur les instances sur site d’Adobe Commerce, vous pouvez [mettre à jour la configuration de chargement automatique](https://experienceleague.adobe.com/docs/commerce-operations/performance-best-practices/deployment-flow.html?lang=fr#update-the-autoloader) : `composer dump-autoload --optimize`

### Etape 4 : Mise à niveau du schéma et des données de la base

Terminez l’installation en utilisant l’`bin/magento setup:upgrade` pour mettre à jour le schéma et les données de la base de données avec les modifications afin de prendre en charge la solution Store Fulfillment.

>[!NOTE]
>
>Pour Adobe Commerce sur les projets d’infrastructure cloud, il n’est pas nécessaire d’enregistrer l’extension. Au lieu de cela, validez les modifications de code de l’étape précédente et poussez-les vers votre branche d’environnement. Les commandes permettant de mettre à jour le schéma et les données de la base de données sont exécutées automatiquement pendant le processus de création et de déploiement dans le cloud.

### Étape 5 : terminer l&#39;installation

1. Enregistrez l’extension avec Adobe Commerce à l’aide de la commande d’interface de ligne de commande `setup:upgrade` Magento.

   ```bash
   bin/magento setup:upgrade
   ```

1. Si vous y êtes invité, recompilez votre projet [!DNL Commerce].

   ```bash
   bin/magento setup:di:compile
   ```

1. Nettoyez le cache.

   ```bash
   bin/magento cache:clean
   ```

1. Désactivez le mode de maintenance.

   ```bash
   bin/magento maintenance:disable
   ```

### Étape 6 : vérifier l’installation

Depuis le serveur Adobe Commerce, vérifiez que les modules de l&#39;extension Store Fulfillment Services sont installés et activés.

1. Connectez-vous au serveur .

   Pour les installations sur Adobe Commerce sur une infrastructure cloud, [utilisez SSH pour vous connecter à l’environnement distant](https://experienceleague.adobe.com/fr/docs/commerce-cloud-service/user-guide/develop/secure-connections#ssh).

1. Vérifiez que les modules Store Fulfillment Services sont activés.

   ```bash
   bin/magento module:status  --enabled | grep Walmart
   ```

   La sortie doit inclure les modules suivants :

   ```
   Walmart_BopisBase
   Walmart_BopisAlternatePickupContact
   Walmart_BopisAlternatePickupContactFrontend
   Walmart_BopisApiConnector
   Walmart_BopisAlternatePickupContactAdminUi
   Walmart_BopisCheckoutPickInStoreApi
   Walmart_BopisInventorySourceAdminUi
   Walmart_BopisCheckoutPickInStore
   Walmart_BopisInventoryCatalogApi
   Walmart_BopisPreferredLocationApi
   Walmart_BopisHomeDeliveryApi
   Walmart_BopisHomeDelivery
   Walmart_BopisPreferredLocation
   Walmart_BopisInventoryCatalog
   Walmart_BopisPreferredLocationFrontend
   Walmart_BopisCheckoutPickInStoreAdminUi
   Walmart_BopisInventorySourceApi
   Walmart_BopisInventorySourceFaasSync
   Walmart_BopisInventorySourceReservation
   Walmart_BopisLocationCheckInApi
   Walmart_BopisLogging
   Walmart_BopisStoreAssociateApi
   Walmart_BopisLocationCheckInFrontend
   Walmart_BopisStoreAssociate
   Walmart_BopisOperationQueue
   Walmart_BopisOperationQueueAdminUi
   Walmart_BopisOperationQueueApi
   Walmart_BopisOrderFaasSync
   Walmart_BopisOrderUpdateApi
   Walmart_BopisLocationCheckIn
   Walmart_BopisInventoryCatalogAdminUi
   Walmart_BopisPreferredLocationAdminUi
   Walmart_BopisDeliverySelection
   Walmart_BopisCheckoutPickInStoreFrontend
   Walmart_BopisLocationCheckInAdminUi
   Walmart_BopisStoreAssociateAdminUi
   Walmart_BopisOrderUpdate
   Walmart_BopisStoreAssociateTfa
   Walmart_BopisStoreAssociateTfaApi
   ```

### Étapes supplémentaires

Si nécessaire, utilisez la commande d’interface de ligne de commande [setup:static-content:deploy](https://experienceleague.adobe.com/fr/docs/commerce-operations/tools/cli-reference/commerce-on-premises){target="_blank"} pour déployer des fichiers de vues statiques dans votre environnement de production.

```bash
php bin/magento setup:static-content:deploy -f
```

L’option `-f` est obligatoire si vous utilisez un thème vide.

>[!NOTE]
>
>Pour plus d’informations, consultez l’article [ Bonnes pratiques de déploiement de contenu statique dans Adobe Commerce ](https://experienceleague.adobe.com/docs/commerce-operations/implementation-playbook/best-practices/development/static-content-deployment.html?lang=fr) du Centre d’aide d’Adobe Commerce.


