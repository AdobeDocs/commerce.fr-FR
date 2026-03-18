---
title: Tutoriel Sur L’Extension Des Estimations De Diffusion
description: Découvrez comment créer une extension d’estimations de date de diffusion pour Adobe Commerce as a Cloud Service à l’aide d’App Builder, de Edge Delivery Services et d’outils de développement assistés par l’IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3fc8982613df7b1155cdfb08ac4b56de6d1ce4f6
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 0%

---

# Tutoriel sur l’extension des estimations de diffusion

Ce tutoriel vous guide tout au long de la création d’une extension d’estimations de date de diffusion pour les [!DNL Adobe Commerce as a Cloud Service] à l’aide d’outils de développement [!DNL Adobe App Builder], [!DNL Edge Delivery Services] et assistés par l’IA. L’extension récupère les estimations de l’heure d’expédition et de la date de livraison à partir d’une API externe et les affiche sur le storefront.

Vous créez deux parties :

- **Extension App Builder** — Une action backend-for-frontend (BFF) qui enveloppe une API d’estimation de diffusion externe, un webhook qui enrichit les méthodes d’expédition avec des dates de diffusion au moment du passage en caisse, ainsi qu’une page de configuration de l’interface utilisateur d’administration pour gérer les paramètres sans redéploiement.
- **Intégration de Storefront** — Estimations de la date de diffusion affichées sur la page de détails du produit (PDP), la page du panier et la page de passage en caisse à l’aide de [!DNL Edge Delivery Services] composants de menu déroulant et d’un module client partagé.

>[!NOTE]
>
>Les agents de l’IA sont non déterministes. Les invites, questions et sorties de ce tutoriel sont des exemples. Votre agent peut formuler différentes questions, exigences ou propositions d’architecture. Utilisez les exemples de ce tutoriel pour diriger l’agent vers un résultat similaire.

Avant de commencer, renseignez les [conditions préalables](./tutorial-prerequisites.md). Ce tutoriel utilise le **kit de démarrage de passage en caisse**. Vérifiez que vous l’avez déjà cloné et effectuez les étapes de configuration décrites sur la page des conditions préalables.

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

Vérifiez également les éléments suivants :

- Vous disposez d’une instance [!DNL Adobe Commerce as a Cloud Service] avec des données de produit. Voir [Instances du service Commerce Cloud](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}.
- Un projet de storefront est connecté à votre instance [!DNL Commerce]. Si vous n’en avez pas, suivez les étapes de la section [Créer un storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}.
- L’interface de ligne de commande `aem` est installée :

  ```bash
  npm install -g @adobe/aem-cli
  ```

- Vous disposez d’un **compte client** — un client enregistré en [!DNL Commerce] avec une adresse de livraison par défaut enregistrée. Les estimations de diffusion sur les pages PDP et Panier s’affichent uniquement pour les acheteurs connectés. Le passage en caisse affiche des estimations pour tous les acheteurs, quel que soit le statut d’authentification.

>[!IMPORTANT]
>
>Ce tutoriel utilise le **Checkout Starter Kit** (et non le kit de démarrage pour l’intégration). Le kit de démarrage pour la commande offre une extensibilité basée sur un webhook pour le paiement, l’expédition, les taxes et les événements. Assurez-vous de démarrer à partir du kit de passage en caisse.

## Configurer l’API d’estimation de diffusion simulée

L’extension appelle une API externe d’estimation de diffusion pour obtenir des estimations de date et d’heure d’expédition. Pour ce tutoriel, vous utilisez une API simulée afin de pouvoir exécuter le flux complet sans compte d’opérateur réel. Deux options sont disponibles :

- **Option A : workflow Pipedream** — Niveau gratuit, configuration rapide, mais avec des limites d’appel mensuelles.
- **Option B : action App Builder Runtime** — Aucune dépendance externe, créée lors des étapes de développement du serveur principal.

>[!TIP]
>
>Pendant le développement, vous pouvez commencer par Pipedream (option A) et passer à une action d’exécution (option B) si vous atteignez le quota d’appel de niveau libre. Les deux options mettent en œuvre le même contrat d’API.

### Spécification d’API

L’API simulée accepte une requête POST et renvoie des estimations de date de diffusion avec le transporteur, les jours de transit, la date limite et une meilleure estimation.

**Corps de la requête** (tous les champs sont facultatifs pour la simulation) :

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**Réponse (200 OK) :**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**Réponses d’erreur :** 401 (clé API manquante/non valide), 400 (format d’`ship_date` non valide), 503 (temps d’arrêt simulé).

### Configurer la simulation

>[!BEGINTABS]

>[!TAB Workflow Pipedream]

L’option Pipedream utilise l’authentification par jeton porteur et accepte une requête POST à l’URL de déclenchement du workflow.

| Poste | Description |
|------|-------------|
| URL de base | L’URL complète de déclenchement du workflow Pipedream (par exemple, `https://<id>.m.pipedream.net`) |
| Authentification | `Authorization: Bearer <API_KEY>` |
| Méthode | POSTER |

{style="table-layout:auto"}

**Créez le workflow :**

1. Créez un workflow dans [Pipedream](https://pipedream.com){target="_blank"} (**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**).

1. Ajoutez un déclencheur **HTTP/Webhook** configuré pour POST. Pipedream attribue une URL webhook.

1. Ajoutez une étape **Exécuter le code Node.js** et collez le code de gestionnaire suivant :

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];
   
   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;
   
   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }
   
   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }
   
   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }
   
   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }
   
   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }
   
   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. (Facultatif) Ajoutez une variable d’environnement `MOCK_API_KEY` dans les paramètres du workflow pour appliquer l’authentification du jeton porteur. Si elle n’est pas définie, toutes les requêtes sont acceptées.

1. Déployez le workflow.

   Votre point d’entrée est l’URL de déclenchement webhook.

**Tester la simulation :**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB Action App Builder Runtime]

L’option Action d’exécution App Builder déploie la simulation en tant qu’action d’exécution dans le même projet [!DNL App Builder]. Cette approche ne comporte aucune dépendance externe et aucun quota d’appel.

Demandez à l’agent de créer l’action simulée :

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

L’agent crée des `actions/mock-delivery-api/index.js` avec le même contrat d’API que l’option Pipedream. Après le déploiement, le point d’entrée est :

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

L’authentification est validée par rapport à une variable d’environnement `MOCK_API_KEY` dans `.env`.

>[!ENDTABS]

## Développement d’extension

Cette section vous guide tout au long du développement du serveur principal [!DNL App Builder] pour l’extension des estimations de diffusion. Le serveur principal propose trois actions :

| Action | Type | Objectif |
|--------|------|---------|
| `delivery-estimates` | Action web autonome | BFF pour storefront — PDP et panier appellent ceci pour les dates de livraison |
| `shipping-methods` | Action Webhook | Enrichit les tarifs d&#39;expédition avec des dates de livraison en `additional_data` au moment du passage en caisse |
| `delivery-estimates-config` | Action Admin du serveur principal | CRUD pour la configuration stockée dans `aio-lib-state` |

{style="table-layout:auto"}

1. À partir des paramètres MCP de vos agents de codage, vérifiez que l’ensemble d’outils `commerce-extensibility` est activé sans erreur.

   Par exemple, dans Cursor, accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

   Si des erreurs s’affichent, désactivez la palette d’outils et activez-la.

   >[!NOTE]
   >
   >Lorsque vous utilisez des outils de développement assistés par l’IA, attendez-vous à des variations naturelles du code et des réponses générées par l’agent.
   >Si vous rencontrez des problèmes avec votre code, demandez à l’agent de vous aider à le déboguer.

1. Si de la documentation est ajoutée au contexte du curseur, désactivez-la.

   Accédez à **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** et supprimez toute documentation répertoriée.

### Étape 1 : fournir l’invite initiale

Donnez à l’agent la spécification d’API externe pour le contexte et demandez-lui de commencer. Indiquer à l’agent d’arrêter et de poser des questions vous aide à piloter l’implémentation au plus tôt.

Saisissez l’invite suivante dans la fenêtre de conversation de l’agent :

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>Le fait de référencer le fichier de spécification de l’API externe (`@docs/API_SPEC.md`) dans l’invite fournit à l’agent un contexte concret sur le contrat de l’API tierce. L’agent l’utilise pour concevoir l’action FFB, le client HTTP partagé et les champs de configuration de l’interface utilisateur d’administration. Indiquer à l’agent d’ARRÊTER et de poser des questions déclenche le workflow guidé et vous aide à piloter l’implémentation au plus tôt.

### Étape 2 : Répondre aux questions de l&#39;agent

L’agent renvoie une série de questions explicatives couvrant des sujets tels que l’environnement cible (PaaS ou SaaS), la portée (action autonome BFF, enrichissement webhook, ou les deux), la source de l’adresse d’origine, la stratégie de mise en cache et la préférence de test. L’exemple suivant illustre des questions et réponses standard. Votre agent peut poser des questions différentes, mais les sujets sont généralement les mêmes.

**Exemples de questions sur l’agent :**

1. **Environnement cible** — Créez-vous pour PaaS (On-Premise) ou SaaS (Adobe Commerce as a Cloud Service) ?
2. **Portée** — Doit-il s’agir d’une action BFF autonome (le storefront l’appelle directement), d’un enrichissement webhook (étendre les méthodes d’expédition au moment du passage en caisse) ou des deux ?
3. **Configurabilité de l’administration** — Les paramètres tels que l’URL de l’API, la clé API et l’adresse d’origine doivent-ils être configurables via l’administration Commerce ou stockés dans `.env` ?
4. **Adresse d&#39;origine** — D&#39;où vient l&#39;adresse d&#39;expédition (entrepôt) ? Doit-il s’agir d’une configuration statique ou résolue dynamiquement ?
5. **Mise en cache** — Les estimations de diffusion doivent-elles être mises en cache côté serveur pour réduire les appels à l’API externe ? Si oui, quelle durée de vie ?

**Exemples de réponses :**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call the 3rd party API directly — or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Let's use a Single-page application (SPA) that uses the Admin UI SDK to integrate with the admin. Since we are adding this config screen, let's make anything else that makes sense configurable to avoid redeployments when changing settings
4. Static configuration — origin address should be configurable in the Admin UI (e.g. warehouse address)
5. Yes, cache on the server side; suggest a TTL (e.g. 30 minutes) and make it configurable in the Admin UI
```

>[!TIP]
>
>Demander à l’agent si le storefront doit appeler directement l’API tierce ou passer par une action d’exécution déclenche une discussion architecturale utile. L’agent explique les avantages du modèle BFF (Backend-for-Frontend) : la clé API reste côté serveur, CORS est géré, la mise en cache est centralisée et vous obtenez une abstraction du fournisseur. Demander la configurabilité de l’interface utilisateur d’administration pousse l’agent à stocker tous les paramètres dans `aio-lib-state` au lieu de `.env`, ce qui élimine les redéploiements lors de la modification des paramètres.

>[!NOTE]
>
>Votre agent peut poser différentes questions. Utilisez ces réponses comme conseils pour orienter l’agent vers le même résultat fonctionnel : une action BFF pour les appels de storefront, un webhook des méthodes d’expédition pour l’enrichissement du passage en caisse et une page de configuration de l’interface utilisateur d’administration qui stocke les paramètres dans `aio-lib-state`.

### Étape 3 : examen des exigences et de l’architecture

L’agent génère des documents relatifs aux exigences et à l’architecture que vous pouvez consulter. Vérifiez que les exigences correspondent aux réponses que vous avez fournies et que l’architecture couvre :

- Une **action BFF** (`delivery-estimates`) : action web autonome que le storefront appelle à partir des pages PDP et du panier. Il lit la configuration à partir de `aio-lib-state`, appelle l’API d’estimation de diffusion externe et renvoie des estimations formatées.
- Une **action webhook** (`shipping-methods`) — Enrichit les frais d’expédition avec des dates de livraison en `additional_data` pendant le passage en caisse. Utilise la méthode webhook `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`.
- Une **action de configuration d’administration** (`delivery-estimates-config`) — CRUD pour la configuration (URL d’API, clé d’API, adresse d’origine, opérateurs, TTL de cache) stockée dans `aio-lib-state`.
- **Bibliothèques partagées** — Un client HTTP pour l&#39;API externe et un module de configuration pour la lecture et l&#39;écriture de `aio-lib-state`.

>[!NOTE]
>
>Les agents d’IA sont non déterministes et leurs comportements diffèrent selon le modèle et l’IDE. Vous pouvez obtenir un ensemble différent de questions qui génère un ensemble différent d’exigences et d’architecture. Si tel est le cas, essayez d’orienter l’agent dans une direction telle que l’implémentation corresponde étroitement à ce qui est présenté dans ce tutoriel avant de continuer.

### Étape 4 : sélection d’un plan de mise en œuvre

L’agent vous donne la possibilité de créer un plan d’implémentation détaillé ou d’effectuer une implémentation directe.

- Si vous souhaitez un plan révisable que vous pouvez exécuter par phases avec plus de contrôle, sélectionnez la première option.
- Si vous souhaitez que l’agent effectue l’implémentation complète avec une intervention minimale, sélectionnez la deuxième option.

### Étape 5 : nettoyage et déploiement

Une fois que l’agent a terminé l’implémentation, il procède au nettoyage. Comme seul le domaine d’expédition est en cours d’utilisation, l’agent supprime la génération de modèles automatique inutilisée :

- Actions de paiement et configuration (`validate-payment/`, `filter-payment/`, `payment-methods.yaml`)
- Actions fiscales et configuration (`collect-taxes/`, `collect-adjustment-taxes/`, `tax-integrations.yaml`)
- Actions liées aux événements et configuration (`commerce-events/`, `3rd-party-events/`, `events.config.yaml`)
- Générique de modèles automatique (`generic/`)
- Composants SPA de l’interface d’administration d’autres domaines (par exemple, pages et points d’extension liés à la taxe)
- Scripts, fichiers de test et variables d’environnement inutilisés

>[!TIP]
>
>Demandez à l’agent de vérifier également les restes d’autres domaines dans la SPA de l’interface d’administration. La page Classes d&#39;impôt et ses points d&#39;extension peuvent toujours être présents sur l&#39;échafaudage du kit de démarrage et doivent être supprimés.

Après le nettoyage, effectuez le déploiement en procédant comme suit **dans cet ordre** :

```bash
# 1. Copy env template and fill in credentials.
cp env.dist .env

# 2. Select your App Builder workspace.
aio app use --merge

# 3. Sync OAuth credentials from workspace.
npm run sync-oauth-credentials

# 4. Deploy the extension.
aio app deploy

# 5. Register shipping carriers in Commerce.
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>N’ignorez pas et ne réorganisez pas les étapes. Les étapes 1 à 3 sont des conditions préalables au déploiement. La commande `aio app deploy` échoue si aucune information d’identification n’a été configurée.

### Étape 6 : configuration du webhook et de l’interface utilisateur d’administration

Après le déploiement, configurez le webhook d’expédition. L’agent peut créer un script pour s’abonner par programmation :

```bash
npm run subscribe-webhook
```

Cette commande s’abonne au webhook d’expédition avec les paramètres suivants :

| Champ | Valeur |
|-------|-------|
| Méthode Webhook | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Type de Webhook | `after` |
| Obligatoire | Facultatif (permet de revenir à l’expédition par défaut) |
| Délai d’expiration | 5 000 ms |

{style="table-layout:auto"}

>[!NOTE]
>
>Pour SaaS, le nom de la méthode webhook est `magento.` du chemin . Le nom webhook pour PaaS est `plugin.magento.out_of_process_shipping_methods...` tandis que le nom webhook pour SaaS est `plugin.out_of_process_shipping_methods...`.

Configurez ensuite l’interface utilisateur d’administration :

1. Activez le **SDK de l’interface utilisateur d’administration** (**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**).

1. Configurez les extensions en sélectionnant votre espace de travail et votre extension [!DNL App Builder].

1. Cliquez sur **[!UICONTROL Refresh registrations]**.

1. Accédez à **[!UICONTROL Apps]** > **[!UICONTROL Delivery Estimates]** dans la barre latérale [!DNL Admin].

1. Terminez la configuration en activant la fonction et en spécifiant les paramètres requis, notamment l’URL d’API et la clé API, l’adresse d’origine, les opérateurs par défaut, la durée de vie du cache et les mappages de code d’opérateur.

### Étape 7 : tester l’extension

Tester directement l&#39;action BFF d&#39;estimation de diffusion :

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

La réponse doit ressembler à ce qui suit :

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

### Créer le contrat de service

Maintenant que le serveur principal est terminé, demandez à l’agent de créer un contrat de service pour le travail de storefront :

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

L’agent produit des `docs/STOREFRONT_API_SPEC.md` avec le contrat de point d’entrée BFF complet (format de requête et de réponse, par exemple payloads, gestion des erreurs) et une invite prête à l’emploi pour l’espace de travail storefront.

Copiez ce fichier dans votre projet storefront avant de commencer les étapes de développement storefront.

>[!TIP]
>
>Si l’agent génère à la fois un contrat de service **et** une invite pour l’autre espace de travail, la transmission entre les équipes principales et les équipes storefront (ou les agents) est nette. L’agent storefront peut commencer à travailler immédiatement sans avoir à poser de questions sur l’API.

## Connexion au storefront

Cette section vous guide tout au long de l’implémentation de la partie storefront de l’extension des estimations de diffusion à l’aide d’outils de développement [!DNL Edge Delivery Services] et assistés par l’IA. Vous ajoutez des estimations de date de diffusion au PDP, à la page du panier et à la page de passage en caisse.

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
- Le fichier `STOREFRONT_API_SPEC.md` copié dans le dossier `docs/` de votre projet de storefront

### Étape 1 : valider l’environnement

Ouvrez votre fichier `config.json` et vérifiez que les valeurs de `commerce-core-endpoint` et `commerce-endpoint` pointent vers votre point d’entrée GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Étape 2 : fournir l’invite initiale

Puisque le contrat de service figure déjà dans votre projet, demandez à l’agent de mettre en œuvre l’intégration du storefront. Utilisez le mode **Plan** s’il est disponible dans votre agent, pour empêcher l’agent de continuer sans plan.

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services with storefront drop-ins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in the `docs/STOREFRONT_API_SPEC.md` file— please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's `additional_data` by a webhook. No API call is needed. Just read `additional_data` from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>L’invite est détaillée, car le contrat d’API complet est déjà disponible auprès de l’agent principal. En référençant `@docs/STOREFRONT_API_SPEC.md`, l’agent connaît l’URL exacte du point d’entrée, le format de requête et de réponse, ainsi que la gestion des erreurs. La liste des exigences explicites empêche l’agent d’inventer la portée. Plus précisément, le mode de demande de plan déclenche le workflow par phases qui vous permet d’orienter rapidement la mise en œuvre.

### Étape 3 : Répondre aux questions de clarification

L’agent renvoie avec des questions sur la portée de l’authentification, l’approche de passage en caisse et le style. L’exemple suivant illustre des questions et réponses standard.

**Exemples de questions sur l’agent :**

1. **Utilisateurs anonymes ou connectés** — Les estimations doivent-elles s’afficher sur les pages PDP et Panier pour tous les acheteurs ou uniquement pour les acheteurs authentifiés ?
2. **Approche de passage en caisse** — Le conteneur de dépôt ShippingMethods n’expose pas `additional_data`, l’agent propose donc deux options :
   - **Option A :** appeler le BFF aux dates de passage en caisse et d’injection DOM (plus simple, cohérent avec le PDP/panier)
   - **Option B :** étendre le fragment de GraphQL de passage en caisse via `overrideGQLOperations` pour inclure `additional_data`
3. **Style** — Émoticônes par rapport aux jetons de conception existants

**Exemples de réponses :**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>Afficher des estimations uniquement pour les acheteurs connectés est un choix pragmatique. L’agent peut utiliser automatiquement l’adresse d’expédition par défaut de l’acheteur (via GraphQL), de sorte qu’aucune entrée de code postal n’est nécessaire. Les acheteurs anonymes sur PDP et Cart auraient besoin de saisir un code postal, ce qui ajoute de la friction. Au passage en caisse, tous les acheteurs voient les dates de livraison parce que l&#39;adresse de livraison a déjà été saisie.

>[!NOTE]
>
>Votre agent peut poser différentes questions. Utilisez ces réponses comme conseils :
>
>- Afficher les estimations de PDP et de panier uniquement pour les acheteurs connectés (aucune entrée de code postal nécessaire).
>- Pour le passage en caisse, utilisez l’option A (appel BFF + injection DOM) pour plus de simplicité.
>- Utilisez des jetons de conception existants pour la mise en forme.

### Étape 4 : examen des exigences et de l’architecture

L’agent conçoit une architecture de module partagée. Vérifiez qu’il couvre :

| Composant | Objectif |
|-----------|---------|
| `scripts/delivery-estimates.js` | Module partagé : client BFF, mise en cache (sessionStorage, TTL de 30 minutes), formatage de la date, logique de compte à rebours, recherche d’adresse du client, mappage d’opérateur |
| Intégration PDP | Affiche « Obtenez-le avant la [ date ] » avec un compte à rebours facultatif entre le prix et la description. |
| Intégration du panier | Affiche la période (« Jeu, 12 mars - Ven, 13 mars ») dans la colonne de droite au-dessus du résumé de la commande |
| Intégration du passage en caisse | Appelle BFF lorsque l&#39;étape d&#39;expédition est active, DOM injecte les dates de diffusion via `MutationObserver` |

{style="table-layout:auto"}

Principales décisions de conception à vérifier :

- Tous les appels BFF ne sont pas bloquants : les pages sont rendues en premier, les estimations apparaissent de manière asynchrone.
- Tous les échecs sont silencieux — `console.debug` seulement, aucune erreur liée à l&#39;acheteur.
- `CARRIER_MAP` mappe les codes d&#39;opérateur Commerce (DPS, Fedex) aux codes d&#39;opérateur BFF (standard, express).
- Dynamic `import()` éloigne le module de diffusion du chemin de rendu critique.

>[!NOTE]
>
>Les agents d’IA sont non déterministes et leurs comportements diffèrent selon le modèle et l’IDE. Vous pouvez obtenir un ensemble différent de questions qui génère un ensemble différent d’exigences et d’architecture. Si tel est le cas, essayez d’orienter l’agent dans une direction telle que l’implémentation corresponde étroitement à ce qui est présenté dans ce tutoriel avant de continuer.

### Étape 5 : sélection d’un plan de mise en œuvre

L’agent vous donne la possibilité de créer un plan d’implémentation détaillé ou d’effectuer une implémentation directe.

- Si vous souhaitez un plan révisable que vous pouvez exécuter par phases avec plus de contrôle, sélectionnez la première option.
- Si vous souhaitez que l’agent effectue l’implémentation complète avec une intervention minimale, sélectionnez la deuxième option.

Lors de l’implémentation, l’agent crée et modifie les fichiers suivants :

**Nouveau fichier :**

- `scripts/delivery-estimates.js` — Module partagé avec `fetchDeliveryEstimates()`, `getCustomerShippingAddress()`, `formatDeliveryDate()`, `buildCountdownText()`, `findEstimateForCarrier()`

**Fichiers modifiés :**

- `blocks/product-details/product-details.js` + `.css` — Division d’estimation de la diffusion dans la colonne de droite, récupération asynchrone après le rendu principal
- `blocks/commerce-cart/commerce-cart.js` + `.css` — Div d&#39;estimation de la diffusion au-dessus du récapitulatif de la commande
- `blocks/commerce-checkout/commerce-checkout.js`, `containers.js`, `.css` — Injection DOM basée sur `MutationObserver` pour étiquettes de méthode d&#39;expédition

Regardez le code en cours de génération et posez des questions ou redirigez l’agent si nécessaire.

### Étape 6 : démarrer le serveur et effectuer un test

Une fois l’implémentation de l’agent terminée, démarrez le serveur de développement et testez les estimations de diffusion.

1. Démarrez le serveur de développement local :

   ```bash
   npm run start
   ```

1. Dans un navigateur, connectez-vous à votre compte d’acheteur.

   Les estimations de livraison sur PDP et Panier nécessitent une session authentifiée avec une adresse d’expédition par défaut enregistrée.

1. Accédez à une page de produit et vérifiez les résultats suivants :

   | Page | Résultat attendu | Authentification requise |
   |------|-----------------|---------------|
   | PDP | « Obtenez-le d’ici le jeudi 12 mars » avec compte à rebours facultatif | Oui (connecté uniquement) |
   | Panier | « Livraison estimée : Jeu. 12 - Ven. 13 mars » | Oui (connecté uniquement) |
   | Extraire | « Livraison estimée : jeudi 12 mars » par mode d&#39;expédition | Non (adresse saisie au passage en caisse) |

   {style="table-layout:auto"}

>[!NOTE]
>
>Les méthodes d’expédition sans transporteur correspondant (par exemple, Taux forfaitaire) n’affichent aucune estimation. C&#39;est à dessein : seuls les transporteurs mappés dans `CARRIER_MAP` obtiennent des dates de livraison.

Vous pouvez effectuer des tests manuels ou demander à l’agent d’utiliser ses fonctionnalités de navigateur pour effectuer des tests à votre place :

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### Étape 7 : Nettoyage

Après avoir ignoré ou terminé le test, l’agent vous invite à procéder au nettoyage. Après confirmation, l’agent archive tous les artefacts de documentation générés lors de l’implémentation.

## Dépannage

Suivez les conseils suivants si vous rencontrez des problèmes au cours du tutoriel.

### Serveur principal (App Builder)

| Symptôme | Cause | Correctif |
|---------|-------|-----|
| L’action de configuration de l’interface utilisateur d’administration renvoie des `400 Bad Request` avec « La requête définit des paramètres non autorisés (propriétés réservées) » | Le hook frontal envoie des `__ow_method` dans le corps de la requête. Les propriétés précédées du préfixe `__ow_` sont réservées par OpenWhisk et rejetées lorsque l’action a `final: true`. | Envoyez une propriété `method` personnalisée au lieu de `__ow_method`. L’action du serveur principal lit d’abord `params.method`, puis revient à `params.__ow_method` (que le Runtime fournit automatiquement). |
| `aio app deploy` échoue avec « maxVersion is required in productDependencies » | La validation de l’interface de ligne de commande nécessite `minVersion` et `maxVersion` dans `app.config.yaml` dépendances de produits. | Ajoutez une valeur `maxVersion` à chaque entrée `productDependencies` dans `app.config.yaml`. |
| Échec de la commande de déploiement | Identifiants non configurés avant le déploiement. La `.env`, la sélection de l’espace de travail et la synchronisation OAuth doivent avoir lieu en premier. | Suivez l’ordre correct : `cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`. |

{style="table-layout:auto"}

### Storefront (Edge Delivery Services)

| Symptôme | Cause | Correctif |
|---------|-------|-----|
| L’estimation de diffusion PDP n’apparaît pas pour les acheteurs connectés | Le bloc PDP n’initialise pas la liste déroulante `account` ; `getCustomerAddress()` échoue donc silencieusement et aucune estimation n’est récupérée. | Utilisez `CORE_FETCH_GRAPHQL.fetchGraphQl()` directement pour interroger les adresses des acheteurs au lieu de vous fier à l’API de liste déroulante de compte. Cela fonctionne sur n’importe quelle page. |
| Le PDP ne s’affiche toujours pas après le correctif GraphQL | Frappe dans le nom de la méthode : `CORE_FETCH_GRAPHQL.fetch()` a été utilisé à la place de `CORE_FETCH_GRAPHQL.fetchGraphQl()`. | Utilisez le nom de méthode correct : `fetchGraphQl` (Q majuscule, l minuscule). |
| Les dates de diffusion du passage en caisse n’apparaissent pas au premier chargement | L’écouteur d’événement `checkout/updated` a été enregistré après le déclenchement de `checkout/initialized`. Les données initiales ont donc été manquantes. | Ajoutez un listener `checkout/initialized` avec des `{ eager: true }` pour capturer les événements émis avant l’enregistrement. Conservez l’écouteur `checkout/updated` pour les modifications ultérieures. |
| L’estimation de la diffusion du panier n’apparaît pas. | `block.appendChild(fragment)` déplace tous les enfants en dehors du fragment, de sorte `fragment.querySelector('.cart__delivery-estimate')` renvoie la valeur null. | Requête à partir de `block` au lieu de `fragment` après l’opération d’ajout. |
| La livraison à taux forfaitaire n&#39;affiche aucune date de livraison au moment de la commande | Par conception : `CARRIER_MAP` mappe uniquement le DPS à la norme et le Fedex à l’expression. Le taux forfaitaire n&#39;a aucun opérateur correspondant dans l&#39;API externe. | Pas un bug. Pour ajouter des estimations pour d’autres opérateurs, étendez la `CARRIER_MAP` dans `scripts/delivery-estimates.js` et configurez l’opérateur dans l’extension du serveur principal. |

{style="table-layout:auto"}

### Sandbox SaaS Commerce

| Symptôme | Cause | Correctif |
|---------|-------|-----|
| Le Webhook renvoie `429 Too Many Requests` | [!DNL App Builder] workspace est en mode débogage, avec des limites de débit par minute strictes. [!DNL Commerce] recalcule fréquemment les frais d’expédition lors de la commande, épuisant ainsi le quota. | Déployez sur un espace de travail de production (`aio app use` pour basculer, puis `aio app deploy`). Les espaces de travail de production n’ont pas de limites de taux de débogage. |
| Avertissement de délai d’expiration soft Webhook (> 1 000 ms) | L’action webhook des méthodes d’expédition a pris plus de temps que le délai d’expiration soft de 1 000 ms [!DNL Commerce]. | Activez plus agressivement la mise en cache côté serveur dans `aio-lib-state` ou augmentez le délai d’expiration du webhook dans [!DNL Commerce Admin] (configuration des Webhooks Commerce). |

{style="table-layout:auto"}

## Résumé du tutoriel

Voici un résumé des sujets abordés dans ce tutoriel :

- **Configuration de l’API simulée :** création d’une API d’estimation de diffusion simulée à l’aide de Pipedream ou d’une action [!DNL App Builder] Runtime.
- **Modèle BFF :** création d’une action back-end pour front-end qui enveloppe l’API externe, conserve les informations d’identification côté serveur et centralise la mise en cache.
- **Enrichissement Webhook :** extension du webhook des méthodes d’expédition pour injecter des dates de livraison dans chaque option d’expédition lors du passage en caisse.
- **Configurabilité de l’interface utilisateur d’administration :** ajout d’une page de configuration à l’aide du [!DNL Admin UI SDK] afin que les commerçants puissent gérer les paramètres d’API, l’adresse d’origine et les mappages d’opérateur sans redéploiement.
- **Contrats de service :** création de contrats d’API qui relient les extensions principales et les implémentations de storefront.
- **Intégration de Storefront :** affichage des estimations de diffusion sur PDP (« Get it by »), le panier (période) et le passage en caisse (par méthode d’expédition) à l’aide d’un module client partagé.
- **UX non bloquante :** garantir que les estimations de diffusion ne bloquent jamais le flux d’achat ; les pages s’affichent en premier et les estimations apparaissent de manière asynchrone.

## Étapes suivantes

Suivez les suggestions suivantes pour étendre votre service d’estimations de diffusion :

- **Connecter une API de transporteur réel :** remplacez la simulation par une API d’expédition en direct telle que UPS, FedEx ou USPS en modifiant l’URL du service et la clé API dans le [!DNL Admin UI].
- **Prendre en charge les acheteurs anonymes :** ajoutez une entrée de code postal sur les pages PDP et de panier afin que les acheteurs non connectés puissent également consulter les estimations de diffusion.
- **Étendre les mappages de transporteur :** ajoutez d’autres codes de transporteur aux `CARRIER_MAP` pour afficher les dates de livraison pour d’autres méthodes d’expédition.
- **Ajouter la mise en cache côté serveur :** implémentez la mise en cache `aio-lib-state` dans l’action BFF pour réduire les appels à l’API externe pour les paires origine-destination répétées.
- **Afficher les estimations dans la confirmation de commande :** afficher la date de livraison estimée sur la page de confirmation de commande et dans les e-mails transactionnels.
