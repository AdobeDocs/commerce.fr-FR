---
title: Configurer votre storefront
description: 'Découvrez comment configurer votre storefront [!DNL Adobe Commerce Optimizer] '
role: Developer
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '2287'
ht-degree: 0%

---

# Configurer votre storefront

>[!NOTE]
>
>Cette documentation décrit un produit en développement à accès anticipé et ne reflète pas toutes les fonctionnalités destinées à une disponibilité générale.

Ce tutoriel explique comment configurer et utiliser [le storefront Adobe Commerce optimisé par Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) pour créer un storefront Commerce performant, évolutif et sécurisé optimisé par les données de votre instance [!DNL Adobe Commerce Optimizer].


## Conditions préalables

* Assurez-vous de disposer d’un compte GitHub (github.com) capable de créer des référentiels et configuré pour le développement local.

* Familiarisez-vous avec le workflow et le vocabulaire de base liés à la création d’un storefront pour les services de diffusion Adobe Edge en consultant la [Présentation](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) dans la documentation du storefront Adobe Commerce.
* Configuration de votre environnement de développement


### Configuration de votre environnement de développement

Pour configurer votre environnement de développement, installez la version requise de Node.js et l’extension de navigateur Sidekick.

#### Installation de Node.js

Pour développer et tester localement votre storefront [!DNL Adobe Commerce Optimizer] sur un projet Edge Delivery Services, vous avez besoin de la version 22.13.1 LTS de Node.js.

Si nécessaire, procédez comme suit pour installer le gestionnaire de versions de nœuds (NVM) et la version requise de Node.js.

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

1. Vérifiez l’installation.

   ```bash
   npm -v
   ```

>[!TIP]
>
>Cette configuration est destinée au développement avec [!DNL Adobe Commerce Optimizer] et le storefront du service Adobe Commerce Edge Delivery. Des ressources supplémentaires pour étendre et personnaliser votre solution [!DNL Adobe Commerce Optimizer] sont disponibles via [App Builder pour Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) et [le maillage API pour Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Pour obtenir des informations d’accès et d’utilisation, contactez votre représentant de compte Adobe.

#### Installation de Sidekick

Installez l’extension de navigateur Sidekick pour modifier, prévisualiser et publier le contenu du storefront. Voir les instructions d’installation de [Sidekick](https://www.aem.live/docs/sidekick#installation).


## Création de votre storefront

Le storefront que vous créez pour votre projet [!DNL Adobe Commerce Optimizer] est créé à l’aide d’une version personnalisée de la norme standard du storefront d’Adobe Commerce sur Edge Delivery Services. Le standard est un ensemble de fichiers et de dossiers qui constituent un point de départ pour la création de votre storefront.

Ce processus de configuration de storefront est personnalisé spécifiquement pour les projets [!DNL Adobe Commerce Optimizer]. Le flux est différent du flux de la configuration standard [de la vitrine](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) Adobe des services de remise de Commerce sur Edge.

>[!NOTE]
>
>Ce didacticiel utilise macOS, Chrome et Visual Studio Code comme environnement de développement. Les captures d’écran et les instructions reflètent cette configuration. Vous pouvez utiliser un système d’exploitation, un navigateur et un éditeur de code différents, mais l’interface utilisateur que vous voyez et les étapes à suivre varient en conséquence.

### Workflow - Aperçu

Suivez ces étapes pour configurer une vitrine à utiliser avec Adobe Commerce Optimizer.

1. **[Créer un dossier](#step-1-create-a-content-folder)** de contenu : créez un dossier de contenu partagé dans Google Drive ou SharePoint. Ce dossier contient l’exemple de contenu et de ressources pour votre storefront.

1. **[Créer un référentiel de code](#step-1-create-a-code-repository)**-Créez un référentiel GitHub à partir du modèle standard Adobe Commerce + Edge Delivery Services. Incluez toutes les branches du référentiel source.
1. **[Mettre à jour le modèle standard de storefront](#step-2-update-the-storefront-boilerplate)**-Mettez à jour le modèle standard personnalisé sur la branche `aco` du référentiel pour connecter votre dossier de contenu au storefront et passez en revue la configuration de storefront qui fournit les données de l’instance de démonstration Adobe Commerce Optimizer à votre storefront.
1. **[Charger le code standard storefront mis à jour](#step-3-upload-the-updated-boilerplate-code)**-Remplacez le code de la branche `main` par le code mis à jour de la branche `aco`.
1. **[Ajoutez l’application CodeSync](#step-4-add-the-aem-code-sync-app)** connectez votre référentiel au service Edge Delivery. Ne connectez pas l’application de synchronisation du code tant que vous n’avez pas terminé la personnalisation du code source et que vous n’êtes pas prêt à transmettre le code à la branche `main`.
1. **[Prévisualiser et publier votre contenu](#step-5-preview-and-publish-your-content)**-Utilisez l’extension Sidekick pour prévisualiser et publier le contenu du site à partir du dossier de contenu vers le storefront.
1. **[Prévisualiser votre site et afficher des exemples de données](#step-6-preview-your-site-and-view-sample-data)**-Connectez-vous à votre site storefront pour afficher les exemples de contenu et de données de l’instance de démonstration [!DNL Adobe Commerce Optimizer].
1. **[Développez le storefront dans votre environnement local](#step-7-develop-the-storefront-in-your-local-environmentdevelop-the-storefront-in-your-local-environment)**-Installez les dépendances requises. Démarrez le serveur de développement local et mettez à jour la configuration du storefront pour vous connecter à l’instance [!DNL Adobe Commerce Optimizer] qu’Adobe a configurée pour vous.
1. **[Gérer le contenu du site](#step-8-manage-site-content)**—En savoir plus sur la mise à jour et la gestion du contenu du site.

### Étape 1 : créer un dossier de contenu

Suivez les instructions de la documentation du storefront Adobe Commerce pour ajouter un dossier de contenu partagé dans Google Drive ou SharePoint et ajouter l’exemple de contenu. L’exemple de contenu comprend des images, du texte et d’autres ressources qui constituent votre site.

* [Créer et partager un lecteur Google ou un dossier SharePoint](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#create-and-share-folder)
* [Chargez l’exemple de contenu](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content) dans votre dossier.

### Étape 2 : créer un référentiel de code

Créez un référentiel de code dans GitHub à l’aide du modèle Edge Delivery Services + Adobe Commerce Boilerplate . Ce modèle fournit le code standard pour votre storefront.

1. Connectez-vous à votre compte GitHub.

1. Accédez au référentiel GitHub [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce).

1. Sélectionnez **Utiliser ce modèle**, puis sélectionnez **Créer un référentiel** dans le menu déroulant.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   La page de configuration du référentiel s’ouvre alors.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Remplissez le formulaire de configuration avec les détails suivants :

   * **Modèle de référentiel** : `hlxsites/aem-boilerplate-commerce` (par défaut).
   * **Inclure toutes les branches** : sélectionnez cette option pour inclure toutes les branches.
   * **Propriétaire** : votre organisation ou compte (obligatoire).
   * **Nom du référentiel** : nom unique de votre nouveau référentiel (obligatoire).
   * **Description** : brève description de votre référentiel (facultatif).
   * **Public ou privé** : Adobe recommande public (par défaut).

1. Sélectionnez **Créer un référentiel**.

   Au bout d’une minute ou deux, votre nouveau référentiel s’ouvre.

   Ignorez les notifications de demande de tirage affichées dans le nouveau référentiel.

### Étape 3 : mettre à jour la norme storefront

Dans cette section, vous effectuez les tâches suivantes :

* Consultez la branche `aco` de votre référentiel pour mettre à jour le modèle standard personnalisé pour les projets [!DNL Adobe Commerce Optimizer]
* Connectez votre dossier de contenu au storefront en mettant à jour le fichier `fstab.yaml` pour pointer vers votre dossier de contenu.
* Consultez le fichier de configuration du storefront, `config.json`
* Configurez l’extension Sidekick pour modifier, prévisualiser et publier du contenu à partir de votre dossier de contenu partagé.

Vous avez besoin des informations suivantes pour effectuer ces étapes :

* **URL du référentiel GitHub de l’étape 2**— `github.com/{ORG}/{SITE}`

   * `{ORG}` est le nom d’organisation ou le nom d’utilisateur du référentiel

   * `{SITE}` est le nom de votre référentiel

* **URL du dossier de contenu de l’étape 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` est l’identifiant du dossier que vous avez créé avec les données d’exemple de contenu.

#### Mettez à jour le code standard pour vous connecter à votre dossier de contenu

1. Clonez le référentiel sur votre ordinateur local.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   Si vous rencontrez des erreurs lors du clonage du référentiel, consultez la section [ Dépannage des erreurs de clonage ](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) dans la documentation GitHub.

1. Ouvrez le référentiel dans votre terminal ou IDE.

1. Extrayez la branche `aco`

   ```bash
   git checkout aco
   ```

1. Créez votre fichier de configuration en copiant le fichier `default-fstab.yaml` dans `fstab.yaml`.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. Mettez à jour le fichier de configuration du storefront pour pointer vers votre URL de contenu.

   1. Ouvrez le fichier de configuration [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary).

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}
      
      folders:
       /products/: /products/default
      ```

   1. Remplacez `{YOUR_MOUNTPOINT_URL}` par l’URL de votre système de gestion de contenu.

      Par exemple, si vous utilisez Google Drive, le code mis à jour doit ressembler à ceci.

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}
      ```

   1. Enregistrez le fichier.

#### Vérifier la configuration de la connexion aux données

La connexion de données établit la communication entre Adobe Commerce Optimizer et le storefront, en veillant à ce que les données du catalogue circulent de manière transparente vers le storefront. Ce processus renseigne diverses interfaces de storefront, notamment le composant de recherche, la liste de produits et les pages de détails de produits requises pour la [!DNL Adobe Commerce Optimizer].

Pour la configuration initiale de storefront, Adobe fournit un fichier de configuration par défaut qui se connecte à une instance de démonstration Adobe Commerce Optimizer avec des exemples de données.

```json
{
  "public": {
    "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
        "cs": {
          "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
          "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
          "ac-price-book-id": "west_coast_inc",
          "ac-scope-locale": "en-US"
        }
      },
      "analytics": {
        "base-currency-code": "USD",
        "environment": "Production",
        "store-id": 1,
        "store-name": "ACO Demo",
        "store-url": "https://www.aemshop.net",
        "store-view-id": 1,
        "store-view-name": "Default Store View",
        "website-id": 1,
        "website-name": "Main Website"
      }
    }
  }
}
```

Consultez le fichier de configuration de storefront dans votre référentiel pour comprendre comment la connexion aux données est établie.

1. Dans votre référentiel de code, accédez au répertoire racine.

1. Ouvrez le fichier `config.json`.

   Dans ce fichier, les valeurs de clé suivantes spécifient l’instance Adobe Commerce Optimizer à laquelle se connecter et déterminent les données qui alimentent le storefront :

   * `commerce-endpoint` définit l’instance Adobe Commerce Optimizer à laquelle se connecter.
   * `headers` déterminer les données qui sont transmises au storefront.
      * `ac-channel-id` est défini sur `west_coast_inc`
      * `ac-price-book-id` est défini sur `west_coast_inc`
      * `ac-scope-locale` est défini sur `en-US`
      * `ac-price-book-id` est défini sur `west_coast_inc`

   Ces valeurs définissent l&#39;identifiant du canal, le paramètre régional et l&#39;identifiant du catalogue pour envoyer des données de catalogue à un canal de vente spécifique et filtrer ces données en fonction des paramètres régionaux et des valeurs du catalogue spécifiés. Plus tard, vous apprendrez à modifier l’instance Adobe Commerce Optimizer et à mettre à jour les en-têtes pour définir les données diffusées au storefront.

1. Après avoir examiné le fichier, fermez-le et poursuivez le tutoriel.


#### Configuration de l’extension Sidekick

Ajoutez la configuration du projet pour l’extension Sidekick. Sidekick permet de modifier, de prévisualiser et de publier le contenu de votre storefront. Cette configuration vous permet d’utiliser Sidekick pour gérer le contenu à la fois dans votre dossier de contenu partagé et sur les pages du site publiées dans les environnements d’évaluation et de production.

>[!NOTE]
>
>Assurez-vous d’avoir installé l’extension [Sidekick](https://www.aem.live/docs/sidekick#installation) dans votre navigateur.

1. Ouvrez le fichier `tools/sidekick/config.json`.

   Fichier de configuration de Sidekick

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   Pour plus d’informations, consultez la documentation de la bibliothèque Sidekick [&#128279;](https://www.aem.live/docs/sidekick-library).

+++

1. Mettez à jour les valeurs de clé `url` avec les valeurs de votre référentiel GitHub.

   * `{ORG}` est le nom du référentiel ou d’utilisateur de votre référentiel de code

   * `{SITE}` est le nom du référentiel

1. Enregistrez le fichier.

### Étape 4 : charger le code standard mis à jour

Pour utiliser le code standard personnalisé du storefront, remplacez le code sur la branche `main` par vos mises à jour.

1. Dans l’éditeur ou l’IDE, validez et enregistrez les fichiers que vous avez mis à jour.

   ```bash
   git add .
   ```

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Envoyez les modifications à la branche `aco` et remplacez la branche `main` :

   ```bash
   git push origin aco:main -f
   ```

### Étape 5 : ajouter l’application de synchronisation du code AEM

Connectez votre référentiel au service Edge Delivery en ajoutant l’application GitHub de synchronisation du code AEM à votre référentiel.

>[!IMPORTANT]
>
>Ne connectez pas l’application de synchronisation du code tant que vous n’avez pas chargé le code standard mis à jour dans la branche principale de votre référentiel GitHub.

1. Ouvrez la page de configuration de l’application de synchronisation de code [AEM](https://github.com/apps/aem-code-sync).

1. Sélectionnez **Configurer**, puis authentifiez-vous auprès de l’**organisation** ou du **compte** qui contient le référentiel que vous avez créé.

1. Dans le formulaire, choisissez **Sélectionner uniquement les référentiels** et sélectionnez le référentiel que vous avez créé.

1. Sélectionnez **Installer** pour ajouter l’application de synchronisation du code AEM à votre référentiel.

   Un message indiquant que l’application a été installée s’affiche normalement.

### Étape 6 : prévisualiser et publier votre contenu

Pour ajouter du contenu à votre storefront, vous devez prévisualiser et publier votre contenu à l’aide de l’extension Sidekick.

1. Ouvrez votre dossier de contenu dans Google Drive ou SharePoint.

1. Activez Sidekick en cliquant sur l’icône Sidekick dans la barre d’outils du navigateur.

   ![[!DNL Turn on Sidekick from browser toolbar]](./assets/storefront-enable-sidekick-toolbar.png){width="700" zoomable="yes"}

1. Utilisez la barre d’outils Sidekick pour prévisualiser et publier votre contenu.

   ![[Sélectionnez les fichiers à prévisualiser et à publier]](./assets/storefront-content-preview-publish.png){width="700" zoomable="yes"}

1. Sélectionnez les fichiers séparément dans chaque dossier et utilisez la barre d’outils Sidekick pour prévisualiser et publier tous les fichiers.

   * **Aperçu** : télécharge le contenu dans l’environnement intermédiaire. Les URL d’évaluation de vitrine se terminent par `.aem.page`.

   * **Publish**–Télécharge le contenu dans l’environnement de production. Les URL de production se terminent par `aem.live`.

Pour plus d’informations, consultez la documentation sur le Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick) .

### Étape 7 : Aperçu de votre site

Affichez un aperçu de votre site pour vérifier que l’exemple de contenu et les données de démonstration de Adobe Commerce Optimizer s’affichent correctement.

* **Les exemples de contenu** sont diffusés à partir de votre dossier de contenu partagé. Cela inclut les mises en page, les bannières et tout autre contenu que vous avez publié à l’aide du sidekick.
* **Les exemples de données** sont diffusés à partir de l’instance [!DNL Adobe Commerce Optimizer] de démonstration. Les données incluent les données de produit avec les attributs de produit, les images, les descriptions de produits et les prix renseignés en fonction des valeurs spécifiées dans le fichier de configuration de vitrine, `config.json`.


#### Connectez-vous à votre site pour afficher des exemples de contenu et de données.

1. Connectez-vous à votre site en accédant à `https://main--{SITE}--{ORG}.aem.live`.

   Remplacez `{ORG}` et `{SITE}` par l’organisation et le nom de votre référentiel standard.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Si la page renvoie une erreur 404, assurez-vous d’avoir publié le contenu à l’aide de l’extension Sidekick. Vérifiez également que le fichier `fstab.yaml` mis à jour utilise l’URL de votre dossier de contenu.

1. Affichez les exemples de données de catalogue provenant de votre instance de démonstration Commerce Optimizer.

   1. Recherchez `tires` pour afficher une liste déroulante des produits de pneus disponibles.

   ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

   Le composant Recherche fait partie du code standard du storefront. Les données des résultats de recherche sont renseignées en fonction de la configuration du storefront.

   1. Appuyez sur **Entrée** pour afficher la page de liste de produits.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. Affichez la page des détails d’un produit en sélectionnant n’importe quel produit de pneumatique de la page.

      Si vous explorez le storefront, notez que certains composants ne fonctionnent pas. Par exemple, l’ajout d’un produit au panier renvoie une erreur et les composants de gestion de compte ne fonctionnent pas. En effet, ces composants n’ont pas été configurés pour recevoir des données d’un serveur principal Commerce. Les données de votre instance Adobe Commerce Optimizer renseignent uniquement les pages du composant de recherche, de la liste de produits et des détails du produit.

   1. Après avoir exploré le storefront, poursuivez avec le tutoriel.


### Étape 8 : développer le storefront dans votre environnement local

Dans cette section, vous testez la configuration du storefront dans votre environnement de développement local en connectant le storefront à l’instance [!DNL Adobe Commerce Optimizer] qu’Adobe vous a configurée.

Pour établir la connexion, vous avez besoin du point d’entrée GraphQL pour les services de marchandisage qui a été fourni dans votre e-mail d’intégration.

```text
https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

#### Démarrer le développement local

1. Dans votre IDE, extrayez la branche principale de votre référentiel de code GitHub.

   ```bash
   git checkout main
   ```

1. Installez les dépendances requises.

   ```bash
   npm install
   ```

1. Démarrez le serveur de développement local.

   ```bash
   npm start
   ```

   La première page de votre storefront standard doit être visible dans votre navigateur à l’adresse `http://localhost:3000`.

![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Mettre à jour la configuration du storefront

Mettez à jour le fichier de configuration de storefront et prévisualisez les modifications dans votre environnement de développement local.


1. Dans votre IDE, mettez à jour la configuration storefront pour vous connecter à l’instance [!DNL Adobe Commerce Optimizer] qu’Adobe a configurée pour vous.

   1. Ouvrez le fichier `config.json`.

   1. Mettez à jour les valeurs suivantes à l’aide du point d’entrée de votre instance [!DNL Adobe Commerce Optimizer] :

      * **`commerce-endpoint`**-Remplacez la valeur existante par l’URL de votre point d’entrée.

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`** : remplacez la valeur existante par l’ID client de l’URL de votre point d’entrée.

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. Enregistrez le fichier.

      Si votre aperçu local fonctionne correctement, les mises à jour sont appliquées à votre storefront local.

1. Consultez le site pour voir les résultats de la modification de configuration.

   1. Dans le navigateur, accédez à `http://localhost:3000` et actualisez la page.

   1. Dans l’en-tête du storefront, cliquez sur la loupe pour rechercher des `tires`.

      ![Rechercher des pneus](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

      Notez que la liste déroulante ne se remplit pas.

   1. Appuyez sur **Entrée** pour afficher la page Liste des produits.

      ![Résultats de recherche vides avec des valeurs d’en-tête non valides](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      La recherche ne renvoie aucun résultat, car les en-têtes de votre fichier de configuration de storefront utilisent des valeurs d’en-têtes basées sur l’instance de démonstration. Maintenant que la configuration pointe vers l’instance [!DNL Adobe Commerce Optimizer] configurée pour vous, ces valeurs ne sont pas valides.

### Étapes suivantes

Voir le cas d’utilisation complet [Storefront and Catalog Administrator](./use-case/admin-use-case.md) pour savoir comment afficher le contenu dans votre storefront en mettant à jour la configuration de storefront à l’aide des valeurs de votre instance de [!DNL Adobe Commerce Optimizer].

>[!MORELIKETHIS]
>
>* Si vous envisagez de l’utiliser [!DNL Adobe Commerce Optimizer] sans Adobe Commerce, consultez la documentation[&#128279;](https://experienceleague.adobe.com/developer/commerce/storefront/) Adobe Experience Manager Storefront pour en savoir plus sur la mise à jour du contenu du site et l’intégration avec vos composants frontaux Commerce et vos données principales.
></br></br>
>* Si vous envisagez d’utiliser [!DNL Adobe Commerce Optimizer] un serveur principal Adobe Commerce, consultez la documentation[&#128279;](https://experienceleague.adobe.com/developer/commerce/storefront/) Adobe Boutique Commerce pour savoir comment mettre à jour le contenu et configurer les composants de la vitrine pour la gestion des comptes, le paiement et d’autres fonctionnalités.
