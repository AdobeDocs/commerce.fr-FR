---
title: Concevoir une plateforme Commerce pour les acheteurs et les agents d’IA
description: Découvrez comment créer une plateforme commerciale qui sert les clients humains et les agents d’IA à partir d’une seule source de vérité, de la conception de catalogues à la gestion multisite, en passant par la télémétrie.
role: Developer, Leader
recommendations: noCatalog
autotag-review: '2026-10-20T20:32:40.424Z'
TQID: 'https://experienceleague.adobe.com/ub4oTxr4IfLGgqqz0S1npY-sn0FZb3mKq-GdjD9eDjI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b4dd41a7-ccf8-4e9d-918e-acaab534a307
    internal-label: Data quality
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%
---

# Concevoir une plateforme commerciale pour les acheteurs et les agents d’IA

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Portrait de Surya Lamech" src="../../assets/guidance-and-insights/agentic-commerce-author-avatar-slamech.png" width="96"><br><strong>Surya Lamech</strong><br><em>Responsable principale du marketing produit</em></td>
</tr>
</table>

![Illustration héroïque d&#39;une plateforme de commerce agentique où les humains et les agents de l&#39;IA interagissent avec une seule source de vérité](../../assets/guidance-and-insights/agentic-commerce-hero.png "Les bases architecturales d&#39;une plateforme de commerce agentique")

*Concevoir une plateforme commerciale où les humains et les agents de l&#39;IA interagissent avec une seule source de vérité.*

Commerce est en pleine mutation structurelle. Les clients ne comptent plus uniquement sur les moteurs de recherche ou la navigation sur les vitrines pour explorer leurs options. Au lieu de cela, ils se tournent vers des interfaces optimisées par LLM, des assistants basés sur le chat et des outils d&#39;achat agentiques pour poser des questions, comparer les produits entre les détaillants et accélérer les prises de décision à un stade précoce.

Ces interfaces sont de puissants moteurs de découverte, d’éducation et de comparaison. Ils aident les clients à clarifier les besoins, à évaluer les compromis et à limiter les choix plus rapidement que la navigation traditionnelle.

Pourtant, quand vient le temps de finaliser un achat, les clients préfèrent toujours largement les vitrines de confiance et les sites de marque où la sécurité des paiements, la transparence de l&#39;exécution et le service après-achat sont bien compris. La conversion reste ancrée dans les environnements où la confiance a déjà été établie.

Il est important de noter que l&#39;IA ne disparaît pas à ce stade. Lorsque les clients accèdent à la vitrine d&#39;une marque, l&#39;IA dédiée aux agences peut améliorer l&#39;expérience en guidant la sélection de produits, en personnalisant les recommandations en temps réel, en répondant aux objections, en regroupant les éléments complémentaires et en rationalisant le passage en caisse. Dans ces environnements approuvés, l’IA devient un accélérateur de conversion, améliorant les taux d’achèvement et la valeur moyenne des commandes.

Pour être compétitives dans ce nouveau paysage, les entreprises ont besoin d’une base commerciale **structurée, gouvernée et optimisée pour la consommation humaine et celle des agents**. Adobe Commerce est conçu pour cette évolution. Les principes présentés ci-dessous expliquent ce qu’il faut faire pour être réellement prêt à intervenir sur les agents.

## Architecture de commerce conçue pour deux audiences

![Diagramme montrant les vitrines et les applications pour les humains à gauche et les assistants de chat et les agents autonomes à droite, tous deux tirés d’un noyau Commerce central de produits, de prix, d’inventaire, de promotions, de panier et de passage en caisse qui est exposé via les API et les MCP](../../assets/guidance-and-insights/agentic-commerce-foundational-model.png){width="800" zoomable="yes"}

*Ce que voient les clients et ce que consomment les agents reste cohérent, précis et intégré à la marque.*

La pile commerciale moderne doit maintenant desservir deux audiences tout aussi importantes : les personnes et les agents d&#39;IA. Les expériences en contact direct avec les utilisateurs comme les storefronts et les applications restent essentielles pour l’engagement, l’expression de la marque et la fidélisation de la clientèle. Mais à côté d&#39;eux se trouve une surface en expansion rapide face à l&#39;agent : des points d&#39;entrée lisibles par machine qui fournissent aux LLM et aux agents autonomes des faits structurés, du contenu régi et des capacités transactionnelles.

Les agents obtiennent de meilleures performances lorsqu’ils utilisent des données propres et structurées, fournies par le biais d’API prévisibles, plutôt que d’essayer d’interpréter JavaScript ou d’inférer des règles métier à partir des couches de présentation. Cela signifie que les spécifications du produit, le prix, la disponibilité et la logique promotionnelle doivent exister en tant que ressources adressables exposées par le biais d’API et d’interfaces normalisées telles que les serveurs MCP. Lorsque les surfaces destinées aux humains et aux agents proviennent de la même source de vérité sous-jacente, les marques s’assurent que ce que les clients voient et ce que les agents consomment restent cohérents, précis et intégrés à la marque.

Cette architecture à double surface est la base du commerce agentique.

## Un catalogue conçu pour le raisonnement automatique

![Diagramme présentant des entités de produit structurées (SKU, attributs, variantes, offres groupées, prix et disponibilité) formées par des couches et des politiques de catalogue, puis diffusées par le biais de vues de catalogue à un storefront de marque, un marketplace, un flux de partenaire, une application mobile et une surface d’IA ou d’agent](../../assets/guidance-and-insights/agentic-commerce-agent-interaction.png){width="800" zoomable="yes"}

*Une seule source de vérité régie, mise en forme par canal sans jamais dupliquer les données de produit.*

Le catalogue est le cœur du commerce d’agence. Il doit être structuré pour les machines, régi par la conformité et suffisamment flexible pour prendre en charge l’ensemble des interactions humaines et agents. Le modèle de catalogue Adobe Commerce construit autour de vues de catalogue, de politiques, de couches et d’entités de produit structurées est conçu pour cet avenir.

Les vues catalogue définissent où et comment les données de produit sont exposées, que ce soit à un storefront, un marketplace, un flux de partenaire ou une surface d’IA. Chaque vue peut comporter ses propres règles de disponibilité des produits, de tarification et de visibilité des attributs, afin que les informations appropriées parviennent au client ou à l’agent approprié. Les calques de catalogue vous permettent d’enrichir les données de produit pour des canaux spécifiques sans modifier les données de produit source. Les politiques régissent l’éligibilité des clients, la logique de stock, les prix et les contraintes de conformité. Combinées, les entreprises contrôlent précisément les données de catalogue auxquelles un agent peut accéder ou sur lesquelles il peut agir.

## Les MCP comme langage commun pour les agents

![Diagramme présentant les assistants d’achat, les agents d’assistance et les outils de développement qui envoient des requêtes par le biais du protocole de contexte de modèle, qui inclut le MCP Commerce et le MCP Développeur, aux fonctionnalités d’Adobe Commerce telles que la création de panier, la commande, les paiements, l’inventaire, les promotions et les retours](../../assets/guidance-and-insights/agentic-commerce-reference-stack.png){width="800" zoomable="yes"}

*MCP normalise la manière dont les agents demandent des actions dans l’intention naturelle, et Adobe Commerce les effectue en tant qu’actions gouvernées et déterministes.*

Pour qu’Agentic Commerce fonctionne de bout en bout, les plateformes d’e-commerce doivent prendre en charge des protocoles normalisés qui permettent aux agents d’exécuter des actions en toute sécurité, telles que la création de panier, le lancement du passage en caisse, l’orchestration des paiements, la validation des stocks, les promotions et les retours.

Grâce à la prise en charge native de Model Context Protocol (MCP), Adobe structure et expose les fonctionnalités commerciales de manière à ce que les gestionnaires de contenu locaux puissent les interpréter de manière cohérente. Le MCP normalise la manière dont les données de produit, les règles métier et le contexte transactionnel sont présentés aux LLM, afin que les agents puissent les raisonner de manière fiable tandis que les entreprises conservent la gouvernance et le contrôle. Avec le MCP Commerce, les entreprises peuvent créer des expériences agentiques personnalisées telles que des assistants d’achat, la création de panier d’agent, des agents d’assistance, etc.

Le Developer MCP offre des fonctionnalités de développement optimisées par l’IA qui permettent aux équipes d’étendre rapidement les fonctionnalités de la plateforme et de déployer des composants storefront composables. En incorporant les sources de connaissances, la documentation et les bonnes pratiques de plateforme d’Adobe directement dans le workflow de développement, le Developer MCP aide les nouveaux développeurs à s’intégrer plus rapidement et à devenir productifs dès leur premier sprint. Il génère un code qui suit des modèles architecturaux éprouvés, est facile à gérer et répond aux normes de qualité exigées par le commerce d’entreprise. Il en résulte un passage accéléré de l’idée à la production, ce qui permet aux entreprises d’expérimenter, d’itérer et de commercialiser plus rapidement leurs capacités que leurs concurrents.

Adobe s’engage également à prendre en charge les protocoles commerciaux tels que le protocole ACP (Agentic Commerce Protocol) et le protocole UCP (Universal Commerce Protocol), pour permettre la découverte de produits et des interactions transactionnelles sécurisées et normalisées entre les agents et votre storefront.

En adoptant des protocoles ouverts plutôt que des intégrations ponctuelles, Adobe garantit que les interactions commerciales sont régies, déterministes et sécurisées, tout en activant un nouveau modèle d’engagement agent-commerçant où les agents de confiance peuvent effectuer des transactions directement selon des politiques clairement définies.

## Télémétrie et optimisation continue

Dans un écosystème médié par l&#39;IA, la télémétrie devient l&#39;avantage stratégique. Les entreprises ont besoin de visibilité sur la manière dont leur marque est représentée sur les LLM, sur la manière dont les agents représentent précisément leur contenu, sur la manière dont le trafic envoyé par l’agent convertit et sur les endroits où des problèmes de gouvernance ou de conformité surviennent. Ils ont également besoin d’une télémétrie opérationnelle qui suit l’exécution des agents et la détection des anomalies dans les interactions des agents.

Adobe vous donne une visibilité sur l’apparence de vos produits dans LLM, améliore les données de produit avec l’IA et accroît la lisibilité de vos données par LLMS. En ajoutant un contexte significatif à votre catalogue, vous aiderez les entreprises à long terme non seulement à découvrir vos produits avec précision, mais aussi à comprendre ce qu&#39;ils sont, pour qui ils sont et pourquoi ils sont importants pour les clients.

En outre, les pages de détails de vos produits qui ont été optimisées pour la consommation humaine peuvent souvent contenir des données invisibles pour les agents. Ces données peuvent être masquées derrière des modèles, des configurateurs et des pages liées. Les agents peuvent ne pas comprendre entièrement les catégories de produits, les lots et les variantes. Adobe peut identifier ces informations manquantes critiques et les déployer sous la forme d’ID JSON sur Edge afin que les agents puissent obtenir toutes les données de produit appropriées.

Grâce à cette télémétrie et à cette optimisation constantes, les marques peuvent assurer une visibilité maximale et rester compétitives sur l&#39;ensemble des LLM.

## Pourquoi cela est important

Le commerce électronique ne se limite plus aux vitrines et aux résultats de recherche. Les LLM et les agents autonomes servent de médiateurs pour la découverte, l’évaluation et les transactions. Ce changement modifie les mécanismes de visibilité, la dynamique du contrôle et les fondements de la confiance. Les marques gagnantes seront les architectes d’une base native à l’IA.

## Conseils connexes

* [Vues du catalogue](/help/optimizer/setup/catalog-view.md)
* [Calques de catalogue](/help/optimizer/setup/catalog-layer.md)
* [Politiques](/help/optimizer/setup/policies.md)
* [Outils de développement du codage de l’IA pour Adobe Commerce App Builder](/help/cloud-service/migration/coding-tools.md)
* [API COMMERCE](../../apis/commerce-apis.md)
* [Liste de lecture de l&#39;agent de développement Commerce &#x200B;](https://experienceleague.adobe.com/en/playlists/commerce-developer-agent)—Regardez des vidéos techniques sur la configuration et l&#39;utilisation de l&#39;agent de développement Commerce.
