---
title: Que sont les recommandations de produits ?
description: Découvrez les recommandations de produits dans Adobe Commerce. Découvrez les unités de storefront pilotées par l’IA, la confidentialité, les chemins d’administration et de storefront et la conservation des données clés.
recommendations: noCatalog
exl-id: 72850cfd-555c-4e0e-ac3e-097e6dac2030
TQID: https://experienceleague.adobe.com/kRTCG6D5k17Ah-1Q-XNZq4o48xqIwlpI8vDQJDTEeoU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 738
ht-degree: 0%

---

# Que sont les [!DNL Product Recommendations] ?

[!DNL Product Recommendations] vous aider à afficher des recommandations de produits personnalisées sur les storefronts Adobe Commerce à l’aide d’[Adobe AI](https://business.adobe.com/fr/ai.html) et du machine learning sur le comportement agrégé des acheteurs et votre catalogue. Cette présentation couvre les contraintes de service (y compris la loi HIPAA), les données et la confidentialité, l’emplacement des unités de recommandation, les chemins d’implémentation de storefront, la manière dont les recommandations complètent les relations produit et la conservation des données de catalogue.

>[!IMPORTANT]
>
>**[!DNL Product Recommendations]n’est pas un service conforme à la loi HIPAA.** N’activez ni n’utilisez [!DNL Product Recommendations] dans aucune implémentation d’Adobe Commerce utilisant l’offre conforme à la loi HIPAA ou traitant d’une autre manière des informations de santé protégées (ISP). [!DNL Product Recommendations] fait partie des services SaaS de Commerce actuellement classés comme non conformes à la loi HIPAA.
>
>Pour plus d’informations sur les fonctionnalités Adobe Commerce prêtes pour la loi HIPAA et les services qui ne doivent pas être utilisés avec les ISP, voir [&#x200B; Préparation de la loi HIPAA pour Adobe Commerce &#x200B;](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/compliance/hipaa-ready-service/overview) et [&#x200B; Opérations &#x200B;](https://experienceleague.adobe.com/fr/docs/commerce-admin/start/compliance/hipaa-ready-service/operations#adobe-commerce-services).

## Gestion des données et confidentialité

La collecte de données pour [!DNL Product Recommendations] n’inclut aucune information d’identification personnelle (PII). Tous les identifiants d’utilisateur, tels que les ID de cookie et les adresses IP, sont strictement anonymisés. Pour en savoir plus, consultez la [Politique de confidentialité d’](https://www.adobe.com/privacy/policy.html).

Pour plus d’informations sur la synchronisation des données, consultez le [Tableau de bord de gestion des données](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=fr).

## Où les recommandations apparaissent

Les recommandations apparaissent sur le storefront sous la forme d’unités avec des étiquettes, telles que « Les clients qui ont consulté ce produit ont également consulté ». Vous pouvez créer, gérer et déployer des recommandations dans les vues de votre boutique à partir de l’administrateur Adobe Commerce. Si votre projet Commerce utilise le connecteur [Adobe Commerce Optimizer](https://experienceleague.adobe.com/fr/docs/commerce/aco-optimizer-connector/overview), vous créez, gérez et déployez des recommandations via [Adobe Commerce Optimizer](../optimizer/overview.md).

## Implémentations de Storefront

Sélectionnez la documentation correspondant à votre storefront :

- **PWA Studio** — [Documentation PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/)
- **Fronts personnalisés (par exemple, React ou Vue.js)** — [Intégrer [!DNL Product Recommendations]](headless.md) dans un storefront découplé
- **Commerce Edge Delivery Services (EDS)** — [Documentation d’Adobe Commerce Storefront pour EDS](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=fr)

>[!NOTE]
>
>Les configurations découplées et personnalisées varient selon la pile. Cette zone de produit documente un chemin PWA Studio et un modèle général d’intégration découplée ; elle ne couvre pas tous les scénarios tiers ou personnalisés.

## Recommandations de produits par rapport aux relations entre les produits

Étant donné la complexité en constante évolution des achats en ligne, ce qui fonctionne le mieux pour votre vitrine est souvent une combinaison de plusieurs technologies clés. L’utilisation des relations [!DNL Product Recommendations] et [produit](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-relationships.html?lang=fr) vous offre davantage de flexibilité lors de la promotion de produits. Vous pouvez tirer parti des [!DNL Product Recommendations] optimisés par Adobe AI pour automatiser intelligemment vos recommandations à grande échelle. Vous pouvez ensuite tirer parti des [&#x200B; Règles de produits associés &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/marketing/promotions/product-relationships/product-related-rules.html?lang=fr) lorsque vous devez intervenir manuellement pour vous assurer qu’une recommandation spécifique est envoyée à un segment d’acheteur cible ou lorsque certains objectifs commerciaux doivent être atteints.

Les recommandations de produits vous permettent d’effectuer les opérations suivantes :

- Choisissez parmi neuf types de recommandations intelligentes distincts en fonction des domaines suivants : basé sur l’acheteur, basé sur l’article, basé sur la popularité, basé sur les tendances et basé sur la similarité
- Utiliser les données comportementales pour personnaliser les recommandations dans l’ensemble du parcours de storefront de l’acheteur
- Mesurer les mesures clés pertinentes pour chaque recommandation afin de vous aider à comprendre l’impact de vos recommandations

## Démonstration des recommandations de produits

Regardez cette vidéo pour en savoir plus sur [!DNL Product Recommendations] :

>[!VIDEO](https://video.tv.adobe.com/v/3449946?captions=fre_fr&quality=12)

## Politique de conservation des données de catalogue

Le service [!DNL Product Recommendations] dépend des données de catalogue qui restent synchronisées avec votre environnement Adobe Commerce. Les catalogues ou environnements inactifs qui arrêtent d’interroger ces données peuvent entrer en veille, ce qui affecte les retours du service jusqu’à ce que vous réactiviez.

Si vous n’envoyez pas de requête pour les données du catalogue dans votre environnement **test** pendant 90 jours consécutifs, les données du catalogue sont définies en mode veille et aucune donnée n’est renvoyée pour une requête. Les données de catalogue de votre environnement **de production** ne sont pas affectées par la règle des 90 jours.

Si votre environnement comporte un **catalogue vide** 45 jours après sa création, les données du catalogue sont définies en mode veille et aucune donnée n’est renvoyée pour une requête. Cela s’applique aux environnements de production et de test.

### Réactiver les données du catalogue

Pour restaurer les données du catalogue après la mise en veille, [envoyez une demande d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) avec le titre « Réactiver le [!DNL Product Recommendations] » et incluez les identifiants d’environnement. Les données du catalogue doivent être restaurées dans un délai de quelques heures.
