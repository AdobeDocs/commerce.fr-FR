---
title: Configurer votre storefront
description: 'Découvrez comment configurer votre storefront [!DNL Adobe Commerce Optimizer] '
role: Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Configurer votre storefront

Ce tutoriel explique comment configurer et utiliser le [storefront Adobe Commerce optimisé par Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=fr) pour créer un storefront Commerce performant, évolutif et sécurisé optimisé par les données de votre instance [!DNL Adobe Commerce Optimizer].


## Conditions préalables

- Assurez-vous de disposer d’un compte GitHub (github.com) capable de créer des référentiels et configuré pour le développement local.

- Découvrez les concepts et le workflow de développement des storefronts Commerce sur Adobe Edge Delivery Services en consultant la [Présentation](https://experienceleague.adobe.com/developer/commerce/storefront/get-started?lang=fr) dans la documentation du storefront Adobe Commerce.
- Configuration de votre environnement de développement


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
>Des ressources supplémentaires pour étendre et personnaliser votre solution [!DNL Adobe Commerce Optimizer] sont disponibles via [App Builder pour Adobe Commerce](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) et [le maillage API pour Adobe Developer App Builder](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Pour obtenir des informations d’accès et d’utilisation, contactez votre représentant de compte Adobe.

#### Installation de Sidekick

Installez l’extension de navigateur Sidekick pour modifier, prévisualiser et publier du contenu sur le storefront. Voir les instructions d’installation de [Sidekick](https://www.aem.live/docs/sidekick#installation).

## Création de votre storefront

Le storefront que vous créez pour votre projet [!DNL Adobe Commerce Optimizer] utilise une version personnalisée de la norme standard du storefront d’Adobe Commerce sur Edge Delivery Services. Le standard est un ensemble de fichiers et de dossiers qui constituent un point de départ pour le développement du storefront. Ce processus de configuration est différent du processus de configuration standard pour un [Adobe Commerce on Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=fr).

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

   - **Modèle de référentiel** : `hlxsites/aem-boilerplate-commerce` (par défaut).
   - **Inclure toutes les branches** : sélectionnez cette option pour inclure toutes les branches.
   - **Propriétaire** : votre organisation ou compte (obligatoire).
   - **Nom du référentiel** : nom unique de votre nouveau référentiel (obligatoire).
   - **Description** : brève description de votre référentiel (facultatif).
   - **Public ou privé** : Adobe recommande public (par défaut).

1. Sélectionnez **Créer un référentiel**.

   Au bout de quelques minutes, votre nouveau référentiel s’ouvre.

   Ignorez les notifications de demande de tirage affichées dans l’interface utilisateur GitHub.

### Étape 2 : mettre à jour la norme storefront

Vous avez besoin des informations suivantes pour mettre à jour le code standard du storefront :

- **URL du référentiel GitHub de l’étape 2**— `github.com/{ORG}/{SITE}`
   - `{ORG}` est le nom d’organisation ou le nom d’utilisateur du référentiel
   - `{SITE}` est le nom de votre référentiel
- **URL du dossier de contenu de l’étape 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
   - `{YOUR_FOLDER_ID}` est l’identifiant du dossier que vous avez créé avec les données d’exemple de contenu.

#### Lier le référentiel à l’environnement de création de documents

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

1. Mettez à jour le point de montage dans le fichier de configuration du storefront pour pointer vers votre URL de contenu.

   1. Ouvrez le fichier de configuration [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=fr#vocabulary).

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

   - Remplacez la chaîne `{ORG}` par l’organisation ou le nom d’utilisateur de votre référentiel.

   - Remplacez la chaîne `{SITE}` par le nom du référentiel.

   +++Exemple de fichier de configuration mis à jour

   Si votre référentiel GitHub est nommé `aco-storefront` et que votre organisation est `early-adopter`, l’URL mise à jour doit se présenter comme suit :

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
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```
