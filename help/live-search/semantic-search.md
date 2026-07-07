---
title: Recherche Sémantique
description: Activez la recherche sémantique d’IA à partir  [!DNL Live Search]  paramètres . Aucune configuration d’attribut ou modification du storefront n’est requise.
role: Admin
recommendations: noCatalog
source-git-commit: 94598c3cbc6b9fa84f92532e42ec5e9027c5b1fc
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Recherche sémantique

La recherche sémantique utilise l’IA pour comprendre ce que les acheteurs signifient, et pas seulement les mots exacts qu’ils tapent. Les requêtes telles que « robe pour un mariage sur la plage » ou « chaussures confortables pour rester debout toute la journée » peuvent renvoyer des produits pertinents même si votre catalogue n’utilise pas ces expressions exactes.

[!DNL Live Search] combine la correspondance de mots-clés et la correspondance sémantique dans une seule expérience de recherche. Vous ne gérez pas de modes mot-clé et sémantique distincts sur le storefront. [!DNL Live Search] ne propose pas de commandes sémantiques avancées (par exemple, des curseurs d’amplification ou de similarité) dans l’Administration. Vous pouvez activer ou désactiver la recherche sémantique.

## Activation par déploiement

La recherche sémantique est gérée à partir de l’espace de travail **Paramètres** dans l’Administration des [!DNL Live Search] (**Marketing** > *SEO et recherche* > **[!DNL Live Search]**). [!DNL Adobe Commerce as a Cloud Service] utilise la même interface [!DNL Live Search] que les commerçants PaaS.

## Avantages

- **Moins de recherches sans résultat** — Les acheteurs trouvent des produits lorsque leur libellé ne correspond pas exactement au texte du catalogue.
- **Résultats plus pertinents** — Les requêtes descriptives naturelles renvoient des correspondances utiles en fonction du sens et du contexte.
- **Gestion des synonymes moins fréquente** — Les variantes de mots courantes (par exemple, canapé et canapé) sont souvent gérées sans listes de synonymes manuelles.
- **Aucun travail de storefront ou de développeur** — La recherche sémantique ne nécessite aucun changement de code de thème, de widget ou d&#39;API. Les commerçants PaaS l’activent dans Paramètres ; [!DNL Adobe Commerce as a Cloud Service] clients la reçoivent activée par défaut.

## Fonctionnement

Lorsque la recherche sémantique est activée, [!DNL Live Search] utilise des attributs de catalogue prédéfinis choisis par le système (tels que le nom et la description du produit) pour interpréter la signification de la requête avec la recherche traditionnelle par mot-clé. Vous ne sélectionnez ni ne donnez la priorité aux attributs dans l’Administration.

Par exemple :

- Une recherche de « canapé en cuir » peut renvoyer des produits étiquetés « canapé en cuir ».
- « Spring dress » peut apparaître des robes de saison même lorsque « spring » n&#39;est pas dans le nom du produit.
- Les « chaussures pour le trail running » peuvent correspondre à des produits décrits comme des chaussures de randonnée ou de tout-terrain.

## Ce qui se passe lorsque vous activez la recherche sémantique

La recherche sémantique fonctionne avec votre configuration de [!DNL Live Search] existante. Vous ne pouvez pas remplacer la recherche par mot-clé ni reconfigurer le storefront.

Lorsque la recherche sémantique est active :

- Vos paramètres existants [règles de recherche](rules.md), [synonymes](synonyms.md), [facettes](facets.md), amplification et [marchandisage de catégorie](category-merch.md) continuent de s’appliquer.
- La recherche sémantique permet une compréhension optimisée par l’IA de l’intention des acheteurs afin d’améliorer la pertinence des résultats avec la correspondance des mots-clés.
- Les attributs de catalogue prédéfinis sont automatiquement indexés. Vous ne sélectionnez pas d’attributs ni ne publiez de configuration distincte.

## Gestion de la recherche sémantique dans l’administration

Accédez à l’espace de travail [Paramètres](settings.md#semantic-search) pour afficher ou modifier le bouton (bascule) **[!UICONTROL Semantic search]**.

>[!NOTE]
>
> La recherche sémantique est disponible uniquement pour les catalogues **anglais**. Si vous modifiez **Langue** en catalogue non anglais dans l’espace de travail **Paramètres**, **[!UICONTROL Semantic search]** est automatiquement désactivé.

### Pour les commerçants PaaS

Les commerçants Adobe Commerce on Cloud et on-premise doivent activer manuellement la recherche sémantique :

1. Dans Admin, accédez à **Marketing** > *SEO et recherche* > **[!DNL Live Search]**.
1. Dans l’espace de travail **Paramètres**, activez **[!UICONTROL Semantic search]**.

   Lorsqu’elle est activée, la recherche correspond aux produits en fonction de leur signification et de leur contexte, ce qui peut produire des résultats plus pertinents, moins de recherches à résultat nul et une conversion améliorée.

1. Cliquez sur **[!UICONTROL Save]**.

   Les résultats de recherche sont mis à jour une fois l’indexation terminée. Pour un catalogue de taille moyenne, l’indexation peut prendre jusqu’à une demi-heure. Pour les catalogues volumineux contenant des millions de produits, cela peut prendre quelques heures.

### Pour les clients [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] clients utilisent le même espace de travail **Paramètres** dans l’administration [!DNL Live Search]. La recherche sémantique est **activée par défaut** pour les catalogues anglais éligibles. Vérifiez **[!UICONTROL Semantic search]** est activé ou désactivez-le si vous ne souhaitez pas que la correspondance sémantique soit activée sur le storefront.

Vous n’avez pas besoin d’une étape de publication ou d’une configuration de storefront distincte après avoir enregistré une modification.

## Valider après activation

Une fois la recherche sémantique active et l’indexation terminée, Adobe recommande de valider les performances de la recherche. Utilisez l’espace de travail [Performances](performance.md) pour passer en revue les mesures et tester les requêtes importantes pour votre entreprise. Ceci s’applique que la recherche sémantique ait été activée par défaut ou que vous l’ayez activée manuellement.

1. Consultez les termes les plus recherchés dans le rapport **Recherches uniques**.
1. Testez les requêtes historiques à résultat nul à partir du rapport **Résultats nuls** sur le storefront.
1. Comparez les résultats de recherche pour les mêmes requêtes avant et après l’activation.
1. Surveillez les mesures d’engagement et de conversion des recherches, y compris le taux de clic publicitaire, le taux de conversion et le taux de résultats nuls.

## Bonnes pratiques

- Utilisez des noms et des descriptions de produits clairs et descriptifs (idéalement de 50 à 100 mots) afin que la correspondance sémantique et les mots-clés disposent d’un texte de catalogue puissant.
- Conservez des synonymes [synonymes](synonyms.md) spécifiques à la marque ou hautement techniques, lorsque la recherche sémantique peut ne pas couvrir des termes spécialisés.

## Dépannage

| Problème | Que faire |
| --- | --- |
| Aucune modification sur le storefront juste après l’enregistrement | Attendez la fin de l’indexation. Les catalogues volumineux peuvent prendre plus de temps. |
| La recherche sémantique est automatiquement indisponible ou désactivée | Vérifiez **Langue** dans l’espace de travail **Paramètres** défini sur **Anglais**. |
| Il manque encore des termes courants dans les résultats | Ajoutez [synonymes](synonyms.md) pour les termes de marque ou de secteur. La recherche sémantique peut ne pas résoudre. |

## Restrictions {#semantic-search-limitations}

- **Langue du catalogue :** la recherche sémantique est disponible uniquement pour les catalogues de langue **anglaise**.
- **Contrôles d’administration :** [!DNL Live Search] fournit un contrôle d’activation/de désactivation uniquement. Vous ne pouvez pas régler l’amplification sémantique, le seuil de similarité ou la recherche floue à partir de l’espace de travail **Paramètres**.

## Plus d’aide sur cette rubrique

- [Paramètres](settings.md#semantic-search)
- [Synonymes](synonyms.md)
- [Performances](performance.md)

