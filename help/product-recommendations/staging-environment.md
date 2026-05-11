---
title: Test dans l’environnement d’évaluation
description: Découvrez comment utiliser à  [!DNL Product Recommendations] ’aide de votre environnement de production dans votre environnement d’évaluation à des fins de test.
feature: Services, Recommendations, Staging
exl-id: 5b6d7615-6021-4419-98ea-006c8a299fe4
TQID: https://experienceleague.adobe.com/7e7e3T-vgkN-Pbqx6TwrBAWTEozhzS0h--tguOGe0yI
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# Test dans l’environnement d’évaluation

Avant de déployer des recommandations dans votre environnement de production, testez le service dans un environnement hors production pour vous assurer que tout fonctionne comme prévu.

[!DNL Product Recommendations] retourne des produits en fonction des [données comportementales de l’acheteur](events.md) collectées auprès de votre storefront. Cependant, dans un environnement hors production, il est probable que vous ne disposiez d’aucune donnée comportementale provenant des acheteurs. Le seul type de recommandation que vous pouvez tester sans données comportementales est `More like this`. Ce type de recommandation ne nécessite aucune donnée d’entrée, car il utilise une correspondance de similarité de contenu directe.

Les types de recommandations suivants nécessitent des données comportementales :

- Les plus consultés
- A consulté ceci, a consulté cela
- J&#39;ai acheté ça, acheté ça

Comment tester vos recommandations dans un environnement hors production à l’aide de données comportementales ? Il y a plusieurs options.

## Récupérer les recommandations de l’environnement de production (recommandé)

Adobe Commerce vous permet de récupérer des recommandations de votre environnement de production et de les prévisualiser dans votre environnement hors production en [changeant](settings.md) l’espace de données SaaS.

Pour récupérer des recommandations à partir de votre environnement de production, vous devez vérifier les points suivants :

- La collecte de données Storefront est [configurée et activée](install-configure.md) dans l’environnement de production.
- Le catalogue de votre environnement hors production est en grande partie identique à celui de l’environnement de production. L’utilisation de catalogues similaires garantit que les produits renvoyés dans les unités de recommandation imitent largement ceux de l’environnement de production.

## Générer des données comportementales sur un environnement hors production

1. Déployez le module `magento/product-recommendations` dans un environnement hors production où les données du catalogue sont similaires à votre catalogue de production.

1. Utilisez l’un des ID d’espace de données hors production pour [configuration](../landing/saas.md#saas-configuration) dans l’interface d’administration.

1. Générez les données vous-même en cliquant autour de votre storefront pour imiter le comportement des acheteurs réels (ou créez un script d’automatisation). Par le biais de vos tests, vous générez des événements comportementaux dans votre environnement hors production. Ces événements sont utilisés pour produire les affinités de produit qui alimentent les recommandations. À des fins de test, [!DNL Commerce] vous suggère d’interagir avec les types de recommandations suivants :

   - Les plus consultés : nécessite un minimum de données d’entrée. Les utilisateurs doivent afficher les produits.
   - A affiché ceci, a affiché cela - Nécessite que plusieurs utilisateurs voient plusieurs produits.
   - Acheté ceci, acheté cela - Nécessite que plusieurs utilisateurs achètent plusieurs produits.

### Avertissements

- Les données comportementales et de catalogue provenant de l’espace de données [SaaS](../landing/saas.md#saas-configuration) hors production identifient un environnement isolé dans lequel les recommandations de produits résultantes sont entièrement basées sur les données comportementales générées sur le storefront associé.

- Comme vous ne disposez pas de grandes quantités de données comportementales, les données d’entrée pour le calcul des associations de produits sont rares. Toutefois, ces données sont toujours envoyées à Sensei pour calculer les modèles de machine learning et fournir des recommandations basées sur les données générées dans cet environnement.
