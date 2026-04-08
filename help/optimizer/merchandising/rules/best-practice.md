---
title: Bonnes pratiques relatives aux règles de marchandisage
description: Découvrez les bonnes pratiques d’implémentation des règles de marchandisage pour les pages de recherche, d’annonces par défaut et de catégories.
role: Admin, Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
source-git-commit: 8abc0593c166a2dd861cfb78674918de1d0744de
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Bonnes pratiques relatives aux règles de marchandisage

Pour optimiser la conversion et le chiffre d’affaires, implémentez des **règles de recherche** efficaces, une règle **liste par défaut** et **[règles de catégorie](add.md#category-rules)** (version bêta). Ajustez les classements à l’aide des données de vente, des stocks, des promotions et du [classement intelligent](add.md#intelligent-ranking).

Il est essentiel d’établir une règle **par défaut** bien pensée. Votre [règle par défaut](overview.md#default-rule) détermine la manière dont les résultats de recherche sont initialement triés lorsqu’aucune règle de recherche plus spécifique ne s’applique, ce qui améliore la probabilité de découverte et d’achat. Consultez-le régulièrement afin qu’il suive le rythme des besoins et des campagnes des acheteurs.

## Conseils pour optimiser les règles de recherche

- Épingler ou stimuler les produits ayant des volumes de vente élevés ou une activité de vente récente.
- Privilégiez les produits ayant des notes élevées et des évaluations positives.
- Assurez-vous que les articles en stock ont un rang supérieur.
- Hiérarchisez légèrement les produits avec des marges bénéficiaires plus élevées sans compromettre la pertinence.
- Mettez en avant les produits en vente ou faisant partie de promotions spéciales.
- Définissez automatiquement des règles de recherche pendant les périodes de promotion ou de vente en utilisant la période pendant votre période de promotion.
- Adaptez les résultats de la recherche en fonction du comportement de chaque acheteur à l’aide du [classement intelligent](add.md#intelligent-ranking) tel que « recommandé pour vous », « le plus consulté », etc.
- Utilisez toujours le panneau « Tester votre règle » pour prévisualiser l’impact de votre stratégie de classement intelligente sur les résultats de recherche réels pour différentes requêtes.

## Conseils pour les règles de catégorie

>[!IMPORTANT]
>
>Les règles de catégorie sont en version Beta.

- Utilisez des [règles de catégorie](add.md#category-rules) sur les pages à trafic élevé ou à marge élevée **pages de catégorie** où l’ordre traité importe autant que la recherche (par exemple, les collections saisonnières ou les services présentés).
- Alignez le **classement intelligent** (par exemple, tendance, les plus consultés) sur la manière dont les acheteurs parcourent cette catégorie ; les pages de catégorie n’utilisent pas le texte de requête de recherche de la même manière que les règles de recherche. Voir [Classement intelligent](add.md#intelligent-ranking).
- Appliquez **épingler**, **booster** et **enterrer** de manière cohérente avec votre plan de campagne. Gardez à l’esprit que les positions manuelles ne s’appliquent généralement que lorsque l’acheteur utilise le **tri par défaut** pour l’annonce. Voir [Classement manuel](add.md#manual-ranking).
- Prévisualisez dans le flux de règles **category** dans l’éditeur et validez sur le storefront après la publication, la même discipline que celle utilisée pour le panneau « Tester votre règle » lors de la recherche.
