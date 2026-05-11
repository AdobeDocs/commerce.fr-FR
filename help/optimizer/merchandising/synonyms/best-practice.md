---
title: Bonnes pratiques relatives aux synonymes
description: Découvrez les bonnes pratiques relatives à l’implémentation de synonymes dans votre boutique.
role: Admin, Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: 026bb17b-14e3-4493-ae10-376837b69de6
TQID: https://experienceleague.adobe.com/2ktYgzsiM-BvHEJNeu0-XkxhgDThHVuXMnDux3Fb9WA
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 433
ht-degree: 0%

---

# Bonnes pratiques relatives aux synonymes

Vous trouverez ci-dessous une liste des bonnes pratiques à suivre lors de la création de synonymes.

- [!DNL Adobe Commerce Optimizer] gère les fautes d&#39;orthographe par défaut. Vous pouvez configurer des synonymes afin d’inclure des mots que les acheteurs peuvent utiliser et qui diffèrent des mots spécifiés dans votre catalogue. Vous ne voulez pas perdre une vente parce que quelqu&#39;un cherche un « canapé », alors que votre produit est listé comme un « canapé ». Vous pouvez saisir un large éventail de termes de recherche en saisissant tous les mots que les clients peuvent utiliser pour trouver vos produits. Vous pouvez [définir des synonymes dans un sens ou deux](add.md#step-2-define-the-synonym-by-type) pour améliorer les résultats.

- Mappez les noms de marque et les abréviations à leurs noms complets, par exemple « HP » vers « Hewlett-Packard » et les surnoms de produit courants, par exemple « iPhone » vers « Apple iPhone ».

- Ajoutez du jargon et des termes spécifiques au secteur que les acheteurs peuvent utiliser de manière interchangeable, par exemple « baskets » et « chaussures de course ».

- Mettez régulièrement à jour la liste de synonymes en fonction des nouvelles tendances de recherche, des ajouts de produits et du comportement de l’acheteur.

- Testez l’efficacité des mappages de synonymes en analysant les résultats de recherche et les commentaires des acheteurs. Affinez les mappages pour améliorer la précision et la pertinence.

- Évitez d’utiliser des mots vides, car ils ne rendent pas les synonymes plus significatifs, mais augmentent la quantité de données à traiter. [!DNL Adobe Commerce Optimizer] filtre les « mots vides » courants en anglais des synonymes, tels que :

  a, an, et, sont, comme, à, être, mais, par, pour, si, dans, dans, est, il, non, pas, de, sur, ou, tel, que, le, leur, alors, là, ceux-ci, eux, ceci, à, était, volonté, avec

- Il n’est pas nécessaire de définir les formes au singulier et au pluriel d’un mot comme synonyme. Si votre catalogue contient un mélange de termes singuliers et pluriels, la recherche trouve l’ensemble correct de produits. Par exemple, si vous utilisez le mot « pant » dans le nom du produit et qu’un acheteur recherche « pant », l’ensemble correct de produits est renvoyé et le mot unique « pant » est proposé comme suggestion. Le terme singulier « pantalon » est souvent utilisé dans l&#39;industrie de la mode et parfois dans la vente au détail, bien que la forme plurielle « pantalon » soit plus couramment utilisée dans certaines régions. (Le mot « pantalon » fait techniquement référence à la partie d&#39;un vêtement qui couvre une jambe, ce qui explique pourquoi vous avez besoin d&#39;une « paire de pantalons » pour couvrir les deux jambes.)

- Respecter la terminologie utilisée dans votre catalogue. Gardez à l&#39;esprit qu&#39;il peut y avoir des différences régionales dans l&#39;utilisation, et parfois des différences au sein d&#39;une industrie.
