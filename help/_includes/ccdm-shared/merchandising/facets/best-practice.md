---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%
---
La fonctionnalité de filtre et de facette est un composant essentiel des expériences Commerce, conçu pour améliorer l’expérience de l’acheteur en permettant à celui-ci de réduire les résultats de recherche et de trouver des produits plus efficacement. Cette fonctionnalité permet aux acheteurs de trier de vastes catalogues d’articles en appliquant des critères spécifiques, ce qui rend le processus d’achat plus rapide, plus facile et plus satisfaisant. En implémentant des filtres et des facettes efficaces et conviviaux pour les acheteurs, vous pouvez aider les clients à trouver rapidement et efficacement ce dont ils ont besoin, ce qui améliore la satisfaction et les taux de conversion.

## Conseils pour optimiser les facettes

- Déterminez les attributs de produit pertinents, tels que le titre, la catégorie, la marque, la gamme de prix, la couleur et la taille, puis définissez-les comme [facettes dynamiques](type.md). 
- Définissez et triez des attributs de produit cohérents dans l’ensemble de votre catalogue et hautement pertinents pour vos produits afin d’améliorer la pertinence et les fonctionnalités de filtrage de vos acheteurs.
- Assurez-vous que les libellés des facettes sont faciles à comprendre et nommés de manière cohérente sur l’ensemble du site. Par exemple, utilisez `Price Range` au lieu de `Cost`.
- Évitez d’accabler les acheteurs en limitant le nombre de facettes aux plus importantes. Un nombre trop élevé d’options peut entraîner une fatigue liée aux décisions. Par défaut, la configuration de facettes est limitée à un maximum de 100 attributs configurés en tant que facettes et 30 intervalles renvoyés dans chaque facette. En savoir plus sur les [limites de facettes](/help/optimizer/boundaries-limits.md#catalog-views-and-policies). 
- Autoriser les acheteurs à sélectionner plusieurs critères de filtre simultanément pour affiner les résultats. Par exemple, laisser les acheteurs sélectionner les couleurs « Rouge » et « Bleu ».
- Affichez le nombre de produits disponibles à côté de chaque facette pour donner aux acheteurs une idée des résultats de recherche auxquels ils peuvent s’attendre.
- Pour que l’interface reste propre et gérable, en particulier sur les appareils mobiles, implémentez des sections de facettes réductibles.
- Permet aux utilisateurs de réinitialiser facilement les facettes individuelles ou tous les filtres sélectionnés pour lancer une nouvelle recherche.
- Si vous disposez d’un grand nombre d’attributs, envisagez de combiner les attributs en un seul méta-attribut. Par exemple, les chaussures ont des tailles numériques, tandis que les chemises sont généralement de taille « S/M/L/XL ». Ces deux types de tailles peuvent être combinés en un seul attribut consultable.
