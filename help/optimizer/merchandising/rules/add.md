---
title: Créer et gérer des règles
description: Découvrez comment créer et gérer des règles de marchandisage.
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: fd4df2b2-83de-4c5c-b18c-e97aa07ef8f6
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 0%

---

# Créer et gérer des règles

Pour créer une règle, la première étape consiste à utiliser l’éditeur de règles pour définir les conditions dans le texte de requête de l’acheteur qui déclenchent les événements associés. Renseignez ensuite les détails de la règle, testez les résultats et publiez la règle.

## Créer une règle

1. Dans le rail de gauche, accédez à _Marchandisage_ > **Règles de marchandisage**.
1. Cliquez sur **Créer une règle** pour lancer l’éditeur de règles.

![Créer une règle](../../assets/create-rule.png)

Dans la section **Créer votre règle**, définissez des critères de recherche, des conditions et des types de classement spécifiques.

1. Dans le champ **[!UICONTROL Name]** , saisissez le nom de la règle. Tous les noms de règle doivent être uniques.
1. Dans le champ **[!UICONTROL Description]** , saisissez une description de la règle.
1. Dans le champ **[!UICONTROL Date range]** , indiquez la date ou la plage de dates à laquelle la règle doit être active.
1. Dans la section **[!UICONTROL Rule applies to]**, vous disposez de deux options : **[!UICONTROL All product listings]** ou **[!UICONTROL Specific conditions]**.

   - **Toutes les listes de produits** - Il s’agit essentiellement de votre règle par défaut qui est appliquée à toutes les requêtes de recherche, sauf si une requête plus spécifique est définie. Vous ne pouvez créer qu’une seule règle par défaut qui ne peut contenir aucune condition. Choisissez le type de classement Intelligent et tout classement manuel que vous souhaitez appliquer à toutes les recherches par défaut.
   - **Conditions spécifiques** - Consultez la section suivante pour en savoir plus sur les types de conditions que vous pouvez définir pour votre règle.

### Conditions

Les conditions sont les conditions requises pour déclencher un événement. Une règle peut contenir jusqu’à dix conditions et 25 événements. Une règle par défaut ne peut pas contenir de conditions.

![Sélectionner la condition de règle](../../assets/rule-set-condition.png)

#### Condition unique

1. Sous *Créer votre règle*, sélectionnez la **Condition** à remplir et suivez les instructions pour terminer l’instruction.

   - La requête de recherche contient : saisissez la chaîne de texte qui doit se trouver dans la requête de l’acheteur. Le paramètre Correspondance détermine le degré auquel la requête de l’acheteur correspond au catalogue. Options : <br /> quelconque - Toute partie du texte de la requête de l’acheteur peut correspondre à la condition.<br />Tous - Toutes les requêtes de l’acheteur doivent correspondre à la condition.
   - La requête de recherche est : saisissez une chaîne de texte qui correspond exactement à la requête de l’acheteur. Par exemple : « pantalon de yoga ». Les règles comportant des `Search query is` `All` et Correspondance ne peuvent comporter qu’une seule condition.
   - La requête de recherche commence par : saisissez un caractère ou une chaîne de texte qui doit se trouver au début de la requête de l’acheteur.
   - La requête de recherche se termine par - Saisissez un caractère ou une chaîne de texte qui doit se trouver à la fin de la requête de l’acheteur.

   Les résultats apparaissent immédiatement dans le volet *Tester votre règle* et sont numérotés par priorité. Vous pouvez utiliser le curseur *Résultats par ligne* en haut à droite pour modifier le nombre de produits dans chaque ligne.

1. Pour tester d’autres requêtes, modifiez le texte de la requête dans la zone de recherche *Tester votre règle* et appuyez sur **Retour**.
Au départ, le volet de test effectue le rendu de la requête à partir de la zone de recherche Conditions . Mais maintenant, il effectue le rendu de la requête à partir de la zone de requête test. Le volet de test effectue le rendu d’une seule requête à la fois.
1. Si le résultat vous convient, mettez à jour le texte dans la zone de recherche *Conditions*. Cliquez ensuite n’importe où sur la page pour mettre à jour les résultats dans le volet de test.

#### Conditions multiples

1. Pour créer une règle comportant plusieurs conditions, cliquez sur **Ajouter une condition**.
Une règle peut contenir jusqu’à dix conditions. L’opérateur logique qui joint deux conditions est basé sur le paramètre *Correspondance* actuel. Par défaut, *Correspondance* est `All` et l’opérateur logique est `AND`.

1. Sélectionnez la deuxième condition et saisissez le texte de requête requis.

1. Pour modifier la logique de la règle, modifiez le paramètre **Correspondance** afin de déterminer dans quelle mesure les critères de recherche de l’acheteur doivent correspondre à la condition de requête. Définissez **Correspondance** sur l’une des valeurs suivantes :

   - Any - (Par défaut) Tous les opérateurs logiques de la règle sont définis sur `OR` et les résultats apparaissent dans le volet de test.
   - Tous : tous les opérateurs logiques de la règle sont définis sur `AND` et les résultats apparaissent dans le volet de test.

   La valeur *Correspondance* détermine l’opérateur logique utilisé pour joindre plusieurs conditions. La modification du paramètre *Correspondance* modifie tous les opérateurs logiques de la règle. Il n’est pas possible de combiner `AND` et `OR` dans la même règle.

   Dans cet exemple, plutôt que de rechercher « pantalon de yoga », il existe deux requêtes distinctes qui recherchent « yoga » ou « pantalon ». Cette règle est moins spécifique et est déclenchée plus souvent dans le storefront que dans l’autre.

1. Pour ajouter une autre condition, cliquez sur **Ajouter une condition** et répétez le processus.

### Classement intelligent

Le classement intelligent combine les comportements des utilisateurs et les statistiques du site pour déterminer le classement des produits.
Les propriétaires de magasin peuvent configurer les types de stratégies de classement suivants :

![Classements intelligents](../../assets/rule-intelligent-ranking.png)

- Les plus achetés : cette option classe les produits en fonction du nombre total d’achats par SKU au cours des 7 jours précédents.
- Les plus ajoutés au panier : classent les activités « Ajouter au panier » par ordre de total au cours des 7 jours précédents.
- Les plus consultés : classe le nombre total de vues par SKU au cours des 7 jours précédents.
- Recommandé pour vous - Utilise le point de données `viewed-viewed` - Les acheteurs qui ont consulté ce SKU ont également consulté ces autres SKU.
- Tendance : examine les événements de pages vues au cours des 72 dernières heures pour les événements en arrière-plan et des 24 dernières heures pour les événements en premier plan.
- Aucun : les produits sont triés par pertinence.

Sélectionnez le type de stratégie de la règle. La fenêtre **Tester votre règle** affiche les résultats attendus.

#### Fonctionnement de la notation intelligente

Le classement intelligent détermine l’ordre final des produits en combinant deux facteurs clés : **pertinence textuelle** et **signaux comportementaux**. Comprendre l’interaction de ces facteurs vous permet de définir des attentes réalistes pour vos résultats de recherche.

**Composants de notation :**

- **Pertinence textuelle** : le facteur dominant dans la notation. Cela permet de mesurer la correspondance entre le nom, la description et les attributs d’un produit et la requête de recherche. Le score de pertinence du texte est illimité (il n’a pas de limite supérieure spécifique) et est influencé par des facteurs tels que :

   - Fréquence d&#39;occurrence des mots correspondants.
   - Longueur (en mots) des noms/descriptions des produits.

- **Signaux comportementaux** : un coup de pouce limité est appliqué en plus du score de pertinence du texte. Lorsque vous sélectionnez une stratégie de classement intelligente telle que « Les plus consultés » ou « Les plus achetés », les produits présentant des signaux comportementaux plus élevés bénéficient d’une amélioration fixe de leurs scores. Cependant, ce coup de pouce a une limite définie.

**Pourquoi le produit le plus consulté peut ne pas apparaître en premier :**

La pertinence textuelle domine généralement le classement parce que son score est illimité, alors que les encouragements comportementaux sont fixes. Par conséquent, les produits dotés de correspondances textuelles solides l’emportent souvent sur ceux présentant des signaux d’engagement plus élevés. Les stimuli comportementaux seuls peuvent ne pas compenser les larges écarts de pertinence du texte. Le classement intelligent résout ce problème en tenant compte à la fois de la qualité des correspondances et de l’interaction client, ce qui améliore la pertinence globale. Cependant, la qualité de la correspondance de texte reste le principal moteur du classement.

**Exemple:**

Un commerçant utilise la stratégie de classement intelligente « Les plus consultés » et recherche « bougie ». Ils s’attendent à ce que le SKU de produit YAN-K-E-512 apparaisse en haut des résultats, car il possède le nombre de vues le plus élevé. Cependant, d’autres produits se classent plus haut :

- **Texas Candle** (1ère position) : a un nom de produit plus court et plus propre qui crée un score de pertinence du texte très élevé. Même s&#39;il a moins de vues que YAN-K-E-512, sa correspondance de texte supérieure l&#39;emporte sur l&#39;amplification comportementale.

- **YAN-K-E-512** (position inférieure) : bien que disposant du centile de vue le plus élevé dans les données comportementales « Les plus consultés », son nom complexe basé sur un SKU génère un score de pertinence du texte inférieur. L’augmentation fixe des comportements ne suffit pas à combler ce fossé de pertinence du texte.

Consultez [règles de recherche](./best-practice.md#tips-to-optimize-search-rules) pour savoir comment améliorer la recherche de produit à l’aide de règles.

#### Avertissements

- Les apostrophes et les guillemets dans les requêtes peuvent entraîner des problèmes mineurs de classement et de pertinence dans certaines langues.
- Pour garantir le bon fonctionnement du classement intelligent, assurez-vous que la **pondération de recherche** de tous les attributs utilisés pour la recherche ou le filtrage (facettes) est `5` ou inférieure.

Pour plus d’informations sur la définition des poids de recherche, voir [API de métadonnées](https://developer.adobe.com/commerce/services/reference/rest/).

### Classement manuel

**Classement manuel** sont des actions qui modifient les résultats de la recherche lorsque des conditions définies sont remplies. Une seule règle peut contenir jusqu’à 25 événements.

- Booster - Fait monter un produit dans les résultats de recherche.
- Enterrer : déplace un SKU vers le bas dans les résultats de recherche.
- Épingler un produit : le produit s’affiche dans la « Position » sélectionnée sur la page.
- Masquer un produit - Exclut un SKU des résultats de recherche.

Le moyen le plus simple d’épingler un produit est de le faire glisser et de le déposer.

1. Cliquez sur un produit et faites-le glisser dans le volet Test. Faites-la glisser et déposez-la à l’emplacement souhaité. Les champs Produit et Position sont automatiquement renseignés dans le volet Événements.

Vous pouvez également cliquer sur l’icône d’épingle pour épingler un produit à son emplacement actuel. Utilisez le menu contextuel représentant des points de suspension pour effectuer l’opération « Épingler en haut » ou « Épingler en bas ».

>[!NOTE]
>
>Vous ne pouvez épingler que les produits renvoyés dans la requête.

Les événements ou peuvent être définis manuellement :

1. Sous *Événements*, sélectionnez l’événement **Événement** qui doit avoir lieu une fois les conditions associées remplies.

   Par exemple, choisissez `Hide a product`. Saisissez ensuite le nom du produit à masquer. Des produits sont suggérés lors de la saisie.

1. Pour plusieurs événements, choisissez tous les autres événements que vous souhaitez déclencher lorsque les conditions sont remplies.

### Finalisation de la règle

1. Examinez les résultats de la règle dans le volet de test.
1. Si la règle comporte plusieurs requêtes, testez chacune d’elles qui peut être affectée par la règle.
1. Une fois l’opération terminée, cliquez sur **Enregistrer et publier**.

   La règle est ajoutée à la liste dans l’espace de travail *Règles*.

1. Bien que les règles actives prennent immédiatement effet, vous devrez peut-être attendre jusqu’à 15 minutes pour que les résultats de la requête mise en cache dans le storefront soient actualisés.

>[!NOTE]
>
>Les règles et les produits classés manuellement sont appliqués aux résultats de la recherche lorsque l’ordre de tri par défaut « Trier par : les plus pertinents » est sélectionné. Si un acheteur modifie l’ordre de tri pour qu’il ressemble à un tri par nom ou prix, les règles et les classements manuels ne sont plus en vigueur.

## Modifier, afficher et supprimer des règles

Suivez ces instructions pour mettre à jour les propriétés des règles existantes.

### Modifier la règle

1. Dans l’espace de travail *Règles de marchandisage*, recherchez la règle de la grille à modifier, puis cliquez sur les options **Plus** (...).
1. Cliquez sur **Modifier** pour accéder à l’éditeur de règles.
1. Mettez à jour les conditions, les opérateurs et les événements selon les besoins.
1. Mettez à jour le nom, la date de début et de fin, ainsi que les champs de description selon les besoins. Tous les noms de règle doivent être uniques.
1. Testez la règle.
1. Publiez les modifications.
La règle est ajoutée à la liste dans l’espace de travail *Règles*. Bien que les règles actives entrent en vigueur immédiatement, l’actualisation des résultats des requêtes mises en cache dans le storefront peut prendre jusqu’à 15 minutes.

### Afficher les détails

Cette option permet d’afficher rapidement tous les paramètres de la règle, tout en restant dans le tableau *Règles*.

1. Dans l’espace de travail *Règles de marchandisage*, recherchez la règle de la grille à modifier, puis cliquez sur les options **Plus** (...).
1. Cliquez sur **Afficher les détails** pour afficher les paramètres de la règle.
1. Choisissez **Modifier** ou **Supprimer**, ou cliquez sur le X pour fermer le panneau.

### Supprimer la règle

1. Dans l’espace de travail *Règles*, recherchez la règle de la grille à modifier, puis cliquez sur les options **Plus** (...).
1. Cliquez sur **Supprimer**.

## Descriptions des champs

### Conditions (le cas échéant)

| Condition | Description |
|--- |--- |
| La requête de recherche contient | Caractère ou chaîne de texte inclus dans la requête de l’acheteur. La requête de l’acheteur ne doit correspondre qu’à un seul caractère pour remplir cette condition. |
| La requête de recherche est | Caractère ou chaîne de texte correspondant exactement à la requête de l’acheteur. Les requêtes complexes avec plusieurs conditions ne peuvent pas être composées lorsque cette condition est utilisée. |
| La requête de recherche commence par | La requête de l’acheteur commence par ce caractère ou cette chaîne de texte. |
| La requête de recherche se termine par | La requête de l’acheteur se termine par ce caractère ou cette chaîne de texte. |

### Opérateurs logiques

| Opérateur | Description |
|--- |--- |
| SOIT | (Par défaut) L’opérateur logique `OR` compare deux conditions et répond aux exigences pour déclencher un événement si au moins une condition est vraie. |
| ET | L’opérateur logique compare `AND` deux conditions et satisfait aux exigences pour déclencher un événement si les deux conditions sont vraies. |

### Faire correspondre les opérateurs

| Opérateur | Description |
|--- |--- |
| N’importe lequel | Remplace tous les opérateurs logiques de la règle par `OR` et renvoie l’ensemble des produits correspondants. |
| Tous | Remplace tous les opérateurs logiques de la règle par `AND` et renvoie l’ensemble des produits correspondants. |

### Classement manuel

| Événement | Description |
|--- |--- |
| Amplifier | Déplace un SKU ou une plage de SKU vers le haut dans les résultats de recherche. Chaque élément est marqué d’un badge d’aperçu « boosté » dans les résultats de la recherche de test. |
| Enterrer | Déplace un SKU ou une plage de SKU plus bas dans les résultats de recherche. Chaque dossier est marqué d’un badge d’aperçu « enterré » dans les résultats de la recherche de test. |
| Épingler un produit | Associe un seul SKU à une position spécifique dans les résultats de recherche. Le produit est marqué d’un badge d’aperçu « épinglé » dans les résultats de la recherche de test. |
| Masquer un produit | Exclut un SKU, ou une plage de SKU, des résultats de recherche. |

### Détails

| Champ | Description |
|--- |--- |
| Nom | Nom de la règle. Les noms des règles doivent être uniques. |
| Type de règle | Par défaut ou Requête. La valeur par défaut est appliquée à toutes les règles, sauf si une règle de requête plus spécifique est définie. |
| Date de début | Date de début de la règle, le cas échéant. |
| Date de fin | Date de fin de la règle, le cas échéant. |
| Description | Brève description de la règle. |
