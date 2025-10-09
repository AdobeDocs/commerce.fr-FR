---
title: Outils de codage pour les extensions
description: Découvrez comment utiliser les outils d’IA pour créer des extensions Commerce App Builder.
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Architect
hide: true
hidefromtoc: true
source-git-commit: 6d2debaeefd65d273c1e0e92f9a7b03740b11520
workflow-type: tm+mt
source-wordcount: '1422'
ht-degree: 0%

---

# Outils de codage pour les extensions

Lors de la migration vers [!DNL Adobe Commerce as a Cloud Service], vous pouvez utiliser les outils de codage de l’IA pour convertir les extensions existantes [!DNL Adobe Commerce] PHP en extensions [!DNL Adobe Developer App Builder]. Il peut également être utilisé pour créer de nouvelles extensions [!DNL App Builder].

L’utilisation des outils de codage de l’IA offre les avantages suivants :

* **Workflow de développement amélioré** : outils de développement Adobe Commerce intégrés.
* **Assistance optimisée par l’IA** : génération et débogage de code contextuel.
* **Fonctionnalités spécifiques à Commerce** : outils spécialisés pour le développement d’Adobe Commerce App Builder.
* **Workflows automatisés** : processus de développement et de déploiement rationalisés.

## Conditions préalables

* [Curseur](https://cursor.com/download)
* [Node.js](https://nodejs.org/en/download) : version LTS
* Gestionnaire de packages : [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) ou [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git) : pour le clonage du référentiel et le contrôle de version

## Installation

1. Installez globalement la dernière [ligne de commande Adobe I/O](https://github.com/adobe/aio-cli) :

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Installez le plug-in Adobe I/O CLI Commerce [&#128279;](https://github.com/adobe-commerce/aio-cli-plugin-commerce) :

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
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

Le processus d’installation vous invite à définir les options de configuration. Pour l’emplacement de configuration, choisissez « Répertoire actuel » pour installer les outils dans votre espace de travail actuel :

```terminal
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

Lors de la sélection du gestionnaire de packages, Adobe recommande d’utiliser `npm` par souci de cohérence :

```terminal
? Which package manager would you like to use?
❯ npm
  yarn
```

1. Une fois les outils de codage installés, le processus d’installation configure :

   * Intégration du serveur MCP pour le développement d’Adobe Commerce
   * Règles de l’IDE du curseur pour une expérience de développement améliorée
   * Outils et workflows de développement spécifiques à Commerce

   Les fichiers suivants sont ajoutés à votre espace de travail :

   * Configuration MCP : `.cursor/mcp.json`
   * Répertoire des règles : `.cursor/rules/`

## Configuration post-installation

1. Redémarrez l’IDE Cursor pour charger les nouveaux outils et la nouvelle configuration MCP.

1. Vérifiez l’installation en vous assurant que les règles sont bien présentes dans le dossier `.cursor/rules/` .

1. Activez le serveur MCP :

   * Ouvrez les paramètres MCP du curseur à l’aide des commandes **Cmd+Maj+P** (macOS) ou **Ctrl+Maj+P** (Windows et Linux).
   * Type **Affichage : ouvrir les paramètres MCP**
   * Localisez **serveur MCP d’extensibilité de commerce** dans la liste
   * Activez/désactivez le serveur **ON** pour activer les outils de codage

1. Vérifiez l’état du serveur : le serveur MCP d’extensibilité de Commerce doit apparaître comme suit :

   ```terminal
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

## Exemple d’invite

L’exemple d’invite suivant crée une extension pour envoyer des notifications lorsqu’une commande est passée.

```terminal
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
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

```terminal
Create a detailed implementation plan for this complex development.
```

Les extensions Adobe Commerce complexes impliquent souvent :

* Plusieurs actions d’exécution
* Configuration d’événement sur plusieurs points de contact
* Intégration avec des systèmes externes
* Exigences de gestion des états
* Test sur plusieurs composants

### Utilisation des outils MCP

L’outil est défini par défaut sur les outils MCP, mais dans certains cas, il peut utiliser des commandes d’interface de ligne de commande à la place. Si vous souhaitez garantir l’utilisation de l’outil MCP, demandez-le explicitement à l’invite.

Si des commandes d’interface de ligne de commande sont utilisées et que vous souhaitez utiliser des outils MCP à la place, utilisez l’invite suivante :

```terminal
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

Il est important de remettre en question la complexité inutile créée par les outils de l’IA.

Lorsque des fichiers inutiles sont ajoutés (`validator.js`, `transformer.js`, `sender.js`) pour des points d’entrée en lecture seule simples, utilisez les invites suivantes :

```terminal
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

```terminal
Help me test the customer-created runtime action running locally
```

**Échecs de débogage** :

```terminal
Why did the subscription-updated runtime action activation fail?
```

**Vérifier les journaux** :

```terminal
Help me check the logs for the last stock-monitoring runtime action invocation
```

**Création de payloads de test** :

```terminal
Generate test data for this Commerce event
```

```terminal
Create a test payload for the customer_save_after event
```

**Rechercher des points d’entrée d’exécution** :

```terminal
What's the URL for this deployed action?
```

**Gérer l’authentification** :

```terminal
How do I authenticate with this external API?
```

**Résolution des problèmes** :

```terminal
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

Déployez uniquement les actions modifiées pour accélérer le développement. Cela réduit le risque de rompre les fonctionnalités existantes et permet de réagir plus rapidement aux modifications. Cela réduit également le risque de rompre les fonctionnalités existantes.

* Utilisation des outils MCP pour déployer des actions spécifiques

  ```bash
  aio-app-deploy --actions action-name
  ```

* Déployer des actions individuelles après un test local
* Déployer de manière incrémentielle et éviter les déploiements d’applications complets pendant le développement

#### Nettoyage de l’exécution

Après des modifications majeures, utilisez les outils pour nettoyer les actions orphelines. Laissez l’outil d’IA gérer le processus de nettoyage de manière systématique, il peut identifier efficacement les actions orphelines, vérifier leur statut et les supprimer en toute sécurité sans intervention manuelle.

```terminal
Help me identify and clean up orphaned runtime actions
```

Demandez à l’outil IA de répertorier les actions déployées et d’identifier celles qui ne sont pas utilisées

```terminal
List all deployed actions and identify which ones are no longer needed
```

Demandez aux outils d’IA de supprimer les actions orphelines à l’aide des commandes appropriées

```terminal
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

Vous devez éviter les antimodèles suivants lors de l’utilisation des outils de codage de l’IA :

* **Ne pas ignorer la phase de clarification** - Assurez-vous toujours que la phase 1 est terminée avant la mise en œuvre.
* **Ne pas ignorer le test après chaque fonctionnalité** - Effectuez un test incrémentiel, n’attendez pas que tout soit terminé.
* **N’ajoutez pas de complexité sans analyse des causes profondes** - Mettez en question les ajouts de fichiers inutiles et demandez une enquête appropriée.
* **Ne déclarez pas votre succès sans tests de données réels** - Testez toujours avec des données réelles, et pas seulement dans des cas particuliers.
* **N’oubliez pas le nettoyage d’exécution** - Nettoyez toujours les actions orphelines après des modifications majeures.
