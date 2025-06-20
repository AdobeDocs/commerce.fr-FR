---
title: Configurer votre storefront
description: 'Découvrez comment exécuter l’outil de génération de modèles automatique pour configurer votre storefront [!DNL Adobe Commerce as a Cloud Service] '
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: c9869e45ed9eb8f04cf3e1bfb3542a42bbf97c0f
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 0%

---

# Configurer votre storefront

{{accs-early-access}}

Les étapes suivantes montrent comment configurer rapidement votre storefront Adobe Commerce optimisé par Edge Delivery à l’aide de la commande `aio commerce init`. Ce processus configure les éléments suivants :

* [Commerce Storefront optimisé par Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=fr) : une vitrine performante, évolutive et sécurisée optimisée par Adobe Edge Delivery Services.
* [Maillage API pour Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/mesh/) : plateforme API qui permet aux développeurs de combiner plusieurs sources de données en un seul point d’entrée GraphQL. Le maillage API orchestre les API tierces avec l’API Adobe par le biais d’une seule passerelle. Une requête vers le point d’entrée GraphQL unique peut renvoyer des résultats provenant de plusieurs sources.
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/) - Ensemble d’outils de développement avec un accès aux API, aux événements, aux fonctions d’exécution et aux modules externes, que vous pouvez utiliser pour créer des projets pour les applications Adobe.
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/) - Moteur sans serveur permettant de déployer du code personnalisé qui répond aux événements et exécute des fonctions dans le cloud.

## Conditions préalables

Avant d’exécuter la commande `aio commerce init`, vous devez remplir les conditions préalables suivantes :

1. Installez Node Version Manager (NVM).

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. Installez Node.js et NPM. Pour plus d’informations, voir [Node.js](https://nodejs.org/en/).

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. Installez l’[interface de ligne de commande Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Installez le plug-in Adobe I/O API Mesh .

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. Installez le plug-in Adobe I/O Commerce.

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. Mettez à jour les modules externes existants.

   ```bash
   aio plugins:update
   ```

1. Connectez-vous à votre compte Adobe Experience Cloud.

   ```bash
   aio login
   ```

   Si la commande `aio login` ne lance pas de fenêtre de navigateur, reportez-vous à la section [Dépannage](#troubleshooting).

1. Sélectionnez l’organisation IMS, le projet et l’espace de travail. Utilisez les touches fléchées et appuyez sur **Entrée** pour effectuer votre sélection. Pour plus d’informations sur les commandes `aio`, consultez la documentation de l’interface de ligne de commande Adobe I/O [&#128279;](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands).

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. Si ce n’est pas déjà fait, acceptez les conditions d’utilisation pour les développeurs dans la console Adobe Developer en accédant à https://developer.adobe.com/console/home et en cliquant sur **Accepter et continuer**.

## Exécuter la commande `aio commerce init`

L’exécution de la commande suivante crée une génération de modèles automatique pour votre storefront Commerce. Cet échafaudage constitue un excellent point de départ pour construire et comprendre votre vitrine. Pour plus d’informations sur l’utilisation du storefront, consultez la [documentation du storefront Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr).


1. Exécutez la commande `init` :

   ```bash
   aio commerce init
   ```

1. Si vous êtes déjà connecté à GitHub, saisissez `Y` pour créer le référentiel sous votre nom d’utilisateur.

1. Saisissez le nom du référentiel que vous souhaitez créer.

1. Sélectionnez l’une des options suivantes :

   * **Utiliser le client Adobe Commerce de démonstration** - Utilisez un client de démonstration.
      * Si vous sélectionnez cette option, vous êtes invité à installer le robot de synchronisation du code AEM dans une fenêtre de navigateur. Vous devez spécifier le référentiel que vous avez créé et autoriser le robot. Revenez à l’interface de ligne de commande et saisissez `y` pour confirmer l’installation du robot de synchronisation du code AEM.
   * **Sélectionner un client Adobe Commerce disponible** - Sélectionnez un client Commerce existant dans l’organisation sélectionnée.
      * Si vous sélectionnez cette option, vous devez sélectionner le projet et l’espace de travail dans lesquels créer un maillage.
   * **Fournir votre propre URL d’API du client Adobe Commerce** - Sélectionnez cette option si vous êtes un participant au programme d’accès anticipé. Saisissez l’URL d’API fournie dans votre e-mail d’intégration Adobe.

   >[!NOTE]
   >
   >Si vous sélectionnez l’option `Pick an available API (Mesh -> SaaS)` , vous devez disposer d’un projet et d’un Workspace existants dans le Adobe Developer Console. [La création d’un projet modélisé](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/) et la sélection d’App Builder créeront automatiquement les espaces de travail nécessaires.

1. Une fois le processus terminé, vous pouvez personnaliser votre storefront à l’aide des méthodes suivantes :

   * Personnalisez votre code : `https://github.com/<username or org>/<repo name>`
   * Modifiez votre contenu : `https://da.live/#/<username or org>/<repo name>`
   * Gérez votre configuration : `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * Prévisualiser votre storefront : `https://main--<repo name>--<username or org>.aem.page/`
   * Exécuter localement : `aio commerce:dev`

Pour personnaliser votre storefront, consultez la documentation du storefront [Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr).

## Dépannage

Si vous rencontrez des problèmes avec la commande `aio login`, Adobe vous recommande de vous déconnecter complètement de l’interface de ligne de commande et du navigateur, puis de vous reconnecter.

1. Pour vous déconnecter de l’interface de ligne de commande, exécutez :

   ```bash
   aio logout
   ```

1. Dans votre navigateur, accédez à [Adobe Developer Console](https://developer.adobe.com/console), cliquez sur l’icône de votre profil dans le coin supérieur droit, puis sélectionnez **Se déconnecter**.

1. Revenez à l’interface en ligne de commande et exécutez à nouveau la commande `aio login`, qui doit lancer une fenêtre de navigateur pour vous connecter. Vous pouvez ensuite poursuivre en sélectionnant votre organisation, votre projet et votre espace de travail.

   ```bash
   aio console org select
   ```

   ```bash
   aio console workspace select
   ```

   ```bash
   aio console project select
   ```
