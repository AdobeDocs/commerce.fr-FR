---
title: Bonnes pratiques relatives aux facettes
description: Découvrez les bonnes pratiques relatives à l’implémentation des facettes dans votre boutique.
role: Admin, Developer
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Bonnes pratiques relatives aux facettes

La fonctionnalité de filtre et de facette est un composant essentiel de votre site [!DNL Adobe Commerce Optimizer], conçu pour améliorer l’expérience de l’acheteur en permettant à celui-ci de réduire les résultats de recherche et de trouver des produits plus efficacement. Cette fonctionnalité permet aux acheteurs de trier de vastes catalogues d’articles en appliquant des critères spécifiques, ce qui rend le processus d’achat plus rapide, plus facile et plus satisfaisant. En implémentant des filtres et des facettes efficaces et conviviaux pour les acheteurs, vous pouvez aider les clients à trouver rapidement et efficacement ce dont ils ont besoin, ce qui améliore la satisfaction et les taux de conversion.

## Conseils pour optimiser les facettes

- Déterminez les attributs les plus pertinents et utiles de vos produits, tels que le titre, la catégorie, la marque, la gamme de prix, la couleur et la taille, puis définissez-les comme [ facettes dynamiques ](type.md). 
- Définissez et triez des attributs de produit cohérents dans l’ensemble de votre catalogue et hautement pertinents pour vos produits afin d’améliorer la pertinence et les fonctionnalités de filtrage de vos acheteurs.
- Assurez-vous que les libellés des facettes sont faciles à comprendre et nommés de manière cohérente sur l’ensemble du site. Par exemple, utilisez « Plage de prix » au lieu de « Coût ».
- Évitez d’accabler les acheteurs en limitant le nombre de facettes aux plus importantes. Un nombre trop élevé d’options peut entraîner une fatigue liée aux décisions. Par défaut, la [!DNL Adobe Commerce Optimizer] est limitée à un maximum de 100 attributs configurés en tant que facettes et 30 intervalles renvoyés dans chaque facette. En savoir plus sur les [limites des facettes](../../boundaries-limits.md#catalog-views-and-policies). 
- Autoriser les acheteurs à sélectionner plusieurs critères de filtre simultanément pour affiner les résultats. Par exemple, laisser les acheteurs sélectionner les couleurs « Rouge » et « Bleu ».
- Affichez le nombre de produits disponibles à côté de chaque facette pour donner aux acheteurs une idée des résultats de recherche auxquels ils peuvent s’attendre.
- Implémentez des sections de facettes réductibles pour que l’interface reste propre et gérable, en particulier sur les appareils mobiles.
- Permet aux utilisateurs de réinitialiser facilement les facettes individuelles ou tous les filtres sélectionnés pour lancer une nouvelle recherche.
- Si vous devez composer avec un grand nombre d’attributs, envisagez de combiner les attributs en un seul « méta-attribut ». Par exemple, les chaussures ont généralement des tailles numériques, tandis que les chemises sont généralement de taille « S/M/L/XL ». Ces deux types de tailles peuvent être combinés en un seul attribut consultable.
