---
title: Qu'est-ce que  [!DNL Live Search] ?
description: '[!DNL Live Search] d’Adobe Commerce offre une expérience de recherche rapide, pertinente et intuitive.'
recommendations: noCatalog
exl-id: 15399216-6a96-4d0b-bbc1-293190cb9e14
source-git-commit: d07f36a71247a96bc2dd950867c2862205238d88
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 1%

---

# Qu’est-ce qu’[!DNL Live Search] ?

[!DNL Live Search] est une fonctionnalité qui remplace les fonctionnalités de recherche standard d’Adobe Commerce. Lorsque la fonction [!DNL Live Search] est activée et configurée, le champ de texte de recherche par défaut est remplacé par le champ de texte [!DNL Live Search]. [!DNL Live Search] inclut également le widget Page de liste de produits (PLP), qui fournit des fonctionnalités de filtrage robustes lors de la navigation dans les résultats de recherche.

Avec [!DNL Live Search], vous pouvez :

- Créez des expériences de recherche significatives pour aider les acheteurs et les acheteurs à trouver ce qu’ils veulent avec le moins d’effort possible.
- Tirez parti de la facettisation et du reclassement dynamiques, optimisés par l’IA, des résultats de recherche en réponse aux comportements d’acheteur en session.
- Utilisez un service SaaS léger qui offre des mises à jour faciles et qui est inclus dans votre licence, ce qui réduit le coût total de possession.
- Soyez technique en activant l’API GraphQL, la flexibilité découplée, les environnements sandbox d’API et le SaaS ultra rapide.

>[!IMPORTANT]
>
>En ce qui concerne la recherche de site, Adobe Commerce vous propose des options. Avant la mise en œuvre, passez en revue les informations [Limites et limites](boundaries-limits.md) pour vous assurer qu’[!DNL Live Search] correspond aux besoins de votre entreprise.

## Architecture

Du côté Adobe Commerce de l’architecture, vous pouvez héberger la recherche *Admin*, synchroniser les données de catalogue et exécuter le service de requête. Une fois [!DNL Live Search] installé et configuré, Adobe Commerce commence à partager les données de recherche et de catalogue avec les services SaaS. À ce stade, les utilisateurs administrateurs peuvent configurer, personnaliser et gérer les [facettes](facets.md), [synonymes](synonyms.md) et [règles de marchandisage](category-merch.md) de recherche.

![Flux de données Live Search](assets/ls-cs-data-flow.png)

## Visite guidée

En mettant l&#39;accent sur la vitesse, la pertinence et la facilité d&#39;utilisation, [!DNL Live Search] change la donne pour les acheteurs et les commerçants. Regardez la vidéo suivante, puis faites un tour rapide de [!DNL Live Search] depuis le storefront.

>[!VIDEO](https://video.tv.adobe.com/v/3418797?learn=on)

Pour visionner une vidéo plus détaillée sur l’utilisation et la configuration de la recherche en direct, reportez-vous à la rubrique [Démonstration complète sur [!DNL Live Search]](https://experienceleague.adobe.com/fr/docs/commerce-learn/tutorials/getting-started/capabilities/live-search-full-demonstration).

### Rechercher en cours de frappe

[!DNL Live Search] répond avec des suggestions de produits et une image miniature des principaux résultats de recherche dans une [fenêtre contextuelle](storefront-popover.md) lorsque les acheteurs saisissent des requêtes dans la zone [Rechercher](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/catalog/search/search). La page [détails du produit](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/storefront/storefront) s’affiche lorsque les acheteurs cliquent sur un produit suggéré ou en vedette. Un lien _Afficher tout_ dans le pied de page de la fenêtre contextuelle affiche la page des résultats de la recherche.

[!DNL Live Search] renvoie des résultats de type « recherche en cours de frappe » pour une requête comportant au moins deux caractères. Pour une correspondance partielle, le nombre maximal de caractères par mot est de 20. Le nombre de caractères de la requête n’est pas configurable. La fenêtre contextuelle inclut les champs `name`, `sku` et `category_ids`.

![Exemple de storefront : effectuez une recherche au fur et à mesure que vous tapez](assets/storefront-search-as-you-type.png)

### Afficher tous les résultats de la recherche

Pour répertorier tous les produits renvoyés par la requête « rechercher en cours de frappe », cliquez sur _Afficher tout_ dans le pied de page de la fenêtre contextuelle.

![Exemple de storefront - facettes de prix](assets/storefront-view-all-search-results.png)

### Gestion [!DNL Live Search] fautes de frappe

Lorsqu’une recherche est effectuée, [!DNL Live Search] exécute une recherche non floue qui ne tient pas compte des fautes de frappe. Si aucun résultat n’est trouvé, [!DNL Live Search] effectue une seconde recherche floue, qui prend en compte les fautes de frappe mineures. La recherche floue est exécutée avec une distance de modification maximale de 1. Cette distance de modification utilise le concept de [distance de Levenshtein](https://en.wikipedia.org/wiki/Levenshtein_distance) et permet trois types d&#39;opérations :

| Fonctionnement | Description | Exemple |
|---|---|---|
| Insertion | Ajout d’un caractère. | « cat » -> « panier » |
| Suppression | Suppression d’un caractère. | « cart » -> « cat » |
| Substitution | Remplacer un caractère par un autre. | « cart » -> « cast » |

En plus de la logique de recherche floue, les transpositions sont également prises en compte, c’est-à-dire que deux caractères adjacents d’un mot sont intervertis, par exemple « the » au lieu de « the ». Notez que ces limites de modification sont définies par mot et non par expression dans son ensemble.

### Recherche filtrée avec facettes

La recherche filtrée utilise plusieurs dimensions de valeurs d’attribut, ou [facettes](facets.md), comme critères de recherche. La sélection des filtres est définie par le commerçant et change en fonction des produits renvoyés, les facettes les plus couramment utilisées étant épinglées en haut de la liste.

Utilisez les facettes comme paramètres d’URL `http://yourwebsite.com?color=red` et les résultats des filtres Live Search en fonction de ces valeurs d’attribut.

### Synonymes

[Synonymes](synonyms.md) élargissent la portée et affinent le focus des requêtes en incluant des mots que les acheteurs peuvent utiliser et qui diffèrent de ceux du catalogue. Vous pouvez affiner le dictionnaire de synonymes pour que les acheteurs restent engagés et sur le chemin de l’achat.

### Règles de marchandisage

Le marchandisage [règles](rules.md) façonne l’expérience d’achat avec des instructions if-then qui ajoutent une logique et des événements à la recherche. Vous pouvez facilement booster ou enterrer des produits pour une promotion, une saison ou une autre période.

### Prise en charge des termes de recherche

[!DNL Live Search] prend en charge Commerce [redirections de termes de recherche](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/catalog/search/search-terms). Par exemple, les utilisateurs peuvent rechercher un terme tel que « Frais d’expédition » et accéder directement à la page des frais d’expédition.

## Composants Live Search

- [!DNL Live Search] [widget contextuel](storefront-popover.md) est la zone qui s’ouvre sous le champ de recherche qui contient les résultats de la recherche.
- Le [widget de page de liste de produits](plp-styling.md) (PLP) fournit une page de liste de produits consultable avec prise en charge des facettes et des synonymes. Le widget est installé et activé dans Live Search 4.0.0+ et remplace l’adaptateur Search.
- (**Obsolète**) L’adaptateur de recherche était le précurseur du widget PLP et a été installé avec une recherche en direct &lt; 4.0.0. Si vous utilisez une version de Live Search antérieure à la version 4.0.0, Commerce vous recommande d’effectuer la mise à niveau pour bénéficier des avantages des fonctionnalités du widget PLP et des améliorations futures. À l’avenir, l’adaptateur de recherche ne sera mis à jour que pour résoudre les problèmes de sécurité.

## Espace de travail [!DNL Live Search]

L’[!DNL Live Search] [espace de travail](workspace.md) est la zone de l’Administration dans laquelle vous configurez [!DNL Live Search] fonctionnalités telles que les synonymes, les facettes et le marchandisage des catégories.

## Événements

[!DNL Live Search] utilise des tableaux de bord [événements](events.md) pour calculer [marchandisage intelligent](category-merch.md) et [performances](performance.md). Les événements sont fournis avec les implémentations par défaut. Les événements pour les storefronts découplés doivent être activés manuellement.

## Politique de conservation des données de catalogue

Si vous n’envoyez pas de requête de recherche pour les données du catalogue dans votre environnement de test pendant 90 jours consécutifs, les données du catalogue sont définies en mode veille et aucune donnée n’est renvoyée pour une requête de recherche. Les données de catalogue de votre environnement de production ne sont pas affectées par cette politique.

Pour réactiver les données du catalogue dans votre environnement de test, [envoyez une demande d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) avec le titre : « Réactiver le [!DNL Live Search] » et incluez les identifiants d’environnement. Les données du catalogue de votre environnement de test doivent être restaurées dans les heures qui suivent.
