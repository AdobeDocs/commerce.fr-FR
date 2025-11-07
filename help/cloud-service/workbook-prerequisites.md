---
title: Conditions préalables de l’atelier ADL Commerce
description: Découvrez les conditions préalables requises pour l’atelier d’extension des évaluations.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba4d096bcb99420c029d0b0674fc00f1f1445cea
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Developers Live - Conditions préalables de l’atelier Adobe Commerce

Cette page répertorie les conditions préalables et les autres étapes de configuration manuelle pour l’atelier d’extension [ratings](./workbook.md). Le Lab contient également un script qui automatise la plupart de ces étapes.

## Conditions préalables à l’extension

Avant de commencer, remplissez les conditions préalables suivantes :

* Installation du [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Installation du plug-in Commerce

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* Téléchargez un IDE assisté par l’IA, tel que [Cursor](https://cursor.com/download) (recommandé). D’autres IDE, tels que Claude Code, Gemini CLI ou Copilot, sont également pris en charge, mais peuvent nécessiter des modifications des invites et d’autres étapes de ce tutoriel.
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### Configuration de l’interface de ligne de commande AIO

1. Effacez la configuration existante :

   ```bash
   aio config clear
   ```

   Connectez-vous à l’aide de l’interface de ligne de commande AIO :

   ```bash
   aio auth login -f
   ```

1. Sélectionnez votre organisation, votre projet et votre espace de travail à l’aide de chacune des commandes suivantes :

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![configuration de l’interface de ligne de commande](./assets/cli-configuration.png){width="600" zoomable="yes"}

### Cloner le kit de démarrage de l’intégration

Clonez le référentiel du kit de démarrage de l’intégration Commerce et préparez votre projet :

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Cloner le kit de démarrage](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Créez le fichier .env

Créez votre fichier de configuration d’environnement :

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

### Télécharger la configuration de l’espace de travail

Exécutez la commande suivante pour télécharger le fichier de configuration de l’espace de travail :

```bash
aio console workspace download workspace.json
```

### Connecter l’espace de travail local à l’espace de travail distant

Liez votre projet local à l’espace de travail distant :

```bash
aio app use workspace.json -m
```

![Se connecter à l’espace de travail](./assets/connect-workspace.png){width="600" zoomable="yes"}

## Conditions préalables requises pour Storefront

Les éléments suivants sont requis pour terminer la section [storefront](#connect-to-the-storefront) de ce tutoriel et afficher les évaluations de produit dans votre boutique.
<!-- 
* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### Obtenir les fichiers du projet

Vous pouvez obtenir les fichiers de projet de l’une des deux façons suivantes :

<!-- 
#### Option A: Clone the repository (recommended) -->

Si vous avez [!DNL Git] installé, ouvrez votre terminal et clonez le référentiel :

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### Installation des dépendances racine

Installez les dépendances principales du projet :

```bash
npm install
```

Cette opération installe tous les packages nécessaires pour l’application storefront.

### Installation des dépendances du serveur MCP

Accédez au répertoire du serveur MCP et installez ses dépendances :

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```

>[!NOTE]
>
>The actual value for `WORKER_RAG_URL` will be provided by the lab facilitator at the start of the session. -->

### Activer MCP dans le curseur

Le serveur MCP (Model Context Protocol) permet aux agents d’IA d’accéder à [!DNL Adobe Commerce] documentation de Storefront.

#### Ouvrir les paramètres MCP du curseur

![Ouvrir les paramètres MCP du curseur](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Ouvrir le [!DNL Cursor]
1. Accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**

#### Activation et configuration des fonctionnalités MCP

Le projet comprend un fichier de configuration MCP à l’adresse `.cursor/mcp.json`. Ce fichier doit déjà être configuré pour utiliser le serveur MCP local.

Vérifiez la configuration MCP :

1. Assurez-vous que le serveur « commerce-documentation-rag » est répertorié et activé

La configuration doit ressembler à ceci :

![Configuration MCP](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>Le script `start-mcp.sh` charge automatiquement les variables d’environnement à partir de votre fichier `.env` dans le répertoire `mcp-server` .

#### Redémarrer le curseur

Après avoir activé MCP et configuré le serveur :

1. Quitter [!DNL Cursor] complètement
1. Rouvrez [!DNL Cursor] et ouvrez le projet `aem-boilerplate-commerce`

#### Vérifier la connexion MCP

Vérifiez que le serveur MCP fonctionne correctement :

1. Ouvrir une nouvelle conversation dans [!DNL Cursor]
1. Recherchez un indicateur indiquant que le serveur MCP est connecté (généralement dans l’interface de conversation)
1. Posez une question du type : « Recherchez des informations sur les emplacements dans la documentation du storefront ».

Si le serveur MCP fonctionne, vous devriez voir les résultats pertinents de la documentation.

![Connexion MCP vérifiée](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}

### Démarrer le serveur de développement

Démarrez le serveur de développement local :

```bash
npm run start
```

Le serveur de développement démarrera à `http://localhost:3000`.

Accédez à la page des vêtements à l’adresse `http://localhost:3000/apparel`.

![Serveur de développement en cours d’exécution](./assets/development-server-running.png){width="600" zoomable="yes"}
