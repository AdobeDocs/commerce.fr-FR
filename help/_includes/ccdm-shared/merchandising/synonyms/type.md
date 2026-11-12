---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%
---
Les synonymes unidirectionnels et bidirectionnels élargissent la définition des mots-clés. Certains sont interchangeables avec le mot-clé, tandis que d’autres représentent un sous-ensemble du mot-clé.

## Bidirectionnel

Les synonymes bidirectionnels ont la même signification et renvoient les mêmes résultats de recherche. Dans l’exemple suivant, le premier mot affiché en gras est le mot-clé utilisé dans le catalogue, suivi de mots ayant la même signification que le mot-clé d’origine. Vous pouvez créer une simple paire de synonymes bidirectionnels ou une chaîne de plusieurs synonymes bidirectionnels pour le même mot-clé.

**veste** ![Sélecteur bidirectionnel](/help/assets/ccdm-shared/synonyms/two-way.png) manteau
**pantalon** ![Sélecteur bidirectionnel](/help/assets/ccdm-shared/synonyms/two-way.png) pantalon ![Sélecteur bidirectionnel](/help/assets/ccdm-shared/synonyms/two-way.png)

## Unidirectionnel

Un synonyme unidirectionnel est un sous-ensemble d’un mot-clé, mais avec une signification plus spécifique. Par exemple, les capris et les shorts sont des pantalons, mais tous les pantalons ne sont pas des capris ou des shorts. Une recherche de pantalon comprend le capris et le short. Cependant, une recherche de shorts ne renvoie pas capris.

**sweat** ![Sélecteur unidirectionnel](/help/assets/ccdm-shared/synonyms/one-way.png) sweat à capuche
**pantalon** ![Sélecteur unidirectionnel](/help/assets/ccdm-shared/synonyms/one-way.png) capris ![Sélecteur unidirectionnel](/help/assets/ccdm-shared/synonyms/one-way.png) pantalon-longueur-mollet ![Sélecteur unidirectionnel](/help/assets/ccdm-shared/synonyms/one-way.png) poussoirs de pédale

## Comportement de synonyme à plusieurs mots

Pour les synonymes à plusieurs mots, le système considère le synonyme comme une expression. Par exemple, si vous créez un synonyme bidirectionnel **table de salle à manger** ![sélecteur bidirectionnel](/help/assets/ccdm-shared/synonyms/two-way.png) **table de cuisine** ![sélecteur bidirectionnel](/help/assets/ccdm-shared/synonyms/two-way.png) **table à manger**, le système recherche dans tous les champs définis pour pouvoir rechercher l’occurrence de **table de salle à manger** ou **table de cuisine** ou **table à manger**.

Si aucun synonyme n’est créé et qu’un acheteur recherche **table de cuisine**, le système recherche les termes n’importe où dans les champs pouvant faire l’objet d’une recherche, même dans différents champs, par exemple **table** dans le champ nom et **cuisine** dans le mot-clé meta.

Après avoir créé un synonyme, le comportement de recherche change pour rechercher l&#39;expression exacte **table de cuisine**. Cela peut réduire le nombre de résultats, car seuls les produits avec l’expression exacte seront affichés.

Si vous souhaitez que les termes soient recherchés séparément comme auparavant, vous pouvez [créer un ticket d&#39;assistance](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide).
