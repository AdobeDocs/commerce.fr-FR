---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---
La recherche sémantique utilise l’IA pour comprendre ce que les acheteurs signifient, et pas seulement les mots exacts qu’ils tapent. Les requêtes telles que « robe pour un mariage sur la plage » ou « chaussures confortables pour rester debout toute la journée » peuvent renvoyer des produits pertinents même si votre catalogue n’utilise pas ces expressions exactes.

Le système de découverte de produits combine la correspondance de mots-clés et la correspondance sémantique dans une seule expérience de recherche. Vous ne gérez pas de modes mot-clé et sémantique distincts sur le storefront.

## Configuration de la recherche sémantique

La recherche sémantique est **activée par défaut** pour les catalogues anglais éligibles. Vous pouvez le gérer dans l’onglet **[!UICONTROL Advanced search]** de l’espace de travail [Paramètres](../settings.md#advanced-search), où vous pouvez confirmer ou modifier le paramètre et éventuellement ajuster l’amplification sémantique, le seuil de similarité et la recherche floue. Consultez [Paramètres](../settings.md#access-the-settings-workspace) pour savoir comment ouvrir l’espace de travail.

Il n’est pas nécessaire de publier une configuration distincte ou de modifier les paramètres du storefront après l’enregistrement.

## Avantages

- **Moins de pages de recherche vides**—Les acheteurs trouvent des produits lorsque leur libellé ne correspond pas exactement au texte du catalogue.
- **Meilleure correspondance d&#39;intention** : les requêtes naturelles et descriptives renvoient des résultats utiles.
- **Moins de maintenance des synonymes** : les variations de mots courantes (par exemple, canapé et canapé) sont souvent gérées sans listes de synonymes manuelles.
- **Pas de travail de storefront ou de développeur** : la recherche sémantique est activée par défaut et ne nécessite aucun code de thème, aucun menu déroulant ni aucune modification d’API.

## Fonctionnement

Lorsque la recherche sémantique est activée, le système utilise des attributs de catalogue prédéfinis (tels que le nom et la description du produit) pour interpréter la signification de la requête avec la recherche traditionnelle par mot-clé. Vous ne sélectionnez ni ne donnez la priorité aux attributs dans les paramètres.

Par exemple :

- Une recherche de « canapé en cuir » peut renvoyer des produits étiquetés « canapé en cuir ».
- « Spring dress » peut apparaître des robes de saison même lorsque « spring » n&#39;est pas dans le nom du produit.
- Les « chaussures pour le trail running » peuvent correspondre à des produits décrits comme des chaussures de randonnée ou de tout-terrain.

## Ce qui se passe lorsque vous activez la recherche sémantique

La recherche sémantique fonctionne avec votre configuration de recherche existante. Vous ne pouvez pas remplacer la recherche par mot-clé ni reconfigurer le storefront.

Lorsque la recherche sémantique est active :

- Vos [règles de marchandisage](../merchandising/rules/overview.md), [synonymes](../merchandising/synonyms/overview.md), [facettes](../merchandising/facets/overview.md), amplifications et filtres existants continuent de s’appliquer.
- La recherche sémantique permet une compréhension optimisée par l’IA de l’intention des acheteurs afin d’améliorer la pertinence des résultats avec la correspondance des mots-clés.
- Les attributs de catalogue prédéfinis sont automatiquement indexés. Vous ne sélectionnez pas d’attributs ni ne publiez de configuration distincte.

## Valider après activation

Une fois la recherche sémantique active et l’indexation terminée, Adobe recommande de valider les performances de la recherche. Utilisez la page [Performances de la recherche](../manage-results/search-performance.md) pour passer en revue les mesures et tester les requêtes importantes pour votre entreprise.

1. Consultez les termes les plus recherchés dans le rapport **Recherches uniques**.
1. Testez les requêtes historiques sans résultat à partir du rapport **Aucun résultat** sur le storefront.
1. Comparez les résultats de recherche pour les mêmes requêtes avant et après l’activation.
1. Surveillez les mesures d’engagement et de conversion des recherches, y compris le taux de clic publicitaire, le taux de conversion et le taux de résultats nuls.

## Bonnes pratiques

- Utilisez des noms et des descriptions de produits clairs et descriptifs (idéalement de 50 à 100 mots) afin que la correspondance sémantique et les mots-clés disposent d’un texte de catalogue puissant.
- Commencez par le paramètre **[!UICONTROL Enable semantic search]** par défaut, puis ajustez **[!UICONTROL Semantic boost]** ou **[!UICONTROL Similarity threshold]** uniquement si les résultats semblent trop larges ou trop étroits.
- Conservez les [synonymes](../merchandising/synonyms/overview.md) spécifiques à la marque ou hautement techniques lorsque la recherche sémantique peut ne pas couvrir des termes spécialisés.

## Dépannage

| Problème | Que faire |
| --- | --- |
| Aucune modification sur le storefront juste après l’enregistrement | Attendez la fin de l’indexation. Les catalogues volumineux peuvent prendre plus de temps. |
| Les résultats semblent trop larges | Augmentez **[!UICONTROL Similarity threshold]** ou moins **[!UICONTROL Semantic boost]** sur l’onglet **[!UICONTROL Advanced search]**. |
| Les résultats semblent trop étroits | Réduire **[!UICONTROL Similarity threshold]** ou augmenter **[!UICONTROL Semantic boost]**. |
| La recherche sémantique n’est pas disponible. | Confirmer que **[!UICONTROL Language]** est défini sur **Anglais**. |

## Restrictions {#semantic-search-limitations}

- **Langue du catalogue :** la recherche sémantique est disponible uniquement pour les catalogues en **anglais**.

## Plus d’aide sur cette rubrique

- [Recherche avancée](../settings.md#advanced-search)
- [Synonymes](../merchandising/synonyms/overview.md)
- [Performances de recherche](../manage-results/search-performance.md)
