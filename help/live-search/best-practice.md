---
title: Bonnes pratiques [!DNL Live Search]
description: Découvrez les bonnes pratiques d’implémentation  [!DNL Live Search]  dans votre boutique.
role: Admin, Developer
exl-id: f7700339-fb13-42fe-a249-17cd4ba36e1b
source-git-commit: a22a57f52503811a3a3e9294174a6626c5630b79
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 0%

---

# Bonnes pratiques

Cet article aide les marchandiseurs à améliorer leurs fonctionnalités de recherche de site, afin d’offrir une expérience d’achat transparente et efficace qui optimise les taux de conversion. En suivant les stratégies décrites, vous apprendrez à mettre en œuvre des fonctionnalités de recherche avancées et à affiner continuellement votre outil de recherche pour obtenir des performances optimales avec Adobe Commerce [!DNL Live Search].

Plusieurs facteurs clés déterminent la pertinence et l’efficacité des résultats de recherche :

- Des données de produit bien structurées garantissent que les algorithmes de recherche peuvent efficacement faire correspondre les produits aux requêtes. Des données de produit de faible qualité entraînent des résultats de recherche peu pertinents. Pour influencer directement le succès de votre stratégie de marchandisage :
   - Configurez les attributs corrects comme pouvant faire l’objet d’une recherche avec leur poids correspondant.
   - Assurez-vous que les données contenues dans ces attributs sont pertinentes.
- Une expérience de recherche bien conçue renforce la confiance des clients et les incite à croire qu’ils trouveront ce dont ils ont besoin.
- Les règles de recherche sont essentielles, car elles peuvent améliorer la visibilité de certains produits en fonction de leur popularité, des nouveaux arrivants, des critères promotionnels ou de toute autre stratégie de marchandisage pour répondre aux besoins de votre entreprise.
- La navigation à facettes permet aux acheteurs d’affiner leur recherche et d’obtenir rapidement des résultats pertinents.

Pour gérer les [!DNL Live Search], accédez à **Marketing** > *SEO et recherche* > **[!DNL Live Search]** dans Adobe [!DNL Commerce] Admin. 

## Optimisation de votre fonctionnalité de recherche

Dans cette section, vous apprendrez à optimiser votre fonctionnalité de recherche en utilisant des fonctionnalités telles que la saisie semi-automatique pour fournir des suggestions en temps réel au fur et à mesure que les acheteurs saisissent des caractères, des synonymes et des orthographes afin de vous assurer que les acheteurs trouvent des produits même s’ils utilisent des mots différents, ainsi que des facettes pour permettre aux acheteurs de réduire les résultats de recherche.

### Saisie automatique

La saisie semi-automatique, également appelée saisie semi-automatique ou suggestion automatique, est une fonctionnalité de recherche interactive qui affiche de manière dynamique des suggestions aux acheteurs lorsqu’ils saisissent leurs termes de recherche. Cela permet aux acheteurs de trouver rapidement et facilement des produits en leur offrant des suggestions en temps réel basées sur leurs entrées.

Le widget [!DNL Live Search] [[!DNL popover]](storefront-popover.md) permet de saisir automatiquement des options de recherche pour suggérer des produits populaires. Avec chaque caractère saisi par l’acheteur, la fenêtre contextuelle se met à jour avec les produits suggérés et les images miniatures des principaux résultats de recherche.

[!DNL Live Search] commence à renvoyer des résultats lorsque l’utilisateur a saisi deux caractères. Pour une correspondance partielle, le nombre maximal de caractères par mot est de 20. Le nombre de caractères dans une requête « recherche en cours de frappe » n’est pas configurable.

En savoir plus sur le widget [popover](storefront-popover.md).

### Synonymes et fautes d&#39;orthographe

Live Search gère les fautes d’orthographe par défaut. Vous pouvez configurer des synonymes afin d’inclure des mots que les acheteurs peuvent utiliser et qui diffèrent des mots spécifiés dans votre catalogue. Vous ne voulez pas perdre une vente parce que quelqu&#39;un cherche un « canapé », alors que votre produit est listé comme un « canapé ». Vous pouvez saisir un large éventail de termes de recherche en saisissant tous les mots que les clients peuvent utiliser pour trouver vos produits. Vous pouvez [définir des synonymes dans un sens ou deux](synonyms-add.md#step-2-define-the-synonym-by-type) pour améliorer les résultats.

#### Conseils pour optimiser les synonymes

- Mappez les noms de marque et les abréviations à leurs noms complets, par exemple « HP » vers « Hewlett-Packard » et les surnoms de produit courants, par exemple « iPhone » vers « Apple iPhone ».
- Ajoutez du jargon et des termes spécifiques au secteur que les acheteurs peuvent utiliser de manière interchangeable, par exemple « baskets » et « chaussures de course ».
- Mettez régulièrement à jour la liste de synonymes en fonction des nouvelles tendances de recherche, des ajouts de produits et du comportement de l’acheteur.
- Testez l’efficacité des mappages de synonymes en analysant les résultats de recherche et les commentaires des acheteurs. Affinez les mappages pour améliorer la précision et la pertinence.

En savoir plus sur les synonymes :

- [Types de synonymes](synonyms-type.md)
- [Créer des synonymes](synonyms-add.md)
- [Gestion des synonymes](synonyms-manage.md)
- [Prise en charge linguistique](settings.md#language)

### Facettes

La fonctionnalité de filtre et de facette est un composant essentiel de votre site [!DNL Commerce], conçu pour améliorer l’expérience de l’acheteur en permettant à celui-ci de réduire les résultats de recherche et de trouver des produits plus efficacement. Cette fonctionnalité permet aux acheteurs de trier de vastes catalogues d’articles en appliquant des critères spécifiques, ce qui rend le processus d’achat plus rapide, plus facile et plus satisfaisant. En implémentant des filtres et des facettes efficaces et conviviaux pour les acheteurs, vous pouvez aider les clients à trouver rapidement et efficacement ce dont ils ont besoin, ce qui améliore la satisfaction et les taux de conversion.

Pour configurer un attribut de produit en tant que facette, les [propriétés](facets-add.md#step-1-add-a-facet) suivantes doivent être définies :

- **[!UICONTROL Use in Search]** -  `Yes`
- **[!UICONTROL Use in Layered Navigation]** -  `Filterable (with results)`
- **[!UICONTROL Use in Search Results Layered Navigation]** -  `Yes`

#### Conseils pour optimiser les facettes

- Déterminez les attributs les plus pertinents et utiles de vos produits, tels que le titre, la catégorie, la marque, la gamme de prix, la couleur et la taille, puis définissez-les comme [&#x200B; facettes dynamiques &#x200B;](facets-type.md). 
- Définissez et triez des attributs de produit cohérents dans l’ensemble de votre catalogue et hautement pertinents pour vos produits afin d’améliorer la pertinence et les fonctionnalités de filtrage de vos acheteurs.
- Assurez-vous que les libellés des facettes sont faciles à comprendre et nommés de manière cohérente sur l’ensemble du site. Par exemple, utilisez « Plage de prix » au lieu de « Coût ».
- Évitez d’accabler les acheteurs en limitant le nombre de facettes aux plus importantes. Un nombre trop élevé d’options peut entraîner une fatigue liée aux décisions. Par défaut, la [!DNL Live Search] est limitée à un maximum de 100 attributs configurés en tant que facettes et 30 intervalles renvoyés dans chaque facette. En savoir plus sur les [limites des facettes](boundaries-limits.md#facets). 
- Autoriser les acheteurs à sélectionner plusieurs critères de filtre simultanément pour affiner les résultats. Par exemple, laisser les acheteurs sélectionner les couleurs « Rouge » et « Bleu ».
- Affichez le nombre de produits disponibles à côté de chaque facette pour donner aux acheteurs une idée des résultats de recherche auxquels ils peuvent s’attendre.
- Implémentez des sections de facettes réductibles pour que l’interface reste propre et gérable, en particulier sur les appareils mobiles.
- Permet aux utilisateurs de réinitialiser facilement les facettes individuelles ou tous les filtres sélectionnés pour lancer une nouvelle recherche.

En savoir plus sur les facettes :

- [Types de facettes](facets-type.md)
- [Ajout de facettes](facets-add.md)
- [Gestion des facettes](facets-manage.md) (modification, épinglage d’une facette, suppression, publication)
- [Facettage des prix](settings.md#price-faceting)

## Améliorer la pertinence des résultats de recherche

Cette section explique comment améliorer la pertinence des résultats de recherche en implémentant des règles de recherche efficaces et en utilisant les métadonnées du produit pour garantir que les attributs précis et détaillés sont consultables.

### Images

Assurez-vous que les produits enfants des produits configurables possèdent des images avec les rôles appropriés. Si vous disposez de produits parents ou enfants, les résultats de la recherche peuvent ne pas contenir d’images.

>[!NOTE]
>
>Les images des résultats de recherche peuvent être différentes en fonction du terme recherché. Si le terme de recherche détermine qu’un produit enfant est plus pertinent, les images du produit enfant seront utilisées au lieu des images du produit parent.

### Règles de recherche

Pour optimiser votre taux de conversion et votre chiffre d’affaires, vous devez mettre en œuvre des règles de recherche efficaces. Ajustez les classements de produits en fonction des données de vente, des niveaux de stock et des promotions avec [Search Merchandising](rules.md).

Il est essentiel d’établir une règle de recherche par défaut bien pensée. Votre [règle par défaut](rules.md#default-rule) détermine la manière dont les résultats de recherche sont initialement triés et affichés pour les acheteurs, ce qui améliore leur expérience globale et augmente la probabilité d’achat. Une surveillance et un ajustement réguliers de cette règle garantissent qu’elle continue à répondre efficacement aux besoins des acheteurs et aux objectifs commerciaux.

#### Conseils pour optimiser les règles de recherche

- Épingler ou stimuler les produits ayant des volumes de vente élevés ou une activité de vente récente.
- Privilégiez les produits ayant des notes élevées et des évaluations positives.
- Assurez-vous que les articles en stock ont un rang supérieur.
- Hiérarchisez légèrement les produits avec des marges bénéficiaires plus élevées sans compromettre la pertinence.
- Mettez en avant les produits en vente ou faisant partie de promotions spéciales.
- Définissez automatiquement des règles de recherche pendant les périodes de promotion ou de vente en utilisant la période pendant votre période de promotion.
- Adaptez les résultats de la recherche en fonction du comportement de chaque acheteur à l’aide du [classement intelligent](rules-add.md#intelligent-ranking) tel que « recommandé pour vous », « le plus consulté », etc. Pour personnaliser le comportement de l’acheteur, vous devez vous assurer que l’événement est correctement implémenté. Pour les commerçants Luma, les événements sont disponibles clé en main. Pour les implémentations découplées ou personnalisées, vous devez [implémenter les événements](https://developer.adobe.com/commerce/services/shared-services/storefront-events/) en fonction de vos besoins spécifiques.

En savoir plus sur les règles de recherche :

- [Espace de travail de marchandisage](rules-workspace.md#set-the-scope)
- [Conditions requises](rules.md#requirements)
- [Règle de recherche par défaut](rules.md#default-rule)
- Gestion des règles de recherche
   - [Créer](rules-add.md)
   - [Modifier, afficher, supprimer](rules-manage.md)
- Collecte de données
   - [[!DNL Live Search] événements](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search)
   - [Collecteur D’Événements Adobe Commerce](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/)
   - [Événements Commerce GitHub](https://github.com/adobe/commerce-events/tree/main/examples) 

### Utilisation des métadonnées de produit

Assurez-vous que des attributs de produit précis et détaillés sont [configurés comme pouvant faire l’objet de recherches](workspace.md#set-attributes-as-searchable). Notez que les attributs SKU, nom et catégorie peuvent être recherchés par défaut et ne peuvent pas être exclus de la recherche. Pour de meilleurs résultats, n’utilisez pas d’espaces dans vos SKU.

Pour accroître la pertinence de la recherche, attribuez un poids à chaque attribut consultable. Les attributs ayant un poids plus élevé doivent apparaître plus haut dans les résultats de la recherche. Le tri par pertinence est affecté par plusieurs critères, tels que le poids de la recherche. Cela signifie que parfois les attributs ayant un poids de recherche inférieur peuvent toujours avoir plus de pertinence que les attributs ayant un poids de recherche supérieur. D’autres critères peuvent inclure le nombre de correspondances dans un attribut donné, la position du terme de recherche trouvé et la structure textuelle globale avant et après un terme de recherche.

Assurez-vous que chaque produit possède du contenu pertinent dans chaque attribut consultable. Il n’est pas recommandé de définir un attribut comme pouvant faire l’objet d’une recherche s’il contient de grandes quantités de contenu, car cela peut réduire la pertinence des résultats de recherche.

En savoir plus sur les attributs de produit pour la recherche :

- [Définir les attributs comme pouvant faire l’objet d’une recherche](workspace.md#set-attributes-as-searchable)
- [Attribuer un poids aux attributs](https://experienceleague.adobe.com/fr/docs/commerce-admin/catalog/catalog/search/search-results#weighted-search)

## Surveillance des résultats de recherche

Pour optimiser les résultats de recherche avec [!DNL Live Search], surveillez les indicateurs clés de performance (KPI) pertinents, tels que les requêtes uniques, la position moyenne des clics, les taux de clics publicitaires, le taux de conversion et le taux de résultats nul pour comprendre comment les acheteurs interagissent avec vos fonctionnalités de recherche. Ces données vous aident à mettre à jour et à affiner régulièrement vos règles de recherche.

Vous pouvez surveiller ces KPI dans l’espace de travail [!DNL Live Search] [Performances](performance.md) où vous trouverez les mesures suivantes : 

- **Recherches uniques** - Nombre de requêtes de recherche distinctes effectuées sur votre site [!DNL Commerce]. Chaque recherche unique n’est comptabilisée qu’une seule fois, même si elle est répétée plusieurs fois par le même acheteur ou par différents acheteurs. Cette mesure vous aide à comprendre la diversité des termes de recherche utilisés par les clients et fournit des informations sur les produits ou les informations recherchés par les acheteurs. Le suivi des recherches uniques vous permet :

   - Identifiez les tendances de recherche populaires et les éléments fréquemment recherchés.
   - Détection des lacunes potentielles dans votre catalogue de produits ou votre contenu
   - Optimisez vos fonctionnalités de recherche en ajoutant des [synonymes](synonyms.md), en créant ou en mettant à jour des règles de recherche.

- **Position moyenne des clics** - Indique que la position moyenne des résultats de recherche sur lesquels les acheteurs ont cliqué après avoir effectué une requête sur votre site. Cette mesure fournit des informations sur la pertinence et l’efficacité de vos résultats de recherche.

  Une position de clic moyenne inférieure (plus proche de 1) suggère que les acheteurs trouvent rapidement des résultats pertinents, ce qui indique que votre stratégie de recherche est efficace. Cela vous aide à comprendre le comportement des acheteurs et jusqu’où ils sont prêts à faire défiler l’écran pour trouver le produit souhaité. Si la position moyenne des clics est élevée, cela peut indiquer que les résultats les plus pertinents n’apparaissent pas en haut de l’écran, ce qui nécessite une révision et une optimisation de votre stratégie de recherche.

- **Taux de clic publicitaire (CTR)** - Mesure le pourcentage d’acheteurs qui cliquent sur un résultat de recherche après avoir exécuté une requête. Un CTR élevé indique que les résultats de la recherche sont pertinents et attrayants pour les acheteurs, car ils cliquent sur les résultats qu’ils trouvent. La surveillance de la RCT peut aider à identifier les domaines à améliorer. Un CTR faible peut suggérer que les résultats de recherche ne correspondent pas à l’intention de l’acheteur, ce qui entraîne un besoin d’affiner les règles de recherche, d’améliorer les données de produit ou la présentation des résultats.

- **Taux de conversion** - Indique l’efficacité de votre fonctionnalité de recherche pour stimuler les ventes et atteindre les objectifs commerciaux. Il reflète l’efficacité globale de votre fonctionnalité de recherche pour répondre aux besoins des acheteurs et faciliter une expérience d’achat fluide. Un taux de conversion élevé indique que vos résultats de recherche sont très pertinents et convaincants, ce qui pousse les acheteurs à effectuer des achats. Si le taux de conversion est faible, il peut suggérer des problèmes de pertinence de la recherche, de disponibilité du produit ou du parcours global d’acheteurs, de la recherche à l’achat.

- **Zéro résultat** - Mesure le pourcentage de requêtes de recherche sur votre site [!DNL Commerce] qui ne renvoient aucun résultat. Cette mesure est essentielle pour comprendre la fréquence à laquelle les recherches d’acheteurs échouent et peut fournir des informations sur les lacunes potentielles de votre catalogue de produits ou de la configuration de la recherche. Un taux de résultats nul élevé peut frustrer les acheteurs, ce qui entraîne une mauvaise expérience d’achat et une perte potentielle de clients. Il peut indiquer les produits ou catégories manquants dans votre catalogue que les acheteurs recherchent, guidant les décisions d’inventaire et d’inscription des produits.

  Pour réduire le taux de résultats nul, vous pouvez :

   - Proposez des termes de recherche alternatifs ou apparentés, tels que des [synonymes](synonyms.md) si aucune correspondance exacte n’est trouvée.
   - Passez régulièrement en revue les requêtes sans résultat pour identifier les modèles et apporter les ajustements nécessaires à votre catalogue de produits et à vos paramètres de recherche.

- **Résultats populaires** - Peut améliorer considérablement vos résultats de recherche en les alignant avec les préférences et les comportements des acheteurs.

Vous pouvez utiliser ces données de mesure pour optimiser votre fonctionnalité de recherche des manières suivantes :

- Implémentez des règles pour classer automatiquement les produits populaires dans les résultats de recherche. Les produits fréquemment cliqués ou achetés peuvent être prioritaires pour apparaître en haut. Conservez manuellement les listes de produits populaires pour des requêtes de recherche spécifiques et assurez-vous que ces éléments sont affichés de manière bien visible.
- Mettez en avant les produits qui sont actuellement en tendance ou qui ont connu récemment un pic de popularité. Cela peut être particulièrement efficace lors d’événements saisonniers, de vacances ou de périodes promotionnelles. Pour ce faire, utilisez le classement intelligent qui convient le mieux à votre cas d’utilisation et à vos besoins professionnels lors de la configuration d’une règle de recherche.
- Mettez en surbrillance les filtres ou facettes populaires, si les acheteurs filtrent fréquemment par certaines marques ou plages de prix, donnez plus d’importance à ces options en épinglant ces facettes et en les triant en conséquence.
- Lorsqu’une recherche ne produit aucun résultat, utilisez les données de résultats populaires pour suggérer d’autres produits ou catégories associées qui ont un fort engagement des acheteurs.
- Analysez les termes de recherche populaires et les données de produit pour identifier les mots-clés importants. Optimisez les attributs pouvant faire l’objet de recherches dans votre produit avec ces mots-clés pour améliorer la pertinence de la recherche.
- Analysez régulièrement vos données de résultats pour comprendre les tendances changeantes, les préférences et le comportement des acheteurs, identifier les principaux termes de recherche et détecter les problèmes. Utilisez cette boucle de commentaires pour affiner et améliorer en permanence vos règles de recherche et vos offres de produits

Pour obtenir des données correctes dans votre rapport [!DNL Live Search], vous devez vous assurer que les événements sont correctement implémentés. Pour les commerçants Luma, les événements sont disponibles clé en main. Pour les implémentations découplées ou personnalisées, vous devez [implémenter les événements](https://developer.adobe.com/commerce/services/shared-services/storefront-events/) en fonction de vos besoins spécifiques.
