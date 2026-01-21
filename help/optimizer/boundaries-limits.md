---
title: Limites et limites
description: Comprenez  [!DNL Adobe Commerce Optimizer]  limites et les limites pour planifier la capacité et éviter les problèmes de performances.
role: Admin, Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 4f238b002d1481126d4fec0a249b7f9ff437248e
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Limites et limites

[!DNL Adobe Commerce Optimizer] comporte deux types de limites :

- **Limites de licence** : en fonction de la capacité achetée ; peut être augmentée en achetant des packages supplémentaires.
- **Limites du système** : limites fixes qui protègent les ressources du système et garantissent des performances fiables pour tous les utilisateurs.

Votre utilisation doit respecter ces limites. Leur dépassement peut entraîner une latence accrue et un ralentissement des demandes.

## Demander une capacité supplémentaire

Les limites de licence peuvent être augmentées en achetant les packages de licence décrits dans la section [&#x200B; Limites de licence et limites système &#x200B;](#license-limits-and-system-boundaries) ou en négociant des licences personnalisées pour des cas d’utilisation uniques. Contactez votre représentant de compte Adobe pour discuter de vos besoins.

Pour toute question sur les limites du système, contactez l’[assistance Adobe](https://experienceleague.adobe.com/home?lang=fr#support).

## Prévention des problèmes de performances

Suivez ces bonnes pratiques pour respecter les limites et éviter les problèmes opérationnels :

- **Examinez vos limites**—Comprenez vos [limites de capacité](#license-limits-and-system-boundaries) avant de lancer de nouveaux vitrines ou de nouvelles campagnes.
- **Suivez votre utilisation** : utilisez des tableaux de bord de mesures intégrés ou des journaux CDN.

## Limites de licence et limites système

Les tableaux suivants résument les limites des licences et les limites du système par domaine de capacité et incluent des informations sur l’ajout de licences supplémentaires pour augmenter la capacité, le cas échéant.

### Limites de l’environnement

| **Environnement** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| **Environnement Sandbox** | Nombre d’environnements sandbox inclus | 2 par instance | Oui<p>Ajouter une licence d’environnement supplémentaire par instance</p> |
| **Environnement de production** | Nombre d’environnements de production inclus | 1 par instance | Licence<p>Ajouter une licence d’environnement supplémentaire par instance</p> |

{style="table-layout:auto"}

### Catalogue

| **Fonction** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Taux d’ingestion du produit | Nombre de produits créés ou mis à jour | 1K mises à jour par minute<p>100 000 mises à jour maximum par jour</p> | Oui<p>Ajouter un pack de licences :</p><ul><li>5 000 mises à jour par minute<br>Un maximum de 500 000 mises à jour par jour</li> <li>10 000 mises à jour par minute<br>Un maximum de 1 million de mises à jour par jour</li></ul><p>La capacité maximale d’ingestion des données est de 1 million de mises à jour par jour.</p> |
| Taille de la payload du produit | La quantité maximale de données autorisée lors de la création, de la mise à jour ou de l’ingestion d’informations sur les produits à l’aide de l’API | 200 KO | Non |
| Variations de catalogue | Le nombre de vues d’un catalogue disponibles pour les utilisateurs de storefront,<p>qui sont comptabilisées comme (*nombre de vues de catalogue × nombre de livres de prix*)</p> | 100 variations | Oui<p>Ajout d’un pack de licences de 100 variations de catalogue</p> |
| Produits dans une seule source de catalogue | SKU pris en charge dans le catalogue | 250 000 SKU | Oui<p>Ajouter un pack de licences SKU 100 000</p> |
| Variantes par produit | Le nombre de variantes de produit (taille, combinaisons de couleurs) autorisées par produit | 10K | Non |
| Sources de catalogue | Le nombre de contextes de données de catalogue (par exemple, des paramètres régionaux ou des sources de données telles que des PIM et des ERP) | 50 | Non |

{style="table-layout:auto"}

### Catalogues de prix

| **Fonction** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Catalogues de prix | Nombre de répertoires de prix autorisés par instance | En fonction du nombre de [variations du catalogue](#catalog) | Oui<br>augmenter les variations de catalogue |
| Remises par enregistrement de prix | Nombre de remises qui peuvent être appliquées à un prix de produit dans un seul catalogue de prix | 10 | Non |

{style="table-layout:auto"}

### Visuels de produit optimisés par AEM Assets

| **Fonction** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Visuels du produit Utilisateurs expérimentés | Utilisateur sous licence disposant de fonctionnalités complètes de gestion des ressources numériques, notamment des outils d’IA, des intégrations Adobe Express/Firefly et du partage Content Hub, qui gère les tâches principales de gestion des ressources numériques et des fonctionnalités avancées natives dans le cloud pour une efficacité optimale. | 2 | Oui<p>Mettre à niveau vers la licence AEM Assets</p> |
| Visuels de produit Utilisateurs collaborateurs | Accédez aux ressources et utilisez-les via l’intégration AEM Commerce, créez et modifiez du contenu à l’aide d’Adobe Express et de Firefly et, si cette option est activée, exploitez les ressources approuvées via le portail Content Hub. | 2 | Oui<p>Mettre à niveau vers la licence AEM Assets</p> |
| Stockage des visualisations de produit | Espace de stockage alloué aux ressources | Stockage de 1 To | Non |
| Utilisation de Dynamic Media | La tolérance pour les opérations de traitement Dynamic Media comprend :<ul><li>Diffusion d’images</li><li>Imagerie dynamique</li><li>Diffusion vidéo</li></ul><p>Pour plus d’informations, consultez *Calcul de l’utilisation de Dynamic Media* ci-dessous. | Basé sur GMV<p>Allocation minimale : 5 millions d’opérations/mois</p> | Oui<ul><li>Achat d’une licence pour des opérations supplémentaires</li><li>Mettre à niveau vers la licence AEM Assets</li></ul> |
| Diffusion vidéo | Possibilité de diffusion ou de téléchargement de vidéos | 300 vidéos, 1 minute par vidéo | Oui<p>Mettre à niveau vers la licence AEM Assets</p> |
| Génération de ressources | Accès à l’IA générative d’Adobe Express et d’Adobe Firefly pour créer des images | Aucune | Achetez les crédits IA génératifs séparément |

{style="table-layout:auto"}


>[!NOTE]
>
>**Utilisateurs expérimentés** peuvent accéder à Adobe Express directement ou depuis Adobe Commerce Optimizer. Les **utilisateurs collaborateurs** peuvent accéder directement à l’application Adobe Express. L’utilisation est régie par les [conditions de licence spécifiques à Adobe Express avec Firefly](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).


>[!BEGINSHADEBOX « Calculer l’utilisation de Dynamic Media »]

L’utilisation de Dynamic Media effectue le suivi des requêtes d’API entrant dans les composants Visuels du produit dans Adobe Commerce Optimizer afin de faciliter l’une des actions suivantes :

- **La diffusion d’images utilise une opération Dynamic Media** pour chaque occurrence des éléments suivants :
   - **transformation d’image de base** d’une ressource numérique, par exemple les opérations de redimensionnement, d’échelle, de conversion de format, de compression ou de recadrage.
   - **diffusion ou téléchargement d’images statiques** desdites ressources numériques ou dudit rendu de ressource numérique (autre que vidéo)
- **La diffusion d’images intelligentes utilise 20 opérations Dynamic Media** pour chaque diffusion optimisée d’une seule ressource numérique en générant automatiquement le rendu d’image le plus approprié pour l’appareil et le navigateur d’un utilisateur final.
- **La diffusion vidéo utilise 20 opérations Dynamic Media** pour une diffusion ou un téléchargement unique d’une vidéo ou une variante transformée d’une vidéo.

>[!ENDSHADEBOX]


### Vues et politiques de catalogue

| **Fonction** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Vues du catalogue | Nombre de sous-ensembles configurables de votre catalogue principal | En fonction du nombre de [variations du catalogue](#catalog) | Oui<br>augmenter les variations de catalogue |
| Politiques par vue de catalogue | Nombre de filtres de données autorisés | 10 | Non |
| Valeurs d’attribut dans une politique | Nombre de caractéristiques de produit configurables pour le filtrage | 100 | Non |

{style="table-layout:auto"}

### Storefront de catalogue

L’allocation de base pour les fonctionnalités de storefront du catalogue est déterminée en fonction du niveau GMV. Le tableau indique l’allocation minimale pour chaque fonctionnalité.

| **Fonction** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Taux de récupération des catalogues | Nombre d’appels mensuels d’une API de catalogue par un système (storefront, système de transactions, ERP ou autre) pour récupérer des données du catalogue | Basé sur le niveau GMV<p>Allocation minimale : 10M/mois</p> | Oui<p>Ajout de 1 million de requêtes par mois de packs de licences</p> |
| Requêtes de contenu | Demandes au storefront Commerce pour les pages vues HTML ou les appels API JSON. Comptabilisé comme 1 page vue ou 5 appels API. | Basé sur le niveau GMV<p>Allocation minimale : 2M/mois</p> | Oui<p>Ajout d’un pack de licences de 1 million par mois</p> |
| Variantes de Storefront GenAI | Autorisation pour la génération de contenu textuel | Basé sur le niveau GMV<p>Allocation minimale : 1 K variations/mois</p> | Oui<p>Achetez les crédits IA génératifs séparément</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>La génération d’images nécessite une licence Adobe Firefly configurée pour la même organisation IMS que Adobe Commerce Optimizer.


### Découverte de produits

| **Fonction** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Produits par requête de recherche | Nombre maximal de produits renvoyés par page dans les résultats de recherche | 100 | Non |
| Attributs filtrables | Nombre de caractéristiques de produit (telles que la couleur, la taille, la marque ou le matériau) qui peuvent être activées pour la navigation superposée et les facettes | 200 | Non |
| Attributs pouvant faire l’objet d’une recherche | Nombre de caractéristiques de produit configurables pour être utilisées avec le service de recherche de catalogue de produits | 200 | Non |
| Attributs triables | Nombre de caractéristiques de produit pouvant être configurées pour déterminer l’ordre des valeurs des résultats de recherche | 50 | Non |
| Profondeur de pagination de recherche | Nombre maximal de produits accessibles par pagination (par exemple, page 100 × 100 produits/page) | 10K | Non |
| Facettes | Nombre d’attributs de produit filtrables (tels que la marque, la couleur, la taille et le prix) qui peuvent être configurés pour aider les acheteurs à affiner les résultats de recherche et à parcourir les catégories | 100<p>Doit être un attribut filtrable</p> | Non |
| Options par facette | Nombre de valeurs d’attribut de produit filtrables (telles que « Rouge », « Bleu » pour la couleur, « Petit », « Medium » pour la taille) que les acheteurs peuvent sélectionner dans une liste | 100 | Oui<p>Peut augmenter via une demande d’assistance</p> |

{style="table-layout:auto"}

### Recommendations

Les fonctionnalités suivantes sont disponibles pour les recommandations de produits. Certaines fonctionnalités disponibles dans d’autres produits Adobe Commerce ne sont pas prises en charge dans [!DNL Adobe Commerce Optimizer].

| **Fonction** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Unités de recommandation actives | Nombre de composants de recommandations en direct sur votre storefront (par exemple, « Les clients ont également consulté » ou « Vous pourriez également aimer ») | 50 | Non |
| Inclusions/exclusions de catégories ou d’attributs | Filtrer les produits selon un ensemble spécifique éligible aux recommandations | Non pris en charge | |

{style="table-layout:auto"}

### Extensibilité

| **Fonction** | **Description** | **Affectation de base** | **Extensible ?** | **Notes** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacité à créer des extensions et des intégrations natives au cloud | Basé sur le niveau GMV<p>Allocation minimale : 1 pack/an</p> | Oui<p>Ajouter des packs supplémentaires</p> | Pour les limites définies par pack, voir :<ul><li>[Description du produit App Builder](https://helpx.adobe.com/fr/legal/product-descriptions/adobe-developer-app-builder.html) pour les limites définies par pack.</li><li>[Paramètres système et limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) dans les *Guides d’exécution d’App Builder*.</li><li>[Exigences de stockage App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your Adobe Commerce Optimizer solution, follow these steps:

1. Review the available packages, and start with a package that most closely matches your requirements.
1. Review the capabilities and metrics to ensure they align with your business requirements.
1. Purchase add-on packages for any metrics where you require additional capacity.

This approach ensures your solution is accurately sized for your business needs.

### Example use cases

1. **Seasonal Catalog Expansion**

   * Need: +20K SKUs
   * Add-On: 2 × SKU Packs (10K each)

1. **High Traffic Surge**

   * Need: +3M content requests/month
   * Add-On: 3 × content request packs (1M each)

1. **Global Presence**

   * Need: Additional environments for testing
   * Add-On: +1 Production, +2 Sandbox instances

1. **GenAI or Media Needs**

   * Need: +10M dynamic media ops/month
   * Add-On: 10 × dynamic media packs (1M each) -->
