---
title: Types de synonymes
description: Les synonymes  [!DNL Live Search]  et bidirectionnels élargissent la définition des mots-clés.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '466'
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

### Utiliser des mots simples

Si un terme de synonyme contient plusieurs mots, l’espace vide entre les mots les traite comme des synonymes distincts. Par exemple, si vous définissez « pièce d’horlogerie » comme synonyme de « montre », les mots « heure » et « pièce » sont traités comme des synonymes distincts.

### Utilisation du singulier et du pluriel

Il n’est pas nécessaire de définir les formes au singulier et au pluriel d’un mot comme synonyme. Si votre catalogue contient un mélange de termes singuliers et pluriels, la recherche trouve l’ensemble correct de produits. Par exemple, si vous utilisez le mot « pant » dans le nom du produit et qu’un acheteur recherche « pant », l’ensemble correct de produits est renvoyé et le mot unique « pant » est proposé comme suggestion. Le terme singulier « pantalon » est souvent utilisé dans l&#39;industrie de la mode et parfois dans la vente au détail, bien que la forme plurielle « pantalon » soit plus couramment utilisée dans certaines régions. (Le mot « pantalon » fait techniquement référence à la partie d&#39;un vêtement qui couvre une jambe, ce qui explique pourquoi vous avez besoin d&#39;une « paire de pantalons » pour couvrir les deux jambes.)

### Cohérence

Respecter la terminologie utilisée dans votre catalogue. Gardez à l&#39;esprit qu&#39;il peut y avoir des différences régionales dans l&#39;utilisation, et parfois des différences au sein d&#39;une industrie.
