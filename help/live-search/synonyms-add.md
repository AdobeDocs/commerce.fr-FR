---
title: Ajouter des synonymes
description: Ajoutez  [!DNL Live Search]  synonymes pour améliorer la réponse aux requêtes de recherche.
exl-id: 2dc535ea-35a3-45a8-8171-901005223cc9
source-git-commit: 81bde302463a70e41318b494565694929703dff9
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Ajouter des synonymes

Améliorez l’engagement des clients en ajoutant votre propre liste de synonymes [!DNL Live Search]. [!DNL Live Search] pouvez gérer jusqu’à 200 synonymes par `Data Space ID`.

![[!DNL Live Search] synonymes ](assets/synonym-workspace.png)

## Étape 1 : ajouter un synonyme

1. Dans Admin, accédez à **Marketing** > SEO et recherche > **[!DNL Live Search]**.
1. Pour plusieurs magasins, définissez **Portée** sur la vue [ magasin](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) où les paramètres de synonyme s’appliquent.
1. Cliquez sur l’onglet **Synonymes**.
1. Cliquez sur le bouton **Ajouter des synonymes**.

## Étape 2 : définir le synonyme par type

Suivez les instructions relatives au [type de synonyme](synonyms-type.md) que vous souhaitez créer.

### Synonyme bidirectionnel

1. Acceptez l’option **Bidirectionnelle** par défaut.

   ![Ajouter un synonyme bidirectionnel](assets/synonym-add-two-way.png)

1. Saisissez le terme ou l’expression **Mot-clé** à faire correspondre.
1. Saisissez le ou les termes **Expansion** que vous souhaitez ajouter comme synonymes du mot-clé. Séparez les différents termes par une virgule.
Dans cet exemple, le mot-clé à associer est « pantalon » et l’ensemble des termes d’extension est « pantalon, pantalon ».

   ![Exemple de synonyme bidirectionnel](assets/synonym-add-two-way-example.png)

1. Une fois l’opération terminée, cliquez sur **Enregistrer**.
L’ensemble des synonymes apparaît dans la liste avec une flèche bidirectionnelle entre chaque terme, ce qui signifie que les termes sont interchangeables.

   ![Synonyme bidirectionnel](assets/synonym-two-way.png)

### Synonyme unidirectionnel

1. Cliquez sur le type de synonyme **Unidirectionnel**.

   ![Ajouter un synonyme unidirectionnel](assets/synonym-add-one-way.png)

1. Saisissez les termes **Mot-clé** et **Expansion**. Séparez les différents termes par une virgule.

   ![Exemple de synonyme unidirectionnel](assets/synonym-add-one-way-example.png)

   Dans cet exemple, le mot-clé est « pantalon » et les termes d’extension unidirectionnels « capris, peddle-pushers » sont chacun un sous-ensemble de « pantalon », mais avec une signification spécifique.

1. Une fois l’opération terminée, cliquez sur **Enregistrer**.
L’ensemble de synonymes apparaît dans la liste avec une flèche à sens unique pointant des termes d’extension vers le mot-clé pour indiquer que les termes sont des sous-ensembles du mot-clé. Un signe plus sépare chaque terme de développement.

   ![Synonyme unidirectionnel](assets/synonym-one-way.png)

## Étape 3 : Publier les modifications

1. Une fois vos synonymes terminés, cliquez sur **Publier les modifications**.
1. Patientez jusqu’à deux heures pour que vos mises à jour soient disponibles dans le storefront.

## Descriptions des champs

| Champ | Description |
|--- |--- |
| [Type ](synonyms.md) | Détermine si les synonymes ont la même signification que le mot-clé ou s’ils sont un sous-ensemble du mot-clé. Options : <br />Bidirectionnel (par défaut) - Termes ayant la même signification que le mot-clé et renvoyant les mêmes résultats de recherche<br />Unidirectionnel - Termes qui sont un sous-ensemble du mot-clé. Les synonymes à sens unique renvoient une liste plus étroite de produits spécifiques. |
| Mot-clé | Mot généralement associé à une sélection de produits dans votre catalogue. |
| Extension | Termes supplémentaires ayant la même signification ou une signification similaire au mot-clé. |
