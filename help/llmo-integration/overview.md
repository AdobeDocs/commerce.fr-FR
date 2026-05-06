---
title: Intégration [!DNL Adobe Commerce] avec  [!DNL Adobe LLM Optimizer]
description: Connectez [!DNL Adobe Commerce] vous à  [!DNL Adobe LLM Optimizer]  pour surveiller les signaux de catalogue dans les LLM et déployer les optimisations de catalogue approuvées.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Intégration de [!DNL Adobe Commerce] à [!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>L’accès à cette intégration est restreint. Contactez votre gestionnaire de compte technique pour plus d’informations.

[!DNL Adobe LLM Optimizer] est une solution d’entreprise qui aide les marques à surveiller, analyser et optimiser l’affichage de leur contenu dans les réponses des grands modèles de langage (LLM) et des assistants d’IA. Comme les acheteurs utilisent de plus en plus les outils de l’IA pour la recherche et la découverte de produits, LLM Optimizer permet de s’assurer que votre marque et votre catalogue sont cités avec précision et replacés dans leur contexte.

Ce guide décrit la place de **[!DNL Adobe Commerce]** dans ce workflow lorsque votre catalogue de produits est stocké dans Commerce. Vous découvrirez les fonctionnalités disponibles, la configuration requise et le comportement des optimisations déployées dans l’administration et sur les canaux d’ingestion.

>[!NOTE]
>
>[!DNL Adobe LLM Optimizer] est une solution Adobe autonome. Les workflows de surveillance de base et d’opportunité ne nécessitent pas de [!DNL Adobe Experience Manager] (AEM) ni d’autres applications Adobe. Les actions de déploiement spécifiques à Commerce s’appliquent uniquement lorsque votre catalogue est connecté à LLM Optimizer et que vous choisissez de pousser les modifications approuvées dans [!DNL Adobe Commerce].

## Ce que l’intégration permet {#what-integration-enables}

La connexion de LLM Optimizer à votre catalogue [!DNL Adobe Commerce] vous permet de passer d’informations générales sur le contenu à des recommandations **adaptées au catalogue** :

- **Identifier** les lacunes et les incohérences dans les données de catalogue, telles que les titres, les descriptions et les signaux structurés, qui affectent la manière dont les gestionnaires de contenu local interprètent vos produits.
- **Examen** améliorations suggérées avec contexte à l&#39;appui, y compris les justifications et les comparaisons avant et après.
- **Déployez** les optimisations sélectionnées, telles que les mises à jour de nom et de description de produit, directement dans le catalogue Commerce, en veillant à ce que les workflows d’administration, les grilles et les données face au storefront restent alignés.

Lorsque la source du catalogue est [!DNL Adobe Commerce], Adobe peut prendre en charge le workflow complet : identification automatique des opportunités, suggestion de modifications et application de correctifs approuvés. Pour les catalogues qui proviennent de l’extérieur de Commerce, LLM Optimizer peut toujours analyser et suggérer des améliorations, mais l’application des modifications dépend de votre modèle d’intégration (par exemple, un catalogue mis en miroir ou des mises à jour manuelles). Voir [Limites et limites de l’intégration](boundaries-limits.md).

## À qui cela s&#39;adresse-t-il {#who-this-is-for}

- **marketeurs et marchandiseurs numériques** qui souhaitent que les données sur les produits soient exactes et cohérentes dans les réponses pilotées par LLM et qui ont besoin d’un moyen contrôlé d’améliorer la copie de catalogue à grande échelle.
- **Administrateurs** propriétaires de l’intégrité du catalogue, des processus d’administration et des intégrations (API, CSV, PIM) qui alimentent les attributs de produit.

## Conditions préalables {#prerequisites}

Les prérequis suivants s’appliquent lorsque vous avez **accès** à l’intégration d’Adobe Commerce avec Adobe LLM Optimizer. Contactez votre gestionnaire de compte technique pour plus d’informations.

- Votre storefront peut être exploré par des robots orientés LLM et agentiques où cette fonctionnalité d’explore fait partie de votre stratégie de mesure et d’optimisation de LLM Optimizer (une condition préalable générale pour les informations basées sur le catalogue).
- Pour les workflows de déploiement pris en charge par Commerce, les services Commerce requis et la connectivité du catalogue sont activés et sains. La configuration au niveau de la tâche est décrite dans [Connexion d’Adobe Commerce à LLM Optimizer](get-started/connect-to-llmo.md).

Vous devez également comprendre le déplacement des données entre les systèmes :

### Flux de données de haut niveau {#high-level-data-flow}

Conceptuellement, les optimisations de catalogue suivent deux schémas (votre projet peut en utiliser un ou les deux, selon les capacités) :

| Direction | Objectif |
| --- | --- |
| **Catalogue Commerce -> LLM Optimizer** | Les signaux de catalogue et d’URL alimentent les opportunités et les suggestions dans l’interface utilisateur de LLM Optimizer. |
| **LLM Optimizer -> Commerce** | Après avoir approuvé une action de déploiement, les mises à jour du nom et de la description du produit sont écrites dans le catalogue Commerce principal afin que l’administrateur et le storefront reflètent les valeurs optimisées. |

### [!DNL Adobe Commerce] par rapport aux catalogues tiers {#commerce-vs-third-party}

| Source du catalogue | Couverture LLM Optimizer standard |
| --- | --- |
| **[!DNL Adobe Commerce]** | Prise en charge renforcée de l’identification et des suggestions, ainsi que du déploiement des mises à jour de champs de catalogue approuvées que vous configurez. |
| **Commerce tiers** | L’identification et les suggestions sont prises en charge. Le déploiement automatisé dans le système du commerçant dépend des workflows d’exportation, de mise en miroir ou de partenaire plutôt que d’écritures directes dans le catalogue source du commerçant. |

## Agent de catalogue, MCP Storefront et LLM Optimizer {#catalog-agent-and-mcp}

Votre [!DNL Adobe Commerce] **catalogue de produits** est le système d’enregistrement des données de produits : noms, descriptions, attributs, prix et inventaire. Pour alimenter la découverte et l’optimisation assistées par l’IA, **le MCP Adobe Commerce Storefront** (Model Context Protocol) est une interface structurée entre vos données de catalogue Commerce actives et vos expériences Adobe AI.

**Catalog Agent** se trouve au-dessus du MCP Storefront. L’agent de catalogue [!DNL Adobe LLM Optimizer] permet d’interroger, d’enrichir et d’agir sur le contexte du catalogue et de la PDP en identifiant les lacunes, en proposant des améliorations et en déployant des modifications lorsque vous les approuvez. Ces fonctionnalités sont répertoriées dans les workflows LLM Optimizer décrits à la section [Utilisation de LLM Optimizer avec Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Comment l’agent de catalogue améliore Commerce pour les LLM {#catalog-agent-optimizations}

L’agent de catalogue traite la capacité de découverte par le biais de deux optimisations complémentaires : enrichissement des pages des détails du produit et enrichissement des catalogues de produits.

### Enrichissement de la page des détails du produit {#pdp-enrichment-overview}

**Enrichissement de la page des détails du produit (PDP)** suggère des améliorations du contenu de la page du produit afin que votre marchandise soit lue plus clairement lorsque les acheteurs découvrent des produits par le biais d’assistants d’IA et d’outils similaires. L’objectif est d’améliorer la clarté et la cohérence sans modifier la disposition du storefront que votre équipe a déjà marchandisée. Vous passez en revue les suggestions dans LLM Optimizer et effectuez le déploiement lorsque vous êtes prêt.

Après le déploiement, vérifiez ponctuellement la page produit active pour vous assurer que l’expérience d’achat reste correcte.

### Enrichissement du catalogue de produits {#catalog-enrichment-overview}

**enrichissement du catalogue de produits** suggère des **noms de produits** et **descriptions de produits** plus clairs lorsque la copie est mince, vague ou incohérente. Chaque suggestion inclut un contexte afin que votre équipe puisse décider des éléments à modifier. Lorsque vous approuvez une mise à jour, elle peut être appliquée à votre catalogue [!DNL Adobe Commerce] afin que l’administration, le storefront et les autres expériences qui utilisent ces champs reflètent la même formulation.

Comme ces champs se trouvent dans Commerce, l’amélioration d’un nom ou d’une description peut bénéficier à chaque canal qui lit ces données de produit (en fonction de la manière dont vos systèmes sont actualisés et du moment où ils le sont).

## Rubriques connexes {#related-topics}

- [Connexion d’Adobe Commerce à LLM Optimizer](get-started/connect-to-llmo.md)
- [Utilisation de LLM Optimizer avec Adobe Commerce](get-started/use-llmo-with-commerce.md)
- [Limites et limites de l’intégration](boundaries-limits.md)
