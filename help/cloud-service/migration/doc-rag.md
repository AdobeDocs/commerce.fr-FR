---
title: Service Rag de documentation
description: Découvrez comment utiliser le service de recherche de documentation optimisé par l’IA pour le développement d’Adobe Commerce.
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 28396828516645abec3b42a2c6874afe9134dfb8
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Service RAG de documentation (Beta)

>[!NOTE]
>
>Le service de documentation RAG est actuellement dans Beta et l’expérience peut faire l’objet de modifications.

Le service de génération augmentée de récupération de la documentation (RAG) fournit des fonctionnalités de recherche sémantique optimisées par l’IA dans la documentation Adobe Commerce et App Builder appropriée.

Ce guide fournit une interface IDE pour poser des questions sur Adobe Commerce et peut vous conseiller sur les bonnes pratiques pour le développement d’applications et d’autres tâches de migration.

Le service RAG fait partie du serveur MCP (Model Context Protocol) [Commerce extensibility tools](./coding-tools.md) qui s’intègre à Cursor et à d’autres assistants d’IA compatibles avec MCP.

## Documentation disponible

Le tableau suivant décrit la documentation actuellement indexée par le service RAG et les mots-clés que vous pouvez utiliser pour déclencher la recherche dans l’index associé. La documentation fournie continuera de s&#39;étendre au fur et à mesure que nous développerons le service RAG.

| Catégorie | Index | Contenu inclus | Mots-clés |
|-------|---------|---------|------------------------|
| [Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=fr) | commerce-storefront-docs | Edge Delivery Services, listes déroulantes, composants storefront | storefront, drop-in, EDS, liste de produits, passage en caisse |
| [Extensibilité](https://developer.adobe.com/commerce/extensibility/) | commerce-extensibility-docs | Webhooks, événements, extensions, intégrations | webhook, événement, extension, maillage API, GraphQL |
| [Commerce](https://experienceleague.adobe.com/fr/docs/commerce/cloud-service/overview) | commerce-core-docs | Commerce de base (catalogue, clients, commandes) | catalogue, produit, client, commande, inventaire |
| [App Builder](https://developer.adobe.com/app-builder/docs/intro_and_overview/) | app-builder-docs | App Builder, actions d’exécution, extensions d’interface utilisateur | générateur d’applications, action d’exécution, React Spectrum |

Pour plus d&#39;informations sur la sélection d&#39;index, consultez les sections [Sélection automatique d&#39;index](#automatic-index-selection-recommended) et [Sélection explicite d&#39;index](#explicit-index-selection).

Pour plus d’informations sur la documentation incluse dans chaque index, reportez-vous à la [liste source ingérée](https://github.com/adobe-commerce/azure-commerce-documentation-agent/blob/develop/docs/INGESTED_SOURCES.md).

## Sécurité et confidentialité

* **Authentification IMS** - Tous les appels API utilisent des jetons OAuth2 Adobe IMS.
* **Aucun stockage de données** - Le serveur MCP ne stocke aucune information d’identification ni donnée.
* **Exécution locale** - Tous les outils s’exécutent localement sur votre ordinateur.
* **Communication sécurisée** - La recherche de documentation utilise HTTPS avec validation de jeton.

Le point d’entrée de production est protégé par la [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview), qui inclut les protections suivantes :

* Pare-feu d’application web (WAF) avec Microsoft Default RuleSet 2.1 et Bot Manager RuleSet 1.0
* Blocage géographique pour les régions sous embargo américain (Cuba, Iran, Corée du Nord, Syrie, Crimée, Louhansk, Donetsk)
* Protection DDoS en périphérie
* Serveur principal de gestion des API verrouillé pour accepter uniquement le trafic provenant de Front Door

Pour différentes exigences de sécurité, vous pouvez utiliser un point d’entrée personnalisé. Voir [Point d’entrée de porte avant personnalisé](#custom-front-door-endpoint) pour plus d’informations.

## Conditions préalables

Avant l’installation, vérifiez que vous disposez des éléments suivants :

* [Node.js](https://nodejs.org/en/download){target="_blank"} 18+ (LTS recommandé)
* [Cursor IDE](https://cursor.com/download){target="_blank"} (recommandé) ou un autre IDE compatible MCP

  >[!NOTE]
  >
  >Bien que d’autres IDE compatibles avec MCP soient pris en charge, Cursor est l’IDE recommandé pour une expérience optimale. Si vous utilisez un autre IDE, vous devrez modifier les invites et les autres étapes de la documentation pour fonctionner avec l&#39;IDE sélectionné.

## Installation

1. Installez l’[interface de ligne de commande Adobe I/O](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/) globalement :

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Authentifiez-vous avec Adobe IMS :

   ```bash
   aio auth login
   ```

1. Clonez le référentiel des outils d’extensibilité de Commerce et accédez au répertoire :

   ```bash
   git clone https://github.com/adobe-commerce/commerce-extensibility-tools.git
   cd commerce-extensibility-tools
   ```

1. Installer les dépendances :

   ```bash
   npm install
   ```

1. Créez ou mettez à jour des `.cursor/mcp.json` dans votre répertoire de projet Commerce (pas globalement) pour inclure le serveur MCP `commerce-extensibility-tools` :

   ```json
   {
     "mcpServers": {
       "commerce-extensibility-tools": {
         "command": "node",
         "args": [
           "/<your-project-directory>/commerce-extensibility-tools/index.js"
         ],
         "env": {
           "NODE_ENV": "production"
         }
       }
     }
   }
   ```

   Veillez à remplacer `<your-project-directory>` par le chemin d’accès réel à l’emplacement où vous avez cloné le référentiel.

   >[!NOTE]
   >
   >Sous Windows, si vous rencontrez des problèmes lors de l’indication du chemin d’accès au répertoire du projet, reportez-vous à la section [Résolution des problèmes de chemin d’accès](#path-issues-windows).

1. Redémarrez l’IDE Cursor pour charger le serveur MCP.

1. Vérifiez l’installation en demandant à l’assistant AI :

   ```shell-session
   Can you show me the available Adobe Commerce tools?
   ```

## Utilisation

Une fois installés, vous pouvez appeler les index [automatiquement](#automatic-index-selection-recommended) ou [explicitement](#explicit-index-selection). Vous pouvez également utiliser la commande [`/search-commerce-docs`](#command-based-search).

>[!NOTE]
>
>Le service RAG renvoie les 5 résultats les plus pertinents.

### Sélection automatique de l’index (recommandée)

En posant des questions en langage naturel sur votre projet Commerce, l’outil recherche automatiquement l’index de documentation approprié et fournit des informations pertinentes :

>[!BEGINSHADEBOX]

L’invite suivante sélectionne automatiquement l’index `commerce-storefront-docs` :

```shell-session
"How do I use Edge Delivery Services drop-ins for product listing?"
```

L’invite suivante sélectionne automatiquement l’index `commerce-extensibility-docs` :

```shell-session
"How do I create a webhook in Adobe Commerce?"
```

L’invite suivante sélectionne automatiquement l’index `commerce-core-docs` :

```shell-session
"How to configure product catalog settings?"
```

L’invite suivante sélectionne automatiquement l’index `app-builder-docs` :

```shell-session
"What are App Builder runtime action best practices?"
```

>[!ENDSHADEBOX]

### Sélection d’index explicite

Vous pouvez également spécifier l’index que vous souhaitez utiliser dans l’invite.

```shell-session
Search commerce-storefront-docs for authentication drop-in
```

```shell-session
Using app-builder-docs, how do I deploy runtime actions?
```

### Recherche par commande

Si vous souhaitez vous assurer que le service RAG est utilisé, vous pouvez appeler manuellement la commande `/search-commerce-docs` Cursor pour rechercher de la documentation avec votre invite :

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Point d’entrée de porte avant personnalisé

Par défaut, la recherche de documentation utilise le point d’entrée de production [Azure Front Door](https://learn.microsoft.com/en-us/azure/frontdoor/front-door-overview) avec protection WAF. À des fins de test ou de développement, vous pouvez remplacer ce paramètre par la variable d’environnement `FRONT_DOOR_URL`.

Pour utiliser un point d’entrée personnalisé, ajoutez-le à la configuration MCP du curseur :

```json
{
  "mcpServers": {
    "commerce-extensibility-tools": {
      "command": "node",
      "args": ["/<your-project-directory>/commerce-extensibility-tools/index.js"],
      "env": {
        "NODE_ENV": "production",
        "FRONT_DOOR_URL": "https://<custom-endpoint>.azurefd.net"
      }
    }
  }
}
```

>[!NOTE]
>
>La plupart des développeurs doivent utiliser le point d’entrée de production par défaut et n’ont pas besoin de définir la variable `FRONT_DOOR_URL`.

## Dépannage

Les sections suivantes fournissent des conseils de dépannage pour les problèmes courants que vous pouvez rencontrer lors de l’utilisation du service de documentation RAG.

### Erreurs d’authentification

L’outil de recherche de documentation nécessite l’authentification Adobe IMS. Si vous rencontrez des erreurs d’authentification, procédez comme suit pour résoudre le problème.

1. Vérifiez votre connexion :

   ```bash
   aio where
   ```

1. Vérifiez que vous pouvez voir votre jeton IMS :

   ```bash
   aio auth login --bare
   ```

1. Si les erreurs d’authentification persistent, essayez de vous déconnecter puis de vous reconnecter :

   ```bash
   aio auth logout
   aio auth login
   ```

### Le serveur MCP ne se charge pas

Si le serveur MCP ne se connecte pas ou si votre agent indique qu&#39;il ne peut pas se connecter au RAG, procédez comme suit pour résoudre le problème.

1. Ouvrez les paramètres du curseur à l’aide des commandes **Cmd ,** (macOS) ou **Ctrl ,** (Windows et Linux).

1. Recherchez « MCP » et vérifiez que `commerce-extensibility-tools` est répertorié et activé.

1. Recherchez les messages d’erreur dans le panneau Paramètres MCP.

1. Vérifiez que le fichier `mcp.json` existe dans votre projet :

   ```bash
   cat .cursor/mcp.json
   ```

1. Vérifiez que le chemin est correct et absolu :

   ```bash
   ls -la /<your-project-directory>/commerce-extensibility-tools/index.js
   ```

### Outil introuvable

1. Quittez le curseur et rouvrez-le.

1. Vérifiez les journaux du serveur MCP dans la Developer Console du curseur en utilisant **Cmd+Maj+P** (macOS) ou **Ctrl+Maj+P** (Windows/Linux) et en recherchant « Developer : Open Logs Folder » (Développeur : ouvrir le dossier des journaux).

1. Vérifiez l’installation :

   ```bash
   cd commerce-extensibility-tools
   npm install
   node index.js
   ```

   Le serveur doit démarrer sans erreur.

### Problèmes de chemin (Windows)

Sous Windows, utilisez des barres obliques `/` ou des barres obliques inverses `\\` :

```json
{
  "args": ["C:/Users/yourname/projects/commerce-extensibility-tools/index.js"]
}
```

```json
{
  "args": ["C:\\Users\\yourname\\projects\\commerce-extensibility-tools\\index.js"]
}
```

## Ressources supplémentaires

* [Documentation Adobe Commerce destinée aux développeurs](https://developer.adobe.com/commerce/docs/){target="_blank"}
* [Documentation App Builder](https://developer.adobe.com/app-builder/docs/){target="_blank"}
* [Modèle de protocole contextuel](https://modelcontextprotocol.io/){target="_blank"}
* [IDE du curseur](https://cursor.sh/docs){target="_blank"}
