---
title: Tutoriel sur l’extension des méthodes d’expédition
description: Découvrez comment créer une extension de méthode d’expédition configurable pour Adobe Commerce as a Cloud Service à l’aide d’App Builder, du kit de démarrage pour le paiement et d’outils de développement assistés par l’IA.
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: e55bc4db196d3d973b981bb2484be950dcd6b7c3
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 0%

---

# Tutoriel sur l’extension des méthodes d’expédition

Ce tutoriel vous guide tout au long de la création d’une extension de méthode d’expédition pour les [!DNL Adobe Commerce as a Cloud Service] qui utilisent [!DNL Adobe App Builder], le [kit de démarrage pour le paiement](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} et les outils de développement assistés par l’IA.

L’extension ajoute une méthode d’expédition configurable au passage en caisse où les taux proviennent d’un service de taux d’expédition simulés externe. Les commerçants configurent l’URL du service, la clé API et l’adresse de l’entrepôt de données (d’expédition) dans l’interface utilisateur d’administration. Lors du passage en caisse, les taux de demandes d’extension de ce service et affichent les options renvoyées au client.

Avant de commencer, renseignez les [conditions préalables](./tutorial-prerequisites.md).

## Vérifier les conditions préalables {#tutorial-verify-prerequisites}

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

## Créer l’API de taux d’expédition simulés

Après avoir rempli les [conditions préalables](./tutorial-prerequisites.md), créez l’API de taux d’expédition simulés afin que l’URL de service et la clé d’API soient prêtes lorsque vous configurez l’extension dans l’[!DNL Commerce Admin]. L’extension appelle une API de taux d’expédition externe. Pour ce tutoriel, vous utilisez une API simulée qui vous permet d’exécuter le flux sans compte d’opérateur réel. Vous allez créer l’API simulée à l’aide de [Pipedream](https://pipedream.com) (compte gratuit requis). L’API simulée utilise un contrat de requête/réponse similaire aux API des taux d’expédition réels standard. La connexion ultérieure de cette extension à un fournisseur réel doit donc être simple.

Pour créer l’API simulée, téléchargez le [fichier de spécification de l’API de taux simulés](../assets/mock-rates-api-spec.zip), ouvrez-le et ajoutez le fichier `.md` à votre projet (par exemple, `docs/mock-rates-api-spec.md`).

**Time :** la création de l’API simulée devrait prendre entre **5 et 10 minutes**.

### Créer un workflow et un déclencheur HTTP

1. Accédez à [pipedream.com](https://pipedream.com) et inscrivez-vous ou connectez-vous.
1. Cliquez sur **Nouveau workflow** (ou **Ajouter un workflow**).
1. Pour le déclencheur , sélectionnez **HTTP/Webhook**.
1. Dans la configuration du déclencheur, définissez **Réponse HTTP** sur **Renvoyer une réponse personnalisée à partir de votre workflow**. Cela permet à l’étape de code d’envoyer la réponse JSON simulée.
1. Pipedream affiche une **URL de point d’entrée HTTP** unique, telle que `https://123456.m.pipedream.net`.
1. **Copiez cette URL** et utilisez-la comme **URL du service** lors de la configuration de l’extension dans Commerce Admin.

   ![Workflow Pipedream avec déclencheur HTTP/Webhook et URL de point d’entrée visible](../assets/mock-api-trigger.png){width="600" zoomable="yes"}

Vous n’avez pas besoin de configurer l’**autorisation** sur le déclencheur ; l’API simulée valide l’en-tête `API-Key` à l’étape Code .

### Ajouter l’étape Code

1. Cliquez sur l’icône **+** pour ajouter une étape.
1. Choisissez **Exécuter le code Node.js** (étape du code).
1. **Remplacez** le code par défaut par le code JavaScript suivant.

   ```javascript
   export default defineComponent({
   async run({ steps, $ }) {
      const event = steps.trigger.event;
      const body = event.body ?? {};
      const headers = event.headers ?? {};
      const apiKey = headers["api-key"] ?? body.api_key ?? "";
   
      if (!apiKey || String(apiKey).trim() === "") {
         await $.respond({
         immediate: true,
         status: 401,
         headers: { "Content-Type": "application/json" },
         body: { error: "Missing or invalid API-Key header" },
         });
         return;
      }
   
      const shipment = body.shipment;
      if (!shipment || typeof shipment !== "object") {
         await $.respond({
         immediate: true,
         status: 400,
         headers: { "Content-Type": "application/json" },
         body: { error: "Missing or invalid shipment" },
         });
         return;
      }
   
      const rates = [
         {
         service_code: "mock_standard",
         service_name: "Mock Standard",
         carrier_friendly_name: "Mock Carrier",
         shipping_amount: { amount: 5.99 },
         shipment_cost: 5.99,
         cost: 5.99,
         },
         {
         service_code: "mock_express",
         service_name: "Mock Express",
         carrier_friendly_name: "Mock Carrier",
         shipping_amount: { amount: 12.99 },
         shipment_cost: 12.99,
         cost: 12.99,
         },
      ];
   
      await $.respond({
         immediate: true,
         status: 200,
         headers: { "Content-Type": "application/json" },
         body: { rates },
      });
   },
   });
   ```

1. Cliquez sur **Déployer**.

   ![Étape Pipedream Code avec script de taux d’expédition simulés](../assets/mock-api-code-step.png){width="600" zoomable="yes"}

La simulation renvoie deux options de taux (Simulation standard et Simulation express) pour toute requête valide qui inclut un en-tête de `API-Key` non vide et un objet `shipment`. Vous configurerez la clé API dans la [!DNL Commerce Admin] plus loin dans ce tutoriel. Vous spécifiez également l’URL du workflow Pipedream sur le même écran de configuration. Prenez-en donc note.

## Développement d’extension

Cette section vous guide tout au long du développement d’une extension de méthode d’expédition pour [!DNL Adobe Commerce as a Cloud Service] à l’aide du [kit de démarrage pour la commande](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} et des outils de développement assistés par l’IA.

1. Accédez aux paramètres MCP dans votre agent de codage. Par exemple, dans Cursor, accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Vérifiez que l&#39;ensemble d&#39;outils `commerce-extensibility` est activé sans erreur. Si des erreurs s’affichent, désactivez la palette d’outils et activez-la.

   ![Paramètres de l’IDE du curseur affichant le jeu d’outils d’extensibilité de commerce MCP activé](../assets/cursor-settings-shipping.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Lorsque vous utilisez des outils de développement assistés par l’IA, attendez-vous à des variations naturelles du code et des réponses générées par l’agent.
   >
   >Si vous rencontrez des problèmes avec votre code, vous pouvez toujours demander à l’agent de vous aider à le déboguer.

1. Si de la documentation est ajoutée au contexte du curseur, désactivez-la. Accédez à [!UICONTROL **Curseur**] > [!UICONTROL **Paramètres**] > [!UICONTROL **Paramètres du curseur**] > [!UICONTROL **Indexation et documents**] et supprimez toute documentation répertoriée.

   ![Indexation du curseur et paramètres des documents avec la liste de documentation vide](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Donnez à l’agent l’accès à la spécification de l’API de taux simulés afin qu’il puisse implémenter correctement le client. Si vous ne l’avez pas déjà fait, téléchargez le [fichier de spécification de l’API de taux simulés](../assets/mock-rates-api-spec.zip), ouvrez-le et ajoutez le fichier `.md` à votre projet (par exemple, `docs/mock-rates-api-spec.md`), puis référencez ce fichier dans votre invite.

1. Générez l’extension du mode d’expédition :

   - Dans la fenêtre de conversation de l’agent, sélectionnez le mode **Planifier**, le cas échéant. Cela empêche l’agent de procéder sans plan.
   - Saisissez l’invite suivante :

   ```shell-session
   Build an Adobe Commerce extension that adds a shipping method at checkout. The rates come from an external mock shipping rates service: the merchant configures the service's URL and API key in Admin, and at checkout the extension asks that service for rates and shows the returned options to the customer.
   
   External service (mock shipping rates API):
   - The service endpoint URL is configurable by the merchant (for example https://123456.m.pipedream.net).
   - The API is specified in ./docs/mock-rates-api-spec.md.
   
   The merchant must be able to configure the following in the Adobe Commerce Admin UI. Use the Adobe Commerce Admin UI SDK (or equivalent App Builder extensibility options for the Admin) to add a configuration screen where the merchant can set:
   - The service URL (where the extension sends rate requests).
   - An API key the service expects (any non-empty value for the mock). The API key is sensitive data: it must be stored securely and must never appear in logs, error messages, or in the UI in full (e.g. mask in the UI).
   - The warehouse (ship-from) address: name, phone, street, city, state, postal code, country. This is the origin used when requesting rates.
   ```

   >[!NOTE]
   >
   >Si l’agent demande à rechercher la documentation, autorisez-la.

   ![Fenêtre de conversation du curseur en mode Agent avec invite d’extension d’expédition saisie](../assets/enter-prompt-shipping.png){width="600" zoomable="yes"}

1. Répondez précisément aux questions de l’agent pour l’aider à générer le meilleur code. Si l’agent demande le kit ou le modèle à utiliser, redirigez-le vers le [kit de démarrage de passage en caisse](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} avec le domaine d’expédition et l’extension SDK de l’interface utilisateur d’administration, de sorte que le webhook d’expédition et l’écran de configuration du commerçant soient mis en œuvre.

   L’agent peut créer un fichier `requirements.md` (ou équivalent) qui sert de source de vérité pour l’implémentation.

1. Consultez le fichier `requirements.md` (ou équivalent) et vérifiez le plan. Si tout semble correct, demandez à l&#39;agent de passer à la planification de l&#39;architecture (ou **Phase 2**). Confirmez que :

   - Une action **shipping-methods** (ou équivalente) gère le webhook Commerce et appelle l’API des taux externes.
   - Une action **shipping-config** (ou équivalente) prend en charge GET (lecture de la configuration, clé d’API masquée) et SET (enregistrement de l’URL du service, clé d’API, adresse d’entrepôt de données), avec la configuration stockée en toute sécurité, par exemple à l’état d’exécution.
   - L’interface utilisateur d’administration comprend un onglet **Simulation d’expédition** (ou similaire) avec des champs pour l’URL du service, la clé API (mot de passe/masqué) et l’adresse de l’entrepôt de données.

   ![Fichier d’exigences créé par l’agent AI avec les détails d’implémentation de l’extension d’expédition](../assets/requirements-file-shipping.png){width="600" zoomable="yes"}

1. Examinez le plan d’architecture lorsque l’agent le fournit.

   Plan de mise en œuvre de l’agent ![AI pour l’extension des tarifs d’expédition simulés](../assets/implementation-plan-shipping.png){width="600" zoomable="yes"}

1. Demandez à l’agent de poursuivre la génération du code. L’agent doit ajouter un transporteur **simulé** à la configuration des transporteurs, ce qui permet à Commerce d’accepter les méthodes renvoyées et d’utiliser la méthode webhook `plugin.magento.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` (type webhook **after**, obligatoire **facultatif**).

   L’agent génère le code nécessaire et fournit un résumé détaillé des étapes suivantes (y compris l’installation des dépendances, l’enregistrement du transporteur simulé, la configuration du Webhook Commerce et le déploiement).

   ![Résumé du code généré et implémentation pour l’extension d’expédition](../assets/code-generation-summary-shipping.png){width="600" zoomable="yes"}

   ![Étapes suivantes de l’agent AI pour installer, configurer webhook et déployer l’extension shipping](../assets/next-steps-shipping.png){width="600" zoomable="yes"}

### Nettoyage avant déploiement

Avant le déploiement, supprimez le code dont l’application n’a pas besoin. Le kit de démarrage de passage en caisse peut inclure des domaines inutilisés (par exemple, paiement, taxe ou événements) et une génération de modèles automatique. Demandez à l&#39;agent de les supprimer et de ne conserver que les pièces d&#39;expédition et de [!DNL Admin UI] en utilisant une invite telle que :

```shell-session
Proceed with Phase 5 cleanup.
```

L’agent génère un rapport de nettoyage, supprime les actions, configurations et scripts inutilisés et met à jour le projet. Effectuez cette étape avant le déploiement.

![Rapport de nettoyage de la phase 5 de l’agent AI affichant les composants supprimés et conservés](../assets/cleanup-report-shipping.png){width="600" zoomable="yes"}

### Déployer l’extension

1. Après avoir vérifié le code généré, déployez l’extension à l’aide de l’invite suivante :

   ```shell-session
   Deploy the app.
   ```

   L’agent effectue une évaluation du niveau de préparation avant le déploiement (par exemple, en vérifiant la `.env` des variables `COMMERCE_WEBHOOKS_PUBLIC_KEY`, `COMMERCE_BASE_URL` et OAuth/IMS si l’interface utilisateur d’administration ou l’API Commerce est utilisée).

   ![Préparation au prédéploiement de l’agent AI et étapes de déploiement pour l’extension Simulation d’expédition](../assets/pre-deployment-assessment-shipping.png){width="600" zoomable="yes"}

1. Lorsque vous êtes certain des résultats de l’évaluation, demandez à l’agent de procéder au déploiement. L’agent utilise la boîte à outils MCP pour vérifier, créer et déployer automatiquement.

   ![Sortie de déploiement de la boîte à outils MCP avec les packages déployés et l’URL webhook pour l’extension d’expédition](../assets/deployment-process-shipping.png){width="600" zoomable="yes"}

### Après le déploiement

Après le déploiement, effectuez les étapes suivantes pour enregistrer l’opérateur simulé, configurer le webhook et le [!DNL Admin UI], puis vérifiez l’extension lors du passage en caisse.

1. **Enregistrez l’opérateur simulé dans Commerce** (exécutez-le une fois après le déploiement) :

   ```bash
   npm run create-shipping-carriers
   ```

   Assurez-vous que votre `.env` dispose de `COMMERCE_BASE_URL` et d’informations d’identification OAuth/IMS valides, de sorte que le script puisse enregistrer l’opérateur.

1. **Configuration du webhook d’expédition dans [!DNL Commerce Admin]:**

   - Accédez à **Magasins** > Paramètres > **Configuration** > **Services Adobe** > **Webhooks Commerce**.
   - Ajoutez un webhook :
      - **Méthode Webhook :** `plugin.magento.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`
      - **Type de Webhook :** **after**
      - **URL :** URL d’action web **shipping-methods** déployée (à partir de la sortie de déploiement ou de la [!DNL Adobe Developer Console]).
      - **Obligatoire :** **Facultatif** - Cela permet à l’extraction de continuer à fonctionner si l’API externe ne renvoie aucun taux.

   ![Configuration du webhook d’administration de Commerce pour les taux d’expédition simulés](../assets/admin-webhook-shipping.png){width="600" zoomable="yes"}

1. **Configurer l’extension [!DNL Admin UI SDK] :**

   - Dans [!DNL Commerce Admin], accédez à **Magasins** > Paramètres > **Configuration**.
   - Ouvrez **Adobe Services** > **Admin UI SDK**.
   - Définissez **Activer Admin UI SDK** sur **Oui** et cliquez sur **Enregistrer la configuration** s’il n’est pas déjà activé.
   - Cliquez sur **Configurer les extensions**, choisissez l’espace de travail sur lequel votre application est déployée, puis cliquez sur **Appliquer**. Vous pouvez également sélectionner l’option **Personnalisé** et saisir le nom de l’espace de travail.
   - Sélectionnez l’application [!DNL App Builder] dans la liste et enregistrez-la. Si l’application n’apparaît pas, cliquez sur **Actualiser les enregistrements** et réessayez.

   ![SDK de l’interface utilisateur d’administration configure la fenêtre modale des extensions avec l’espace de travail et la sélection des extensions](../assets/admin-ui-configure-extensions.png){width="600" zoomable="yes"}

1. **Configurez la méthode d’expédition simulée dans l’interface utilisateur d’administration d’Adobe Commerce :**
   - Ouvrez **Applications** et sélectionnez votre application.
   - Ouvrez l’onglet **Expédition simulée** (ou l’équivalent).
   - Saisissez les informations suivantes :
      - **URL du service :** l’URL du workflow Pipedream que vous avez copiée (par exemple, `https://123456.m.pipedream.net`).
      - **Clé API :** toute valeur non vide pour la simulation, par exemple `tutorial-key`.
      - **Adresse de l’entrepôt de données (d’expédition) : nom** téléphone, rue, ville, État, code postal, pays.
   - Cliquez sur **Enregistrer**. La configuration est stockée dans l’état d’exécution et est utilisée par l’action shipping-methods.

   ![Formulaire de configuration d’expédition simulé avec URL de service, clé API et adresse d’entrepôt](../assets/admin-ui-mock-shipping.png){width="600" zoomable="yes"}

1. **Vérifier au passage en caisse :** ajoutez un produit au panier, accédez au passage en caisse et saisissez une adresse de livraison. Vous devriez voir les options d’expédition simulées, par exemple **Simulation standard** et **Simulation express**.

   ![Page de passage en caisse affichant les options d’expédition simulée de l’API de taux externes](../assets/checkout-mock-shipping.png){width="600" zoomable="yes"}

### Dépannage

- **La configuration n’est pas enregistrée dans l’interface utilisateur d’administration :** si vous voyez « La réponse n’est pas valide « message/http » ou que les valeurs ne se mettent pas à jour après l’enregistrement, vérifiez les journaux d’activation d’exécution pour l’action de configuration à l’aide d’une commande similaire à la suivante :

  ```bash
  aio app logs --action CustomMenu/shipping-config --limit 20
  ```

  Les causes courantes incluent le fait que la passerelle s’attend à un format de réponse spécifique (par exemple, un corps et un `Content-Type: application/json` de chaîne) ou que la bibliothèque d’états requiert des valeurs de chaîne. Assurez-vous que l’action stocke la configuration sous forme de chaîne et l’analyse lors de la lecture et que l’action shipping-methods utilise la même analyse. Consultez le ou les journaux de l’agent pour connaître la cause exacte et la solution.

- **« La réponse doit contenir au moins une opération »** (dans les journaux webhook) : Commerce exige que le webhook d’expédition renvoie au moins une opération. Demandez à l’agent de s’assurer que l’action shipping-methods ne renvoie jamais un tableau d’opérations vide (par exemple en renvoyant un taux de secours lorsque l’API externe ne renvoie aucun taux).

- **Aucun taux d’expédition au passage en caisse :** vérifiez que l’URL du webhook et la méthode sont correctes, que le transporteur simulé est enregistré (`npm run create-shipping-carriers`) et que la configuration de l’expédition simulée est définie dans le [!DNL Admin UI]. Vérifiez les journaux d’exécution pour l’action des méthodes d’expédition pour les erreurs d’API ou de validation, assurez-vous que l’action renvoie au moins une opération, de sorte [!DNL Commerce] n’affiche pas « La réponse doit contenir au moins une opération ».

### Résumé du tutoriel

Voici un résumé des sujets abordés dans ce tutoriel :

- **Conditions préalables et configuration :** vérification des outils et création de l’API de taux d’expédition simulés.
- **Développement piloté par les agents :** à l’aide de l’ensemble d’outils d’extensibilité de Commerce pour générer les exigences, un plan d’implémentation et le code du webhook d’expédition et de l’interface utilisateur d’administration.
- **Nettoyage de la phase 5 :** suppression des domaines inutilisés du kit de démarrage de passage en caisse et de la génération de modèles automatique avant le déploiement.
- **Déploiement :** évaluation préalable au déploiement et déploiement de la boîte à outils MCP.
- **Configuration post-déploiement :** enregistrement du transporteur simulé, configuration du webhook [!DNL Commerce], activation de l’extension [!DNL Admin UI SDK] et définition de l’envoi simulé (URL de service, clé d’API, entrepôt de données) dans le [!DNL Admin UI].
- **Vérification :** la confirmation des options d’expédition simulée s’affiche lors du passage en caisse.

### Étapes suivantes

Pour tester davantage ce tutoriel, tenez compte des points suivants :

- Automatisez la configuration post-déploiement avec un hook qui enregistre le transporteur simulé en [!DNL Commerce] et configure le webhook d’expédition après chaque déploiement.
- Pointez l’extension sur une API de frais de livraison réels en modifiant l’URL du service et la clé d’API dans la [!DNL Admin UI] .
- Étendez la [!DNL Admin UI] pour afficher le statut de l&#39;opérateur ou tester la connectivité au service Tarifs.
