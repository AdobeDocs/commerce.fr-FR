---
title: Tutoriel sur l’extension d’évaluations
description: Découvrez comment créer une extension d’évaluations de produit pour Adobe Commerce as a Cloud Service à l’aide d’App Builder et d’outils de développement assistés par l’IA.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 453b21f89d2024a8d6927fa082affdd5abb6e5cd
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Adobe Developers Live - classeur de l’atelier Adobe Commerce

Ce Lab vous guide tout au long de la création d’une extension d’évaluations de produit pour les [!DNL Adobe Commerce as a Cloud Service] qui utilisent des outils de développement [!DNL Adobe App Builder] et assistés par l’IA.

## Vérifier les conditions préalables

Vérifiez que les prérequis suivants sont installés :

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git
git --version

# Check Bash
bash --version
```

## Connexion à Adobe Developer Console

1. Accédez à [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Si vous êtes déjà connecté, cliquez sur l’icône de votre profil en haut à droite, puis sur le bouton **Se déconnecter**.
1. Connectez-vous à l&#39;aide de l&#39;ID de messagerie et du mot de passe fournis pour votre poste.
1. Si vous êtes invité à ajouter une adresse e-mail ou un numéro de téléphone secondaire, cliquez sur **Pas maintenant**.
1. Lorsque vous êtes invité à sélectionner un profil d’organisation, sélectionnez **Adobe Commerce Labs**.

   ![select-organization](./assets/select-org.png){width="600" zoomable="yes"}

1. Si vous êtes invité à accepter les termes et conditions, cliquez sur le lien pour lire les termes, puis cliquez sur **Accepter et continuer**.

   ![accept-terms](./assets/accept-terms.png){width="600" zoomable="yes"}

## Exécuter le script de configuration

Si les [prérequis](#verify-prerequisites) sont installés et que vous vous êtes connecté au Adobe Developer Console, téléchargez et exécutez le script de configuration. Vous pouvez également configurer manuellement le script en suivant les étapes [conditions préalables de l’atelier](workbook-prerequisites.md).

1. Clonez le référentiel contenant le script de configuration :

   ```bash
   git clone https://github.com/adobe-commerce/commerce-adl-2025.git
   ```

   >[!NOTE]
   >
   >Si le script échoue, reportez-vous aux [conditions préalables](workbook-prerequisites.md) et continuez là où le script a rencontré une erreur.

1. Accédez au référentiel :

   ```bash
   cd commerce-adl-2025
   ```

1. Exécutez le script de configuration :

   ```bash
   bash adl-setup.sh
   ```

   Pendant l’exécution du script, vous serez invité à saisir votre nom d’utilisateur et votre mot de passe, qui seront fournis pendant l’atelier. Votre nom d&#39;utilisateur reflétera votre emplacement et votre numéro de poste. Par exemple, si vous êtes à San Jose, CA, seat 123, votre nom d&#39;utilisateur sera `sjc-adl-123@adobeeventlab.com`.

   De plus, vous devez sélectionner le projet qui correspond à votre numéro de poste et l’espace de travail **étape**. Le nom de votre projet reflétera votre emplacement et votre numéro de poste. Par exemple, si vous êtes à San Jose, CA, siège 123, le nom de votre projet sera `SJC ADL 123`.

## Développement d’extension

Cette section vous guide tout au long du processus de développement d’une extension de notes pour Adobe Commerce as a Cloud Service à l’aide d’outils de développement assistés par l’IA.

### Installation des outils d’IA dédiés à l’extensibilité

Configurez les outils de développement assistés par l’IA dans le dossier `extension` :

```bash
cd extension
```

```bash
aio commerce extensibility tools-setup
```

![Installation des outils d’IA](./assets/install-ai-tools.png){width="600" zoomable="yes"}

### Ouvrir le curseur

>[!NOTE]
>
>Lorsque vous travaillez avec des outils de développement assistés par l’IA, il existe des variations naturelles dans le code et les réponses générées par l’agent.
>Si vous rencontrez des problèmes avec votre code, vous pouvez toujours demander à l’agent de vous aider à le déboguer.

Ouvrez l’application [!DNL Cursor] et accédez au dossier `extension` ou, si l’interface de ligne de commande [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) est installée, saisissez la commande suivante dans votre terminal :

```bash
cursor .
```

![Ouvrir le curseur](./assets/open-cursor.png){width="600" zoomable="yes"}

À ce stade, toutes les règles de [!DNL Cursor] sont installées dans le dossier `.cursor/rules` . Les outils MCP sont disponibles dans la section **Paramètres MCP** de la [!DNL Cursor]. Vérifiez que l&#39;ensemble d&#39;outils `commerce-extensibility` est activé sans erreur. Si des erreurs s’affichent, désactivez la palette d’outils et activez-la.

![Paramètres du curseur](./assets/cursor-settings.png){width="600" zoomable="yes"}

Si de la documentation est ajoutée au contexte du curseur, vous devez la désactiver. Accédez à [!UICONTROL **Curseur**] > [!UICONTROL **Paramètres**] > [!UICONTROL **Paramètres du curseur**] > [!UICONTROL **Indexation et documents**] et supprimez toute documentation répertoriée.

![Désactiver la documentation](./assets/disable-documentation.png){width="600" zoomable="yes"}

### Génération de code

Cette section explique comment utiliser des outils assistés par l’IA pour générer du code pour une extension d’évaluation de produit.

#### Définition des exigences

Vous implémenterez une extension qui sert de notes de produit en tant qu’API. L’extension [!DNL App Builder] répond avec les détails d’évaluation pour un SKU donné.

**Invite initiale :**

Utilisez l’invite suivante dans [!DNL Cursor] :

1. Ouvrez la fenêtre de conversation dans Cursor.
1. Sélectionnez le mode **Agent**.
1. Saisissez l’invite suivante :

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   Implement a REST API to handle GET ratings requests.
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

1. Si l’agent demande à rechercher la documentation, autorisez-la.

![Entrez l&#39;invite dans Cursor](./assets/enter-prompt.png){width="600" zoomable="yes"}

L&#39;agent fait des recherches sur les exigences et pose des questions pour clarifier les choses. Répondez précisément aux questions de l’agent pour l’aider à générer le meilleur code.

![L’agent pose des questions pour clarifier les choses](./assets/agent-questions.png){width="600" zoomable="yes"}

**Invite de réponse :**

Utilisez la réponse suivante pour répondre aux questions de l’agent :

```text
Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
This extension will be called directly from the storefront,
no async invocation, such as events or webhooks, is required.
Let's start with just the GET API for now,
we will implement other CRUD operations at a later time.
We do not need a DB or storage mechanism right now,
just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
The API should only return the average rating for the product and the total number of ratings.
We do not need to add tests right now.
```

L’agent crée un fichier `requirements.md` qui sert de source de vérité pour l’implémentation.

![Fichier d’exigences créé](./assets/requirements-file.png){width="600" zoomable="yes"}

#### Vérification des exigences et planification de l’architecture

1. Vérifiez le fichier `requirements.md`.
1. Si tout semble correct, demandez à l&#39;agent de passer à **Phase 2 - Planification de l&#39;architecture**.
1. Examinez le plan d’architecture.
1. Demandez à l’agent de poursuivre la génération du code.

![Planification de l’architecture](./assets/architecture-planning.png){width="600" zoomable="yes"}

#### Générer le code

L’agent génère le code nécessaire et fournit un résumé détaillé des étapes suivantes.

![Résumé de la génération du code](./assets/code-generation-summary.png){width="600" zoomable="yes"}

![Étapes suivantes](./assets/next-steps.png){width="600" zoomable="yes"}

### Test local

Demandez à l’agent de vous aider à tester le code localement.

```text
Test the ratings API locally on a dev server using cURL.
```

Suivez les instructions de l’agent et vérifiez que l’API fonctionne localement.

![Test local](./assets/local-testing.png){width="600" zoomable="yes"}

![Résultats des tests locaux](./assets/local-testing-1.png){width="600" zoomable="yes"}

### Déployer l’extension

Après avoir vérifié le code généré, vous êtes prêt à déployer l’extension à l’aide de l’invite suivante :

```text
Deploy the ratings API.
```

#### Évaluation préalable au déploiement

L’agent effectue une évaluation de préparation avant le déploiement.

![ Évaluation préalable au déploiement ](./assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

#### Déployer

Lorsque vous êtes certain des résultats de l’évaluation, demandez à l’agent de procéder au déploiement. L’agent utilise la boîte à outils MCP pour vérifier, créer et déployer automatiquement.

![ Déploiement ](./assets/deployment-process.png){width="600" zoomable="yes"}

### Tester l’API

Vous pouvez tester l’API avant de l’intégrer au storefront.

L’agent fournit l’emplacement de la nouvelle action et une stratégie de test.

![Stratégie de test](./assets/testing-strategy.png){width="600" zoomable="yes"}

#### Test manuel avec cURL

Testez manuellement l’API à l’aide de cURL dans un terminal :

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

Test ![cURL](./assets/curl-test.png){width="600" zoomable="yes"}

### Intégration à Edge Delivery Services

Pour intégrer l’API de notes à un storefront [!DNL Adobe Commerce] optimisé par [!DNL Edge Delivery Services], demandez à l’agent de créer un contrat de service avec les exigences de l’API de notes :

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![ Contrat de service ](./assets/create-contract.png){width="600" zoomable="yes"}

![Détails du contrat de service](./assets/contract.png){width="600" zoomable="yes"}

Revenez au terminal et exécutez la commande suivante dans le dossier `extension` pour copier le fichier dans le dossier `storefront` :

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## Connexion au storefront

Cette section vous aidera à mettre en œuvre de véritables fonctionnalités de storefront, en vous montrant comment communiquer efficacement avec les agents d’IA lors de l’utilisation de dropings et de [!DNL Adobe Commerce] [!DNL Edge Delivery Services].

>[!NOTE]
>
>Les invites fournies sont des points de départ, vous devriez vous sentir libre d&#39;avoir une conversation naturelle avec l&#39;agent. Lorsque vous travaillez avec des outils de développement assistés par l’IA, il existe des variations naturelles dans le code et les réponses générées par l’agent.
>
>Si vous rencontrez des problèmes avec votre code, vous pouvez toujours demander à l’agent de vous aider à le déboguer.

### Implémenter les étoiles d’évaluation et le nombre de révisions

1. Accédez au dossier `storefront` :

   ```bash
   cd storefront
   ```

1. Ouvrez le dossier storefront dans une nouvelle fenêtre Cursor . Si l’interface de ligne de commande [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) est installée, saisissez la commande suivante dans votre terminal :

   ```bash
   cursor .
   ```

1. Démarrez le serveur de développement local :

   ```bash
   npm run start
   ```

1. Dans un navigateur, accédez à la page Vêtements :

   ```text
   http://localhost:3000/apparel
   ```

1. Observez la disposition standard de l’interface utilisateur du storefront.

1. Utilisez l’invite suivante avec votre agent :

   ```text
   Implement product ratings to the storefront.
   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.
   Use the dropin slot system where available.
   
   Use the @RATINGS_API_CONTRACT.md to understand how to use the ratings api.
   ```

   >[!NOTE]
   >
   >Si vous êtes invité à démarrer le serveur de développement local, informez l’agent qu’il est déjà en cours d’exécution.

1. Observez les modifications apportées à la base de code et observez les mises à jour sur la page Vêtements .

**Résultat attendu :**

* Un « composant » d’évaluation de produit est automatiquement créé.
* Le composant est intégré aux blocs product-details, product-list-page et product-recommendations à l’aide d’emplacements.
* Les étoiles s’affichent avec des proportions de remplissage appropriées basées sur des valeurs d’évaluation simulées.

![Implémentation des évaluations de produits](./assets/product-ratings-implementation.png){width="600" zoomable="yes"}

### Modification des couleurs des étoiles

Utilisez l’invite suivante pour envoyer un e-mail à votre agent :

```text
Change the star fill color to red.
```

**Résultat attendu :**

Les étoiles sont changées en rouge.

![Couleurs Étoiles Rouges](./assets/red-star-colors.png){width="600" zoomable="yes"}

## Récapitulatif du storefront

Tout au long de ce tutoriel, nous avons abordé les sujets suivants :

* **Implémentation des fonctionnalités** : description des nouvelles fonctionnalités d’un agent d’IA.
* **Modifications itératives** : modification rapide du code existant.
* **Composants d’IU complexes** : création de fonctions interactives avec des références visuelles.
* **Intégration Dropin** : utilisation des conteneurs et des emplacements de dépôt [!DNL Adobe Commerce].
* **Réutilisation des composants** : création de composants partagés utilisés sur plusieurs blocs.

## Étapes suivantes

Si le temps le permet, vous pouvez personnaliser davantage votre extension d’évaluation en ajoutant les fonctionnalités suivantes :

### Boîte de dialogue modale Ajouter une distribution d’évaluation (facultatif)

Les étapes suivantes montrent comment l’agent gère les fonctionnalités complexes de l’interface utilisateur avec des références visuelles.

1. **Avant de commencer :** enregistrez l’image simulée suivante et collez-la dans la conversation avec votre agent storefront.

   ![Maquette de distribution d’évaluation](./assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Suivez les étapes ci-dessous pour vous guider tout au long de la création de la boîte de dialogue modale de distribution des évaluations basée sur l’image de référence :

   * Mettez à jour l’API pour renvoyer des données supplémentaires représentant la distribution des évaluations.
   * Mettez à jour le contrat d’API.
   * Mettez à jour le contact dans la base de code du storefront.
   * Demandez à l’agent storefront d’utiliser l’image de référence et le contrat d’API mis à jour pour ajouter la distribution des évaluations à la page PDP.

1. Observez les modifications suivantes dans la base de code et observez les mises à jour sur la page Vêtements :

   * Comment l’agent interprète la maquette visuelle
   * Utilisation ou non de la structure HTML appropriée pour l’accessibilité
   * Gestion des états de positionnement et d’interaction

**Dépannage :**

* Si la boîte de dialogue modale n’apparaît pas, recherchez les erreurs dans la console du navigateur.
* Si le positionnement est désactivé, vous pouvez demander à l’agent de :

  ```text
  adjust the modal position to be...
  ```

![Boîte de dialogue modale de distribution d’évaluation](./assets/rating-distribution-modal.png){width="600" zoomable="yes"}
