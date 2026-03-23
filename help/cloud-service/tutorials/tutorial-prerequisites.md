---
title: Tutorial Prerequisites
description: Découvrez les conditions préalables et les étapes de configuration pour les tutoriels Adobe Commerce as a Cloud Service, y compris les outils de développement d’extensions et de storefront.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 0ece7b58bdafd664297cbdee809c53ef2389fb12
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 0%

---

# Tutoriels préalables

Cette page répertorie les conditions préalables et les étapes de configuration pour les tutoriels [!DNL Adobe Commerce as a Cloud Service], tels que le tutoriel sur l’extension [ratings](./ratings-extension.md) et le tutoriel sur l’extension de méthode d’expédition [](./shipping-method-extension.md).

## Conditions préalables générales

Les outils suivants sont nécessaires pour le développement de l’extension et du storefront dans ce tutoriel.

* [!DNL Node.js] (version `22.x.x`) et npm (`9.0.0` ou ultérieure) : vérifiez votre installation à l’aide de la commande suivante :

  ```bash
  node --version
  npm --version
  ```

* Installation de [Git](https://git-scm.com) - Vérifiez votre installation :

  ```bash
  git --version
  ```

* Coquille de Bash
   * macOS/Linux : aucune installation requise
   * Windows : utilisez [Git Bash](https://git-scm.com/install) ou [sous-système Windows pour Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* Téléchargez un IDE assisté par l’IA, tel que [Cursor](https://cursor.com/download) (recommandé). D’autres IDE, tels que Claude Code, Gemini CLI ou Copilot, sont également pris en charge, mais peuvent nécessiter d’apporter des modifications aux invites et à d’autres étapes du tutoriel.

## Conditions préalables [!DNL Adobe Commerce as a Cloud Service]

* Installation du [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Installez les plug-ins [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce), [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime) et [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev) :

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
  ```

Après avoir installé le [!DNL Adobe I/O CLI] et les modules externes requis, configurez votre espace de travail d’extensibilité. Adobe recommande d’utiliser la configuration automatisée pour une expérience plus rapide.

* **[Configuration automatisée](#automated-setup) (recommandée)** — Exécutez une seule commande pour configurer automatiquement votre espace de travail.
* **[Configuration manuelle](#manual-setup)** — Suivez les instructions étape par étape pour configurer chaque composant individuellement.

### Configuration automatisée (recommandée) {#automated-setup}

>[!TIP]
>
>Si vous rencontrez des problèmes avec la configuration automatisée, suivez les étapes [configuration manuelle](#manual-setup) ci-dessous.

La commande `app-setup` automatise le processus de configuration de Workspace, notamment la création d’un projet [!DNL Adobe Developer Console], l’ajout des API requises, la configuration du [!DNL Adobe I/O CLI], le clonage du kit de démarrage, la connexion de votre espace de travail local et l’installation des outils d’IA dédiés à l’extensibilité.

La commande `app-setup` vous guide tout au long des étapes suivantes :

* Sélection ou création d’un projet [!DNL Adobe Developer Console] avec les API requises
* Configuration de l’[!DNL Adobe I/O CLI] avec votre organisation, projet et espace de travail
* Clonage du kit de démarrage approprié et configuration du projet
* Configuration de l’environnement et connexion de l’espace de travail local à l’espace de travail distant
* Installation des outils d’extensibilité de Commerce et des compétences en agent de codage

Exécutez la commande suivante et suivez les invites interactives :

```bash
aio commerce extensibility app-setup
```

Une fois la commande terminée, accédez au répertoire de votre projet et redémarrez votre agent de codage pour charger les nouveaux outils et compétences MCP. Si votre tutoriel nécessite un storefront, exécutez à nouveau la commande et sélectionnez le kit de démarrage [!DNL AEM Boilerplate Commerce].

L’exemple d’installation suivant montre les invites interactives et la sortie pour le kit de démarrage de passage en caisse.

+++Exemple d’installation (checkout starter kit)

```shell-session
aio commerce extensibility app-setup

🚀 Adobe Commerce Extensibility App Setup

✔ Logged in
📁 Working directory: /Users/username/projects/my-commerce-project

✔ Which starter kit would you like to use? Checkout Starter Kit
✔ Enter a name for your project directory: my-extension
✔ Which coding agent would you like to install the skills for? Cursor

📦 Cloning Checkout Starter Kit...
   ✔ Repository cloned
   Using npm (package-lock.json found)
   ✔ Dependencies installed

📋 Current Adobe I/O Console configuration:
   Org: My Organization (1234567)
   Project: My Commerce Project (1234567890123456789)
   Workspace: Stage (9876543210987654321)
✔ Do you want to continue with this configuration? (Answer "No" to select a different org/project/workspace)
No

🔧 Selecting Adobe I/O Console org, project, and workspace...

? Select Org: My Organization
Org selected My Organization
You are currently in:
1. Org: My Organization
2. Project: <no project selected>
3. Workspace: <no workspace selected>

? Select Project: My Commerce Project
Project selected : My Commerce Project
You are currently in:
1. Org: My Organization
2. Project: My Commerce Project
3. Workspace: <no workspace selected>

? Select Workspace: Stage
Workspace selected Stage
You are currently in:
1. Org: My Organization
2. Project: My Commerce Project
3. Workspace: Stage

✅ Console configured:
   Org: My Organization
   Project: My Commerce Project
   Workspace: Stage

🔐 Configuring workspace credentials and services...
   ✔ Workspace configuration loaded
   ✔ OAuth server-to-server credentials already configured
   ✔ All required services available in organization
   ✔ Subscribed to: Adobe Commerce as a Cloud Service

📋 Configuring Checkout Starter Kit...
   Creating .env from env.dist...
✔ Select tenant (type to search) My Commerce Instance:
https://<region>.api.commerce.adobe.com/<tenant-id>/graphql
   ✔ Commerce instance configured
✔ Enter the event prefix for your workspace: my-prefix
   ✔ Workspace IDs configured
   ✔ OAuth credentials configured
   ✔ Checkout Starter Kit configured

🔧 Installing Commerce Extensibility tools and agent skills...
   ✔ Commerce Extensibility tools installed

🎉 App setup complete!

📁 Project directory: /Users/username/projects/my-commerce-project/my-extension

Next steps:
   1. cd into your project directory
   2. Restart your coding agent to load the Commerce Extensibility tools and skills
```

+++

### Configuration manuelle {#manual-setup}

Les sections suivantes décrivent comment configurer manuellement chaque composant de votre espace de travail d’extensibilité. Suivez ces étapes si vous préférez une configuration manuelle ou si vous rencontrez des problèmes avec la [configuration automatisée](#automated-setup).

### Conditions préalables requises pour Adobe Developer Console

Configurez un projet dans Adobe Developer Console avec les API et les informations d’identification requises.

1. Accédez à [](https://developer.adobe.com/console){target="_blank"}.
1. Connectez-vous à l’aide de votre adresse e-mail et de votre mot de passe.

#### Créer un projet

Créez un projet App Builder dans le Adobe Developer Console pour héberger votre extension.

1. Accédez à [](https://developer.adobe.com/).
1. Cliquez sur **[!UICONTROL Create project from a template]**.
1. Sélectionnez le modèle de **[!UICONTROL App Builder]**.
1. Saisissez un **[!UICONTROL Project Title]** et un **[!UICONTROL App Name]**.
1. Assurez-vous que la case **[!UICONTROL Include Runtime]** est cochée.

   ![Création de projet Adobe Developer Console avec le modèle App Builder sélectionné](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Cliquez sur **[!UICONTROL Save]**.

#### Ajouter des API à l’espace de travail

Ajoutez les API requises à votre espace de travail d’évaluation pour la gestion des événements et l’intégration de Commerce.

1. Cliquez sur l’espace de travail **[!UICONTROL Stage]** , puis répétez les étapes suivantes pour chaque API.

   ![Espace de travail d’évaluation avec l’option Ajouter un service pour les API](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Cliquez sur **[!UICONTROL Add Service]** et sélectionnez **[!UICONTROL API]**.

1. Sélectionnez l’une des API suivantes. Répétez ce processus pour chaque API répertoriée ci-dessous :

   * **[!UICONTROL Adobe Services]** le filtre :
      * **[!UICONTROL I/O Management API]**
      * API **[!UICONTROL I/O Events]**
   * **[!UICONTROL Experience Cloud]** le filtre :
      * API **[!UICONTROL Adobe I/O Events for Adobe Commerce]**

1. Cliquez sur **[!UICONTROL Next]**.

1. Cliquez sur **[!UICONTROL Save configured API]**.

1. Répétez les étapes précédentes jusqu’à ce que vous ajoutiez toutes les API à l’espace de travail.

   ![Workspace affichant toutes les API requises ajoutées](../assets/apis-added.png){width="600" zoomable="yes"}

### Configuration de l’interface de ligne de commande Adobe I/O

Connectez le [!DNL Adobe I/O CLI] à votre organisation, projet et espace de travail.

1. Effacez toute configuration existante :

   ```bash
   aio config clear
   ```

1. Connectez-vous à l’aide de l’[!DNL Adobe I/O CLI] :

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

### Cloner les kits de démarrage

Clonez l’un des référentiels de kit de démarrage Commerce suivants pour l’extension que vous créez et préparez votre projet :

Kit de démarrage d’intégration :

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

Passage en caisse du kit de démarrage :

```bash
git clone https://github.com/adobe/commerce-checkout-starter-kit.git extension
cd extension
```

>[!BEGINTABS]

>[!TAB Kit de démarrage d’intégration]

### Créer un fichier .env

Créez votre fichier de configuration d’environnement :

```bash
cp env.dist .env
```

Ouvrez le fichier `.env` dans un éditeur de texte et ajoutez les informations d’identification OAuth suivantes :

```bash
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

Copiez ces valeurs de la page **[!UICONTROL Credential details]** dans [Developer Console](https://developer.adobe.com/) en cliquant sur l’onglet **[!UICONTROL OAuth Server-to-Server]** dans votre espace de travail.

![Page d’identification de serveur à serveur OAuth dans Adobe Developer Console](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Ajout de la configuration Commerce

Ajoutez les détails d’instance Commerce suivants à votre fichier `.env` :

```bash
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

Pour rechercher ces valeurs :

1. Accédez à [Instances de service ](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Cliquez sur l’icône d’informations en regard de votre instance.
1. Copiez le point d’entrée REST en tant que `COMMERCE_BASE_URL`.
1. Copiez le point d’entrée GraphQL en tant que `COMMERCE_GRAPHQL_ENDPOINT`.

#### Définir le préfixe d’événement

Définissez une valeur temporaire pour le préfixe d’événement :

```bash
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

>[!TAB Kit de démarrage pour la commande]

### Connecter l’espace de travail local à l’espace de travail distant

Liez votre projet local à l’espace de travail distant. À partir de la racine du projet (le dossier `extension`), exécutez :

```bash
aio app use --merge
```

Lorsque vous y êtes invité, choisissez l’option qui utilise l’organisation, le projet et l’espace de travail que vous avez sélectionnés lors de la configuration de l’interface de ligne de commande Adobe I/O. Cette opération écrit la configuration de l’espace de travail dans votre application afin que le déploiement et le développement local utilisent cet espace de travail.

![Terminal affichant une connexion réussie à l’espace de travail avec la commande d’utilisation de l’application aio](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!ENDTABS]

### Installation des outils d’IA dédiés à l’extensibilité

Ce processus crée la configuration du MCP (`.<agent>/mcp.json`), le répertoire des compétences (`.<agent>/skills/`) et `AGENTS.md` ajoute à la racine du projet. Vous serez invité à choisir un kit de démarrage, un agent de codage et un gestionnaire de packages.


1. Configurez les outils de développement assisté par l’IA dans le dossier `extension` à l’aide des commandes suivantes :

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Terminal affichant la sortie de commande de configuration des outils d’extensibilité de l’IA](../assets/install-ai-tools.png){width="600" zoomable="yes"}

1. Une fois la configuration terminée, redémarrez votre agent de codage pour lui permettre de charger les nouveaux outils et compétences MCP. Les outils Commerce App Builder sont désormais disponibles dans votre environnement.

   >[!NOTE]
   >
   >Si vous voyez un avertissement indiquant qu’aucune compétence n’a été trouvée pour le kit de démarrage, quelque chose s’est mal passé, souvent parce que la configuration a été exécutée dans un dossier autre que celui où le kit de démarrage a été cloné. Exécutez le `aio commerce extensibility tools-setup` à partir du dossier `extension` (racine du projet du kit de démarrage) et sélectionnez le kit de démarrage approprié lorsque vous y êtes invité.

   ![Terminal affichant la configuration des outils d’extensibilité de l’IA avec le kit de démarrage de passage en caisse sélectionné](../assets/tools-setup-checkout.png){width="600" zoomable="yes"}

## Configuration manuelle de Storefront

Cette section décrit comment configurer manuellement votre storefront pour le tutoriel d’extension [Ratings](./ratings-extension.md) et d’autres tutoriels de storefront.

Pour configurer automatiquement votre storefront, exécutez la commande `app-setup` décrite dans la section [Configuration automatisée](#automated-setup) et sélectionnez le kit de démarrage [!DNL AEM Boilerplate Commerce].

### Conditions préalables

Les éléments suivants sont requis pour terminer la section [storefront](./ratings-extension.md#connect-to-the-storefront) du tutoriel de l’extension [Ratings](./ratings-extension.md) et afficher les évaluations de produit dans votre boutique.

* [Google Chrome](https://www.google.com/chrome/) - Requis pour tester le storefront

* Un projet de storefront connecté à votre instance [!DNL Commerce]. Si vous ne disposez pas d’un projet de storefront, suivez les étapes de la section [Créer un storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}, y compris la section [Lier le référentiel aux données commerciales](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#link-repo-to-commerce-data){target="_blank"}.

### Cloner le référentiel storefront

Ouvrez votre terminal et clonez le référentiel :

```bash
git clone https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

### Installation des dépendances

Installez les dépendances du projet :

```bash
npm install
```

### Installation des outils d’IA de storefront

Configurez les outils de développement assistés par l’IA dans le dossier `storefront` .

Exécutez la commande suivante à partir de la racine de votre projet standard. La commande installe le package `@adobe-commerce/commerce-extensibility-tools` en tant que dépendance de développement, copie les fichiers de compétences dans le répertoire des compétences de votre agent et configure MCP (Model Context Protocol) afin que votre agent puisse accéder aux outils de recherche de documentation Commerce.

```bash
aio commerce extensibility tools-setup
```

La commande vous guide à travers deux invites :

1. **Sélectionner un kit de démarrage** — Choisissez **AEM Boilerplate Commerce**.

1. **Sélectionnez votre agent de codage** — Choisissez votre agent dans la liste des agents pris en charge.
