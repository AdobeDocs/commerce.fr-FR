---
title: Tutoriel sur l’extension Product Reviews
description: Découvrez comment créer des révisions de produit et une extension de questions/réponses pour Adobe Commerce as a Cloud Service à l’aide d’App Builder, de Edge Delivery Services et d’outils de développement assistés par l’IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 9c76bae29c05909406a40ca03a2b3d242db05f3f
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---

# Tutoriel sur l’extension des révisions de produits

Ce tutoriel vous guide tout au long de la création d’une extension qui permet aux clients de soumettre du contenu de révision de produit et de questions-réponses (Q&amp;R) pour les storefronts avec un serveur principal [!DNL Adobe Commerce as a Cloud Service] à l’aide d’outils de développement [!DNL Adobe App Builder] et assistés par l’IA. L’extension fournit des points d’entrée de l’API REST aux acheteurs pour qu’ils visualisent et envoient le contenu de la révision du produit et des questions/réponses et l’affichent sur la page des détails du produit (PDP).

Vous créez deux parties :

- **Extension App Builder** — Une API REST avec des opérations GET et POST pour créer et afficher du contenu de révision de produit et de questions/réponses avec validation, pagination et persistance dans `aio-lib-state`.
- **Intégration de Storefront** — Un bloc de révision de produit sur le PDP qui affiche les révisions et les questions/réponses, avec des formulaires permettant aux acheteurs de soumettre des révisions, des questions et des réponses.

>[!NOTE]
>
>Les agents de l’IA sont non déterministes. Les invites, questions et sorties de ce tutoriel sont des exemples. Votre agent peut formuler différentes questions, exigences ou propositions d’architecture. Utilisez les exemples de ce tutoriel pour diriger l’agent vers un résultat similaire.

Avant de commencer, renseignez les [conditions préalables](./tutorial-prerequisites.md). Ce tutoriel utilise le **kit de démarrage d’intégration**. Vérifiez que vous l’avez déjà cloné et effectuez les étapes de configuration décrites sur la page des conditions préalables.

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

Si l’une des commandes précédentes ne renvoie pas les résultats attendus, consultez les [conditions préalables](./tutorial-prerequisites.md) pour obtenir des conseils.

Vérifiez également les éléments suivants :

- Vous disposez d’une instance [!DNL Adobe Commerce as a Cloud Service] avec des données de produit. Voir [Instances du service Commerce Cloud](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}.
- Un projet de storefront est connecté à votre instance [!DNL Commerce]. Si vous n’en avez pas, suivez les étapes de la section [Créer un storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}.
- L’interface de ligne de commande `aem` est installée :

  ```bash
  npm install -g @adobe/aem-cli
  ```

## Développement d’extension

Cette section vous guide tout au long du développement d’une extension pour envoyer et afficher la révision du produit et le contenu des questions/réponses pour l’extension des storefronts avec un serveur principal [!DNL Adobe Commerce as a Cloud Service] à l’aide d’outils de développement assistés par l’IA. L’extension fournit une API REST pour envoyer et afficher la révision du produit et le contenu des questions/réponses, et pour l’afficher sur le PDP.

1. Accédez aux paramètres MCP dans votre agent de codage. Par exemple, dans Cursor, accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Vérifiez que l&#39;ensemble d&#39;outils `commerce-extensibility` est activé sans erreur. Si des erreurs s’affichent, désactivez la palette d’outils et activez-la.

   >[!NOTE]
   >
   >Lorsque vous utilisez des outils de développement assistés par l’IA, attendez-vous à des variations naturelles du code et des réponses générées par l’agent.
   >Si vous rencontrez des problèmes avec votre code, demandez à l’agent de vous aider à le déboguer.

1. Si de la documentation est ajoutée au contexte du curseur, désactivez-la.

   Accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** et supprimez toute documentation répertoriée.

### Étape 1 : fournir l’invite initiale

Demandez à l’agent AI de commencer l’implémentation. Indiquer à l’agent d’arrêter et de poser des questions vous aide à piloter l’implémentation au plus tôt.

Saisissez l’invite suivante dans la fenêtre de conversation de l’agent :

```shell-session
I want to build an Adobe Commerce as a Cloud Service extension that allows shoppers to submit and view product review and question and answer (Q&A) content that displays on product detail pages (PDP).

## Product Reviews
The application has REST API endpoints that can be called by a storefront to retrieve and submit product reviews for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch reviews for
- limit (integer, optional): The maximum number of reviews to return (default: 10)
- offset (integer, optional): The number of reviews to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a review for
- rating (integer, required): The rating for the product (1-5)
- review (string, optional): The text of the review
- user (string, optional): The name of the user submitting the review

The POST endpoint validates the input and returns appropriate error responses for invalid data. The reviews are stored and associated with the corresponding product SKU.

## Questions and Answers
The application has REST API endpoints that can be called by a storefront to retrieve and submit questions and answers for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch questions and answers for
- limit (integer, optional): The maximum number of questions and answers to return (default: 10)
- offset (integer, optional): The number of questions and answers to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a question or answer for
- type (string, required): The type of submission ("question" or "answer")
- questionId (string, required if type is "answer"): The ID of the question being answered
- content (string, required): The text of the question or answer
- user (string, optional): The name of the user submitting the question or answer

The POST endpoint validates the input and returns appropriate error responses for invalid data. The questions and answers are stored and associated with the corresponding product SKU. Answers are also associated with the corresponding question.

Do not require Adobe IMS authentication for these endpoints. They will be called directly from the storefront.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>Indiquer à l’agent d’ARRÊTER et de poser des questions avant de continuer vous aide à piloter l’implémentation au début du processus. Cela permet de s’assurer que les hypothèses clés et les exigences manquantes sont identifiées rapidement. Cela est nécessaire pour lancer le workflow guidé dans ce tutoriel.

### Étape 2 : Répondre aux questions de l&#39;agent

L’agent revient avec une série de questions auxquelles il doit répondre avant de pouvoir commencer à former une solution. L’exemple suivant illustre des questions et réponses standard. Votre agent peut poser des questions différentes, mais les sujets sont généralement les mêmes.

**Exemples de questions sur l’agent :**

1. **API REST — hôte et consommateurs** — L’API REST CRUD doit-elle faire partie de cette application App Builder (actions web sur Adobe I/O Runtime) que storefronts appelle ? Qui l’appellera (storefront EDS, storefront personnalisé/découplé, ou les deux) ? Avez-vous besoin d’un accès CORS ou public (non authentifié), ou les appelants utiliseront-ils des clés API ou OAuth ?
1. **Modèle de données** — Que doit représenter un « examen » ou une « question » ? Identifiant client (e-mail uniquement ou également identifiant client) ? Identifiant du produit (SKU uniquement ou SKU + vue magasin) ? Un même client peut-il soumettre plusieurs avis pour le même SKU ?
1. **Persistance** — Est-`aio-lib-state` l’endroit approprié pour conserver les révisions et les questions/réponses, ou disposez-vous d’un magasin externe ? La conception doit-elle prendre en compte plusieurs clients ou un seul client ?
1. **Sémantique de pagination** — Pour le GET des questions-réponses, s’applique-t-`limit` uniquement aux questions (avec des réponses imbriquées) ou au nombre total de questions plus réponses ?

**Exemples de réponses :**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>Votre agent peut poser différentes questions. Utilisez ces réponses comme conseils pour diriger l’agent vers le même résultat fonctionnel : une API REST publique avec des révisions et des questions/réponses, une persistance du `aio-lib-state` et aucune authentification.

### Étape 3 : examen des exigences et de l’architecture

L’agent génère des documents relatifs aux exigences et à l’architecture que vous pouvez consulter. Vérifiez que les exigences correspondent aux réponses que vous avez fournies et que l’architecture couvre :

- Quatre actions web : `reviews-get`, `reviews-post`, `qa-get`, `qa-post`
- Persistance à l’aide de `aio-lib-state` avec des clés conformes au modèle autorisé (`[a-zA-Z0-9-_.]` — pas de deux-points)
- Valeurs d’état stockées sous forme de chaînes JSON (et non d’objets ou de tableaux bruts)
- Package autonome : code partagé (utils, constantes) à l’intérieur du package `product-reviews`, et non via les chemins d’accès `../../` qui échappent au lot

>[!NOTE]
>
>Les agents d’IA sont non déterministes et leurs comportements diffèrent selon le modèle et l’IDE. Vous pouvez obtenir un ensemble différent de questions qui génère un ensemble différent d’exigences et d’architecture. Si tel est le cas, essayez d’orienter l’agent dans la direction afin que l’implémentation corresponde étroitement à ce qui est présenté dans ce tutoriel avant de continuer.

### Étape 4 : sélection d’un plan de mise en œuvre

L’agent vous donne la possibilité de créer un plan d’implémentation détaillé ou d’effectuer une implémentation directe.

- Si vous souhaitez un plan révisable que vous pouvez exécuter par phases avec plus de contrôle, sélectionnez la première option.
- Si vous souhaitez que l’agent effectue l’implémentation complète avec une intervention minimale, sélectionnez la deuxième option.

### Étape 5 : déployer l’extension

Une fois l’implémentation de l’agent terminée, déployez l’extension :

```bash
aio app deploy
```

Si l’agent a ajouté des `require-adobe-auth: true` aux actions, demandez-lui de supprimer l’authentification afin que les points d’entrée puissent être appelés directement à partir du storefront :

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

Redéployez ensuite :

```bash
aio app deploy
```

### Étape 6 : créer des données simulées et pré-remplir pour les tests

Créez un fichier de données simulé et utilisez la commande curl pour pré-remplir l’API afin d’avoir un exemple de contenu de révision et de questions/réponses pour les tests dans l’interface de ligne de commande et le storefront.

1. Créez un fichier `docs/mock-product-reviews-data.json` (ou similaire) avec des exemples de données. Par exemple :

   ```json
   {
     "reviews": [
       { "sku": "ADB153", "rating": 5, "review": "Great product, highly recommend!", "user": "shopper@example.com" },
       { "sku": "ADB153", "rating": 4, "review": "Good value for money.", "user": "buyer@example.com" }
     ],
     "questions": [
       { "sku": "ADB153", "type": "question", "content": "Does this come in other colors?", "user": "curious@example.com" }
     ]
   }
   ```

1. Utilisez curl pour PUBLIER les données dans l’API déployée.

   Remplacez `<your-runtime-url>` par l’URL d’exécution d’App Builder actuelle (par exemple, `https://1172492-prodreviewqa135-stage.adobeioruntime.net`) :

   ```bash
   API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
   
   # Submit reviews
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":5,"review":"Great product, highly recommend!","user":"shopper@example.com"}'
   
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":4,"review":"Good value for money.","user":"buyer@example.com"}'
   
   # Submit a question (save the returned id for the answer)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"question","content":"Does this come in other colors?","user":"curious@example.com"}'
   
   # Submit an answer (replace <QUESTION-UUID> with the id from the question response)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it comes in blue and red.","user":"seller@example.com"}'
   ```

1. Vérifiez les données avec les requêtes GET :

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>Utilisez les `ADB153` de SKU pour un produit qui comporte à la fois des révisions et des questions/réponses, ainsi que des `ADB152` pour un produit sans révision. Cette configuration de données permet de tester les états renseignés et vides dans le storefront.

### Étape 7 : tester l’extension

Demandez à l’agent de fournir des étapes de test ou utilisez les exemples de curl de l’étape précédente. Les exemples suivants présentent des commandes de test standard.

**Envoyer un commentaire :**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**Liste des révisions :**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**Poser une question :**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**Envoyez une réponse** (utilisez le `id` de la réponse à la question comme `questionId`) :

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### Créer le contrat de service

Maintenant que l’implémentation du service est terminée, demandez à l’agent de créer un contrat de service pour le travail de storefront :

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

Copiez ce fichier dans votre projet storefront afin que l’agent storefront puisse le référencer.

## Connexion au storefront

Cette section vous guide tout au long de l’implémentation de la partie storefront des révisions de produit et de l’extension de questions/réponses à l’aide d’outils de développement assistés par [!DNL Edge Delivery Services] et IA. Vous ajoutez un bloc de révision de produit au PDP qui affiche le contenu de la révision et des questions/réponses, et permet aux acheteurs d’envoyer un nouveau contenu.

>[!NOTE]
>
>Les invites fournies sont des points de départ. Bien que vous puissiez les utiliser sans modification, pensez à avoir une conversation naturelle avec l&#39;agent.
>
>Lorsque vous utilisez des outils de développement assistés par l’IA, il existe toujours des variations naturelles dans le code et les réponses générés par l’agent.
>
>Si vous rencontrez des problèmes avec votre code, demandez à l’agent de vous aider à le déboguer.

### Conditions préalables requises pour Storefront

Avant de démarrer l’intégration du storefront, vérifiez que vous disposez des éléments suivants :

- Un projet de storefront connecté à votre instance [!DNL Commerce]
- Outils d’IA pour storefront Commerce [installés à l’aide de l’interface de ligne de commande](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- Le fichier `PRODUCT_REVIEW_QA_CONTRACT.md` copié dans votre projet de storefront

### Étape 1 : valider l’environnement

Ouvrez votre fichier `config.json` et vérifiez que les valeurs de `commerce-core-endpoint` et `commerce-endpoint` pointent vers votre point d’entrée GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Étape 2 : fournir l’invite initiale

Le contrat de service étant déjà dans votre projet, demandez à l’agent de mettre en œuvre le bloc de révision du produit. Utilisez le mode **Plan** s’il est disponible dans votre agent, pour empêcher l’agent de continuer sans plan.

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>Le fait de demander spécifiquement à utiliser la compétence de chef de projet déclenche le workflow par phases qui vous aide à diriger la mise en œuvre. Cela permet de s’assurer que les hypothèses clés et les exigences manquantes sont identifiées tôt dans le processus.

### Étape 3 : Répondre aux questions de clarification

L’agent revient avec une série de questions auxquelles il doit répondre avant de pouvoir commencer à former une solution. L’exemple suivant illustre des questions et réponses standard. Votre agent peut poser des questions différentes, mais les sujets sont généralement les mêmes.

**Exemples de questions sur l’agent :**

1. **URL de base de l’API** — Comment le storefront doit-il obtenir l’URL de base de l’API product-views ? Les options peuvent inclure un bloc de configuration (par exemple, un tableau avec des `apiBaseUrl`), des espaces réservés globaux ou une autre approche.
1. **Source SKU** — Le bloc doit-il lire le SKU à partir du contexte PDP (produit actuel) ou de la configuration du bloc ?
1. **Comportement du formulaire** — Après un envoi réussi, le formulaire doit-il être masqué, afficher un message de réussite ou rester visible mais désactivé ?

**Exemples de réponses :**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>Remplacez l’espace réservé dans la configuration de bloc par votre URL d’exécution App Builder actuelle (par exemple, `https://1172492-prodreviewqa135-stage.adobeioruntime.net`).
>
>Votre agent peut poser différentes questions. Utilisez ces réponses comme conseils :
>
>- L’URL de base de l’API doit provenir du tableau de blocs afin qu’elle puisse être modifiée sans modification de code.
>- SKU du tableau des blocs s’il est défini ; sinon du produit actuel sur le PDP.
>- Après un envoi réussi, affichez un message de réussite et désactivez le formulaire.

### Étape 4 : examen des exigences et de l’architecture

L’agent met à jour le document des exigences que vous pouvez examiner. Vérifiez que :

- Le bloc effectue le rendu des révisions (avec évaluation, utilisateur, date, texte) et des questions/réponses (questions avec réponses imbriquées).
- Forms permet d’envoyer des révisions, des questions et des réponses.
- La pagination est prise en charge pour le contenu de révision et de questions/réponses.
- L’intégration de l’API utilise l’URL de base du tableau de blocs.
- Les états de réussite et d’erreur sont gérés conformément au contrat.

>[!NOTE]
>
>Les agents d’IA sont non déterministes et leurs comportements diffèrent selon le modèle et l’IDE. Vous pouvez obtenir un ensemble différent de questions qui génère un ensemble différent d’exigences et d’architecture. Si tel est le cas, essayez d’orienter l’agent dans la direction afin que l’implémentation corresponde étroitement à ce qui est présenté dans ce tutoriel avant de continuer.

### Étape 5 : sélection d’un plan de mise en œuvre

L’agent vous donne la possibilité de créer un plan d’implémentation détaillé ou d’effectuer une implémentation directe.

- Si vous souhaitez un plan révisable que vous pouvez exécuter par phases avec plus de contrôle, sélectionnez la première option.
- Si vous souhaitez que l’agent effectue l’implémentation complète avec une intervention minimale, sélectionnez la deuxième option.

Pendant l’implémentation, l’agent crée et modifie les fichiers de bloc. Regardez le code en cours de génération et posez des questions ou redirigez l’agent si nécessaire. Si le bloc ne s’affiche pas, demandez à l’agent d’analyser la décoration de la section et le motif de découverte de blocs ; l’élément de bloc doit être un enfant direct de la section pour que le framework puisse le trouver.

### Étape 6 : ajouter le bloc à la page produit dans la création de documents

Ajoutez le bloc de révision du produit au modèle de page produit afin qu’il apparaisse sur tous les PDP. Utilisez le service de création de documents (da.live) pour ajouter et configurer le bloc.

1. Ouvrez votre service de création de documents, par exemple [da.live](https://da.live/)

1. Cliquez sur l’espace de votre projet, ouvrez le dossier **products** et sélectionnez **default** (`products/default`).

1. Ajoutez une nouvelle section de bloc.

   Dans le tableau des blocs, ajoutez une ligne portant le nom de bloc **product-review** (ou le nom de bloc créé par votre agent).

1. Configurez le bloc avec les paramètres requis :
   - **apiBaseUrl** — Votre URL d’exécution App Builder (par exemple, `https://<namespace>-<app-name>-stage.adobeioruntime.net`).
   - **sku** — Laissez ce champ vide pour utiliser le SKU du produit actuel sur le PDP ou saisissez un SKU spécifique pour afficher uniquement les avis pour ce produit.

1. Cliquez sur **[!UICONTROL Publish]** pour publier vos modifications.

### Étape 7 : démarrer le serveur et effectuer le test

Après avoir ajouté le bloc à la page de produit dans la création de documents, démarrez le serveur de développement et testez le bloc.

1. Démarrez le serveur de développement local :

   ```bash
   npm run start
   ```

1. Dans un navigateur, accédez à une page de produit qui contient des révisions et des questions/réponses préremplies. Par exemple :

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. Vérifiez que le bloc de révision du produit affiche les révisions et le contenu des questions/réponses, et que les formulaires d’envoi fonctionnent.

Vous pouvez effectuer des tests manuels ou demander à l’agent d’utiliser ses fonctionnalités de navigateur pour effectuer des tests à votre place :

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### Étape 8 : Nettoyage

Après avoir ignoré ou terminé le test, l’agent vous invite à passer à la phase finale **Nettoyage**. Après confirmation, l’agent archive tous les artefacts de documentation créés lors de l’implémentation.

## Dépannage

Suivez les conseils suivants si vous rencontrez des problèmes au cours du tutoriel.

### Serveur principal (App Builder)

| Symptôme | Cause | Correctif |
|---------|-------|-----|
| GET ou POST renvoie 500 « Impossible de trouver le module » | Les actions de révisions de produits utilisent `require("../../utils")` ou `require("../../constants")`, ce qui permet d’échapper le lot du package. Ces fichiers ne sont pas inclus lorsque le package est déployé. | Rendre le package d’avis de produits autonome. Ajoutez des `actions/product-reviews/lib/constants.js` et des `actions/product-reviews/lib/utils.js`, et mettez à jour les quatre actions à exiger de `../lib/...` au lieu de `../../`. |
| GET renvoie 500 avec « la clé doit correspondre au modèle » | Les clés d’état utilisent les deux-points (par exemple, `reviews:ADB153`). `aio-lib-state` autorise uniquement les `[a-zA-Z0-9-_.]`. | Remplacez les préfixes `reviews:` et `qa:` par `reviews.` et `qa.`. Ajoutez un assistant `stateKey(prefix, sku)` qui assainit le SKU (remplacez les caractères non valides par des `_`). |
| POST renvoie 500 avec « la valeur doit être une chaîne » | `aio-lib-state` accepte uniquement les valeurs de chaîne. Le code transmet des tableaux ou des objets à `state.put()`. | Sérialisez avec `JSON.stringify()` lors de l’écriture et `JSON.parse()` lors de la lecture. Mettez à jour les quatre actions. |

{style="table-layout:auto"}

### Storefront (Edge Delivery Services)

| Symptôme | Cause | Correctif |
|---------|-------|-----|
| Le bloc n’est pas rendu sur la page de test. | L’élément de bloc est imbriqué dans un `div` supplémentaire, de sorte qu’après `decorateSections` le sélecteur de bloc (`div.section > div > div`) ne correspond pas. | Faire du bloc un enfant direct de la section. Structure : `section > div.product-review` (ou classe de bloc équivalente). Évitez les `section > div > div.product-review`. |
| Jetons CSS non valides | Le bloc utilise des jetons de conception qui n’existent pas dans `styles/styles.css` (par exemple, `--color-error-100`, `--type-detail-font-size`). | Demandez à l’agent de valider les jetons par rapport au `styles/styles.css` du projet et de remplacer les jetons non valides par des jetons existants (par exemple, `--color-alert-*`, `--type-details-caption-*`). |

{style="table-layout:auto"}

## Résumé du tutoriel

Voici un résumé des sujets abordés dans ce tutoriel :

- **Développement d’extensions :** description de la fonctionnalité de création et d’affichage de contenu de révision de produit et de questions/réponses sur un storefront avec un serveur principal Adobe Commerce as a Cloud Service à un agent d’IA et de la manière d’implémenter cette fonctionnalité en générant une API REST fonctionnelle avec quatre points d’entrée à l’aide de [!DNL App Builder].
- **Persistance :** utilisation de `aio-lib-state` avec un format de clé correct et des valeurs sérialisées JSON.
- **Données simulées et pré-remplissage :** création d’un fichier de données simulées et utilisation de curl pour pré-remplir l’API pour les tests d’interface de ligne de commande et de storefront.
- **Contrats de service :** création de contrats d’API qui relient les extensions principales et les implémentations de storefront.
- **Intégration progressive du storefront :** en fonction des exigences, de l’architecture et de la mise en œuvre à l’aide de compétences assistées par l’IA.
- **Bloc PDP :** ajout d’un bloc de révision du produit au PDP qui affiche les révisions et les questions/réponses avec les formulaires d’envoi et la pagination.

## Étapes suivantes

Suivez les suggestions suivantes pour étendre votre service d’examen des produits :

- **Ajouter une modération :** implémentez un workflow de modération pour la révision et le contenu des questions/réponses avant qu’il ne soit publié.
- **Ajouter une authentification :** exiger que les acheteurs soient connectés pour envoyer des commentaires ou du contenu de questions/réponses et associer des envois à des comptes clients.
- **Ajouter une page de gestion des abonnements :** créez une page storefront où les acheteurs peuvent afficher et modifier leurs commentaires.
- **Prise en charge des déploiements à plusieurs clients :** permet d’étendre la gestion des états afin de prendre en charge plusieurs clients Commerce dans une seule application App Builder.
- **Ajouter une limite de débit :** implémentez des limites de débit sur l’API pour empêcher les abus.
