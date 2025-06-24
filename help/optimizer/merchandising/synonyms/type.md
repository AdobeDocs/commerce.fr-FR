---
title: Types de synonymes
description: Découvrez les différents types de synonymes dans  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Types de synonymes

Les synonymes unidirectionnels et bidirectionnels élargissent la définition des mots-clés. Certains sont interchangeables avec le mot-clé, tandis que d’autres représentent un sous-ensemble du mot-clé.

## Bidirectionnel

Les synonymes bidirectionnels ont la même signification et renvoient les mêmes résultats de recherche. Dans l’exemple suivant, le premier mot affiché en gras est le mot-clé utilisé dans le catalogue, suivi de mots ayant la même signification que le mot-clé d’origine. Vous pouvez créer une simple paire de synonymes bidirectionnels ou une chaîne de plusieurs synonymes bidirectionnels pour le même mot-clé.

**veste** ![sélecteur bidirectionnel](../../assets/btn-two-way.png) manteau
**pantalon** ![Sélecteur bidirectionnel](../../assets/btn-two-way.png) pantalon ![Sélecteur bidirectionnel](../../assets/btn-two-way.png) pantalon

## Unidirectionnel

Un synonyme unidirectionnel est un sous-ensemble d’un mot-clé, mais avec une signification plus spécifique. Par exemple, les capris et les shorts sont des pantalons, mais tous les pantalons ne sont pas des capris ou des shorts. Une recherche de pantalon comprend le capris et le short. Cependant, une recherche de shorts ne renvoie pas capris.

**sweat-shirt** ![Sélecteur unidirectionnel](../../assets/btn-one-way.png) sweat à capuche
**pantalon** ![Sélecteur unidirectionnel](../../assets/btn-one-way.png) capris ![Sélecteur unidirectionnel multiple](../../assets/btn-multiple-one-way.png) pantalon-longueur-mollet ![Sélecteur unidirectionnel multiple](../../assets/btn-multiple-one-way.png) poussoirs à pédale

## Comportement de synonyme à plusieurs mots

Pour les synonymes à plusieurs mots, [!DNL Adobe Commerce Optimizer] considère le synonyme comme une expression. Par exemple, si vous créez un synonyme bidirectionnel **table de salle à manger** ![sélecteur bidirectionnel](../../assets/btn-two-way.png) **table de cuisine** ![sélecteur bidirectionnel](../../assets/btn-two-way.png) **table à manger**, [!DNL Adobe Commerce Optimizer] effectue des recherches dans tous les champs définis pour pouvoir rechercher l’occurrence de **table de salle à manger** ou **table de cuisine** ou **table**.

Si aucun synonyme n’est créé et qu’un acheteur recherche **table de cuisine**, [!DNL Adobe Commerce Optimizer] recherche les termes n’importe où dans les champs pouvant faire l’objet d’une recherche, même dans différents champs, par exemple **table** dans le champ nom et **cuisine** dans le mot-clé meta.

Après avoir créé un synonyme, le comportement de recherche change pour rechercher l’expression exacte **table de cuisine**. Cela peut réduire le nombre de résultats, car seuls les produits avec l’expression exacte seront affichés.

Si vous souhaitez que les termes soient recherchés séparément comme auparavant, vous pouvez [créer un ticket d’assistance](https://experienceleague.adobe.com/fr/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Si la demande est suffisante, [!DNL Adobe Commerce Optimizer] envisagerons d’ajouter cette fonctionnalité au produit dans une version ultérieure.
