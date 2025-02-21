---
title: Test dans l’environnement d’évaluation
description: Découvrez comment utiliser à  [!DNL Product Recommendations] ’aide de votre environnement de production dans votre environnement d’évaluation à des fins de test.
feature: Services, Recommendations, Staging
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '426'
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
