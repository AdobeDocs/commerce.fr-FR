---
title: Projection de catalogue partagé B2B
description: Découvrez comment le connecteur B2B projette les catalogues partagés B2B d’Adobe Commerce dans des vues de catalogue Commerce Optimizer protégées et comment les storefronts résolvent et autorisent l’accès des acheteurs.
feature: Integration, Configuration
role: Admin, Developer
level: Intermediate
TQID: 'https://experienceleague.adobe.com/b37PBjcVQXRSLrB6c7nEf3A3U5cuLs1lQzwPUbp9fdA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
feature_v2:
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
subfeature_v2:
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%
---
# Projection de catalogue partagé B2B

Les projets [!DNL Adobe Commerce Optimizer Connector for B2B] [!DNL Adobe Commerce] des catalogues partagés et des affectations d’entreprise dans des vues de catalogue [!DNL Adobe Commerce Optimizer] protégées.

## Synchronisation de base et projection B2B

Le [!DNL Adobe Commerce Optimizer Connector] de base synchronise les flux de catalogue et de tarification, en mappant les vues de magasin aux sources de catalogue, les sites web aux répertoires de tarification et les groupes de clients aux répertoires de tarification.

Le [!DNL Adobe Commerce Optimizer Connector for B2B] projette l’assortiment et les prix de chaque catalogue partagé personnalisé dans une vue protégée. Adobe Commerce sélectionne la vue à partir de l&#39;affectation société de l&#39;acheteur. La clé d’accès restreint vérifie les requêtes signées, mais ne détermine pas l’accès au catalogue. Adobe Commerce est le système d’enregistrement pour les données de catalogue, de tarification et de projection B2B gérées par connecteur. Gérez la découverte de produits et les recommandations dans la configuration [!DNL Adobe Commerce Optimizer].

## Mapping des données

La projection B2B combine le contenu et la tarification synchronisés du catalogue avec l’assortiment de catalogues partagés et le contexte d’affectation de l’entreprise.

![Mappage de diagramme [!DNL Adobe Commerce] les vues de magasin, la tarification, les catalogues partagés et les affectations d’entreprise aux vues de catalogue privé projetées dans [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-projection-mapping.svg){width="800"}

| [!DNL Adobe Commerce] des données | [!DNL Adobe Commerce Optimizer] résultat | Objectif |
| --- | --- | --- |
| Activation de la vue de magasin et des données de produit | Source du catalogue | Fournit du contenu de produit localisé. |
| Tarification du site Web et du groupe de clients | Catalogue de prix | Fournit les prix applicables mais n&#39;autorise pas l&#39;accès |
| Assortiment de catalogue partagé personnalisé | Politiques | Filtre la vue du catalogue sur l&#39;assortiment de catalogue partagé. |
| Catalogue partagé personnalisé et vue de magasin activée | Vue catalogue privée | Crée une vue protégée pour chaque combinaison, avec la source de catalogue, la politique et le catalogue de prix applicables. |
| Affectation d’entreprise à un catalogue partagé | Contexte d&#39;acheteur résolu | Permet au serveur principal authentifié de résoudre la vue de catalogue associée à la société de l’acheteur. |
| Clé d’accès restreinte affectée à une vue protégée | Protection des catalogues | Autorise les requêtes à accéder à la vue de catalogue protégée, mais ne sélectionne pas de prix. |

Chaque vue de catalogue privée ne peut référencer qu&#39;un seul catalogue de prix. Les vues de magasin avec le même site web et le même contexte de tarification de groupe de clients peuvent partager un catalogue de prix tout en utilisant différentes sources de catalogue localisées. Le connecteur ne crée pas de catalogue de prix par catalogue partagé.

Le catalogue partagé par défaut n’est pas projeté en tant qu’affichage de catalogue privé B2B.

## Autorisation d’exécution

Une fois qu’un acheteur s’est connecté, le serveur principal Commerce authentifie la session et utilise l’affectation de société et la vue de magasin de l’acheteur pour résoudre la vue de catalogue et le catalogue de prix appropriés.

Le storefront envoie l’identifiant de vue de catalogue, l’identifiant de catalogue et le jeton signé avec chaque requête de l’API de marchandisage. [!DNL Adobe Commerce Optimizer] vérifie la signature RS256 du jeton JWT par rapport aux clés d’accès restreint affectées à la vue catalogue. Elle renvoie des données de catalogue uniquement lorsque le jeton et la clé sont valides et n’ont pas expiré.

Flux d’autorisation d’exécution ![&#x200B; pour les requêtes de catalogue B2B d’un acheteur par le biais d’un storefront et d’un serveur principal Commerce vers [!DNL Adobe Commerce Optimizer]](./assets/b2b-catalog-runtime-authorization.svg){width="700"}

Pour les requêtes de catalogue privé, envoyez les en-têtes suivants :

| En-tête | Objectif |
| --- | --- |
| `AC-View-ID` | Identifie la vue Catalogue. |
| `AC-Price-Book-ID` | Indique le catalogue de prix à utiliser. |
| `AC-Catalog-View-Access-Token` | Transporte le jeton JWT signé qui autorise l’accès à la vue de catalogue protégée. |

Pour connaître l’ensemble des exigences en matière de requête et de jeton, consultez [Authentification de l’API de marchandisage](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api#authentication) et [Vérification de l’accès à une vue de catalogue privée](/help/optimizer/setup/private-catalog-view.md#verify-access-is-enforced).

## Limite de protection

La protection des catalogues couvre uniquement les requêtes de catalogue et de recherche. Il ne sécurise pas les opérations de panier, de passage en caisse ou de commande. Renforcez l’éligibilité des achats dans Adobe Commerce ou le système de transactions connecté.

## Configuration et surveillance des projections

Le connecteur B2B projette des vues de catalogue privé, des politiques, des références de catalogue de prix et une configuration de clé d’accès restreint à partir de [!DNL Adobe Commerce]. Vous n’avez pas besoin de créer manuellement ces objets de projection gérés par le connecteur. Pour obtenir des instructions de configuration, voir [Prise en main du connecteur B2B](get-started-b2b-shared-catalogs.md).

Pour surveiller les vues de catalogue projetées et réconcilier la dérive de configuration, consultez [Surveillance de la synchronisation des vues de catalogue](catalog-view-sync-status.md). Pour gérer les clés affectées, consultez [Gérer les clés d’accès restreint pour les catalogues partagés B2B](restricted-access-keys.md).
