---
title: Paramètres
description: Configurez les paramètres de  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: 6ac223de-8e03-4842-8b67-92ce321d323d
TQID: https://experienceleague.adobe.com/9-BMXoWad0bbvsnwgHQrs19ZC9ngGrVE9J7PszcX4Zc
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: 867
ht-degree: 0%

---

# Paramètres

Utilisez l’espace de travail *Paramètres* pour configurer la recherche et la découverte de produits pour votre storefront. Les onglets suivants sont disponibles :

- **Facettes de prix** — Configurez les groupes et intervalles de plages de prix utilisés comme filtres de recherche.
- **Langue** — Définissez la langue du catalogue utilisée pour l&#39;indexation et la recherche.
- **Recherche avancée** — Activez la recherche sémantique et la recherche floue, et ajustez les seuils d&#39;amplification sémantique et de similarité.

>[!BEGINTABS]

>[!TAB Facettes de prix]

## Facettes de prix {#price-facets}

Vous pouvez spécifier le nombre de groupes de fourchettes de prix et la manière dont les valeurs de prix sont réparties entre eux. Chaque gamme de prix chevauche le groupe précédent d&#39;une seule. Par exemple, lorsque vous utilisez cinq groupes avec un intervalle de 20, vous obtenez des plages de prix telles que 0-20, 20-40, 40-60, 60-80 et >80. Si le catalogue ne contient pas suffisamment de produits pour remplir toutes les plages définies, l’affichage des groupes disponibles est ajusté en conséquence. Par exemple : 0-20, 60-80, >80.

**Pour configurer les facettes de prix, procédez comme suit**

1. Dans l’espace de travail **Paramètres**, sélectionnez **[!UICONTROL Facets]**.
1. Dans la section **Facette Prix**, procédez comme suit :
   - Entrez les **[!UICONTROL Number of selections]** ou les regroupements de prix qui doivent être disponibles. Jusqu&#39;à 100 regroupements de prix peuvent être définis.
   - Entrez la **[!UICONTROL Interval value]** ou la fourchette de prix de chaque groupe. La valeur maximale est de 40 000 000.
1. Cliquez sur **[!UICONTROL Save]**.

   Il faut environ 15 minutes pour que les paramètres mis à jour soient disponibles dans le storefront.

### Descriptions des champs

| Champ | Description |
| --- | --- |
| Nombre de sélections | Spécifie le nombre de regroupements de plages de prix qui peuvent être utilisés comme filtres de recherche dans le storefront. Valeur par défaut : 8, valeur maximale : 100 |
| Valeur de l’intervalle | Spécifie l&#39;intervalle de fourchette de prix pour chaque groupe. Par exemple, cinq sélections avec une valeur d’intervalle de 20 regroupements de rendement de 0 à 20, 20 à 40, 40 à 60, 60 à 80 et >80. Valeur par défaut : 5, valeur maximale : 40 000 000 |

>[!TAB Langue]

## Langue {#language}

Le paramètre Langue [!DNL Adobe Commerce Optimizer] indique la langue attendue lors de la lecture du catalogue et de l’écriture de l’index.

Les langues ont différents ensembles de règles grammaticales : la façon dont les mots sont séparés, les verbes et les formes de mots, par exemple.
Le paramètre Langue garantit que l’ensemble correct de règles est appliqué au mécanisme d’indexation.

Définissez le paramètre Langue sur la langue principale du catalogue. Lorsque vous modifiez la langue de l’index, il peut s’écouler de 5 à 60 minutes avant que la modification n’apparaisse sur le storefront, selon la taille et la complexité du catalogue.

| Langue | Code |
|----|----|
| Arabe | ar |
| Arménien | hy |
| Basque | ue |
| Bengali | bn |
| Brésilien | pt-br |
| Bulgare | bg |
| Catalan | ca |
| Chinois (simplifié) | zh-cn |
| Chinois (traditionnel) | zh-tw |
| Tchèque | cs |
| Danois | jour |
| Néerlandais | nl |
| Anglais | fr |
| Estonien | et |
| Finlandais | fi |
| Français | fr |
| Galicien | gl |
| Allemand | de |
| Grec | el |
| Hindi | bonjour |
| Hongrois | hu |
| Indonésien | id |
| Irlandais | ga |
| Italien | it |
| Japonais (Katakana) | ja |
| Coréen | ko |
| Letton | lv |
| Lituanien | lt |
| Norvégien | non |
| Perse | fa |
| Portugais | pt |
| Roumain | ro |
| Russe | ru |
| Sorani | ku |
| Espagnol | es |
| Suédois | sv |
| Turc | tr |
| Thaïlandais | ème |

>[!TAB Recherche avancée]

## Recherche avancée {#advanced-search}

Utilisez l’onglet **[!UICONTROL Advanced search]** pour gérer la recherche au même endroit. [!DNL Adobe Commerce Optimizer] offre une expérience de recherche unifiée sur le storefront ; vous ne configurez pas la recherche par mot-clé et la recherche sémantique séparément pour les acheteurs. **[!UICONTROL Enable semantic search]** est **activé par défaut** pour les catalogues anglais éligibles. La recherche sémantique fonctionne parallèlement à votre configuration existante ; les [règles de marchandisage](./merchandising/rules/overview.md), [synonymes](./merchandising/synonyms/overview.md), [facettes](./merchandising/facets/overview.md), Boosts et filtres continuent de s’appliquer. Le système utilise automatiquement des attributs de catalogue prédéfinis ; vous ne sélectionnez pas d’attributs ni ne leur donnez de priorité dans l’Administration. Aucune modification du storefront ou du développeur n’est requise.

![Paramètres de recherche avancée](./assets/advanced-search.png)

**Pour gérer la recherche sémantique :**

1. Dans l’espace de travail **Paramètres**, sélectionnez l’onglet **[!UICONTROL Advanced search]** .
1. Sous **[!UICONTROL Enable semantic search]**, confirmez que la recherche sémantique est activée ou désactivez-la si vous ne souhaitez pas de correspondance sémantique.
1. Cliquez sur **[!UICONTROL Save]** si vous modifiez les commandes de basculement ou de réglage.

   Les résultats de recherche sont mis à jour une fois l’indexation terminée. Pour un catalogue de taille moyenne, l’indexation peut prendre jusqu’à une demi-heure. Pour les catalogues volumineux contenant des millions de produits, cela peut prendre quelques heures.

### Réglage facultatif

Une fois la recherche sémantique activée, vous pouvez ajuster les éléments suivants sur le même onglet :

- **[!UICONTROL Semantic boost]** — Donner un coup de pouce pour prioriser les résultats pertinents sémantiquement dans le classement. Augmentez la valeur lorsque les correspondances sémantiques doivent peser plus lourd dans le jeu de résultats ; réduisez-la lorsque les résultats semblent trop larges.
- **[!UICONTROL Similarity threshold]** — Définit le score de similarité minimal (en pourcentage) pour une correspondance sémantique. Des valeurs inférieures renvoient plus de résultats (rappel plus élevé) mais peuvent inclure des correspondances plus faibles. Des valeurs plus élevées renvoient moins de correspondances plus précises (précision plus élevée).

  >[!NOTE]
  >
  > La recherche sémantique est prise en charge pour les catalogues **anglais** uniquement. La sélection d’une autre langue dans l’onglet **[Langue](#language)** désactive **[!UICONTROL Enable semantic search]**.

- **[!UICONTROL Fuzzy search]** — Activez **** pour trouver des correspondances proches pour les requêtes de recherche, ce qui permet de corriger les fautes de frappe et les variations mineures.
- **[!UICONTROL Fuzzy search similarity threshold]** — Définissez la similarité minimale (en pourcentage) requise pour que les correspondances floues apparaissent. Les seuils inférieurs renvoient des correspondances plus approximatives ; augmentez le seuil si les résultats flous semblent trop larges.

Pour en savoir plus sur les avantages, les conseils de validation, les bonnes pratiques, le dépannage et les limites, voir [Recherche sémantique](setup/semantic-search.md).

### Descriptions des champs

| Contrôle | Description |
| --- | --- |
| Activer la recherche sémantique | Lorsqu’elle est activée, la recherche utilise la signification et le contexte ainsi que la correspondance des mots-clés. Les attributs de catalogue prédéfinis sont utilisés automatiquement ; aucune configuration d’attribut n’est requise dans l’administration. Activé par défaut pour les clients [!DNL Adobe Commerce Optimizer]. |
| Amplification sémantique | Amplification appliquée pour prioriser les résultats pertinents sémantiquement dans le classement. |
| Seuil de similarité | Score de similarité minimal (pourcentage) pour une correspondance sémantique. Des valeurs faibles favorisent le rappel ; des valeurs élevées favorisent la précision. |
| Recherche floue | Lorsque **on**, la recherche trouve des correspondances proches pour les requêtes (par exemple, des variations mineures). |
| Seuil de similarité de recherche floue | Les correspondances approximatives de similarité minimale (pourcentage) doivent être satisfaites pour apparaître dans les résultats. |

>[!ENDTABS]
