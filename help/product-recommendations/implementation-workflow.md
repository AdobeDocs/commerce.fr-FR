---
title: Workflow de mise en œuvre
description: Découvrez les étapes à suivre pour réussir l [!DNL Product Recommendations] implémentation sur votre storefront.
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
TQID: https://experienceleague.adobe.com/-nvORlxBNwoCcZb6s-OvaX8TtIh28Q-fjeUxsDXpe9E
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 563
ht-degree: 0%

---

# Workflow de mise en œuvre

[!DNL Product Recommendations] utilise des données comportementales et de catalogue :

- Comportemental : données issues de l’engagement d’un acheteur sur votre site, telles que les consultations de produits, les articles ajoutés au panier et les achats. Adobe Commerce et Adobe AI ne collectent pas d’informations d’identification personnelle.

- Catalogue - Métadonnées du produit, telles que le nom, le prix et la disponibilité.

Lors de l’installation du `magento/product-recommendations module`, Adobe AI agrège les données comportementales et de catalogue et crée des [!DNL Product Recommendations] pour chaque type de recommandation. Le service [!DNL Product Recommendations] déploie ensuite ces recommandations sur votre storefront. Pour vous aider à implémenter des recommandations de produits sur votre storefront, utilisez le workflow suivant :

>[!NOTE]
>
> Si votre storefront est implémenté à l’aide de PWA Studio, consultez la documentation de [PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Si vous utilisez une technologie frontale personnalisée telle que React ou Vue JS, apprenez à [intégrer](headless.md) [!DNL Product Recommendations] dans votre storefront découplé.

## Workflow

1. **Déployer la collecte de données en production**

   Le déploiement de [!DNL Product Recommendations] nécessite deux [sources de données](type.md) principales : le catalogue et le comportement. La production étant le seul environnement où les actions de vos acheteurs sont capturées et analysées, commencez la collecte de données en production dès que possible. [Découvrez &#x200B;](events.md) comment Adobe AI entraîne des modèles de machine learning qui génèrent des recommandations de meilleure qualité. Lorsque vous commencez à collecter des données comportementales en production, vous pouvez en outre [récupérer des recommandations](staging-environment.md#fetch-recommendations-from-production-environment-recommended) basées sur ces données de production, tout en opérant dans des environnements hors production. Vous pouvez ensuite tester et tester différentes recommandations qui sont calculées en fonction des données réelles d’acheteurs collectées en production.

   Pour déployer la collecte de données en production, vous devez [installer et configurer](install-configure.md) le module [!DNL Product Recommendations] en fournissant une clé [API](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html).

   >[!TIP]
   >
   > Le déploiement de la collecte de données ne modifie pas l’apparence de votre storefront ni l’expérience de vos clients. Seules la création et le déploiement d’unités de recommandation modifient l’expérience client sur votre storefront. Veillez à effectuer des tests sur votre environnement hors production avant de procéder au déploiement en production. En outre, ne créez pas d’unités de recommandation tant que vous n’avez pas personnalisé votre modèle. Pour plus d’informations, reportez-vous à l’étape suivante.

1. **Personnalisez le modèle en fonction de votre style**

   Votre storefront représente votre marque. Veillez donc à modifier le modèle de recommandations de produits pour qu’il corresponde au thème de votre site.

   >[!TIP]
   >
   > En personnalisant le modèle, vous pouvez spécifier votre feuille de style, remplacer l’emplacement où une unité de recommandation apparaît sur une page, etc.

   Voir [Personnaliser](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html) dans la documentation destinée aux développeurs pour savoir comment effectuer cette étape.

1. **Test de recommandations sur votre environnement hors production**

   Il est toujours recommandé de tester une nouvelle technologie dans votre environnement hors production avant de la déployer en production. Le test des recommandations sur votre environnement hors production vous permet de jouer avec différents types d’unités de recommandation, de positionnement et de pages. Vous pouvez extraire des recommandations en fonction de données comportementales déjà collectées en production lors des tests dans votre environnement hors production, de sorte que les résultats des recommandations soient basés sur le comportement d’achat des clients réels.

   >[!TIP]
   >
   > Assurez-vous que votre catalogue d’environnements hors production est largement identique à celui que vous avez en production. L’utilisation de catalogues similaires garantit que les produits renvoyés dans les unités de recommandation imitent fidèlement les produits en production.

   Voir [Récupérer](staging-environment.md) données comportementales à partir de votre environnement de production pour savoir comment effectuer cette étape.

1. **Créer et déployer des recommandations sur votre storefront de production**

   Maintenant que vous avez déployé la collecte de données comportementales en production, modifié le modèle de recommandations de produits et testé les recommandations à l’aide du comportement réel de l’acheteur, vous êtes prêt à promouvoir tout le code en production et [créer](create.md) les recommandations de produits en direct.
