---
source-git-commit: e3be9274ca8db80d3559b24a5c8be36f5d61b2ba
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/rules/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Bonnes pratiques relatives aux règles de marchandisage

Pour optimiser la conversion et le chiffre d’affaires, implémentez des **règles de recherche** efficaces, une **règle de liste par défaut** forte et des **[règles de catégorie](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types)**. Ajustez les classements à l&#39;aide des données de vente, des stocks, des promotions et du [classement intelligent](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking).

Utilisez les [règles de suppression de la recherche](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#search-suppression-rules) uniquement lorsque les requêtes d’acheteurs correspondantes doivent renvoyer zéro produit, et non lorsque les produits doivent avoir un classement différent.

Il est essentiel d&#39;établir une **règle par défaut** bien pensée. Votre [règle par défaut](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#default-rule) détermine la manière dont les résultats de recherche sont initialement triés lorsqu’aucune règle de recherche plus spécifique ne s’applique, ce qui améliore la probabilité de découverte et d’achat. Consultez-le régulièrement afin qu’il suive le rythme des besoins et des campagnes des acheteurs.

## Conseils pour optimiser les règles de recherche

- Épingler ou stimuler les produits ayant des volumes de vente élevés ou une activité de vente récente.
- Privilégiez les produits ayant des notes élevées et des évaluations positives.
- Assurez-vous que les articles en stock ont un rang supérieur.
- Hiérarchisez légèrement les produits avec des marges bénéficiaires plus élevées sans compromettre la pertinence.
- Mettez en avant les produits en vente ou faisant partie de promotions spéciales.
- Définissez automatiquement des règles de recherche pendant les périodes de promotion ou de vente en utilisant la période pendant votre période de promotion.
- Adapter les résultats de recherche en fonction du comportement de chaque acheteur à l&#39;aide du [classement intelligent](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking), tel que « recommandé pour vous », « le plus consulté », etc.
- Lorsqu’une stratégie intelligente autre que **Aucune** est sélectionnée, réglez **[L’amplification du classement intelligent](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** par règle et validez dans **Testez votre règle** avant de la publier.
- Utilisez toujours le panneau « Tester votre règle » pour prévisualiser l’impact de votre stratégie de classement intelligente sur les résultats de recherche réels pour différentes requêtes.

## Conseils pour les règles de catégorie

- Utilisez des [règles de catégorie](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types) sur les **pages de catégorie** à trafic élevé ou à marge élevée où l’ordre traité compte autant que la recherche (par exemple, les collections saisonnières ou les services présentés).
- Alignez le **classement intelligent** (par exemple, tendance, les plus consultés) sur la manière dont les acheteurs parcourent cette catégorie ; les pages de catégorie n’utilisent pas le texte de requête de recherche de la même manière que les règles de recherche. Voir [Classement intelligent](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking). Pour les méthodes intelligentes autres que **Aucune**, utilisez **[Amplification intelligente du classement](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** et l’aperçu des catégories pour ajuster la force comportementale de cette règle de catégorie.
- Appliquez **épingle**, **boost** et **bury** de manière cohérente avec votre plan de campagne. N’oubliez pas que les positions manuelles s’appliquent généralement uniquement lorsque l’acheteur utilise le **tri par défaut** pour la liste. Voir [Classement manuel](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#manual-ranking).
- Prévisualisez dans le flux de règles de **catégorie** dans l’éditeur et validez sur le storefront après la publication, la même discipline que celle que vous utilisez pour le panneau « Tester votre règle » dans la recherche.

## Bonnes pratiques et cas d’utilisation de suppression de recherche {#search-suppression-best-practices}

Une règle de suppression de la recherche bloque les résultats des requêtes qui correspondent à ses conditions, de sorte que le storefront affiche une page de résultats de recherche sans produit. L’éditeur de règles ne fournit pas d’aperçu pour les règles de suppression. Utilisez la condition la plus étroite qui répond à la restriction, puis suivez les [règles de création et de gestion de la suppression des recherches](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules). Une fois la règle activée, vérifiez les recherches correspondantes et non correspondantes sur le storefront. Vérifiez la présentation du storefront sur les résultats.

| Cas d’utilisation | Configuration suggérée | Éléments à vérifier |
| --- | --- | --- |
| Conformité réglementaire pour la recherche | Étendez la règle à la vue de catalogue affectée et faites correspondre les termes de recherche restreints. | Confirmez les conditions avec votre équipe de conformité. La suppression de la recherche seule n’empêche pas l’accès par le biais de la navigation par catégorie, des pages de marchandisage, des recommandations ou des URL de produits directes. |
| Restrictions de marque | Utilisez **La requête contient** lorsqu’un nom de marque restreint doit être bloqué dans des requêtes plus longues. | Une fois la règle activée, vérifiez les requêtes de storefront non liées contenant du texte similaire pour éviter de supprimer les recherches légitimes. |
| Empêcher un terme de recherche spécifique de renvoyer des résultats | Utilisez **La requête est** pour une expression exacte qui ne doit renvoyer aucun produit. | Vérifiez séparément les expressions associées. Une condition de correspondance exacte ne bloque pas toutes les requêtes contenant cette expression. |
| Restrictions relatives aux préfixes ou suffixes de requête | Utilisez **La requête commence par** ou **La requête se termine par** lorsque l’emplacement du texte restreint est important. | Une fois la règle activée, vérifiez les requêtes de storefront avec le texte au début, au milieu et à la fin pour confirmer la portée prévue. |
| Restrictions de recherche temporaires | Définissez des dates de début et de fin pour une restriction limitée dans le temps. | Confirmez le planning et le statut activé, puis vérifiez si la règle est toujours nécessaire une fois la restriction terminée. |

- Attribuez un nom explicite à chaque règle et notez la raison de la restriction dans sa description.
- Consultez les conditions des requêtes avant de publier les modifications. Une fois la règle activée, vérifiez les requêtes de storefront qui doivent être bloquées et les requêtes qui doivent toujours renvoyer des produits. L’actualisation des résultats de la requête mise en cache peut prendre jusqu’à 15 minutes.
- Passez en revue l’état sans résultats du storefront et assurez-vous que les acheteurs disposent d’un moyen utile de continuer à naviguer, comme de réviser la requête ou d’accéder à une catégorie, lorsque cela est pris en charge par le storefront.
- N’utilisez pas la suppression de requêtes comme substitut aux exclusions au niveau du produit. Pour exclure des produits dans les résultats de recherche, les suggestions de recherche et la saisie semi-automatique, utilisez des exclusions manuelles ou des **Événements de marchandisage basés sur les attributs** avec une action **Masquer** dans la **règle de recherche par défaut**.
- Consultez régulièrement les règles de suppression actives. Désactivez les règles qui ne sont plus nécessaires ou modifiez-les et publiez-les lorsque les restrictions changent.
