---
title: Gouvernance du Centre d’informations Commerce
description: Découvrez le modèle de gouvernance interne du Centre d’informations Commerce. Non publié sur Experience League.
source-git-commit: a91925091da28cd0745923894a3faab0374f0a0c
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%
---

# Gouvernance du Centre d’informations Commerce

Cette référence interne pour l’équipe de documentation n’est pas répertoriée dans `TOC.md`. Elle n’est donc pas publiée sur Adobe Experience League.

## Propriété

L’équipe de documentation d’Adobe Commerce est propriétaire du Centre d’informations. Il est créé dans `Adobe-Enterprise-Docs/commerce.en`, le référentiel répertorié comme `git-repo` dans `metadata.md`.

Il n’appartient à aucune équipe de produits, car il s’agit d’un produit interspécifique. Envoyez les corrections spécifiques au produit au contact de documentation de l’équipe produit propriétaire au lieu de les corriger ici.

## Contenu du Centre d’informations

| Appartient ici | Appartient au référentiel de produit. |
| --- | --- |
| Contenu couvrant plusieurs produits ou services, comme des conseils de sélection de produits, des parcours d’implémentation interproduits, des modèles d’architecture et des livres blancs | Contenu d’un seul produit, comme une configuration détaillée, une référence API/CLI/configuration et un dépannage |
| Pages de traitement courtes qui renvoient à des documents de produit faisant autorité | |

- Si une page accumule ici les détails d’un seul produit, déplacez-la vers le guide du produit et créez un lien vers celui-ci.
- Le Centre d’informations ne consolide ni ne migre la documentation des produits, et ne documente pas les fonctionnalités individuelles des produits. Créez un lien vers le contenu existant faisant autorité avant d’écrire quelque chose de nouveau.

## Ajouter du nouveau contenu

### Articles d’une section existante

1. Ajoutez le fichier au dossier correspondant à la section .
1. Ajoutez une entrée à `TOC.md` sous cette section.

Aucune approbation n’est requise au-delà de l’examen PR normal.

| Section table des matières | Dossier |
| --- | --- |
| Explorer les plateformes et services Commerce | `portfolio/`, `storefronts/`, `aem-assets/`, `apis/` |
| Prise en main par rôle | `get-started/` |
| Informations et conseils | `guidance-and-insights/` |
| Architecture | `architecture-options/` |
| Migration et adoption | `migration-adoption/` |
| Guides de mise en œuvre | `implementation-guides/` |

### Articles d’informations et de conseils

1. Copiez le `whitepaper-template.md` ou le `security-guidance-template.md` de `guidance-and-insights/templates/` dans `guidance-and-insights/`. Les modèles ne sont pas publiés. Pour le processus de création complet, y compris le ticket d’admission COMDOX, voir [readme.md](guidance-and-insights/readme.md).
1. Supprimez les commentaires de l’espace réservé du modèle.
1. Ajoutez une entrée `TOC.md` sous Informations et conseils lorsque le contenu est prêt à être publié.

### Sections de niveau supérieur

Un nouveau groupe de niveau supérieur dans `TOC.md` modifie la navigation du guide, ce qui nécessite une révision IA. Contactez le propriétaire de la révision Commerce IA. Réutilisez d’abord une section existante, telle que Prise en main par rôle pour le contenu de partenaire ou d’activation.

### URL publiées

Les URL sont créées à partir de l’ID du guide, des ID de section dans `TOC.md` (par exemple, `{#insights-and-guidance}`) et du nom de fichier. Les noms de dossier n’apparaissent pas dans l’URL. Attribuez un ID unique à chaque section et assurez-vous qu’aucun article ne se résout sur la même URL.

## Rythme de révision

- **Piloté par les événements** consultez les sections Exploration des plateformes et des services Commerce, Prise en main par rôle, Architecture, Migration et adoption et Guides de mise en œuvre lorsqu’un produit Commerce est renommé, lancé ou obsolète, ou lorsque sa disponibilité change. Par exemple, passez-les en revue si Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer obtiennent une intégration. Ces pages deviennent d’abord obsolètes.
- **Planifié** : pour détecter toute terminologie obsolète, marque ou inexactitude technique, exécutez un audit et un examen de contenu automatisés tous les six mois.

## Relation avec l’aide/la destination/

`help/landing/` (« Adobe Commerce Services Guides ») est un guide distinct qui ne fait pas partie du Centre d’informations. Il se concentre sur les services Commerce tels que le service de catalogue, la recherche en direct, les recommandations de produits et les services de paiement, et propose des liens vers le centre d’informations pour plus de détails. Rescoping ou consolidation des deux est une décision de suivi que ce guide ne résout pas.
