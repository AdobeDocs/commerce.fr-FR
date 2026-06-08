---
title: Recherche Sémantique
description: Activez la recherche sémantique d’IA dans les paramètres  [!DNL Adobe Commerce Optimizer] . Aucune configuration d’attribut ou modification du storefront n’est requise.
role: Admin, User
recommendations: noCatalog
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

# Recherche sémantique

La recherche sémantique utilise l’IA pour comprendre ce que les acheteurs signifient, et pas seulement les mots exacts qu’ils tapent. Les requêtes telles que « robe pour un mariage sur la plage » ou « chaussures confortables pour rester debout toute la journée » peuvent renvoyer des produits pertinents même si votre catalogue n’utilise pas ces expressions exactes.

[!DNL Adobe Commerce Optimizer] combine la correspondance de mots-clés et la correspondance sémantique dans une seule expérience de recherche. Vous ne gérez pas de modes mot-clé et sémantique distincts sur le storefront. Dans Admin, accédez à l’espace de travail [Paramètres](../settings.md#advanced-search) pour gérer la recherche sémantique et éventuellement régler les commandes avancées sur l’onglet **[!UICONTROL Advanced search]**.

## Avantages

- **Moins de pages de recherche vides** — Les acheteurs trouvent des produits dont le libellé ne correspond pas exactement au texte du catalogue.
- **Meilleure correspondance d’intention** — Les requêtes naturelles et descriptives renvoient des résultats utiles.
- **Gestion des synonymes moins fréquente** — Les variantes de mots courantes (par exemple, canapé et canapé) sont souvent gérées sans listes de synonymes manuelles.
- **Pas de travail de storefront ou de développeur** — La recherche sémantique est activée par défaut et ne nécessite aucun code de thème, aucun drop-in, ni aucune modification d&#39;API.

## Fonctionnement

Lorsque la recherche sémantique est activée, [!DNL Adobe Commerce Optimizer] utilise des attributs de catalogue prédéfinis choisis par le système (tels que le nom et la description du produit) pour interpréter la signification de la requête avec la recherche traditionnelle par mot-clé. Vous ne sélectionnez ni ne donnez la priorité aux attributs dans l’Administration.

Par exemple :

- Une recherche de « canapé en cuir » peut renvoyer des produits étiquetés « canapé en cuir ».
- « Spring dress » peut apparaître des robes de saison même lorsque « spring » n&#39;est pas dans le nom du produit.
- Les « chaussures pour le trail running » peuvent correspondre à des produits décrits comme des chaussures de randonnée ou de tout-terrain.

## Ce qui se passe lorsque vous activez la recherche sémantique

La recherche sémantique fonctionne avec votre configuration de recherche [!DNL Adobe Commerce Optimizer] existante. Vous ne pouvez pas remplacer la recherche par mot-clé ni reconfigurer le storefront.

Lorsque la recherche sémantique est active :

- Vos [règles de marchandisage](../merchandising/rules/overview.md), [synonymes](../merchandising/synonyms/overview.md), [facettes](../merchandising/facets/overview.md), amplifications et filtres existants continuent de s’appliquer.
- La recherche sémantique permet une compréhension optimisée par l’IA de l’intention des acheteurs afin d’améliorer la pertinence des résultats avec la correspondance des mots-clés.
- Les attributs de catalogue prédéfinis sont automatiquement indexés. Vous ne sélectionnez pas d’attributs ni ne publiez de configuration distincte.

## Gestion de la recherche sémantique dans l’administration

La recherche sémantique est **activée par défaut** pour les catalogues anglais éligibles. Accédez à **[!UICONTROL Settings]** > **[!UICONTROL Advanced search]** pour confirmer le paramètre ou le modifier :

1. Dans Admin, accédez à **[!UICONTROL Settings]**.
1. Dans l’onglet **[!UICONTROL Advanced search]** , passez en **[!UICONTROL Enable semantic search]**.

   Lorsqu’elle est activée, la recherche correspond aux produits en fonction de leur signification et de leur contexte, ce qui peut produire des résultats plus pertinents, moins de pages de recherche vides et une conversion améliorée.

1. Cliquez sur **[!UICONTROL Save]** si vous modifiez les commandes de basculement ou de réglage.

   Les résultats de recherche sont mis à jour une fois l’indexation terminée. Pour un catalogue de taille moyenne, l’indexation peut prendre jusqu’à une demi-heure. Pour les catalogues volumineux contenant des millions de produits, cela peut prendre quelques heures.

>[!NOTE]
>
> La recherche sémantique est disponible uniquement pour les catalogues **anglais**. Si vous modifiez **[!UICONTROL Language]** catalogue en langue autre que l’anglais, **[!UICONTROL Enable semantic search]** est automatiquement désactivé.

Il n’est pas nécessaire de publier une configuration distincte ou de modifier les paramètres du storefront après l’enregistrement.

## Valider après activation

Une fois la recherche sémantique active et l’indexation terminée, Adobe recommande de valider les performances de la recherche. Utilisez la page [Performances de recherche](../manage-results/search-performance.md) pour passer en revue les mesures et tester les requêtes qui sont importantes pour votre entreprise.

1. Consultez les termes les plus recherchés dans le rapport **Recherches uniques**.
1. Testez les requêtes historiques à résultat nul à partir du rapport **Résultats nuls** sur le storefront.
1. Comparez les résultats de recherche pour les mêmes requêtes avant et après l’activation.
1. Surveillez les mesures d’engagement et de conversion des recherches, y compris le taux de clic publicitaire, le taux de conversion et le taux de résultats nuls.

## Réglage facultatif

Dans l’onglet **[!UICONTROL Advanced search]** , vous pouvez ajuster le comportement de la recherche une fois que la recherche sémantique est activée :

- **[!UICONTROL Semantic boost]** — Augmentez ou réduisez l&#39;influence des correspondances basées sur la signification sur le classement. Par exemple, supposons qu’une correspondance de produit récupérée par le biais d’une recherche sémantique s’affiche à la fin du résultat. L’ajout d’un coup de pouce le déplace vers le haut dans le résultat.
- **[!UICONTROL Similarity threshold]** — Définir la proximité d&#39;une correspondance avant l&#39;apparition d&#39;un produit. Les valeurs faibles affichent plus de résultats ; les valeurs élevées affichent moins de correspondances, plus étroites.
- **[!UICONTROL Fuzzy search]** et **[!UICONTROL Fuzzy search similarity threshold]** — Aidez les acheteurs à trouver des produits lorsque les requêtes comportent de petites différences d&#39;orthographe.

Voir [Recherche avancée](../settings.md#advanced-search) pour obtenir des descriptions des commandes et des conseils détaillés.

## Bonnes pratiques

- Utilisez des noms et des descriptions de produits clairs et descriptifs (idéalement de 50 à 100 mots) afin que la correspondance sémantique et les mots-clés disposent d’un texte de catalogue puissant.
- Commencez par le paramètre de **[!UICONTROL Enable semantic search]** par défaut, puis ajustez **[!UICONTROL Semantic boost]** ou **[!UICONTROL Similarity threshold]** uniquement si les résultats semblent trop larges ou trop étroits.
- Conservez des synonymes [synonymes](../merchandising/synonyms/overview.md) spécifiques à la marque ou hautement techniques, lorsque la recherche sémantique peut ne pas couvrir des termes spécialisés.

## Dépannage

| Problème | Que faire |
| --- | --- |
| Aucune modification sur le storefront juste après l’enregistrement | Attendez la fin de l’indexation. Les catalogues volumineux peuvent prendre plus de temps. |
| Les résultats semblent trop larges | Augmentez la **[!UICONTROL Similarity threshold]** ou réduisez la **[!UICONTROL Semantic boost]** sur l’onglet **[!UICONTROL Advanced search]** . |
| Les résultats semblent trop étroits | **[!UICONTROL Similarity threshold]** inférieur ou **[!UICONTROL Semantic boost]** supérieur. |
| La recherche sémantique n’est pas disponible. | Vérifiez **[!UICONTROL Language]** est défini sur **Anglais**. |

## Restrictions {#semantic-search-limitations}

- **Langue du catalogue :** la recherche sémantique est disponible uniquement pour les catalogues de langue **anglaise**.

## Plus d’aide sur cette rubrique

- [Recherche avancée](../settings.md#advanced-search)
- [Synonymes](../merchandising/synonyms/overview.md)
- [Performances de recherche](../manage-results/search-performance.md)
