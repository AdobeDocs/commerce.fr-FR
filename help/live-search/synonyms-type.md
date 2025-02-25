---
title: Types de synonymes
description: Les synonymes  [!DNL Live Search]  et bidirectionnels élargissent la définition des mots-clés.
exl-id: f5522428-c7cc-4627-a09b-d9148918c127
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---

# Types de synonymes

Les synonymes unidirectionnels et bidirectionnels élargissent la définition des mots-clés. Certains sont interchangeables avec le mot-clé, tandis que d’autres représentent un sous-ensemble du mot-clé.

## Bidirectionnel

Les synonymes bidirectionnels ont la même signification et renvoient les mêmes résultats de recherche. Dans l’exemple suivant, le premier mot affiché en gras est le mot-clé utilisé dans le catalogue, suivi de mots ayant la même signification que le mot-clé d’origine. Vous pouvez créer une simple paire de synonymes bidirectionnels ou une chaîne de plusieurs synonymes bidirectionnels pour le même mot-clé.

**veste** ![sélecteur bidirectionnel](assets/btn-two-way.png) manteau
**pantalon** ![Sélecteur bidirectionnel](assets/btn-two-way.png) pantalon ![Sélecteur bidirectionnel](assets/btn-two-way.png) pantalon

## Unidirectionnel

Un synonyme unidirectionnel est un sous-ensemble d’un mot-clé, mais avec une signification plus spécifique. Par exemple, les capris et les shorts sont des pantalons, mais tous les pantalons ne sont pas des capris ou des shorts. Une recherche de pantalon comprend le capris et le short. Cependant, une recherche de shorts ne renvoie pas capris.

**sweat-shirt** ![Sélecteur unidirectionnel](assets/btn-one-way.png) sweat à capuche
**pantalon** ![Sélecteur unidirectionnel](assets/btn-one-way.png) capris ![Sélecteur unidirectionnel multiple](assets/btn-multiple-one-way.png) pantalon-longueur-mollet ![Sélecteur unidirectionnel multiple](assets/btn-multiple-one-way.png) poussoirs à pédale

## Bonnes pratiques

Gardez à l’esprit les bonnes pratiques suivantes pour tirer le meilleur parti des synonymes [!DNL Live Search].

### Éviter les « mots vides »

[!DNL Live Search] filtre les « mots vides » courants en anglais des synonymes, tels que :

a, an, et, sont, comme, à, être, mais, par, pour, si, dans, dans, est, il, non, pas, de, sur, ou, tel, que, le, leur, alors, là, ceux-ci, eux, ceci, à, était, volonté, avec

Les mots vides ne rendent pas les synonymes plus significatifs, mais augmentent la quantité de données à traiter.

### Utilisation du singulier et du pluriel

Il n’est pas nécessaire de définir les formes au singulier et au pluriel d’un mot comme synonyme. Si votre catalogue contient un mélange de termes singuliers et pluriels, la recherche trouve l’ensemble correct de produits. Par exemple, si vous utilisez le mot « pant » dans le nom du produit et qu’un acheteur recherche « pant », l’ensemble correct de produits est renvoyé et le mot unique « pant » est proposé comme suggestion. Le terme singulier « pantalon » est souvent utilisé dans l&#39;industrie de la mode et parfois dans la vente au détail, bien que la forme plurielle « pantalon » soit plus couramment utilisée dans certaines régions. (Le mot « pantalon » fait techniquement référence à la partie d&#39;un vêtement qui couvre une jambe, ce qui explique pourquoi vous avez besoin d&#39;une « paire de pantalons » pour couvrir les deux jambes.)

### Cohérence

Respecter la terminologie utilisée dans votre catalogue. Gardez à l&#39;esprit qu&#39;il peut y avoir des différences régionales dans l&#39;utilisation, et parfois des différences au sein d&#39;une industrie.

## Comportement de synonyme à plusieurs mots

Pour les synonymes à plusieurs mots, Commerce considère le synonyme comme une expression. Par exemple, si vous créez un synonyme bidirectionnel **table de salle à manger** ![Sélecteur bidirectionnel](assets/btn-two-way.png) **table de cuisine** ![Sélecteur bidirectionnel](assets/btn-two-way.png) **table à manger**, Commerce effectue une recherche dans tous les champs définis sur « searchable » pour l’occurrence de **table de salle à manger** ou **table de cuisine** ou **table**.

Si aucun synonyme n’est créé et qu’un acheteur recherche **table de cuisine**, Commerce recherche les termes n’importe où dans les champs pouvant faire l’objet d’une recherche, même dans différents champs, par exemple **table** dans le champ nom et **cuisine** dans le mot-clé meta.

Après avoir créé un synonyme, le comportement de recherche change pour rechercher l’expression exacte **table de cuisine**. Cela peut réduire le nombre de résultats, car seuls les produits avec l’expression exacte seront affichés.

Si vous souhaitez que les termes soient recherchés séparément comme auparavant, vous pouvez [créer un ticket d’assistance](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Si la demande est suffisante, Commerce envisagera d’ajouter cette fonctionnalité au produit dans une version ultérieure.
