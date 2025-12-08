---
title: Tutoriel sur l’extension d’évaluations
description: Découvrez comment créer une extension d’évaluations de produit pour Adobe Commerce as a Cloud Service à l’aide d’App Builder et d’outils de développement assistés par l’IA.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e153e974be1dc5ec8ff2eff8d699ce87ef6708dc
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Tutoriel sur l’extension d’évaluations (Beta)

>[!NOTE]
>
>L’outil d’IA utilisé dans ce tutoriel est actuellement dans Beta et peut inclure des bogues ou d’autres problèmes.

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

Si l’une des commandes précédentes ne renvoie pas les résultats attendus, consultez les [conditions préalables](tutorial-prerequisites.md) pour obtenir des conseils.

## Développement d’extension

Cette section vous guide tout au long du processus de développement d’une extension de notes pour Adobe Commerce as a Cloud Service à l’aide d’outils de développement assistés par l’IA.

1. Accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]** et vérifiez que l’ensemble d’outils `commerce-extensibility` est activé sans erreur. Si des erreurs s’affichent, désactivez la palette d’outils et activez-la.

   ![Paramètres du curseur](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Lorsque vous travaillez avec des outils de développement assistés par l’IA, il existe des variations naturelles dans le code et les réponses générées par l’agent.
   >Si vous rencontrez des problèmes avec votre code, vous pouvez toujours demander à l’agent de vous aider à le déboguer.

1. Si de la documentation est ajoutée au contexte du curseur, désactivez-la :

   - Accédez à [!UICONTROL **Curseur**] > [!UICONTROL **Paramètres**] > [!UICONTROL **Paramètres du curseur**] > [!UICONTROL **Indexation et documents**] et supprimez toute documentation répertoriée.

   ![Désactiver la documentation](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Générer le code pour une extension d’évaluation de produit :
   - Dans la fenêtre de conversation avec le curseur, sélectionnez le mode **Agent**.
   - Saisissez l’invite suivante :

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >Si l’agent demande à rechercher la documentation, autorisez-la.

1. Répondez précisément aux questions de l’agent pour l’aider à générer le meilleur code.

   ![Entrez l&#39;invite dans Cursor](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![L’agent pose des questions pour clarifier les choses](../assets/agent-questions.png){width="600" zoomable="yes"}

1. Utilisez l’exemple de texte suivant pour répondre aux questions de l’agent afin de configurer les données d’évaluation randomisées :

   ```text
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension will be called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   L’agent crée un fichier `requirements.md` qui sert de source de vérité pour l’implémentation.

   ![Fichier d’exigences créé](../assets/requirements-file.png){width="600" zoomable="yes"}

1. Consultez le fichier `requirements.md` et vérifiez le plan.

   Si tout semble correct, demandez à l&#39;agent de passer à **Phase 2 - Planification de l&#39;architecture**.
1. Examinez le plan d’architecture.
1. Demandez à l’agent de poursuivre la génération du code.

   L’agent génère le code nécessaire et fournit un résumé détaillé des étapes suivantes.

   ![Planification de l’architecture](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![Résumé de la génération du code](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![Étapes suivantes](../assets/next-steps.png){width="600" zoomable="yes"}

### Test local

1. Demandez à l’agent de vous aider à tester le code localement.

   ```text
   Test the ratings API locally on a dev server using cURL.
   ```

1. Suivez les instructions de l’agent et vérifiez que l’API fonctionne localement.

   ![Test local](../assets/local-testing.png){width="600" zoomable="yes"}

   ![Résultats des tests locaux](../assets/local-testing-1.png){width="600" zoomable="yes"}

### Déployer l’extension

1. Après avoir vérifié le code généré, déployez l’extension à l’aide de l’invite suivante :

   ```text
   Deploy the ratings API.
   ```

   L’agent effectue une évaluation de préparation avant le déploiement.

   ![ Évaluation préalable au déploiement ](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. Lorsque vous êtes certain des résultats de l’évaluation, demandez à l’agent de procéder au déploiement.

   L’agent utilise la boîte à outils MCP pour vérifier, créer et déployer automatiquement.

   ![ Déploiement ](../assets/deployment-process.png){width="600" zoomable="yes"}

### Après le déploiement

Vous pouvez tester l’API avant de l’intégrer au storefront. L’agent doit indiquer l’emplacement de la nouvelle action et une stratégie de test.

![Stratégie de test](../assets/testing-strategy.png){width="600" zoomable="yes"}

Vous pouvez également tester l’API manuellement à l’aide de cURL dans un terminal :

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

Test ![cURL](../assets/curl-test.png){width="600" zoomable="yes"}

### Intégration à Edge Delivery Services

Pour intégrer l’API de notes à un storefront [!DNL Adobe Commerce] optimisé par [!DNL Edge Delivery Services], demandez à l’agent de créer un contrat de service avec les exigences de l’API de notes :

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![ Contrat de service ](../assets/create-contract.png){width="600" zoomable="yes"}

![Détails du contrat de service](../assets/contract.png){width="600" zoomable="yes"}
<!-- 
Return to the terminal and run the following command in the `extension` folder to copy the file to the `storefront` folder:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
``` -->

### Étapes suivantes

Maintenant que vous disposez du contrat d’API de notes, vous pouvez commencer à créer la partie storefront (front-end) de l’extension notes.

<!-- 
## Connect to the storefront

This section teaches you how to implement real storefront features and communicate effectively with AI agents when working with [!DNL Adobe Commerce] dropins and [!DNL Edge Delivery Services].

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Ratings stars and review count implementation

1. Navigate to the `storefront` folder:

   ```bash
   cd storefront
   ```

1. Open the storefront folder in a new Cursor window.

    Alternatively, if you have the [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installed, open the window by using the following command in your terminal:

   ```bash
   cursor .
   ```

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, navigate to the Apparel page:

   ```text
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```text
   Implement product ratings in the storefront.

   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.

   Use the dropin slot system where available.

   Use @RATINGS_API_CONTRACT.md to understand how to use the ratings API.
   ```

1. Observe the changes in the codebase, and watch the Apparel page for updates.

   You should see the following changes in your development environment and browser:

   * A product rating "component" is automatically created.
   * The component is integrated into product-details, product-list-page, and product-recommendations blocks using [dropin slots](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots).
   * Stars display with proper fill proportions based on mock rating values.

![Product Ratings Implementation](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

* **Feature implementation**: How to describe new functionality to an AI agent.
* **Iterative changes**: Making quick modifications to existing code.
* **Complex UI components**: Building interactive features with visual references.
* **Dropin integration**: Working with [!DNL Adobe Commerce] dropin containers and slots.
* **Component reusability**: Creating shared components used across multiple blocks.

## Next steps

For further experimentation with this tutorial, use the following suggestions to further customize your ratings extension, or create your own modifications:

### Change the star colors

Use the following prompt to your agent:

```text
Change the star fill color to red.
```

**Expected outcome:**

The stars are changed to red.

![Red Star Colors](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Add rating distribution modal

The following steps show how the agent handles complex UI features with visual references.

1. **Before starting:** Save the following mock image and paste it into the chat with your storefront agent.

   ![Rating Distribution Mockup](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Follow these steps to create the ratings distribution modal using the reference image as a guide:

   * Update the API to return additional data representing the ratings distribution.
   * Update the API Contract.
   * Update the contact in the storefront codebase.
   * Ask the storefront agent to use the reference image and updated API Contract to add the ratings distribution to the PDP page.

1. Observe the following changes in the codebase, and watch the Apparel page for updates:

   * How the agent interprets the visual mockup
   * Whether it uses appropriate HTML structure for accessibility
   * How it handles the positioning and interaction states

#### Troubleshooting

* If the modal does not appear, check the browser console for errors.
* If positioning is off, ask the agent to fix it using the following format:

   ```text
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
