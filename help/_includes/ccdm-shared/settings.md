---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%
---
Utilisez l’espace de travail *Paramètres* pour configurer la recherche et la découverte de produits pour votre storefront. Les onglets suivants sont disponibles :

- **Facettes** : configurez les groupes de gammes de prix et les intervalles utilisés comme filtres de recherche.
- **Langue** : définissez la langue du catalogue utilisée pour l&#39;indexation et la recherche.
- **Recherche avancée** : activez la recherche sémantique et la recherche floue, et ajustez les seuils d’amplification sémantique et de similarité.

## Accès à l’espace de travail Paramètres

La façon dont vous ouvrez l’espace de travail *Paramètres* dépend du produit que vous utilisez :

- **Administrateur Adobe Commerce** (Adobe Commerce as a Cloud Service) : Sélectionnez *Marchandisage* > **Paramètres De Marchandisage**.
- **Adobe Commerce Optimizer Studio** : Sélectionnez *Marchandisage* > **Paramètres**.

>[!BEGINTABS]

>[!TAB Facettes de prix]

## Facettes de prix {#price-facets}

Vous pouvez spécifier le nombre de groupes de fourchettes de prix et la manière dont les valeurs de prix sont réparties entre eux. Chaque gamme de prix chevauche le groupe précédent d&#39;une seule. Par exemple, cinq groupes avec un intervalle de 20 créent des plages de prix : 0-20, 20-40, 40-60, 60-80 et >80. Si le catalogue ne contient pas suffisamment de produits pour remplir toutes les plages définies, l’affichage des groupes disponibles est ajusté en conséquence. Par exemple : 0-20, 60-80, >80.

**Pour configurer les facettes de prix :**

1. Dans l’espace de travail **Paramètres**, sélectionnez **[!UICONTROL Facets]**.
1. Dans la section **Facette de prix**, procédez comme suit :
   - Entrez les **[!UICONTROL Number of selections]**, ou les regroupements de prix qui seront disponibles. Jusqu&#39;à 100 regroupements de prix peuvent être définis.
   - Entrez **[!UICONTROL Interval value]**, ou la plage de prix pour chaque groupe. La valeur maximale est de 40 000 000.
1. Cliquez sur **[!UICONTROL Save]**.

   Il faut environ 15 minutes pour que les paramètres mis à jour soient disponibles dans le storefront.

### Descriptions des champs de facettes de prix

| Champ | Description |
| --- | --- |
| Nombre de sélections | Spécifie le nombre de regroupements de plages de prix qui peuvent être utilisés comme filtres de recherche dans le storefront. Valeur par défaut : 8, valeur maximale : 100 |
| Valeur de l’intervalle | Spécifie l&#39;intervalle de fourchette de prix pour chaque groupe. Par exemple, cinq sélections avec une valeur d’intervalle de 20 regroupements de rendement de 0 à 20, 20 à 40, 40 à 60, 60 à 80 et >80. Valeur par défaut : 5, valeur maximale : 40 000 000 |

>[!TAB Langue]

## Langue {#language}

Le paramètre Langue indique au système la langue attendue lors de la lecture du catalogue et de l’écriture de l’index.

Les langues ont différents ensembles de règles grammaticales : la façon dont les mots sont séparés, les verbes et les formes de mots, par exemple.
Le paramètre Langue garantit que l’ensemble correct de règles est appliqué au mécanisme d’indexation.

Définissez le paramètre Langue sur la langue principale du catalogue. La modification de la langue d’index prend entre 5 et 60 minutes pour apparaître sur le storefront, selon la taille et la complexité du catalogue.

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

Utilisez l’onglet **[!UICONTROL Advanced search]** pour gérer la recherche au même endroit. Le système offre une expérience de recherche unifiée sur le storefront ; vous ne configurez pas la recherche par mot-clé et la recherche sémantique séparément pour les acheteurs. **[!UICONTROL Enable semantic search]** est **activé par défaut** pour les catalogues anglais éligibles. La recherche sémantique fonctionne avec votre configuration existante ; [les règles de marchandisage](./merchandising/rules/overview.md), [les synonymes](./merchandising/synonyms/overview.md), [les facettes](./merchandising/facets/overview.md), les amplifications et les filtres continuent de s’appliquer. Le système utilise automatiquement des attributs de catalogue prédéfinis ; vous ne sélectionnez pas d’attributs ni ne leur donnez de priorité dans les paramètres. Aucune modification du storefront ou du développeur n’est requise.

![Paramètres de recherche avancée](/help/assets/ccdm-shared/advanced-search.png)

**Pour gérer la recherche sémantique :**

1. Dans l’espace de travail **Paramètres**, sélectionnez l’onglet **[!UICONTROL Advanced search]**.
1. Sous **[!UICONTROL Enable semantic search]**, confirmez que la recherche sémantique est activée ou désactivez-la si vous ne souhaitez pas de correspondance sémantique.
1. Cliquez sur **[!UICONTROL Save]** si vous modifiez les commandes de basculement ou de réglage.

   Les résultats de recherche sont mis à jour une fois l’indexation terminée. Pour un catalogue de taille moyenne, l’indexation peut prendre jusqu’à 30 minutes. Pour les catalogues volumineux contenant des millions de produits, cela peut prendre quelques heures.

### Réglage facultatif

Une fois la recherche sémantique activée, vous pouvez ajuster les éléments suivants sur le même onglet :

- **[!UICONTROL Semantic boost]** : pour prioriser les résultats pertinents sémantiquement dans le classement, appliquez un coup de pouce. Augmentez la valeur lorsque les correspondances sémantiques doivent peser plus lourd dans le jeu de résultats ; réduisez-la lorsque les résultats semblent trop larges.
- **[!UICONTROL Similarity threshold]** : définissez le score de similarité minimal (en pourcentage) pour une correspondance sémantique. Des valeurs inférieures renvoient plus de résultats (rappel plus élevé) mais peuvent inclure des correspondances plus faibles. Des valeurs plus élevées renvoient moins de correspondances plus précises (précision plus élevée).
- **[!UICONTROL Fuzzy search]** : pour rechercher des correspondances proches pour les requêtes de recherche et corriger les fautes de frappe et les variations mineures, activez **l&#39;option**.
- **[!UICONTROL Fuzzy search similarity threshold]** : définissez la similarité minimale (en pourcentage) requise pour que les correspondances floues apparaissent. Les seuils inférieurs renvoient des correspondances plus approximatives ; augmentez le seuil si les résultats flous semblent trop larges.

>[!NOTE]
>
> La recherche sémantique est prise en charge pour les catalogues **anglais** uniquement. La sélection d&#39;une autre langue dans l&#39;onglet **[!UICONTROL Language]** désactive **[!UICONTROL Enable semantic search]**.

Pour en savoir plus sur les avantages, les conseils de validation, les bonnes pratiques, le dépannage et les limites, consultez [Recherche sémantique](/help/optimizer/setup/semantic-search.md).

### Descriptions des champs de recherche avancée

| Contrôle | Description |
| --- | --- |
| Activer la recherche sémantique | Lorsqu’elle est activée, la recherche utilise la signification et le contexte ainsi que la correspondance des mots-clés. Les attributs de catalogue prédéfinis sont utilisés automatiquement ; aucune configuration d’attribut n’est requise dans les paramètres. Activé par défaut. |
| Amplification sémantique | Amplification appliquée pour prioriser les résultats pertinents sémantiquement dans le classement. |
| Seuil de similarité | Score de similarité minimal (pourcentage) pour une correspondance sémantique. Des valeurs faibles favorisent le rappel ; des valeurs élevées favorisent la précision. |
| Recherche floue | Lorsque **on**, la recherche trouve des correspondances proches pour les requêtes (par exemple, des variations mineures). |
| Seuil de similarité de recherche floue | Les correspondances approximatives de similarité minimale (pourcentage) doivent être satisfaites pour apparaître dans les résultats. |

>[!ENDTABS]
