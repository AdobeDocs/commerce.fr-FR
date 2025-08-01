---
title: Performances de recherche
description: La page Performances de la recherche fournit insight dans les termes de recherche utilisés par les acheteurs.
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: 75b43c6f-d876-4379-ad70-5c2a2f29a5ac
source-git-commit: b8b7af1119163589b7d83654b13edae656fea339
workflow-type: tm+mt
source-wordcount: '1737'
ht-degree: 0%

---

# Performances de recherche

La page *Performances de recherche* fournit insight dans les termes de recherche utilisés par les acheteurs. Ces informations peuvent être utilisées pour identifier les tendances, augmenter les clics publicitaires et améliorer le taux de conversion. La page Performances de la recherche fournit un instantané des mesures de recherche pour une période spécifique et inclut les rapports suivants :

- Recherches uniques
- Position moyenne des clics
- Taux de clic publicitaire
- Taux de conversion
- Taux de résultats nuls

![Performances de recherche](../assets/search-performance.png){zoomable="yes"}

>[!IMPORTANT]
>
>Si vous ne voyez aucune mesure de performances de recherche, assurez-vous que les données d’événement de recherche sont [collectées](../setup/events/overview.md).

## Choisissez la vue **Catalogue**

Sélectionnez la [vue du catalogue](../setup/catalog-view.md) pour afficher des résultats de performances de recherche spécifiques.

![Vue Catalogue](../assets/catalog-view.png)

## Affichage d’un rapport

Cliquez sur le calendrier et effectuez l’une des opérations suivantes :

- Pour spécifier une seule date, double-cliquez sur la date dans le calendrier.
- Pour spécifier une plage de dates, cliquez sur la première et la dernière date du calendrier.

>[!NOTE]
>
>La plage de dates ne peut pas dépasser un an.

Cliquez sur **[!UICONTROL Export to CSV]** pour générer un fichier CSV des performances de votre recherche.

## Amélioration des performances de recherche

La section suivante fournit des stratégies que vous pouvez utiliser pour améliorer les fonctionnalités de recherche de votre site, afin d’offrir une expérience client fluide et efficace qui optimise les taux de conversion.

Plusieurs facteurs clés déterminent la pertinence et l’efficacité des résultats de recherche :

- Des données de produit bien structurées garantissent que les algorithmes de recherche peuvent efficacement faire correspondre les produits aux requêtes. Des données de produit de faible qualité entraînent des résultats de recherche moins pertinents. Pour influencer directement le succès de votre stratégie de marchandisage :
   - Paramétrez les [attributs corrects comme pouvant faire l’objet d’une recherche](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata) avec leur poids correspondant.
   - Assurez-vous que les données contenues dans ces attributs sont pertinentes.
- Une expérience de recherche bien conçue renforce la confiance des clients et les incite à croire qu’ils trouveront ce dont ils ont besoin.
- Les règles de recherche sont essentielles, car elles peuvent améliorer la visibilité de certains produits en fonction de leur popularité, des nouveaux arrivants, des critères promotionnels ou de toute autre stratégie de marchandisage pour répondre aux besoins de votre entreprise.
- La navigation à facettes permet aux acheteurs d’affiner leur recherche et d’obtenir rapidement des résultats pertinents.

### Surveillance des résultats de recherche

Pour optimiser les résultats de recherche avec [!DNL Adobe Commerce Optimizer], surveillez les indicateurs clés de performance (KPI) pertinents, tels que les requêtes uniques, la position moyenne des clics, les taux de clics publicitaires, le taux de conversion et le taux de résultats nul pour comprendre comment les acheteurs interagissent avec vos fonctionnalités de recherche. Ces données vous aident à mettre à jour et à affiner régulièrement vos règles de recherche.

- **Recherches uniques** - Nombre de requêtes de recherche distinctes effectuées sur votre site [!DNL Adobe Commerce Optimizer]. Chaque recherche unique n’est comptabilisée qu’une seule fois, même si elle est répétée plusieurs fois par le même acheteur ou par différents acheteurs. Cette mesure vous aide à comprendre la diversité des termes de recherche utilisés par les clients et fournit des informations sur les produits ou les informations recherchés par les acheteurs. Le suivi des recherches uniques vous permet :

   - Identifiez les tendances de recherche populaires et les éléments fréquemment recherchés.
   - Détection des lacunes potentielles dans votre catalogue de produits ou votre contenu
   - Optimisez vos fonctionnalités de recherche en ajoutant [synonymes](../merchandising/synonyms/overview.md), en créant ou en mettant à jour des [règles de recherche](../merchandising/rules/overview.md).

- **Position moyenne des clics** - Indique que la position moyenne des résultats de recherche sur lesquels les acheteurs ont cliqué après avoir effectué une requête sur votre site. Cette mesure fournit des informations sur la pertinence et l’efficacité de vos résultats de recherche.

  Une position de clic moyenne inférieure (plus proche de 1) suggère que les acheteurs trouvent rapidement des résultats pertinents, ce qui indique que votre stratégie de recherche est efficace. Cela vous aide à comprendre le comportement des acheteurs et jusqu’où ils sont prêts à faire défiler l’écran pour trouver le produit souhaité. Si la position moyenne des clics est élevée, cela peut indiquer que les résultats les plus pertinents n’apparaissent pas en haut de l’écran, ce qui nécessite une révision et une optimisation de votre stratégie de recherche.

- **Taux de clic publicitaire (CTR)** - Mesure le pourcentage d’acheteurs qui cliquent sur un résultat de recherche après avoir exécuté une requête. Un CTR élevé indique que les résultats de la recherche sont pertinents et attrayants pour les acheteurs, car ils cliquent sur les résultats qu’ils trouvent. La surveillance de la RCT peut aider à identifier les domaines à améliorer. Un CTR faible peut suggérer que les résultats de recherche ne correspondent pas à l’intention de l’acheteur, ce qui entraîne un besoin d’affiner les règles de recherche, d’améliorer les données de produit ou la présentation des résultats.

- **Taux de conversion** - Indique l’efficacité de votre fonctionnalité de recherche pour stimuler les ventes et atteindre les objectifs commerciaux. Il reflète l’efficacité globale de votre fonctionnalité de recherche pour répondre aux besoins des acheteurs et faciliter une expérience d’achat fluide. Un taux de conversion élevé indique que vos résultats de recherche sont très pertinents et convaincants, ce qui pousse les acheteurs à effectuer des achats. Si le taux de conversion est faible, il peut suggérer des problèmes de pertinence de la recherche, de disponibilité du produit ou du parcours global d’acheteurs, de la recherche à l’achat.

- **Taux de résultats nuls** - Mesure le pourcentage de requêtes de recherche sur votre site [!DNL Adobe Commerce Optimizer] qui ne renvoient aucun résultat. Cette mesure est essentielle pour comprendre la fréquence à laquelle les recherches d’acheteurs échouent et peut fournir des informations sur les lacunes potentielles de votre catalogue de produits ou de la configuration de la recherche. Un taux de résultats nul élevé peut frustrer les acheteurs, ce qui entraîne une mauvaise expérience d’achat et une perte potentielle de clients. Il peut indiquer les produits ou catégories manquants dans votre catalogue que les acheteurs recherchent, guidant les décisions d’inventaire et d’inscription des produits.

  Pour réduire le taux de résultats nul, vous pouvez :

   - Proposez des termes de recherche alternatifs ou apparentés, tels que des [synonymes](../merchandising/synonyms/overview.md) si aucune correspondance exacte n’est trouvée.
   - Passez régulièrement en revue les requêtes sans résultat pour identifier les modèles et apporter les ajustements nécessaires à votre catalogue de produits et à vos paramètres de recherche.

Vous pouvez utiliser ces données de mesure pour optimiser votre fonctionnalité de recherche des manières suivantes :

- Implémentez des règles pour classer automatiquement les produits populaires dans les résultats de recherche. Les produits fréquemment cliqués ou achetés peuvent être prioritaires pour apparaître en haut. Conservez manuellement les listes de produits populaires pour des requêtes de recherche spécifiques et assurez-vous que ces éléments sont affichés de manière bien visible.
- Mettez en avant les produits qui sont actuellement en tendance ou qui ont connu récemment un pic de popularité. Cela peut être particulièrement efficace lors d’événements saisonniers, de vacances ou de périodes promotionnelles. Pour ce faire, utilisez le classement intelligent qui convient le mieux à votre cas d’utilisation et à vos besoins professionnels lors de la configuration d’une règle de recherche.
- Mettez en surbrillance les filtres ou facettes populaires, si les acheteurs filtrent fréquemment par certaines marques ou plages de prix, donnez plus d’importance à ces options en épinglant ces facettes et en les triant en conséquence.
- Lorsqu’une recherche ne produit aucun résultat, utilisez les données de résultats populaires pour suggérer d’autres produits ou catégories associées qui ont un fort engagement des acheteurs.
- Analysez les termes de recherche populaires et les données de produit pour identifier les mots-clés importants. Optimisez les attributs pouvant faire l’objet de recherches dans votre produit avec ces mots-clés pour améliorer la pertinence de la recherche.
- Analysez régulièrement vos données de résultats pour comprendre les tendances changeantes, les préférences et le comportement des acheteurs, identifier les principaux termes de recherche et détecter les problèmes. Utilisez cette boucle de commentaires pour affiner et améliorer en permanence vos règles de recherche et vos offres de produits

## Optimisation de votre fonctionnalité de recherche

Pour optimiser votre fonctionnalité de recherche, utilisez [synonymes et orthographes](../merchandising/synonyms/overview.md) pour vous assurer que les acheteurs trouvent des produits même s’ils utilisent des mots et des [facettes](../merchandising/facets/overview.md) différents, afin de permettre aux acheteurs de réduire les résultats de recherche.

## Améliorer la pertinence des résultats de recherche

Pour améliorer la pertinence des résultats de recherche, implémentez des [règles de recherche](../merchandising/rules/overview.md) efficaces et utilisez les métadonnées du produit afin de garantir que les attributs [ précis et détaillés sont consultables](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata).

### Images

Assurez-vous que les produits enfants des produits configurables possèdent des images avec les rôles appropriés. Si vous disposez de produits parents ou enfants, les résultats de la recherche peuvent ne pas contenir d’images.

>[!NOTE]
>
>Les images des résultats de recherche peuvent être différentes en fonction du terme recherché. Si le terme de recherche détermine qu’un produit enfant est plus pertinent, les images du produit enfant seront utilisées au lieu des images du produit parent.

### Utilisation des métadonnées de produit

Assurez-vous que les attributs de produit [attributs) précis et détaillés sont configurés comme pouvant faire l’objet de recherches](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata). Notez que les attributs SKU, nom et catégorie peuvent être recherchés par défaut et ne peuvent pas être exclus de la recherche. Pour de meilleurs résultats, n’utilisez pas d’espaces dans vos SKU.

Pour accroître la pertinence de la recherche, attribuez un poids à chaque attribut consultable. Les attributs ayant un poids plus élevé doivent apparaître plus haut dans les résultats de la recherche. Le tri par pertinence est affecté par plusieurs critères, tels que le poids de la recherche. Cela signifie que parfois les attributs ayant un poids de recherche inférieur peuvent toujours avoir plus de pertinence que les attributs ayant un poids de recherche supérieur. D’autres critères peuvent inclure le nombre de correspondances dans un attribut donné, la position du terme de recherche trouvé et la structure textuelle globale avant et après un terme de recherche.

Assurez-vous que chaque produit possède du contenu pertinent dans chaque attribut consultable. Il n’est pas recommandé de définir un attribut comme pouvant faire l’objet d’une recherche s’il contient de grandes quantités de contenu, car cela peut réduire la pertinence des résultats de recherche.

En savoir plus sur les attributs de produit pour la recherche :

- [Définir les attributs comme pouvant faire l’objet d’une recherche](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)
- [Attribuer un poids aux attributs](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata)

## Descriptions des champs

| Données de capture instantanée | Description |
|--- |--- |
| Recherches uniques | Nombre total de recherches uniques pour la période spécifiée. Les recherches multiples effectuées par le même acheteur, même si pour la même requête, sont considérées comme uniques si elles sont envoyées à plus d’une heure d’intervalle. |
| Taux de clic publicitaire | Pourcentage de recherches qui se terminent par un clic de l’acheteur sur un produit. Par exemple, le taux de clic publicitaire est de 50 % si l’acheteur recherche « pantalon » et « chemise », puis clique sur un résultat de la recherche « chemise ». |
| Taux de conversion | Pourcentage de produits achetés par l’acheteur par rapport au nombre de produits sur lesquels l’acheteur clique pendant la période spécifiée. Par exemple, le taux de conversion de l’interaction est de 100 % si l’acheteur consulte six produits dans la fenêtre contextuelle, clique sur un produit et effectue un achat. <br /><br />Le taux de conversion n’est pas affecté par le nombre de consultations d’un produit donné. Par exemple, le taux de conversion reste le même si l’acheteur utilise la recherche, mais ne clique sur aucun produit. |
| Taux de résultats nuls | Pourcentage de recherches uniques qui ne renvoie aucun résultat pour la période spécifiée. Par exemple, le taux de zéro des résultats est de 66,67 % si l&#39;acheteur recherche « fjjajfjf » deux fois (sans résultats) et « pants » une fois (avec résultats). |
| Moy. position de clic | Position relative du taux de clics publicitaires moyen en fonction des recherches uniques pour la période spécifiée. |

| Rapports | Description |
|--- |--- |
| Zéro résultat | Répertorie les requêtes de recherche qui ne renvoient aucun résultat et le nombre de fois où elles ont été utilisées au cours de la période spécifiée. Limite de rapport : 500 premiers termes |
| Résultats populaires | Répertorie les noms des produits qui ont reçu le plus de vues au cours de la période spécifiée. Les résultats populaires sont calculés en fonction des impressions uniquement et ne sont pas affectés par le nombre de clics ou le chiffre d’affaires généré. Limite de rapport : 500 premiers termes |
| Recherches uniques | Répertorie les requêtes de recherche uniques utilisées au cours de la période spécifiée. Les données du rapport sont calculées de la même manière que les données d’instantané de recherche unique. Si un acheteur saisit deux fois la même requête de recherche, mais à plus d’une heure d’intervalle, la recherche est considérée comme deux recherches uniques. Limite de rapport : 500 premiers termes |
