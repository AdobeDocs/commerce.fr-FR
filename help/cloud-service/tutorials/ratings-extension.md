---
title: Tutoriel sur l’extension d’évaluations
description: Découvrez comment créer une extension d’évaluations de produit pour Adobe Commerce as a Cloud Service à l’aide d’App Builder et d’outils de développement assistés par l’IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 33ba97fd6766c9d11baea74170a7119d72e06379
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 0%

---

# Tutoriel sur l’extension d’évaluations

Ce tutoriel vous guide tout au long de la création d’une extension d’évaluations de produit pour [!DNL Adobe Commerce as a Cloud Service] à l’aide d’outils de développement [!DNL Adobe App Builder] et assistés par l’IA.

Avant de commencer, renseignez les [conditions préalables](./tutorial-prerequisites.md).

## Vérifier les conditions préalables

Vérifiez que les prérequis suivants sont installés :

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

Si l’une des commandes précédentes ne renvoie pas les résultats attendus, reportez-vous à la [conditions préalables](./tutorial-prerequisites.md) pour obtenir des conseils.

## Développement d’extension

Cette section vous guide tout au long du développement d’une extension d’évaluations pour Adobe Commerce as a Cloud Service à l’aide d’outils de développement assistés par l’IA.

1. Accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]** et vérifiez que l’ensemble d’outils `commerce-extensibility` est activé sans erreur. Si des erreurs s’affichent, désactivez la palette d’outils et activez-la.

   ![Paramètres de l’IDE du curseur affichant le jeu d’outils d’extensibilité de commerce MCP activé](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Lorsque vous utilisez des outils de développement assistés par l’IA, attendez-vous à des variations naturelles du code et des réponses générées par l’agent.
   >Si vous rencontrez des problèmes avec votre code, vous pouvez toujours demander à l’agent de vous aider à le déboguer.

1. Désactivez toute documentation dans le contexte du curseur :

   * Accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** et supprimez toute documentation répertoriée.

   ![Indexation du curseur et paramètres des documents avec la liste de documentation vide](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Générer le code pour une extension d’évaluation de produit :
   * Dans la fenêtre de conversation Cursor, sélectionnez le mode **[!UICONTROL Agent]**.
   * Saisissez l’invite suivante :

   ```shell-session
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >Si l’agent demande à rechercher la documentation, autorisez-la.

1. Répondez précisément aux questions de l’agent pour l’aider à générer le meilleur code.

   ![Fenêtre de conversation du curseur en mode Agent avec invite d’extension entrée](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![Un agent d’IA pose des questions pour clarifier les exigences d’extension](../assets/agent-questions.png){width="600" zoomable="yes"}

1. Utilisez l’exemple de texte suivant pour répondre aux questions de l’agent afin de configurer les données d’évaluation randomisées :

   ```shell-session
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension is called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   L’agent crée un fichier `requirements.md` qui sert de source de vérité pour l’implémentation.

   ![Fichier Requirements.md créé par l’agent AI avec les détails d’implémentation](../assets/requirements-file.png){width="600" zoomable="yes"}

1. Consultez le fichier `requirements.md` et vérifiez le plan.

   Si tout semble correct, demandez à l&#39;agent de passer à **Phase 2 - Planification de l&#39;architecture**.

1. Examinez le plan d’architecture.

1. Demandez à l’agent de poursuivre la génération du code.

   L’agent génère le code nécessaire et fournit un résumé détaillé des étapes suivantes.

   ![Plan d’architecture de l’agent AI Phase 2 pour l’API de notation](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![Résumé des fichiers de code générés et structure](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   Agent ![AI fournissant les étapes suivantes pour le test et le déploiement](../assets/next-steps.png){width="600" zoomable="yes"}

### Tester l’extension localement

Les étapes suivantes expliquent comment vérifier le fonctionnement de l’extension avant de la déployer.

1. Demandez à l’agent de vous aider à tester le code localement.

   ```shell-session
   Test the ratings API locally on a dev server using cURL.
   ```

1. Suivez les instructions de l’agent et vérifiez que l’API fonctionne localement.

   ![Instructions de l’agent AI pour les tests d’API locaux](../assets/local-testing.png){width="600" zoomable="yes"}

   ![Terminal affichant les résultats du test d’API local avec cURL](../assets/local-testing-1.png){width="600" zoomable="yes"}

### Déployer l’extension

Déployez l’extension sur [!DNL Adobe I/O Runtime] à l’aide de l’agent.

1. Après avoir vérifié le code généré, déployez l’extension à l’aide de l’invite suivante :

   ```shell-session
   Deploy the ratings API.
   ```

   L’agent effectue une évaluation de préparation avant le déploiement.

   ![Liste de contrôle d’évaluation du niveau de préparation au déploiement de l’agent AI](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. Lorsque vous êtes certain des résultats de l’évaluation, demandez à l’agent de procéder au déploiement.

   L’agent utilise la boîte à outils MCP pour vérifier, créer et déployer automatiquement.

   ![Création et processus de déploiement de la vérification de la boîte à outils MCP](../assets/deployment-process.png){width="600" zoomable="yes"}

### Vérification du déploiement

Tester l’API avant de l’intégrer au storefront L’agent doit indiquer l’emplacement de la nouvelle action et une stratégie de test.

Stratégie de test de l’agent ![AI avec URL d’action déployée et commandes de test](../assets/testing-strategy.png){width="600" zoomable="yes"}

Vous pouvez également tester l’API manuellement à l’aide de cURL dans un terminal :

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![Terminal affichant le test cURL réussi de l’API de notation déployée](../assets/curl-test.png){width="600" zoomable="yes"}

### Intégration à Edge Delivery Services

Pour intégrer l’API de notes à un storefront [!DNL Adobe Commerce] optimisé par [!DNL Edge Delivery Services], demandez à l’agent de créer un contrat de service avec les exigences de l’API de notes :

```shell-session
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![Agent AI créant un fichier de contrat de service pour l’intégration de storefront](../assets/create-contract.png){width="600" zoomable="yes"}

![Fichier Markdown de contrat de l’API Ratings avec le point d’entrée et les détails de réponse](../assets/contract.png){width="600" zoomable="yes"}

Revenez au terminal et exécutez la commande suivante dans le dossier `extension` pour copier le fichier de contrat dans le dossier `storefront` :

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## Connexion au storefront

Cette section vous guide tout au long de l’implémentation de la partie storefront de l’extension ratings à l’aide d’outils de développement [!DNL Edge Delivery Services] et assistés par l’IA.

>[!NOTE]
>
>Les invites fournies sont des points de départ. Bien que vous puissiez les utiliser sans modification, pensez à avoir une conversation naturelle avec l&#39;agent.
>
>Lorsque vous utilisez des outils de développement assistés par l’IA, il existe toujours des variations naturelles dans le code et les réponses générés par l’agent.
>
>Si vous rencontrez des problèmes avec votre code, demandez à l’agent de vous aider à le déboguer.

### Conditions préalables requises pour Storefront

Avant de démarrer l’intégration du storefront, vérifiez que vous disposez des éléments suivants :

* Un projet de storefront connecté à votre instance [!DNL Commerce]
* Outils d’IA pour storefront Commerce [installés à l’aide de l’interface de ligne de commande](./tutorial-prerequisites.md#install-the-storefront-ai-tools)

### Configurer l’espace de travail storefront

Préparez votre environnement de storefront local pour le développement.

1. Accédez au dossier `storefront` :

   ```bash
   cd storefront
   ```

1. Ouvrez le dossier storefront dans une nouvelle fenêtre Cursor .

   Si l’interface de ligne de commande [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) est installée, vous pouvez également ouvrir la fenêtre à l’aide de la commande suivante dans votre terminal :

   ```bash
   cursor .
   ```

1. Démarrez le serveur de développement local :

   ```bash
   npm run start
   ```

1. Dans un navigateur, accédez à une page de produit :

   ```shell-session
   http://localhost:3000/products/llama-plush-shortie/adb336
   ```

1. Observez la page standard des détails du produit (PDP) du storefront et notez l’absence d’évaluations visuelles du produit.

### Intégrer l’API de notation

Utilisez l’agent pour intégrer l’API de notes à la page des détails du produit storefront.

1. Utilisez l’invite suivante avec votre agent :

   ```shell-session
   Integrate the ratings API into the PDP to show star ratings and a review count for products. Here's the service contract: @RATINGS_API_CONTRACT.md
   ```

1. L’agent évalue la complexité de la tâche et appelle un workflow échelonné. Au cours de la **phase 1 (collecte des exigences)** l&#39;agent crée un document d&#39;exigences et pose des questions de clarification telles que :

   * Où les notes devraient-elles apparaître sur le PDP ?
   * S’agit-il d’un nouveau bloc autonome ou d’une personnalisation d’emplacement dans le composant de dépôt PDP existant ?
   * Quelle doit être la solution de secours si l’API n’est pas disponible ou ne renvoie aucune donnée ?
   * Les évaluations doivent-elles également apparaître sur le PLP (liste de produits) ou le PDP uniquement ?
   * Existe-t-il des spécifications de conception ou des maquettes ?

   Répondez à ces questions en fonction des exigences de votre projet. L’agent met à jour le document des exigences et marque la phase comme terminée.

1. Au cours de **Phase 2 (planification architecturale)** l’agent effectue des recherches dans la documentation et votre base de code avant de proposer une architecture. Attendez-vous à ce que l’agent :

   * Recherchez dans [!DNL Commerce] documentation les conteneurs de dépôt PDP, les emplacements et les payloads d’événement.
   * Recherchez du code lié au PDP dans le répertoire `blocks` et le dossier `scripts/initializers/`.
   * Explorez les définitions TypeScript pour les conteneurs et les formes contextuelles d&#39;emplacement disponibles.

   L’agent présente ensuite des options d’architecture telles que :

   * **Option A :** personnalisez un emplacement de dépôt PDP existant pour injecter des évaluations près du titre du produit, une touche plus légère qui permet une mise à niveau.
   * **Option B :** créez un bloc de `product-ratings` autonome qui récupère l’API indépendamment : plus flexible et découplé.
   * **Option C :** créer un bloc qui écoute également les événements déroulants PDP pour le SKU du produit ; il s’agit d’une approche hybride.

   Le plan comprend également des détails sur l’intégration de l’API, des considérations sur les performances (chargement différé, mise en cache), la sécurité (nettoyage des entrées) et une approche de test.

   Passez en revue le plan d’architecture et demandez à l’agent de continuer.

1. Au cours de **Phase 3 (Approche d’implémentation)** l’agent vous demande de choisir entre :

   * **Option A :** passez en revue un plan d’implémentation détaillé avant la génération du code (consultez d’abord tous les fichiers, modèles et structures de code).
   * **Option B :** passer directement à la génération du code.

   Sélectionnez l’approche de votre choix.

1. Au cours de **Phase 4 (implémentation)** l’agent génère le code en fonction de l’architecture choisie. Selon l&#39;approche, l&#39;agent utilise plusieurs compétences spécialisées :

   * **Modélisation de contenu :** si un nouveau bloc est nécessaire, l’agent conçoit une structure de contenu conviviale pour la création, telle qu’une table de configuration avec l’URL du point d’entrée de l’API.
   * **Développement de blocs :** l’agent crée des fichiers de bloc en respectant les conventions [!DNL Edge Delivery Services], notamment les fonctions de décoration JavaScript, les styles CSS étendus, les libellés ARIA pour l’accessibilité, ainsi que le chargement et la gestion des états d’erreur.
   * **Personnalisation du Drop-in :** si l’architecture utilise la personnalisation des emplacements, l’agent importe le conteneur approprié, utilise un emplacement vérifié à proximité du titre du produit et s’abonne aux événements de données de produit pour le SKU actuel.

   Regardez le code en cours de génération et posez des questions ou redirigez l’agent si nécessaire. L’agent génère un résumé du niveau de préparation pour la production une fois la génération du code terminée.

1. Au cours de la **phase 4.5 (test)**, l’agent propose de tester l’implémentation. Si vous acceptez, l’agent :

   * Crée une page de test locale avec les scripts et les styles appropriés.
   * Démarre un serveur de développement.
   * Exécute une vérification basée sur un navigateur pour le rendu visuel, l’interactivité, le comportement réactif, l’accessibilité et les performances.
   * Génère un rapport de test structuré avec les résultats.

   Suivez les instructions dans le navigateur pour confirmer le comportement et signaler tout problème.

1. Observez les modifications apportées à la base de code et observez les mises à jour sur la page produit.

   Les modifications suivantes devraient s’afficher dans votre environnement de développement et votre navigateur :

   * Un composant d’évaluation de produit est automatiquement créé.
   * Le composant est intégré au PDP à l’aide de [emplacements d’accueil](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots?lang=fr) ou sous la forme d’un bloc autonome, selon l’architecture choisie.
   * Les étoiles s’affichent avec des proportions de remplissage appropriées en fonction des valeurs d’évaluation de votre API.

   ![Page des détails du produit présentant les évaluations par étoiles intégrées sous le titre du produit](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Résumé du tutoriel

Voici un résumé des sujets abordés dans ce tutoriel :

* **Développement d’extensions :** découvrez comment décrire une nouvelle fonctionnalité à un agent d’IA et générer une API REST fonctionnelle à l’aide de [!DNL App Builder].
* **Test et déploiement locaux :** test local de l’API et déploiement à l’aide de la boîte à outils MCP.
* **Contrats de service :** création de contrats d’API qui relient les extensions principales et les implémentations de storefront.
* **Intégration progressive du storefront :** en fonction des exigences, de l’architecture et de la mise en œuvre à l’aide de compétences assistées par l’IA.
* **Intégration d’un conteneur de dépôt :** utilisation de conteneurs et d’emplacements de dépôt [!DNL Adobe Commerce].
* **Réutilisation des composants :** création de composants partagés utilisés sur plusieurs blocs.

## Étapes suivantes

Suivez les suggestions suivantes pour personnaliser votre extension d’évaluations ou créer vos propres modifications :

### Modification des couleurs des étoiles

Utilisez l’invite suivante avec votre agent :

```shell-session
Change the star fill color to red.
```

**Résultat attendu :**

Les étoiles changent en rouge.

![Évaluation des produits affichée avec la couleur de remplissage rouge étoile](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Ajouter une boîte de dialogue modale de distribution d’évaluation

Les étapes suivantes montrent comment l’agent gère les fonctionnalités complexes de l’interface utilisateur avec des références visuelles.

1. **Avant de commencer :** enregistrez l’image simulée suivante et collez-la dans la conversation avec votre agent storefront.

   ![Maquette montrant la répartition de la distribution d’évaluation par niveau d’étoile](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Pour créer la boîte de dialogue modale de distribution des évaluations à l’aide de l’image de référence comme guide, procédez comme suit :

   * Mettez à jour l’API pour renvoyer des données supplémentaires représentant la distribution des évaluations.
   * Mettez à jour le contrat d’API.
   * Mettez à jour le contrat dans la base de code du storefront.
   * Demandez à l’agent storefront d’utiliser l’image de référence et le contrat d’API mis à jour pour ajouter la distribution des évaluations à la page PDP.

1. Observez les modifications suivantes dans la base de code et observez les mises à jour sur la page produit :

   * Comment l’agent interprète la maquette visuelle
   * Utilisation ou non de la structure HTML appropriée pour l’accessibilité
   * Gestion des états de positionnement et d’interaction

#### Résolution des problèmes liés à la distribution modale

Si la boîte de dialogue modale ne se comporte pas comme prévu, essayez les méthodes suivantes :

* Si la boîte de dialogue modale n’apparaît pas, recherchez les erreurs dans la console du navigateur.
* Si le positionnement est désactivé, demandez à l’agent de le corriger au format suivant :

  ```shell-session
  adjust the modal position to be...
  ```

![Boîte de dialogue modale affichant la distribution d’évaluation détaillée avec des barres de répartition au niveau des étoiles](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
