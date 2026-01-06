---
title: Outils de codage de l’IA pour les extensions
description: Découvrez comment utiliser les outils d’IA pour créer des extensions Commerce App Builder.
feature: App Builder, Cloud
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
level: Intermediate
hide: true
hidefromtoc: true
source-git-commit: 991a8683b9a333d2699f1ef22f3dc54d7b401573
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 0%

---

# Outils de codage de l’IA pour les extensions

Lors de la migration vers [!DNL Adobe Commerce as a Cloud Service], vous pouvez utiliser les outils de codage de l’IA pour convertir les extensions existantes [!DNL Adobe Commerce] PHP en extensions [!DNL Adobe Developer App Builder]. Vous pouvez également utiliser ces outils pour créer de nouvelles extensions [!DNL App Builder].

Les outils de codage de l’IA offrent les avantages suivants :

* **Workflow de développement amélioré** : outils de développement Adobe Commerce intégrés.
* **Assistance optimisée par l’IA** : génération et débogage de code contextuel.
* **Fonctionnalités spécifiques à Commerce** : outils spécialisés pour le développement d’Adobe Commerce App Builder.
* **Workflows automatisés** : processus de développement et de déploiement rationalisés.

## Conditions préalables

* Un des agents de codage suivants :
   * [Cursor](https://cursor.com/download) (recommandé)
   * [&#x200B; Copilote Github &#x200B;](https://github.com/features/copilot)
   * [Google Gemini CLI](https://github.com/google-gemini/gemini-cli)
   * [Code Claude](https://www.claude.com/product/claude-code)
* [Node.js](https://nodejs.org/en/download) : version LTS
* Gestionnaire de packages : [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) ou [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git) : pour le clonage du référentiel et le contrôle de version

## Installation

>[!NOTE]
>
>Si vous souhaitez uniquement installer le service Documentation RAG et non le package complet des outils de codage d’IA, voir [Service Documentation RAG](./doc-rag.md).

1. Installez globalement la dernière [ligne de commande Adobe I/O](https://github.com/adobe/aio-cli) :

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Installez les modules externes suivants :

   * [Commerce de l’interface de ligne de commande Adobe I/O](https://github.com/adobe-commerce/aio-cli-plugin-commerce)
   * [Exécution de l’interface de ligne de commande Adobe I/O](https://github.com/adobe/aio-cli-plugin-runtime)
   * [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev)

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
   ```

1. Clonez le Commerce [kit de démarrage de l’intégration](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration) :

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. Accédez au répertoire du kit de démarrage :

   ```bash
   cd commerce-integration-starter-kit
   ```

1. Installez les outils d’extensibilité de l’IA Commerce en exécutant la commande de configuration interactive :

   ```bash
   aio commerce extensibility tools-setup
   ```

Le processus de configuration vous invite à spécifier les options de configuration. Pour l’emplacement de configuration, choisissez « Répertoire actuel » pour installer les outils dans votre espace de travail actuel :

```shell-session
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

Lors de la sélection de l’agent de codage, Adobe recommande de sélectionner `Cursor` pour une expérience de développement optimale :

```shell-session
? Which coding agent would you like to use?
❯ Cursor
  Copilot
  Gemini CLI
  Claude Code
```

Lors de la sélection du gestionnaire de packages, Adobe recommande d’utiliser `npm` par souci de cohérence :

```shell-session
? Which package manager would you like to use?
❯ npm
  yarn
```

1. Une fois les outils de codage installés, le processus d’installation configure :

   * Intégration du serveur MCP pour le développement d’Adobe Commerce
   * Règles de l’IDE du curseur pour une expérience de développement améliorée
   * Outils et workflows de développement spécifiques à Commerce

   Les fichiers suivants sont ajoutés à votre espace de travail :

   **Curseur**

   * Configuration MCP : `.cursor/mcp.json`
   * Répertoire des règles : `.cursor/rules/`

   **Copilote**

   * Configuration MCP : `.vscode/mcp.json`
   * Répertoire des règles : `.github/copilot-instructions.md`

>[!NOTE]
>
>Avant de déployer votre projet, vous devez effectuer les tâches de configuration suivantes :
>
>* Connectez-vous à [Adobe Developer Console](https://developer.adobe.com/console) à l’aide de l’interface de ligne de commande Adobe I/O.
>* Créez un projet App Builder (voir [&#x200B; Configuration du projet &#x200B;](https://developer.adobe.com/commerce/extensibility/events/project-setup)).
>* Configurez les variables d’environnement dans un fichier `.env`.
>
>Vous pouvez effectuer ces étapes de configuration manuellement ou utiliser les outils de codage de l’IA pour vous guider tout au long du processus. Voir [Création d’une intégration](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/) pour obtenir des instructions de configuration détaillées.

## Configuration post-installation

### Connexion à l’interface de ligne de commande d’Adobe I/O

Après avoir installé le [!DNL Adobe I/O CLI], vous devez vous connecter à chaque fois que vous souhaitez utiliser le serveur MCP.

```bash
aio auth login
```

Pour vérifier que vous êtes connecté, exécutez la commande suivante :

```bash
aio where
```

Si vous rencontrez des problèmes, essayez de vous déconnecter puis de vous reconnecter :

```bash
aio auth logout
aio auth login
```

>[!NOTE]
>
>Certaines fonctionnalités du serveur MCP fonctionnent sans connexion, mais le service RAG (Retrieval-Augmentated Generation) ne fonctionne pas. Le service RAG fournit à l’agent de codage de l’IA un accès en temps réel à l’ensemble de la documentation d’Adobe Commerce, ce qui lui permet de répondre aux questions et de générer du code en fonction des pratiques de développement, des API et des modèles architecturaux Commerce actuels.
>
>Pour installer le service RAG indépendamment, voir [Documentation du service RAG](./doc-rag.md).

### Curseur

1. Redémarrez l’IDE Cursor pour charger les nouveaux outils et la nouvelle configuration MCP.

1. Vérifiez l’installation en vous assurant que les règles sont bien présentes dans le dossier `.cursor/rules/` .

1. Activez le serveur MCP :

   * Ouvrez les paramètres MCP du curseur à l’aide des commandes **Cmd+Maj+P** (macOS) ou **Ctrl+Maj+P** (Windows et Linux).
   * Type **Affichage : ouvrir les paramètres MCP**
   * Localisez **serveur MCP d’extensibilité de commerce** dans la liste
   * Activez/désactivez le serveur **ON** pour activer les outils de codage

1. Vérifiez l’état du serveur : le serveur MCP d’extensibilité de Commerce doit apparaître comme suit :

   ```shell-session
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

1. Utilisez l’invite suivante pour voir si l’agent utilise le serveur MCP. Si ce n’est pas le cas, demandez explicitement à l’agent d’utiliser les outils MCP disponibles.

```shell-session
What are the differences between Adobe Commerce PaaS and Adobe Commerce as a Cloud Service when configuring a webhook that activates an App Builder runtime action?
```

### Copilote

1. Redémarrez Visual Studio Code pour charger les nouveaux outils et la nouvelle configuration MCP.

1. Vérifiez l’installation en vous assurant que le fichier `copilot-instructions.md` existe dans le dossier `.github`.

1. Activez le serveur MCP :

   * Ouvrez le panneau Extensions en cliquant sur l’icône **Extensions** dans la barre d’activités située sur la barre latérale gauche, ou à l’aide des combinaisons **Cmd+Maj+X** (macOs) ou **Ctrl+Maj+X** (Windows et Linux).
   * Cliquez sur [!UICONTROL **SERVEURS MCP - INSTALLÉS**].
   * Cliquez sur l’icône d’engrenage en regard de [!UICONTROL **Serveur MCP d’extensibilité de commerce**] et sélectionnez [!UICONTROL **Démarrer le serveur**], si le serveur est arrêté.
   * Cliquez à nouveau sur l’icône d’engrenage, puis sélectionnez [!UICONTROL **Afficher la sortie**].

1. Vérifiez l’état du serveur. La sortie `MCP:commerce-extensibility` doit correspondre aux éléments suivants :

   ```shell-session
   2025-11-13 12:58:50.652 [info] Starting server commerce-extensibility
   2025-11-13 12:58:50.652 [info] Connection state: Starting
   2025-11-13 12:58:50.652 [info] Starting server from LocalProcess extension host
   2025-11-13 12:58:50.657 [info] Connection state: Starting
   2025-11-13 12:58:50.657 [info] Connection state: Running
   
   (...)
   
   2025-11-13 12:58:50.753 [info] Discovered 10 tools
   ```

1. Utilisez l’invite suivante pour voir si l’agent utilise le serveur MCP. Si ce n’est pas le cas, demandez explicitement à l’agent d’utiliser les outils MCP disponibles.

   ```shell-session
   What are the differences between Adobe Commerce PaaS and SaaS when configuring a webhook that activates an App Builder runtime action?
   ```

## Exemple d’invite

L’exemple d’invite suivant crée une extension pour envoyer des notifications lorsqu’une commande est passée.

```shell-session
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## Commandes d’invite

Outre l’invite, vous pouvez utiliser la commande `/search-commerce-docs` pour rechercher de la documentation dans les conversations avec votre agent. Par exemple :

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Bonnes pratiques

Adobe recommande de suivre les bonnes pratiques suivantes lors de l’utilisation des outils de codage de l’IA :

### Checklist

Avant de commencer une session de développement :

* Vérifier les `REQUIREMENTS.md`
* Vérification du fonctionnement des outils MCP
* Examiner la phase et les objectifs actuels
* Commencez par l’exemple de code ou les projets structurés

Pendant le développement :

* Approuvez le [protocole](#protocol) en quatre phases
* Demander des plans de mise en œuvre pour un développement complexe
* Utilisation des outils MCP, le cas échéant
* Tester chaque fonctionnalité après l’implémentation
* Testez d’abord localement, puis déployez et testez à nouveau
* Utilisation des outils de codage pour la prise en charge des tests
* Remettre en question une complexité inutile
* Déploiement incrémentiel pour un développement plus rapide

Lors du démarrage d’une nouvelle conversation :

* Fournir une remise de session appropriée
* Fichiers de clé de référence avec `@`
* Fixer des objectifs clairs pour la session
* Utiliser des limites basées sur les phases

### Workflow

Lors du développement avec les outils de codage de l’IA, commencez par utiliser un exemple de code ou des projets structurés. Cette approche vous assure de construire sur une base solide plutôt que de partir de rien, tout en optimisant votre workflow de développement d’IA.

Cela vous permet également d’exploiter les modèles Adobe et de tirer parti de modèles et d’architectures éprouvés, tout en conservant les structures et conventions de répertoires établies.

Consultez les ressources suivantes pour commencer :

* [Kit de démarrage d’intégration](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [Modèles de kit de démarrage Adobe Commerce](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Modèles de démarrage Adobe I/O Events](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [Exemples d’applications App Builder](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### Pourquoi utiliser ces ressources ?

* **Modèles éprouvés** : les kits de démarrage incarnent les bonnes pratiques et les décisions architecturales d’Adobe
* **Développement plus rapide** : réduit le temps consacré à la conception standard et à la configuration
* **Cohérence** : s’assure que votre extension respecte les conventions établies
* **Maintenabilité** : facilité de maintenance et de mise à jour selon les schémas standard
* **Documentation** : les kits de démarrage sont fournis avec des exemples et de la documentation
* **Soutien de la communauté** : aide plus facile à obtenir lorsque vous utilisez des approches standard
* **Efficacité du contexte de l’IA** : utilisez des modèles et des structures familiers, ce qui réduit le besoin d’explications détaillées et améliore la précision de la génération du code
* **Utilisation réduite des jetons** : référencez les modèles existants au lieu de tout générer de A à Z, ce qui entraîne des conversations plus efficaces et moins de résumés de contexte

### Protocole

Le protocole en quatre phases suivant est automatiquement appliqué par le système de règles. Les outils doivent suivre automatiquement ce protocole lors du développement d’extensions :

* Phase 1 : analyse et clarification des exigences
   * Lorsqu’on vous pose des questions pour clarifier les choses, donnez des réponses complètes.
* Phase 2 : planification architecturale et approbation des utilisateurs
   * Lorsqu’un plan est présenté, examinez-le attentivement avant de l’approuver.
* Phase 3 : génération et mise en œuvre du code
* Phase 4 : documentation et validation

### Demander des plans de mise en œuvre pour un développement complexe

Pour un développement complexe impliquant plusieurs actions d’exécution, points de contact ou intégrations, demandez explicitement aux outils d’IA de créer un plan de mise en œuvre détaillé. Lorsque vous voyez un plan général en [Phase 2](#protocol) qui implique plusieurs composants, demandez un plan d’implémentation détaillé pour le diviser en tâches gérables :

```shell-session
Create a detailed implementation plan for this complex development.
```

Les extensions Adobe Commerce complexes impliquent souvent :

* Plusieurs actions d’exécution
* Configuration d’événement sur plusieurs points de contact
* Intégration avec des systèmes externes
* Exigences de gestion des états
* Test sur plusieurs composants

### Utilisation des outils MCP

>[!NOTE]
>
>Avant d’utiliser les outils MCP, vérifiez que vous êtes [connecté à l’interface de ligne de commande Adobe I/O](#log-in-to-the-adobe-io-cli).

L’outil est défini par défaut sur les outils MCP, mais dans certains cas, il peut utiliser des commandes d’interface de ligne de commande à la place. Pour garantir l’utilisation de l’outil MCP, demandez-le explicitement à l’invite.

Si des commandes d’interface de ligne de commande sont utilisées et que vous souhaitez utiliser des outils MCP à la place, utilisez l’invite suivante :

```shell-session
Use only MCP tools and not CLI commands
```

* Outils MCP : aio-app-deploy, aio-app-dev, aio-dev-invoke
* Commandes de l’interface de ligne de commande : déploiement d’application aio, développement d’application aio

Les commandes de l’interface de ligne de commande peuvent être utilisées dans les scénarios suivants :

* Scénarios de déploiement complexes
* Débogage de problèmes spécifiques
* Lorsque les outils de MCP présentent des limites
* Opérations ponctuelles qui ne bénéficient pas de l’intégration MCP

### Développement

Remettez en question la complexité inutile créée par les outils d’IA.

Lorsque des fichiers inutiles sont ajoutés (`validator.js`, `transformer.js`, `sender.js`) pour des points d’entrée en lecture seule simples, utilisez les invites suivantes :

```shell-session
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### Test

Appliquez les bonnes pratiques suivantes lors du test :

#### Tester chaque fonctionnalité après l’implémentation

Une fois le développement d’une fonctionnalité de votre plan d’implémentation terminé, testez-la immédiatement. Les tests précoces évitent les problèmes complexes et facilitent le débogage.

* N’attendez pas que toutes les fonctionnalités soient terminées
* Test incrémentiel pour détecter les problèmes dès le début
* Valider la fonctionnalité avant de passer à la fonctionnalité suivante

#### Tester localement en premier

Effectuez toujours d’abord un test local à l’aide de l’outil `aio-app-dev`. Vous obtenez ainsi un retour d’informations immédiat et pouvez accélérer les cycles d’itération, faciliter le débogage et supprimer les frais de déploiement.

1. Démarrez le serveur de développement local :

   ```bash
   aio-app-dev
   ```

1. Tester les actions localement :

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### Déployer et tester à nouveau

Une fois le test local réussi, déployez et testez-le dans l’environnement d’exécution. Les environnements d’exécution peuvent avoir un comportement différent de celui du développement local.

1. Déployer au moment de l’exécution :

   ```bash
   aio-app-deploy
   ```

1. Test des actions déployées

1. Utiliser un navigateur web ou des requêtes HTTP directes

1. Vérifier les journaux d’activation pour le débogage

#### Utilisation des outils de codage pour la prise en charge des tests

Demandez de l’aide pour les tests. Les outils peuvent vous aider à déboguer, à analyser les journaux et à créer des données de test appropriées pour vos actions d’exécution spécifiques.

**Tester les actions d’exécution** :

```shell-session
Help me test the customer-created runtime action running locally
```

**Échecs de débogage** :

```shell-session
Why did the subscription-updated runtime action activation fail?
```

**Vérifier les journaux** :

```shell-session
Help me check the logs for the last stock-monitoring runtime action invocation
```

**Création de payloads de test** :

```shell-session
Generate test data for this Commerce event
```

```shell-session
Create a test payload for the customer_save_after event
```

**Rechercher des points d’entrée d’exécution** :

```shell-session
What's the URL for this deployed action?
```

**Gérer l’authentification** :

```shell-session
How do I authenticate with this external API?
```

**Résolution des problèmes** :

```shell-session
Help me debug why this action is returning 500 errors
```

### Débogage

Arrêtez-vous et évaluez quand les choses tournent mal. Si vous rencontrez des problèmes :

* Arrêter et évaluer - Ne pas continuer dans un état rompu
* Vérifier les journaux : utilisez les journaux d’activation pour identifier les problèmes.
* Simplifier - Supprimer la complexité pour isoler les problèmes
* Test incrémentiel - Correction d’un problème à la fois
* Valider - Tester chaque correctif avant de continuer

### Déploiement

Appliquez les bonnes pratiques suivantes lors du déploiement d’ :

#### Déploiement incrémentiel

Déployez uniquement les actions modifiées pour accélérer le développement. Cette approche réduit le risque de rompre les fonctionnalités existantes et fournit des commentaires plus rapides sur les modifications.

* Utilisation des outils MCP pour déployer des actions spécifiques

  ```bash
  aio-app-deploy --actions action-name
  ```

* Déployer des actions individuelles après un test local
* Déployer de manière incrémentielle et éviter les déploiements d’applications complets pendant le développement

#### Nettoyage de l’exécution

Après des modifications majeures, utilisez les outils pour nettoyer les actions orphelines. Laissez l’outil d’IA gérer le processus de nettoyage de manière systématique. Il peut identifier efficacement les actions orphelines, vérifier leur statut et les supprimer en toute sécurité sans intervention manuelle.

```shell-session
Help me identify and clean up orphaned runtime actions
```

Demandez à l’outil IA de répertorier les actions déployées et d’identifier celles qui ne sont pas utilisées

```shell-session
List all deployed actions and identify which ones are no longer needed
```

Demandez aux outils d’IA de supprimer les actions orphelines à l’aide des commandes appropriées

```shell-session
Remove the orphaned actions that are no longer part of the current implementation
```

### Surveillance

Appliquez les bonnes pratiques suivantes lors de la surveillance de votre application :

#### Surveiller les indicateurs de qualité du contexte

* **Bon contexte** : l’IA se souvient des décisions récentes, référence les fichiers corrects
* **Mauvais contexte** : l’IA demande des informations fournies précédemment et répète les problèmes résolus

#### Suivre la vitesse de développement

* **Vitesse élevée** : progression claire, clarification minimale nécessaire
* **Faible vitesse** : explications répétées, confusion de l’IA, progression lente

#### Surveillance de la rentabilité

Suivre les modèles d’utilisation des jetons :

* **Efficace** : faible utilisation des jetons, peu de résumés du contexte
* **Inefficace** : utilisation élevée des jetons, synthèses multiples, travail répété

## Éléments à éviter

Évitez les antimodèles suivants lors de l’utilisation des outils de codage de l’IA :

* **Ne pas ignorer la phase de clarification** - Assurez-vous toujours que la phase 1 est terminée avant la mise en œuvre.
* **Ne pas ignorer le test après chaque fonctionnalité** - Effectuez un test incrémentiel, n’attendez pas que tout soit terminé.
* **N’ajoutez pas de complexité sans analyse des causes profondes** - Mettez en question les ajouts de fichiers inutiles et demandez une enquête appropriée.
* **Ne déclarez pas votre succès sans tests de données réels** - Testez toujours avec des données réelles, et pas seulement dans des cas particuliers.
* **N’oubliez pas le nettoyage d’exécution** - Nettoyez toujours les actions orphelines après des modifications majeures.
