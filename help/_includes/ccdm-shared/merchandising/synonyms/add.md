---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%
---
Augmentez l’engagement des clients en ajoutant votre propre liste de synonymes sélectionnée. Vous pouvez ajouter jusqu’à 200 synonymes par source de catalogue.

![Synonyme Workspace](/help/assets/ccdm-shared/synonyms/synonym-workspace.png)

## Étape 1 : ajouter un synonyme

1. Accédez à _Marchandisage_ > **Synonymes**.
1. Cliquez sur le bouton **[!UICONTROL Create synonyms]**.

## Étape 2 : définir le synonyme par type

Suivez les instructions relatives au type de synonyme [&#128279;](type.md) que vous souhaitez créer.

### Synonyme bidirectionnel

1. Saisissez le terme ou l&#39;expression **Mot-clé** à faire correspondre.
1. Saisissez le ou les termes de l&#39;extension **Expansion** que vous souhaitez ajouter comme synonymes du mot-clé. Séparez les différents termes par une virgule.
Dans cet exemple, le mot-clé à associer est « pantalon » et l’ensemble des termes d’extension est « pantalon, pantalon ».

   ![Synonyme bidirectionnel](/help/assets/ccdm-shared/synonyms/synonym-add-two-way.png)

1. Une fois l’opération terminée, cliquez sur **Enregistrer**.

   L’ensemble des synonymes apparaît dans la liste avec une flèche bidirectionnelle entre chaque terme, ce qui signifie que les termes sont interchangeables.

   ![Exemple de synonyme bidirectionnel](/help/assets/ccdm-shared/synonyms/synonym-add-two-way-example.png)

### Synonyme unidirectionnel

1. Cliquez sur le type de synonyme **Unidirectionnel**.

1. Saisissez les termes **Mot-clé** et **Extension**. Séparez les différents termes par une virgule.

   ![Synonyme unidirectionnel](/help/assets/ccdm-shared/synonyms/synonym-add-one-way.png)

   Dans cet exemple, le mot-clé est « pantalon » et les termes d’extension unidirectionnels « capris, peddle-pushers » sont chacun un sous-ensemble de « pantalon », mais avec une signification spécifique.

1. Une fois l’opération terminée, cliquez sur **Enregistrer**.

   L’ensemble de synonymes apparaît dans la liste avec une flèche à sens unique pointant des termes d’extension vers le mot-clé pour indiquer que les termes sont des sous-ensembles du mot-clé. Un signe plus sépare chaque terme de développement.

   ![Exemple de synonyme unidirectionnel](/help/assets/ccdm-shared/synonyms/synonym-add-one-way-example.png)

## Étape 3 : Publier les modifications

1. Une fois vos synonymes terminés, cliquez sur **Publier**.
1. Patientez jusqu’à deux heures pour que vos mises à jour soient disponibles dans le storefront.

## Descriptions des champs

| Champ | Description |
|--- |--- |
| [Type](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/merchandising/synonyms/type) | Détermine si les synonymes ont la même signification que le mot-clé ou s’ils sont un sous-ensemble du mot-clé. Options :<br />Bidirectionnel (par défaut) - Termes ayant la même signification que le mot-clé et renvoyant les mêmes résultats de recherche<br />Unidirectionnel - Termes qui sont un sous-ensemble du mot-clé. Les synonymes à sens unique renvoient une liste plus étroite de produits spécifiques. |
| Mot-clé | Mot généralement associé à une sélection de produits dans votre catalogue. |
| Extension | Termes supplémentaires ayant la même signification ou une signification similaire au mot-clé. |

## Gestion des synonymes

Suivez ces instructions pour gérer les [synonymes](https://experienceleague.adobe.com/fr/docs/commerce/optimizer/merchandising/synonyms/overview) existants.

## Rechercher le synonyme

Pour faciliter la recherche d’un synonyme, vous pouvez filtrer la liste par type et effectuer une recherche par mot-clé ou terme d’extension. Ces méthodes peuvent être utilisées individuellement ou conjointement.

1. Pour filtrer la liste, définissez **Type** sur l&#39;une des valeurs suivantes :

   - Tous
   - Unidirectionnel
   - Bidirectionnel

1. Pour rechercher un mot-clé ou un terme d&#39;extension, saisissez au moins trois caractères dans la zone **[!UICONTROL Search]**.

## Modifier le synonyme

1. Recherchez le synonyme à modifier et cliquez sur **Plus** (...) options.

1. Cliquez sur **Modifier**.
Le mot-clé est le premier terme de la liste et chaque terme est séparé par une virgule. Le mot-clé et les termes d’extension peuvent être mis à jour, mais le type du synonyme ne peut pas être modifié.
1. Cliquez sur l’élément à modifier. Mettez ensuite à jour le texte selon vos besoins.

1. Une fois l’opération terminée, cliquez sur **Enregistrer**.

## Supprimer le synonyme

1. Recherchez le synonyme à supprimer dans la liste et cliquez sur **Plus** (...) options.
1. Cliquez sur **Supprimer**.
1. Lorsque vous y êtes invité, cliquez sur **Supprimer le synonyme** pour confirmer.

## Publier les modifications

Pour terminer le processus, vos modifications enregistrées doivent être publiées sur le storefront. L’activation des mises à jour peut prendre jusqu’à deux heures.

1. Cliquez sur **Publier**.
1. Recherchez le message en haut de la page qui confirme que vos modifications ont été publiées.
