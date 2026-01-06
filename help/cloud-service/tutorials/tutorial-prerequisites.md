---
title: Conditions préalables du tutoriel de l’extension d’évaluation
description: Découvrez les conditions préalables requises pour l’atelier d’extension des évaluations.
feature: App Builder, Cloud
role: Developer
level: Intermediate
hide: true
hidefromtoc: true
source-git-commit: 4ca909c2f8f95fbc404ce6a745d769958b2c01f4
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Conditions préalables du tutoriel sur l’extension d’évaluation (Beta)

>[!NOTE]
>
>L’outil d’IA utilisé dans ce tutoriel est actuellement dans Beta et peut inclure des bogues ou d’autres problèmes.

Cette page répertorie les conditions préalables et les étapes de configuration pour les tutoriels [!DNL Adobe Commerce as a Cloud Service], tels que le tutoriel [évaluation des extensions](./ratings-extension.md).

## Conditions préalables d’Adobe Commerce as a Cloud Service

* Installation du [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Installez les plug-ins [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce), [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime) et [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev) :

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

* Téléchargez un IDE assisté par l’IA, tel que [Cursor](https://cursor.com/download) (recommandé). D’autres IDE, tels que Claude Code, Gemini CLI ou Copilot, sont également pris en charge, mais peuvent nécessiter des modifications des invites et d’autres étapes du tutoriel.

### Conditions préalables requises pour Adobe Developer Console

1. Accédez à [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Connectez-vous à l’aide de votre adresse e-mail et de votre mot de passe.

#### Créer un projet

1. Accédez à [Adobe Developer Console](https://developer.adobe.com/).
1. Cliquez sur [!UICONTROL **Créer un projet à partir d’un modèle**].
1. Sélectionnez le modèle [!UICONTROL **App Builder**].
1. Saisissez un [!UICONTROL **Titre du projet**] et un [!UICONTROL **Nom de l’application**].
1. Assurez-vous que la case **[!UICONTROL Include Runtime]** est cochée.

   ![Création de projet Adobe Developer Console avec le modèle App Builder sélectionné](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Cliquez sur [!UICONTROL **Enregistrer**].

#### Ajouter des API à l’espace de travail

1. Cliquez sur l’espace de travail [!UICONTROL **Stage**], puis répétez les étapes suivantes pour chaque API.

   ![Espace de travail d’évaluation avec l’option Ajouter un service pour les API](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Cliquez sur [!UICONTROL **Ajouter un service**] et sélectionnez [!UICONTROL **API**].

1. Sélectionnez l’une des API suivantes. Vous devrez répéter ce processus pour chaque API répertoriée ci-dessous :

   * [!UICONTROL **Adobe Services**] filtrez :
      * [!UICONTROL **API I/O Management**]
      * [!UICONTROL **Événements I/O**] API
   * Filtre [!UICONTROL **Experience Cloud**] :
      * API [!UICONTROL **Adobe I/O Events pour Adobe Commerce**]

1. Cliquez sur [!UICONTROL **Suivant**].

1. Cliquez sur Enregistrer [!UICONTROL **’API configurée**].

1. Répétez les étapes précédentes jusqu’à ce que toutes les API soient ajoutées à l’espace de travail.

   ![Workspace affichant toutes les API requises ajoutées](../assets/apis-added.png){width="600" zoomable="yes"}

### Configuration de l’interface de ligne de commande Adobe I/O

1. Effacez toute configuration existante :

   ```bash
   aio config clear
   ```

   Connectez-vous à l’aide de l’[!DNL Adobe I/O CLI] :

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

   ![Terminal affichant la sélection de projet d’organisation et d’espace de travail de l’interface de ligne de commande Adobe I/O](../assets/cli-configuration.png){width="600" zoomable="yes"}

### Clonage du kit de démarrage de l’intégration

Clonez le référentiel du kit de démarrage de l’intégration Commerce et préparez votre projet :

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Sortie de terminal affichant la commande de clone Git pour le kit de démarrage de l’intégration Commerce](../assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Créer un fichier .env

Créez votre fichier de configuration d’environnement :

```bash
cp env.dist .env
```

Ouvrez le fichier `.env` dans un éditeur de texte et ajoutez les informations d’identification OAuth suivantes :

```shell-session
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

Vous pouvez copier ces valeurs à partir de la page **[!UICONTROL Credential details]** dans [Developer Console](https://developer.adobe.com/) en cliquant sur l&#39;onglet **[!UICONTROL OAuth Server-to-Server]** dans votre espace de travail.

![Page d’identification de serveur à serveur OAuth dans Adobe Developer Console](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Ajout de la configuration Commerce

Ajoutez les détails d’instance Commerce suivants à votre fichier `.env` :

```shell-session
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

Pour rechercher ces valeurs :

1. Accédez à [Instances de service Commerce Cloud](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Cliquez sur l’icône d’informations en regard de votre instance.
1. Copiez le point d’entrée REST en tant que `COMMERCE_BASE_URL`.
1. Copiez le point d’entrée GraphQL en tant que `COMMERCE_GRAPHQL_ENDPOINT`.

#### Définir le préfixe d’événement

Définissez une valeur temporaire pour le préfixe d’événement :

```shell-session
EVENT_PREFIX=test
```

### Télécharger la configuration de l’espace de travail

Exécutez la commande suivante pour télécharger le fichier de configuration de l’espace de travail :

```bash
aio console workspace download workspace.json
```

Copiez le fichier de configuration de l’espace de travail dans le répertoire `scripts` :

```bash
cp workspace.json scripts/
```

### Connecter l’espace de travail local à l’espace de travail distant

Liez votre projet local à l’espace de travail distant :

```bash
aio app use workspace.json -m
```

![Terminal affichant une connexion réussie à l’espace de travail avec la commande d’utilisation de l’application aio](../assets/connect-workspace.png){width="600" zoomable="yes"}

### Installation des outils d’IA dédiés à l’extensibilité

Mettez à jour le fichier de règles de curseur et la configuration MCP pour inclure le package `commerce-extensibility-tools`.

1. Configurez les outils de développement assisté par l’IA dans le dossier `extension` à l’aide des commandes suivantes :

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Terminal affichant la sortie de commande de configuration des outils d’extensibilité de l’IA](../assets/install-ai-tools.png){width="600" zoomable="yes"}
<!--
## Storefront prerequisites

The following items are required to complete the [storefront](./ratings-extension.md#connect-to-the-storefront) section of [this tutorial](./ratings-extension.md) and see the product ratings in your store.

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
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront

### Get the project files

You can obtain the project files using one of the following methods:

#### Option A: Clone the repository (recommended)

If you have [!DNL Git] installed, open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

#### Option B: Download the zip file

If you do not have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ```

### Install root dependencies

Install the main project dependencies:

```bash
npm install
```

This will install all the necessary packages for the storefront application.

### Install MCP server dependencies

Navigate to the MCP server directory and install its dependencies:

```bash
cd mcp-server
npm install
cd ..
```

### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create an `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values:

```env
RAG_MODE=worker
WORKER_RAG_URL=
```

### Enable MCP in Cursor

The Model Context Protocol (MCP) server provides AI agents with access to [!DNL Adobe Commerce] Storefront documentation.

#### Open Cursor MCP settings

![Open Cursor MCP Settings](../assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor].
1. Navigate to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

#### Enable and configure MCP features

The project includes an MCP configuration file at `.cursor/mcp.json`. This file should already be configured to use the local MCP server.

Verify the MCP configuration:

1. Ensure the "commerce-documentation-rag" server is listed and enabled

The configuration should look similar to this:

![MCP Configuration](../assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>The `start-mcp.sh` script will automatically load the environment variables from your `.env` file in the `mcp-server` directory.

#### Restart Cursor

After enabling MCP and configuring the server:

1. Quit [!DNL Cursor] completely.
1. Reopen [!DNL Cursor] and open the `aem-boilerplate-commerce` project.

#### Verify MCP connection

Check that the MCP server is running correctly:

1. Open a new chat in [!DNL Cursor].
1. Look for an indicator showing the MCP server is connected. This indicator is typically located in the chat interface.
1. Try entering a prompt like the following:

   ```shell-session
   Search the storefront docs for information about slots
   ```

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](../assets/mcp-connection-verified.png){width="600" zoomable="yes"}

If this works, you are ready to continue with the [tutorial](./ratings-extension.md).
 -->
