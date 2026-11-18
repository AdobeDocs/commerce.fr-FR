---
title: Limites et limites d’Adobe Commerce as a Cloud Service
description: Découvrez les limites de licence et les limites système d’Adobe Commerce as a Cloud Service. Planifiez la capacité, suivez l’utilisation et évitez la latence et le ralentissement lorsque les limites sont dépassées.
role: Admin, Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et [!DNL Adobe Commerce as a Cloud Service] (infrastructure SaaS gérée par Adobe)."
nudge: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: a13aaee57732f27b51a2d2acdd0ca3de364ee6ab
workflow-type: tm+mt
source-wordcount: '1378'
ht-degree: 1%
---
# Limites et limites

[!DNL Adobe Commerce as a Cloud Service] applique **des limites de licence** et **des limites système** qui définissent la capacité que votre projet peut utiliser :

- **Les limites de licence** sont basées sur la capacité achetée et peuvent être augmentées en achetant des packages supplémentaires.
- **Les limites du système** sont des limites fixes qui protègent les ressources système et garantissent des performances fiables pour tous les utilisateurs.

>[!IMPORTANT]
>
> Votre utilisation doit respecter ces limites. Leur dépassement peut entraîner une latence accrue et un ralentissement des demandes.

## Demander une capacité supplémentaire

Vous pouvez augmenter vos limites de licence en achetant les packages de licence décrits dans [Limites de licence et limites système](#license-limits-and-system-boundaries), ou en négociant des licences personnalisées pour des cas d’utilisation uniques. Contactez votre représentant de compte Adobe pour discuter de vos besoins.

Pour toute question sur les limites du système, contactez [l’assistance Adobe](https://experienceleague.adobe.com/home?lang=en#support).

## Prévention des problèmes de performances

Suivez ces bonnes pratiques pour respecter les limites et éviter les problèmes opérationnels :

- **Examinez vos limites** - Comprenez vos [limites de capacité](#license-limits-and-system-boundaries) avant de lancer de nouveaux storefronts ou de nouvelles campagnes.
- **Suivre votre utilisation** - Utilisez des tableaux de bord de mesures intégrés ou des journaux CDN.

## Limites de licence et limites système

Les tableaux suivants résument les limites de licence et les limites du système par domaine de capacité et incluent des informations sur l’utilisation de licences supplémentaires pour augmenter la capacité, le cas échéant.

### Limites de l’environnement

| **Environnement** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| **Environnement Sandbox** | Nombre d’environnements sandbox inclus | 2 par instance | Oui<p>Ajouter une licence d’environnement supplémentaire par instance</p> |
| **Environnement de production** | Nombre d’environnements de production inclus | 1 par instance | Oui<p>Ajouter une licence d’environnement supplémentaire par instance</p> |

{style="table-layout:auto"}

### Catalogue

| **Fonctionnalité** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Taux d’ingestion du produit | Nombre de produits créés ou mis à jour | 1K mises à jour par minute<p>100 000 mises à jour maximum par jour</p> | Oui<p>Ajouter un pack de licences :</p><ul><li>5K mises à jour par minute<br>Un maximum de 500K mises à jour par jour</li><li>10 000 mises à jour par minute<br>Un maximum de 1 million de mises à jour par jour</li></ul><p>La capacité maximale d’ingestion des données est de 1 million de mises à jour par jour.</p> |
| Taille de la payload du produit | La quantité maximale de données autorisée lors de la création, de la mise à jour ou de l’ingestion d’informations sur les produits à l’aide de l’API | 200 KO | Non |
| Catégories | Le nombre de catégories de produits peut être regroupé sous . | 6,000 | Non |
| Nombre de produits | Nombre de SKU pris en charge dans le catalogue | 250 000 SKU | Oui<p>Ajouter un pack de licences SKU 100 000</p> |
| Variantes par produit | Le nombre de variantes de produit (taille, combinaisons de couleurs) autorisées par produit | 10K | Non |
| Vues de la boutique | Nombre de contextes de vue de magasin (par exemple, paramètres régionaux) | 50 | Non |
| SLA pour qu’une mise à jour du produit apparaisse dans la recherche | Heure d’affichage d’une création/mise à jour de produit dans la recherche storefront | 10 à 15 minutes | Non |

{style="table-layout:auto"}

### Extraire

| **Fonctionnalité** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Produits dans le panier | Nombre de produits autorisés par panier | 650 | Non |
| Adresses des clients par compte | Nombre d’adresses client autorisées par compte | 2,000 | Non |
| Règles de prix du panier | Nombre de règles de prix de panier qui appliquent des remises aux articles du panier, en fonction d’un ensemble de conditions | 100,000 | Non |
| Coupons | Nombre de codes coupon utilisés avec les règles de prix de panier | 1,000,000 | Non |

{style="table-layout:auto"}

<!--
# Price books

# | **Capability** | **Description** | **Base allocation** | **Expandable?** |
# | --- | --- | --- | --- |
# | Price books | The number of price books allowed per instance | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
# | Discounts per price record | The number of discounts that can be applied to a product price within a single price book | 10 | No |

{style="table-layout:auto"}
-->

### [!DNL Product Visuals] limites

| **Fonctionnalité** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Visuels du produit Utilisateurs expérimentés | Utilisateur sous licence disposant de fonctionnalités complètes de gestion des ressources numériques, notamment des outils d’IA, des intégrations [!DNL Adobe Express]/[!DNL Firefly] et du partage Content Hub, qui gèrent les tâches principales de gestion des ressources numériques et des fonctionnalités avancées natives dans le cloud pour une efficacité optimale. | 2 | Oui<p>Mettre à niveau vers la licence [!DNL AEM Assets]</p> |
| Visuels de produit Utilisateurs collaborateurs | Accédez aux ressources et travaillez avec elles via l’intégration d’AEM Commerce, créez et modifiez du contenu à l’aide de [!DNL Adobe Express] et [!DNL Firefly] et, si cette option est activée, exploitez les ressources approuvées via le portail Content Hub. | 2 | Oui<p>Mettre à niveau vers la licence [!DNL AEM Assets]</p> |
| Stockage des visualisations de produit | Espace de stockage alloué aux ressources | Stockage de 1 To | Non |
| Utilisation de Dynamic Media | La tolérance pour les opérations de traitement Dynamic Media comprend :<ul><li>Diffusion d’images</li><li>Imagerie dynamique</li><li>Diffusion vidéo</li></ul><p>Pour plus d’informations, consultez *Calcul de l’utilisation de Dynamic Media* ci-dessous. | Basé sur la valeur brute (VMG)<p>Allocation minimale : 5 millions d’opérations/mois</p> | Oui<ul><li>Achat d’une licence pour des opérations supplémentaires</li><li>Mettre à niveau vers la licence [!DNL AEM Assets]</li></ul> |
| Diffusion vidéo | Possibilité de diffusion ou de téléchargement de vidéos | 300 vidéos, 1 minute par vidéo | Oui<p>Mettre à niveau vers la licence [!DNL AEM Assets]</p> |
| Génération de ressources | Accès à l’IA générative [!DNL Adobe Express] et [!DNL Adobe Firefly] pour la création d’images | Aucune | Achetez les crédits IA génératifs séparément |

{style="table-layout:auto"}

>[!NOTE]
>
>**Les utilisateurs expérimentés** peuvent accéder à [!DNL Adobe Express] directement ou dans [!DNL Adobe Commerce as a Cloud Service].
>
>**Les utilisateurs collaborateurs** peuvent accéder directement à l&#39;application [!DNL Adobe Express]. L’utilisation est régie par les [conditions de licence spécifiques à Adobe Express avec Firefly](https://www.adobe.com/content/dam/cc/en/legal/terms/enterprise/pdfs/PSLT-AdobeExpressWFirefly-WW-2025v1.pdf).

>[!BEGINSHADEBOX « Calculer l’utilisation de Dynamic Media »]

L’utilisation de Dynamic Media effectue le suivi des requêtes d’API entrant dans les composants Visuels de produit dans [!DNL Adobe Commerce as a Cloud Service] afin de faciliter l’une des actions suivantes :

- **La diffusion d’images utilise une opération Dynamic Media** pour chaque occurrence des éléments suivants :
  - **transformation de base de l’image** d’une ressource numérique, par exemple redimensionnement, mise à l’échelle, conversion de format, compression ou opérations de recadrage.
  - **diffusion ou téléchargement d’images statiques** desdites ressources numériques ou dudit rendu de ressource numérique (autre que vidéo).
- **La diffusion d’images intelligentes utilise 20 opérations Dynamic Media** pour chaque diffusion optimisée d’une ressource numérique unique en générant automatiquement le rendu d’image le plus approprié pour l’appareil et le navigateur d’un utilisateur final.
- **La diffusion vidéo consomme 20 opérations Dynamic Media** pour une seule diffusion ou un seul téléchargement de vidéo, ou une variante transformée d’une vidéo.

>[!ENDSHADEBOX]

>[!NOTE]
>
>Les limites ci-dessus couvrent les allocations de capacité et d’utilisation. Pour obtenir une présentation de la fonctionnalité Visuels du produit et des contraintes fonctionnelles, consultez [Visuels du produit avec AEM Assets](../optimizer/setup/product-visuals.md).

<!--
### Catalog views and policies

| **Capability** | **Description** | **Base allocation** | **Expandable?** |
| --- | --- | --- | --- |
| Catalog views | Number of configurable subsets of your master catalog | Based on the number of [Catalog variations](#catalog) | Yes<br>Increase catalog variations |
| Policies per catalog view | Number of data filters allowed | 10 | No |
| Attribute values in a policy | Number of product characteristics that can be configured for filtering | 100 | No |
| [Restricted access key assignment](setup/private-catalog-view.md) | Number of restricted access keys that can be assigned to a single catalog view | 3 | No |
| RSA key size (restricted access keys) | Minimum and maximum key strength accepted for a restricted access key | 2048-bit minimum, 8192-bit maximum | No |
| Restricted access keys | Key revocation propagation delay | Up to 5 minutes, due to caching. Tokens signed by a removed key are denied once the delay elapses. | Not applicable |

{style="table-layout:auto"}
-->

### Storefront de catalogue

L’allocation de base pour les fonctionnalités de storefront du catalogue est déterminée en fonction du niveau de la valeur brute (VGM). Le tableau indique l’allocation minimale pour chaque fonctionnalité.

| **Fonctionnalité** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Taux de récupération des catalogues | Nombre d’appels mensuels d’une API de catalogue par un système (storefront, système de transactions, ERP ou autre) pour récupérer des données du catalogue | Basé sur le niveau GMV<p>Allocation minimale : 10M/mois</p> | Oui<p>Ajout de 1 million de requêtes par mois de packs de licences</p> |
| Requêtes de contenu | Demandes au storefront de pages vues HTML ou d’appels API JSON. Comptabilisé comme 1 page vue ou 5 appels API. | Basé sur le niveau GMV<p>Allocation minimale : 2 millions par mois</p> | Oui<p>Ajout d’un pack de licences de 1 million par mois</p> |
| Variantes de Storefront GenAI | Autorisation pour la génération de contenu textuel | Basé sur le niveau GMV<p>Allocation minimale : 1 K variations/mois</p> | Oui<p>Achetez les crédits IA génératifs séparément</p> |

{style="table-layout:auto"}

>[!NOTE]
>
>La génération d’images nécessite une licence [!DNL Adobe Firefly] configurée pour la même organisation IMS que [!DNL Adobe Commerce as a Cloud Service].

### Découverte de produits

Les limites suivantes s’appliquent à la recherche de produits, aux listes et à la configuration de marchandisage du storefront.

| **Fonctionnalité** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- |---------------------------------------------------|
| Récupération du produit | SKU maximum par requête GraphQL [!DNL Catalog Service] lors de la récupération des données de produit avec `products`, `productSearch`, `refineProduct` et `variants`. Répartissez les requêtes les plus volumineuses sur plusieurs appels. | 100 | Non |
| Attributs filtrables | Nombre de caractéristiques de produit (telles que la couleur, la taille, la marque ou le matériau) qui peuvent être activées pour la navigation superposée et les facettes | 200 | Non |
| Attributs pouvant faire l’objet d’une recherche | Nombre de caractéristiques de produit qui peuvent être indexées pour la recherche catalogue | 200 | Non |
| Attributs triables | Nombre de caractéristiques de produit disponibles en tant qu’options de tri sur les pages de recherche et de catégorie. | 50 | Non |
| Profondeur de pagination de recherche | Nombre maximal de produits accessibles par la pagination de la recherche (par exemple, page 100 × 100 produits/page). | 10K | Non |
| Facettes | Nombre d’attributs de produit filtrables (tels que la marque, la couleur, la taille et le prix) qui peuvent être configurés pour aider les acheteurs à affiner les résultats de recherche et à parcourir les catégories | 100<p>Doit être un attribut filtrable</p> | Oui<p>Peut passer à 500 via une demande d’assistance</p> |
| Options par facette | Nombre de valeurs d’attribut de produit filtrables que les acheteurs peuvent sélectionner dans une facette (par exemple, « Rouge », « Bleu » pour la couleur, « Petit », « Medium » pour la taille). | 100 | Oui<p>Peut augmenter via une demande d’assistance</p> |

{style="table-layout:auto"}

### Recommendations

Les fonctionnalités suivantes sont disponibles pour les recommandations de produits. Certaines fonctionnalités disponibles dans d&#39;autres produits Adobe Commerce ne sont pas prises en charge dans [!DNL Adobe Commerce as a Cloud Service].

| **Fonctionnalité** | **Description** | **Affectation de base** | **Extensible ?** |
| --- | --- | --- | --- |
| Unités de recommandation actives | Nombre de composants de recommandations en direct sur votre storefront (par exemple, « Les clients ont également consulté » ou « Vous pourriez également aimer ») | 50 unités actives par type de page pour les recommandations de produits, avec une portée explicite du modèle de catalogue si nécessaire | Non |

{style="table-layout:auto"}
<!-- Talos complained about this even thought it was copied directly from the ACO version of this page. Commenting out for now, | Category or attribute inclusions/exclusions | Filter products to a specific set that qualifies for recommendations | Not supported | — | -->

### Extensibilité

| **Fonctionnalité** | **Description** | **Affectation de base** | **Extensible ?** | **Notes** |
| --- | --- | --- | --- | --- |
| Adobe Developer App Builder | Capacité à créer des extensions et des intégrations natives au cloud | Basé sur le niveau GMV<p>Allocation minimale : 1 pack/an</p> | Oui<p>Ajouter des packs supplémentaires</p> | Pour les limites définies par pack, voir :<ul><li>[Description du produit App Builder](https://helpx.adobe.com/legal/product-descriptions/adobe-developer-app-builder.html).</li><li>[Paramètres système et limitations](https://developer.adobe.com/app-builder/docs/guides/runtime_guides/system-settings) dans les *guides d’exécution App Builder*.</li><li>[Exigences de stockage App Builder](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/)</li></ul> |

{style="table-layout:auto"}

<!--
## How to size your solution

Ask your Adobe representative for a list of available packages to determine which most closely matches your project

To accurately size your [!DNL Adobe Commerce as a Cloud Service] solution, follow these steps:

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
   * Add-On: 10 × dynamic media packs (1M each)
-->
