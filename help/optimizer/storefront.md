---
title: Configurer votre storefront
description: 'Découvrez comment configurer votre storefront [!DNL Adobe Commerce Optimizer] '
role: Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 475706df971e75091ee72e89d64088fa56aec4dd
workflow-type: tm+mt
source-wordcount: '1858'
ht-degree: 0%

---

# Configurer votre storefront

Ce tutoriel fournit des instructions détaillées sur la configuration et l’utilisation du [storefront Adobe Commerce optimisé par Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) afin de créer un storefront Commerce performant, évolutif et sécurisé, optimisé par les données de votre instance [!DNL Adobe Commerce Optimizer].


>[!TIP]
>
>Accélérez le processus de configuration du storefront à l’aide de l’outil Créateur de site pour configurer votre référentiel de code storefront et votre environnement de création de documents
>&#x200B;>automatiquement. Ensuite, vous pouvez utiliser ces instructions pour comprendre comment le storefront a été créé et en savoir plus sur les composants disponibles.

## Conditions préalables

* Assurez-vous de disposer d’un compte GitHub (github.com) capable de créer des référentiels et configuré pour le développement local.

* Découvrez les concepts et le workflow de développement des storefronts Commerce sur Adobe Edge Delivery Services en consultant la [Présentation](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) dans la documentation du storefront Adobe Commerce.
* Configuration de votre environnement de développement


### Configuration de votre environnement de développement

Installez Node.js et l’extension de navigateur Sidekick requise pour développer et tester votre storefront [!DNL Adobe Commerce Optimizer] sur Edge Delivery Services.

#### Installation de Node.js

Installez Node Version Manager (NVM) et la version requise de Node.js (22.13.1 LTS).

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
>Des ressources supplémentaires pour étendre et personnaliser votre solution [!DNL Adobe Commerce Optimizer] sont disponibles via [App Builder pour Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) et [le maillage API pour Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Pour obtenir des informations d’accès et d’utilisation, contactez votre représentant de compte Adobe.

#### Installation de Sidekick

Installez l’extension de navigateur Sidekick pour modifier, prévisualiser et publier du contenu sur le storefront. Voir les instructions d’installation de [Sidekick](https://www.aem.live/docs/sidekick#installation).

## Création de votre storefront

Le storefront que vous créez pour votre projet [!DNL Adobe Commerce Optimizer] utilise une version personnalisée de la norme standard du storefront d’Adobe Commerce sur Edge Delivery Services. Le standard est un ensemble de fichiers et de dossiers qui constituent un point de départ pour le développement du storefront. Ce processus de configuration est différent du processus de configuration standard pour un [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>Ce tutoriel utilise macOS, Chrome et Visual Studio Code comme environnement de développement. Les captures d’écran et les instructions reflètent cette configuration. Vous pouvez utiliser un autre système d’exploitation, un autre navigateur et un autre éditeur de code, mais l’interface utilisateur qui s’affiche et les étapes que vous suivez varient en conséquence.

### Présentation des workflows

Pour configurer un storefront à utiliser avec [!DNL Adobe Commerce Optimizer], procédez comme suit.

1. **[Créer un référentiel de code](#step-1-create-site-code-repository)**-Créez un référentiel GitHub à partir du modèle standard Adobe Commerce + Edge Delivery Services. Incluez toutes les branches du référentiel source.
1. **[Mettre à jour le modèle standard du storefront](#step-2-update-the-storefront-boilerplate)**-Mettez à jour le modèle standard personnalisé sur la branche `aco` pour connecter votre dossier de contenu au storefront.
1. **[Déployer les modifications](#step-3-deploy-changes)**-Remplacez le code de la branche `main` par le code mis à jour de la branche `aco`.
1. **[Ajoutez l’application CodeSync](#step-5-add-the-aem-code-sync-app)** connectez votre référentiel au service Edge Delivery. Ne connectez pas l’application de synchronisation du code tant que vous n’avez pas terminé la personnalisation du code source et envoyé le code vers la branche `main`.
1. **[Ajouter du contenu](#step-6-add-content)**-Utilisez l’outil de clonage de contenu de démonstration pour créer et initialiser votre contenu storefront dans l’environnement de création de documents hébergé sur `https://da.live`.
1. **[Prévisualiser le site de démonstration](#step-7-preview-demo-site)**-Connectez-vous à votre site storefront pour afficher l’exemple de contenu et les données de l’instance de démonstration [!DNL Adobe Commerce Optimizer].
1. **[Développez dans votre environnement local](#step-8-develop-in-your-local-environment)**-Installez les dépendances requises. Démarrez le serveur de développement local et mettez à jour la configuration du storefront pour vous connecter à l’instance [!DNL Adobe Commerce Optimizer] qu’Adobe a configurée pour vous.
1. **[Étapes suivantes](#next-steps)**-En savoir plus sur la gestion et l’affichage du contenu et des données dans le storefront.


### Étape 1 : créer un référentiel de code de site

Créez un référentiel GitHub pour le code standard du site pour votre storefront à l’aide du modèle Edge Delivery Services + Adobe Commerce Boilerplate .

1. Connectez-vous à votre compte GitHub.

1. Accédez au référentiel GitHub [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce).

1. Sélectionnez **Utiliser ce modèle**, puis sélectionnez **Créer un référentiel** dans le menu déroulant.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   La page de configuration du référentiel s’affiche.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Remplissez le formulaire de configuration avec les détails suivants :

   * **Modèle de référentiel** : `hlxsites/aem-boilerplate-commerce` (par défaut).
   * **Propriétaire** : votre organisation ou compte (obligatoire).
   * **Nom du référentiel** : nom unique de votre nouveau référentiel (obligatoire).
   * **Description** : brève description de votre référentiel (facultatif).
   * **Public ou privé** : Adobe recommande public (par défaut).

1. Sélectionnez **Créer un référentiel**.

   Au bout de quelques minutes, votre nouveau référentiel s’ouvre.

   Ignorez les notifications de demande de tirage affichées dans l’interface utilisateur GitHub.

### Étape 2 : mettre à jour la norme storefront

Vous avez besoin des informations suivantes pour mettre à jour le code standard du storefront :

* **URL du référentiel GitHub de l’étape 2**— `github.com/{ORG}/{SITE}`

   * `{ORG}` est le nom d’organisation ou le nom d’utilisateur du référentiel

   * `{SITE}` est le nom de votre référentiel

* **URL du dossier de contenu de l’étape 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` est l’identifiant du dossier que vous avez créé avec les données d’exemple de contenu.

#### Lier le référentiel à l’environnement de création de documents

1. Clonez le référentiel sur votre ordinateur local.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   Si vous rencontrez des erreurs lors du clonage du référentiel, consultez la section [ Dépannage des erreurs de clonage ](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) dans la documentation GitHub.

1. Ouvrez le référentiel dans votre terminal ou IDE.

1. Créez votre fichier de configuration en copiant le fichier `default-fstab.yaml` dans `fstab.yaml`.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. Mettez à jour le point de montage dans le fichier de configuration du storefront pour pointer vers votre URL de contenu.

   1. Ouvrez le fichier de configuration [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary).

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. Remplacez les chaînes `{ORG}` et `{SITE}` par les valeurs du référentiel GitHub que vous avez créé pour votre code standard.

      Par exemple, le code mis à jour doit se présenter comme suit :

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. Enregistrez le fichier.

#### Configuration de l’extension Sidekick

1. Ajoutez la configuration du projet pour l’extension Sidekick. Cette configuration garantit que Sidekick est disponible pour gérer le contenu de votre projet de storefront.

>[!NOTE]
>
>Assurez-vous d’avoir installé l’extension [Sidekick](https://www.aem.live/docs/sidekick#installation) dans votre navigateur.

1. Créez un `tools/sidekick` de répertoire.

   ```shell
   mkdir tools/sidekick
   ```

1. Copiez le fichier `demo-sidekick.json` du répertoire racine dans le répertoire `tools/sidekick` et renommez-le en `config.json`.

   ```shell
   cp demo-sidekick.json tools/sidekick/config.json
   ```

1. Personnalisez la configuration Sidekick de votre site.

   Dans `tools/sidekick/` répertoire , modifiez le fichier `config.json`.

   +++Fichier de configuration Sidekick

   ```json
   {
     "project": "My Project",
     "editUrlLabel": "Document Authoring",
     "editUrlPattern": "https://da.live/edit#/{{org}}/{{site}}{{pathname}}"
   }
   ```

1. Mettez à jour les valeurs de clé `url` avec les valeurs de votre référentiel GitHub.

   * Remplacez la chaîne `{{ORG}}` par l’organisation ou le nom d’utilisateur de votre référentiel.

   * Remplacez la chaîne `{{SITE}}` par le nom du référentiel.

   * La variable `pathname` est renseignée par le système.

   +++Exemple de fichier de configuration mis à jour

   Si votre référentiel GitHub est nommé `aco-storefront` et que votre organisation est `early-adopter`, l’URL mise à jour doit se présenter comme suit :

   ```json
   {
     "project": "My Project",
     "editUrlLabel": "Document Authoring",
     "editUrlPattern": "https://da.live/edit#/aco-storefront/early-adopter{{pathname}}"
   }
   ```

   +++

1. Enregistrez le fichier.

### Étape 3 : déployer les modifications

Pour utiliser le code standard personnalisé du storefront, remplacez le code sur la branche `main` par vos mises à jour.

1. Dans l’éditeur ou l’IDE, validez et enregistrez les fichiers que vous avez mis à jour.

   ```bash
   git add .
   ```

1. Vérifiez que vous validez les deux fichiers mis à jour.

   ```bash
   git status
   On branch main
   Your branch is up to date with 'origin/main'.
   
   Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   fstab1.yaml
        modified:   tools/sidekick/config.json
   ```

1. Validez les modifications.

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Appliquez vos modifications.

   ```bash
   git push
   ```

### Étape 5 : ajouter l’application de synchronisation du code AEM

Connectez votre référentiel au service Edge Delivery en ajoutant l’application GitHub de synchronisation du code AEM à votre référentiel.

>[!IMPORTANT]
>
>Ne connectez pas l’application de synchronisation du code tant que vous n’avez pas chargé le code standard mis à jour dans la branche principale de votre référentiel GitHub.

1. Ouvrez la page de configuration de l’application de synchronisation de code [AEM](https://github.com/apps/aem-code-sync).

1. Sélectionnez **Configurer**, puis authentifiez-vous auprès de l’**organisation** ou du **compte** qui contient le référentiel que vous avez créé.

1. Dans le formulaire, choisissez **Sélectionner uniquement les référentiels**, puis sélectionnez le référentiel que vous avez créé.

1. Sélectionnez **Installer** pour ajouter l’application de synchronisation du code AEM à votre référentiel.

   Un message indiquant que l’application a été installée s’affiche normalement.

### Étape 6 : ajouter du contenu

Créez et initialisez votre contenu storefront dans l’environnement de création de documents hébergé sur `https://da.live` à l’aide de l’outil Créateur de site. Cet outil importe l’exemple de contenu dans l’environnement de création de documents et termine le processus de prévisualisation et de publication du contenu pour tous les documents de l’exemple de contenu. L’exemple de contenu comprend les mises en page, les bannières, les libellés et d’autres éléments pour renseigner votre storefront.

1. Ouvrez l’outil [ Créateur de site ](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

1. Configurez votre référentiel :

   * Sélectionnez **[!UICONTROL Use Existing Repository]**.
   * Saisissez le **[!UICONTROL Organization/Username]** de votre projet storefront standard.
   * Saisissez le **[!UICONTROL Repository Name]**.

1. Importez, prévisualisez et publiez le contenu dans l’environnement de création de documents en sélectionnant **Créer un site**.

   ![[!DNL AEM demo content clone tool]](./assets/storefront-edit-initial-content.png){width="700" zoomable="yes"}

   Une fois le site créé, vous pouvez utiliser les liens des sections [!UICONTROL Edit content] et [!UICONTROL View Site] pour explorer le storefront de démonstration.

   Les principaux liens vers votre contenu et votre site suivent les formats suivants :

   * **Dossier de contenu racine**— `https://da.live/#/{ORG}/{SITE}`
   * **Aperçu du site**—   `https://main--{SITE}--{ORG}.aem.page/`
   * **Exploitation du site :**— `https:/main--{SITE}--{ORG}.ae.live/`

1. Ouvrez le lien du dossier de contenu racine pour afficher le contenu.

   ![[!DNL Storefront Document Author environment]](./assets/storefront-document-author-environment.png){width="700" zoomable="yes"}

   >[!TIP]
   >
   >Dans la navigation latérale, utilisez les liens [!UICONTROL **Apprendre**] et [!UICONTROL **Découvrir**] pour accéder aux ressources de formation afin de gérer le site et son contenu.

### Étape 7 : aperçu du site de démonstration

Vérifiez que l’exemple de contenu et les données de l’instance de démonstration Adobe Commerce Optimizer s’affichent correctement.

* **L’exemple de contenu** est diffusé à partir du dossier de contenu dans l’environnement de création de documents. Il comprend les mises en page, les bannières et les étiquettes de votre site.
* **Données d’exemple** est diffusée à partir de l’instance de démonstration [!DNL Adobe Commerce Optimizer]. Les données incluent des données de produit avec des attributs de produit, des images, des descriptions de produit et des prix renseignés en fonction des valeurs d’en-tête spécifiées dans le fichier de configuration du storefront, `config.json`.

#### Connectez-vous à votre site pour afficher des exemples de contenu et de données

1. Affichez votre site en accédant à `https://main--{SITE}--{ORG}.aem.live`.

   Remplacez `{ORG}` et `{SITE}` par l’organisation et le nom de votre référentiel standard.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Si la page renvoie une valeur 404, vérifiez les points suivants :

   * [ Le point de montage de votre fichier `fstab.yaml` pointe vers l’URL de contenu appropriée ](#link-the-repository-to-the-document-author-environment) : `https://content.da.live/{ORG}/{SITE}/`
   * [Vous avez configuré l’application de synchronisation du code pour qu’elle se connecte à votre référentiel GitHub](#step-5%3A-add-the-aem-code-sync-app).
   * [Vous avez publié le contenu dans l’environnement de création de documents à l’aide de l’outil de clonage de contenu de démonstration](#step-6%3A-add-content-documents-for-your-storefront).


1. Affichez les exemples de données de catalogue provenant de l’instance par défaut de Commerce Optimizer.

   1. Dans l’en-tête du storefront, cliquez sur la loupe pour rechercher des `tires`.

      ![[!DNL View product list page]](./assets/storefront-site-with-aco-data.png){width="675" zoomable="yes"}

   1. Appuyez sur **Entrée** pour afficher la page des résultats de la recherche.

      ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

      Les composants de la page des résultats de la recherche sont définis par le document de contenu `search`. Les données des résultats de recherche sont renseignées en fonction de la configuration de storefront dans `config.json`.

   1. Affichez la page des détails du produit en sélectionnant n’importe quel produit de pneumatique de la page.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

      Les composants de la page Détails du produit sont définis par le document de contenu `default` dans le dossier `product` .

### Étape 8 : développement dans votre environnement local

Dans cette section, vous mettez à jour la configuration de storefront à partir de votre environnement de développement local.

* Mettez à jour la configuration storefront pour vous connecter au point d’entrée GraphQL pour l’instance [!DNL Adobe Commerce Optimizer] qu’Adobe a configurée pour vous.
* Mettez à jour les valeurs d’en-tête pour récupérer les données de votre instance.

#### Démarrer le développement local

1. Dans votre IDE, extrayez votre branche principale et réinitialisez-la à la dernière validation sur la branche distante.

   ```bash
   git checkout main
   git reset --hard origin/main
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

   1. Appuyez sur **Entrée** pour afficher la page Résultats de la recherche.

      ![Résultats de recherche vides avec des valeurs d’en-tête non valides](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      La recherche ne renvoie aucun résultat, car les valeurs d’en-tête de votre fichier de configuration de storefront sont basées sur l’instance par défaut. Maintenant que la configuration pointe vers l’instance [!DNL Adobe Commerce Optimizer] configurée pour vous, ces valeurs ne sont pas valides.

### Étapes suivantes

Voir le cas pratique complet [Storefront and Catalog Administrator](./use-case/admin-use-case.md) pour en savoir plus sur la gestion et l’affichage du contenu et des données dans le storefront.

>[!MORELIKETHIS]
>
> Consultez la [documentation du storefront Adobe Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/) pour en savoir plus sur la mise à jour du contenu du site et l’intégration aux composants frontend Commerce et aux données principales.
