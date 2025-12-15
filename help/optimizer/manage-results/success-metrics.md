---
title: Mesures de succès
description: Les mesures de succès fournissent insight dans les mesures de performances clés de votre  [!DNL Adobe Commerce Optimizer] .
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: 7202a531-fec3-4698-89b9-6bdbcc37015e
source-git-commit: 4e85d70dc1b099a5b40a807a76ca589aa9a28f07
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# Mesures de succès

Cette page présente un aperçu des mesures de performances clés de votre boutique [!DNL Adobe Commerce Optimizer]. L’objectif est que vous compreniez rapidement les résultats de l’implémentation de [!DNL Adobe Commerce Optimizer], puis que vous et votre équipe identifiiez les opportunités de croissance et mettiez en évidence les domaines à optimiser.

![Rapport des mesures de succès](../assets/success-metrics.png)

Les mesures du rapport sont extraites des données d’événement du storefront. [En savoir plus](../setup/events/overview.md) sur les données d’événement collectées.

## Compréhension de vos mesures

Le rapport des mesures de succès fournit des informations exploitables sur cinq domaines de performances clés qui ont un impact direct sur les résultats de votre entreprise. Chaque mesure révèle des modèles de comportement des clients et des clientes, ainsi que des performances de magasin qui vous aident à découvrir des opportunités et à relever des défis. Tirez parti de ces informations pour prendre des décisions plus intelligentes et optimiser votre expérience commerciale.

**Principales caractéristiques** résume les mesures clés de chaque domaine de performance. Utilisez cette section pour identifier rapidement les principales opportunités d’amélioration.

Les principaux indicateurs de performance sont les suivants :

- **Chiffre d’affaires** : votre principale mesure financière indiquant le chiffre d’affaires total.
- **Conversion** : pourcentage de visiteurs et visiteuses qui effectuent des achats.
- **Engagement** : comment les utilisateurs interagissent activement avec votre site.
- **Acquisition** : efficacité de vos efforts d’acquisition de clients.
- **Taux de rebond** : pourcentage de visiteurs et visiteuses qui quittent après avoir consulté une seule page.

### Actualisation et précision des données

**Fréquence de mise à jour** les données des mesures de succès sont traitées et mises à jour régulièrement lorsque des événements de storefront sont collectés et traités.

**Quand vérifier les mesures :** pour une analyse des tendances la plus précise, passez en revue les mesures après un délai suffisant pour collecter des données significatives. Les fluctuations quotidiennes sont normales ; concentrez-vous sur les tendances hebdomadaires ou mensuelles pour prendre des décisions stratégiques.

**Précision des données :** les mesures sont calculées à partir des interactions client réelles capturées par le biais d’événements de storefront. Assurez-vous que votre boutique dispose du [suivi des événements configuré](../setup/events/overview.md) approprié pour des rapports précis.

## Générer un rapport

1. Dans le rail de gauche, sélectionnez **Mesures de succès**.
1. Sous **Configuration du rapport** spécifiez la **Période**, **Source du catalogue**, en fonction de vos paramètres régionaux, et **Devise**.
1. Cliquez sur **[!UICONTROL Apply]**.

   Les **Principales caractéristiques**, **Chiffre d’affaires**, **Conversion**, **Engagement**, **Acquisition** et **Taux de rebond** sont toutes mises à jour en fonction de la configuration de votre rapport.

1. Cliquez sur **[!UICONTROL Export]** pour enregistrer le rapport en tant que PDF.

## Utilisation conjointe des mesures de succès et de Sites Optimizer

Les mesures de succès et Sites Optimizer ([Opportunités](opportunities.md)) sont des outils complémentaires conçus pour fonctionner ensemble et vous aider à améliorer les performances de votre site de commerce. Comprendre la différence entre ces fonctionnalités vous aide à prendre de meilleures décisions et à obtenir des résultats mesurables.

### Principales différences

| Aspect | Mesures de succès | Sites Optimizer (opportunités) |
|---|---|---|
| **Objectif** | Mesure les performances et les résultats | identifie les problèmes et fournit des recommandations ; |
| **Type** | Tableau de bord analytique | Détection proactive des problèmes |
| **Ce qu’il montre** | Indicateurs clés de performance (chiffre d’affaires, conversion, engagement, acquisition, taux de rebond) | Recommandations optimisées par l’IA pour les problèmes affectant les performances du site |
| **Source de données** | Données d’événement de storefront | Catalogues de produits, journaux de recherche, données de recommandation |
| **Utiliser quand** | Vous souhaitez suivre les résultats au fil du temps. | Vous souhaitez identifier et résoudre des problèmes spécifiques |

### Utilisation conjointe de ces fonctionnalités

L’approche la plus efficace consiste à combiner les deux outils dans un cycle d’amélioration continue :

1. **Mesurer avec des mesures de succès** : commencez par consulter votre tableau de bord de mesures de succès pour comprendre vos performances actuelles. Identifiez les KPI à améliorer (par exemple, un taux de conversion faible ou un taux de rebond élevé).

1. **Diagnostiquer avec les opportunités** : accédez à la page Opportunités pour découvrir des problèmes spécifiques qui peuvent entraîner une baisse des performances. Sites Optimizer analyse votre catalogue de produits, vos journaux de recherche et vos données de recommandation afin d’identifier des problèmes tels que des données de produit manquantes, une faible pertinence de la recherche ou des problèmes de navigation.

1. **Implémenter les recommandations** : suivez les recommandations pilotées par l’IA fournies dans Opportunités pour résoudre les problèmes détectés. Il peut s’agir de résoudre les problèmes de qualité des données produit, d’améliorer le SEO ou d’optimiser la recherche et la découverte.

1. **Suivre les améliorations** : revenez aux Mesures de succès pour surveiller l’impact des modifications sur vos indicateurs de performance clés au fil du temps. Utilisez le sélecteur de période pour comparer les performances avant et après l’implémentation des recommandations.

1. **Itérer et optimiser** : poursuivez ce cycle en utilisant les Opportunités pour identifier les nouveaux problèmes et les mesures de succès afin de mesurer l’impact de vos optimisations.

### Exemple de workflow

Un commerçant remarque que son taux de conversion diminue dans les mesures de succès. Voici comment ils peuvent utiliser les deux fonctionnalités pour y remédier :

1. **Identifier le problème** : le tableau de bord des mesures de succès indique une baisse de 15 % du taux de conversion au cours du dernier mois.

1. **Trouver la cause** : la page Opportunités révèle plusieurs problèmes :
   - Plusieurs produits ne possèdent pas d’attributs clés affectant la pertinence de la recherche.
   - Requêtes de recherche populaires renvoyant de mauvais résultats.
   - Temps de chargement de page lent sur les pages de catégorie.

1. **Prendre des mesures** : le commerçant donne la priorité à la résolution des problèmes de qualité des données de produit, car Sites Optimizer les classe comme des opportunités à fort impact affectant la recherche et les recommandations.

1. **Mesurer les résultats** : après la mise à jour des attributs du produit et l’implémentation des modifications recommandées, le commerçant surveille les mesures de succès une fois par semaine. Au cours du mois suivant, le taux de conversion augmentera de 12 % et les mesures d’engagement dans la recherche s’amélioreront considérablement.

1. **Poursuivre l’optimisation** : grâce à l’amélioration du taux de conversion, le commerçant se concentre sur la priorité suivante affichée dans Opportunités, à savoir l’optimisation de la vitesse de chargement des pages pour réduire le taux de rebond.

### Quand utiliser chaque fonctionnalité

**Utiliser des mesures de succès pour effectuer les opérations suivantes :**

- Effectuez le suivi des performances globales de l’entreprise.
- Mesurez l’impact des modifications au fil du temps.
- Identifiez les domaines de votre entreprise qui nécessitent une attention particulière.
- Partagez les rapports de performance avec les parties prenantes.
- comprendre les tendances du comportement des clients ;

**Utilisez Sites Optimizer (Opportunités) lorsque vous souhaitez :**

- Identifiez les problèmes spécifiques affectant les performances.
- Obtenez des recommandations pratiques pour résoudre les problèmes.
- Comprendre pourquoi certaines mesures sont en baisse.
- Hiérarchisez les optimisations à traiter en premier.
- Utilisez l’IA pour identifier les problèmes que vous pouvez manquer manuellement.

Ensemble, ces fonctionnalités fournissent une solution complète : les mesures de succès vous indiquent *ce qui se passe*, tandis que Sites Optimizer vous indique *pourquoi* et *comment résoudre le problème*.

## Étapes suivantes et stratégies d’optimisation

Utilisez vos données de mesures de succès pour identifier les opportunités d’amélioration et mettre en œuvre des stratégies d’optimisation ciblées. Les sections suivantes fournissent des conseils spécifiques et exploitables pour chaque zone de mesure.

>[!BEGINTABS]

>[!TAB Optimisation des revenus]

Pour le chiffre d’affaires, votre objectif est d’augmenter les ventes totales et la valeur moyenne des commandes.

![Revenu des mesures de succès](../assets/revenue.png)

### Comprendre la mesure du chiffre d’affaires

**Ce qu’il mesure :** revenu total généré par votre boutique au cours de la période sélectionnée.

**Calcul du chiffre d&#39;affaires :** chiffre d&#39;affaires correspond à la somme de toutes les commandes terminées (prix de base × quantité) pour tous les produits vendus au cours de la période de déclaration. Le calcul utilise les données d’événements `place-order` capturés sur votre storefront.

>[!IMPORTANT]
>
>Les calculs du produit excluent les commandes annulées, les retours et les commandes pour lesquelles l&#39;événement `place-order` n&#39;a pas été capturé. Les événements peuvent être manquants en raison de paramètres de consentement, de problèmes de navigateur (bloqueurs de publicités, échecs de script) ou d’erreurs de traitement technique.

**Formule:**

```
Total Revenue = Sum of (Product Base Price × Quantity) for all completed orders
```

**Source de données :** événements Storefront (en particulier les événements `place-order`)

**Éléments inclus :**

- Toutes les commandes terminées pendant la période sélectionnée.
- Prix des produits de base multipliés par les quantités achetées.
- Chiffre d’affaires de tous les canaux de vente suivi par Commerce Optimizer.

**Remarques importantes :**

- Le chiffre d’affaires est calculé en fonction des prix de base capturés dans les événements de storefront.
- La période de création de rapports est déterminée par la période que vous sélectionnez dans la configuration du rapport.
- Les mesures de chiffre d’affaires sont mises à jour à mesure que de nouveaux événements de commande sont traités.

### Stratégies

- **Implémenter des recommandations optimisées par l’IA** : utilisez le moteur de recommandations de l’optimiseur pour faire apparaître les produits pertinents qui génèrent des taux de conversion plus élevés. Déployer *Les clients qui l’ont consulté ont également consulté* et *l’ont acheté* ont acheté ces types de recommandations afin d’augmenter les opportunités de vente croisée.

- **Créer des règles de marchandisage** : améliorez les produits à marge élevée dans les résultats de recherche à l’aide de [règles de marchandisage](../merchandising/rules/overview.md). Épinglez les articles les plus vendus en haut des résultats de recherche pour les requêtes à trafic élevé.

- **Optimiser la découverte de produits** : utilisez les [facettes intelligentes](../merchandising/facets/overview.md) pour aider les clients à trouver les produits plus efficacement, ce qui entraîne des taux de conversion plus élevés et une augmentation des recettes.

- **Tirer parti des opportunités saisonnières** : créez des règles de marchandisage temporelles pour promouvoir les articles saisonniers ou promotionnels pendant les périodes de pointe des achats.

>[!TAB Amélioration du taux de conversion ]

Pour améliorer votre taux de conversion, votre objectif est de convertir davantage de visiteurs en clients.

![&#x200B; Taux de conversion des mesures de succès &#x200B;](../assets/conversion-rate.png)

### Comprendre la mesure du taux de conversion

**Ce qu’il mesure :** pourcentage de visiteurs et visiteuses qui consultent des produits, puis effectuent un achat, indiquant à quel point votre boutique convertit efficacement les navigateurs en acheteurs.

**Méthode de calcul** taux de conversion compare le nombre de visiteurs uniques qui ont acheté des produits au nombre de visiteurs uniques qui ont consulté des produits.

**Formule:**

```
Conversion Rate = (Total Number of Orders ÷ Total Unique Visitors) × 100
```

**Source de données :** événements Storefront.

**Fonctionnement :**

- Les **consultations de produits** sont suivies lorsque les visiteurs consultent des pages de produits (à l’aide d’événements `product-view`).
- Les **achats** sont suivis une fois les commandes terminées (à l’aide d’événements `place-order`).
- Le calcul fait correspondre les utilisateurs et utilisatrices qui ont consulté des produits spécifiques avec ceux qui les ont achetés.

**Remarques importantes :**

- Un visiteur qui consulte plusieurs produits mais effectue un seul achat compte comme une seule conversion.
- La mesure effectue le suivi des visiteurs uniques à l’aide d’identifiants de navigateur.
- Les événements de consultation de produit incluent toujours un clic, de sorte que les vues représentent un intérêt réel de l’utilisateur.

### Stratégies

- **Optimiser la pertinence de la recherche** : implémentez des [synonymes](../merchandising/synonyms/overview.md) pour vous assurer que les clients trouvent ce qu’ils recherchent, même avec des termes de recherche différents. Utilisez la facettisation dynamique pour fournir des options de filtrage pertinentes.

- **Emplacement de recommandation stratégique** : déployez des unités de recommandation sur les pages à trafic élevé, telles que les pages de détails du produit et les pages de catégories. Utilisez les recommandations *Les plus consultés* et *Les plus achetés* pour créer de la confiance et de l’urgence.

- **Améliorer la visibilité des produits** : utilisez les règles de marchandisage pour vous assurer que les produits les plus vendus et à forte conversion apparaissent bien en vue dans les résultats de recherche.

- **Types de recommandations de test A/B** : testez différents types de recommandations et emplacements pour trouver celui qui convient le mieux à votre audience.

>[!TAB Amélioration de l’engagement]

Pour améliorer l’engagement, votre objectif est d’augmenter l’interaction client et le temps passé sur le site.

![Engagement des mesures de succès](../assets/engagement.png)

### Compréhension de la mesure d’engagement

**Ce qu’il mesure :** la façon dont les utilisateurs interagissent activement avec votre boutique, en suivant les actions significatives depuis la navigation initiale jusqu’au processus de passage en caisse.

**Calcul de l’engagement :** l’engagement effectue le suivi de toutes les interactions qui indiquent une participation active à votre boutique, y compris la navigation dans les produits, les activités liées au panier et les actions de passage en caisse.

**Source de données :** événements Storefront

**Ce qui compte comme engagement :**

L’engagement comprend les catégories d’événement et les actions suivantes :

- **Interactions de produits :** consultations de produits, clics de produits et comparaisons de produits.
- **Activités de panier :** ajout d’articles au panier, mise à jour des quantités, suppression d’articles.
- **Actions de passage en caisse :** Lancement du passage en caisse, finalisation des étapes de passage en caisse.
- **Navigation dans les catégories :** affichage des pages de catégorie, filtrage par facettes.
- **Activités de liste de souhaits :** Ajout à une liste de souhaits, affichage d’éléments de liste de souhaits.

**Détails de suivi des événements :**

Le système effectue le suivi de l’engagement lorsque les événements ont :

- Catégorie : `product`, `shopper`, `shopping-cart` ou `checkout`.
- Propriété : `Product`, `Checkout`, `Cart`, `Category` ou `Wishlist`.

**Remarques importantes :**

- Un engagement plus important est généralement corrélé à des taux de conversion plus élevés.
- Les mesures d’engagement permettent d’identifier les utilisateurs les plus actifs dans leur parcours.
- Utilisez les données d’engagement pour optimiser les pages à trafic élevé et améliorer l’expérience client.

### Stratégies

- **Diversifier les types de recommandations** : évitez d’afficher les mêmes recommandations à plusieurs reprises. Utilisez un mélange de *Recommandé pour vous*, *Tendance* et *Récemment consultés* pour garder le contenu à jour et attrayant.

- **Implémenter une recherche intelligente** : utilisez la facettisation dynamique et le reclassement des résultats pilotés par l’IA pour adapter les résultats de recherche en temps réel en fonction du comportement de l’acheteur.

- **Création d’expériences personnalisées** : déployez des unités « Recommandé pour vous » sur la page d’accueil et sur l’ensemble du parcours client pour fournir des suggestions de produits personnalisées.

- **Optimiser l’expérience de recherche** : utilisez des synonymes pour améliorer la pertinence de la recherche et vous assurer que les clients trouvent rapidement ce qu’ils recherchent.

>[!TAB  Croissance des acquisitions ]

Pour augmenter votre croissance, vous avez pour objectif d&#39;attirer davantage de nouveaux clients et d&#39;améliorer l&#39;efficacité de vos acquisitions.

![Acquisition des mesures de succès](../assets/acquisition.png)

### Comprendre la mesure d’acquisition

**Ce qu’il mesure :** le nombre de nouveaux visiteurs uniques qui se rendent dans votre magasin, ce qui vous aide à comprendre l’efficacité de vos efforts de marketing et d’acquisition de clients.

**Méthode de calcul :** l’acquisition comptabilise les visiteurs uniques en fonction des identifiants de navigateur attribués lors de leur première visite dans votre boutique.

**Source de données :** événements Storefront.

**Fonctionnement :**

- Le navigateur de chaque visiteur reçoit un identifiant unique (`domain_userid`) via un cookie propriétaire.
- Les nouveaux visiteurs sont identifiés lorsque leur index de session est égal à 1 (première visite).
- Le système suit ces identifiants pour distinguer les nouveaux visiteurs des visiteurs récurrents.

**Remarques importantes :**

Cette méthode de suivi présente certaines limites connues :

- **Utilisateurs de plusieurs appareils :** une même personne visitant à partir de différents appareils (bureau, mobile, tablette) ou navigateurs est comptabilisée comme plusieurs visiteurs uniques, car chaque appareil et navigateur reçoit un identifiant différent.
- **Effacement des cookies :** un nouvel identifiant est attribué aux utilisateurs qui effacent les cookies de leur navigateur et ils sont de nouveau comptabilisés comme de nouveaux visiteurs.
- **Paramètres de confidentialité :** les utilisateurs avec des paramètres de confidentialité stricts ou des bloqueurs de cookies peuvent ne pas être suivis.

**Idéal pour :**

- Suivi des nouvelles tendances des visiteurs au fil du temps.
- Analyse de l’efficacité des campagnes marketing.
- Comprendre les modèles de croissance du trafic.

**Conseil d’interprétation :** bien qu’elles ne soient pas parfaitement précises en raison des limitations ci-dessus, les mesures d’acquisition sont fiables pour identifier les tendances et comparer les périodes pendant lesquelles la plupart des utilisateurs et utilisatrices naviguent sur le même appareil et n’effacent pas fréquemment les cookies.

### Stratégies

- **Exploiter les données de performances de recherche** : utilisez le rapport [performances de recherche](../manage-results/search-performance.md) pour identifier les produits en tendance et les termes de recherche populaires. Créez des règles de marchandisage pour mettre en évidence ces éléments.

- **Optimiser les performances des recommandations** : surveillez les mesures [performances des recommandations](../manage-results/recommendation-performance.md) pour identifier les types de recommandations qui génèrent le plus de trafic et de conversions.

- **Mettre en surbrillance les nouveaux articles et les articles promotionnels** : utilisez les règles de marchandisage pour améliorer les nouveaux produits ou articles promotionnels dans les résultats de recherche pour attirer l’attention des nouveaux visiteurs.

- **Suivre les sources de trafic** : utilisez les données d’événement pour comprendre quels canaux apportent le trafic le plus précieux et optimisez vos efforts marketing en conséquence.

>[!TAB Réduction du taux de rebond]

Pour réduire le taux de rebond, votre objectif est de maintenir l’engagement des visiteurs et de réduire les visites sur une seule page.

![Taux de rebond des mesures de succès](../assets/bounce-rate.png)

### Comprendre la mesure du taux de rebond

**Ce qu’il mesure :** pourcentage de visiteurs et visiteuses qui quittent votre site après n’avoir consulté qu’une seule page, indiquant des problèmes potentiels d’expérience utilisateur, de pertinence des pages ou d’engagement du site.

**Calcul du taux de rebond :** le taux de rebond compare les sessions monopages au nombre total de sessions afin de déterminer le pourcentage de visiteurs qui quittent sans autre interaction.

**Formule:**

```
Bounce Rate = (Number of Bounced Sessions ÷ Total Sessions) × 100
```

**Source de données :** événements Storefront.

**Fonctionnement :**

- Une **session rebond** est comptabilisée lorsqu’un visiteur ne consulte qu’une seule page pendant toute sa visite.
- Le système effectue le suivi des pages vues au cours de chaque session afin d’identifier les visites sur une seule page.
- Les sessions sont déterminées par l’activité de l’utilisateur et la durée entre les interactions.

**Quelle est la cause des bounces**

- Visiteurs et visiteuses accédant à des pages non pertinentes (mauvais ciblage des annonces/recherches).
- Temps de chargement de page lent.
- Expérience utilisateur médiocre ou navigation déroutante.
- Recherche rapide d’informations sans avoir à en explorer davantage.
- Problèmes ou erreurs techniques.

**Remarques importantes :**

- Les taux de rebond élevés ne sont pas toujours négatifs. Certaines pages (telles que les coordonnées ou les spécifications de produits spécifiques) peuvent naturellement présenter des taux de rebond élevés.
- Comparez les taux de rebond sur différents types de page et sources de trafic pour identifier les zones problématiques.
- Les augmentations soudaines du taux de rebond indiquent souvent des problèmes techniques ou un mauvais ciblage de campagne.

**Qu’est-ce qu’un bon taux de rebond ?** Cela varie en fonction du secteur et du type de page, mais généralement :

- 40 à 60 % : moyenne pour les sites d’e-commerce.
- En dessous de 40 % : Excellent engagement.
- Plus de 70 % : peut indiquer des problèmes nécessitant une enquête.

### Stratégies

- **Améliorez la pertinence de la recherche** : utilisez des synonymes et une facettisation intelligente pour vous assurer que les clients trouvent rapidement des produits pertinents. De mauvais résultats de recherche sont une cause majeure des taux de rebond élevés.

- **Implémenter des unités de recommandation** : déployez des unités de recommandation sur les pages de résultats de catégorie et de recherche pour fournir des options de produit supplémentaires et maintenir l’engagement des visiteurs.

- **Optimiser la découverte de produits** : utilisez les règles de marchandisage pour vous assurer que les produits les plus pertinents et les plus populaires apparaissent en premier dans les résultats de recherche.

- **Créer des expériences de page d’accueil attrayantes** : utilisez les types de recommandation « Recommandé pour vous » et « En tendance » sur votre page d’accueil pour intéresser immédiatement les visiteurs et visiteuses avec du contenu pertinent.

>[!ENDTABS]

## Dépannage et optimisation

### Lorsque les mesures diminuent

**Recettes en baisse** :

- Vérifiez si les unités de recommandation sont toujours actives et performantes.
- Examinez les règles de marchandisage pour vous assurer que les produits à marge élevée sont promus.
- Analysez les performances de recherche pour déterminer si les produits populaires se classent toujours bien.

**Baisse du taux de conversion** :

- Vérifiez que la pertinence de la recherche est conservée (vérifiez les synonymes et les facettes).
- Vérifiez que les unités de recommandation s’affichent correctement.
- Consultez les règles de marchandisage pour tout conflit ou problème.

**Taux de rebond élevés** :

- Vérifiez la pertinence des résultats de recherche et implémentez des synonymes si nécessaire.
- Vérifiez que les unités de recommandation se chargent correctement.
- Examinez la qualité et la disponibilité des données sur les produits.

**Faible engagement** :

- Diversifiez les types de recommandations pour éviter la fatigue des clients.
- Mettre en œuvre des stratégies de recommandation plus personnalisées.
- Optimisez l’expérience de recherche avec de meilleures facettes et de meilleurs synonymes.

## Descriptions des champs

### Configuration du rapport

| Champ | Description |
|---|---|
| Période | Les options incluent **3 derniers mois**, **7 derniers jours**, **30 derniers jours**, **6 derniers mois**, **12 derniers mois** et **Année à ce jour**. Utilisez des plages plus courtes pour obtenir des informations d’optimisation immédiates et des plages plus longues pour l’analyse des tendances. |
| Pays | En fonction de la source de catalogue spécifiée pour votre [vue de catalogue](../setup/catalog-view.md). Sélectionnez le marché approprié pour une analyse des performances précise. |
| Devise monétaire | Devise spécifiée pour l’affichage du catalogue. Assurez-vous que cela correspond à votre marché cible pour un reporting précis des recettes. |
| Exporter | Enregistre le rapport en tant que PDF pour le partage avec les parties prenantes ou l’analyse hors ligne. |

## Plus comme ceci

- [Performances de la recherche](../manage-results/search-performance.md) - Analysez les termes de recherche et optimisez la pertinence de la recherche.
- [Performances des recommandations](../manage-results/recommendation-performance.md) - Surveillez et optimisez l’efficacité des recommandations.
- [Présentation de Recommendations](../merchandising/recommendations/overview.md) - Découvrez les recommandations de produits optimisées par l’IA.
- [Règles de marchandisage](../merchandising/rules/overview.md) - Booster, enterrer, épingler ou masquer des produits dans les résultats de recherche.
- [Facettes](../merchandising/facets/overview.md) - Améliorez la recherche avec le filtrage intelligent.
- [Synonymes](../merchandising/synonyms/overview.md) - Améliorez la pertinence de la recherche et l’expérience client.
- [Présentation des événements](../setup/events/overview.md) - Comprenez les données qui alimentent vos mesures.
