---
title: Création et gestion des facettes
description: Découvrez comment ajouter et gérer des facettes dans  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
exl-id: d6b7ff1f-a9b8-4fb8-8bd3-b3596695045c
source-git-commit: ad8fb7d1d7e1ad124647ba84377079dcfbd46a3c
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 0%

---

# Création et gestion des facettes

Tout attribut de produit filtrable peut être utilisé comme facette. Les facettes aident les clients à filtrer et à trouver plus facilement des produits dans votre magasin. Cet article explique comment ajouter, gérer et configurer des facettes dans votre storefront.

![Créer une facette](../../assets/create-facet.png)

## Créer une facette

1. Dans le rail de gauche, sélectionnez _Marchandisage_ > **Facettes**, puis cliquez sur **Créer des facettes**.
1. Dans la liste *Créer des facettes*, chaque attribut disponible comporte un bouton ![Ajouter](../../assets/btn-add.png) distinct. Effectuez l’une des opérations suivantes :

   - Dans la liste *Attributs de facettes*, sélectionnez l’attribut de produit à utiliser comme facette et cliquez sur **Ajouter**.
   - Pour rechercher un attribut de produit spécifique, saisissez les premiers caractères du nom de l’attribut dans la zone *Rechercher*. Cliquez ensuite sur **Ajouter**.

   La facette est ajoutée en bas de la liste *Facettes dynamiques* et le bouton *Publier les modifications* devient disponible.

1. Si la facette à ajouter est introuvable, utilisez l’[API Metadata](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata) pour définir le paramètre `searchable` :

   `"searchable": true`

   La facette sera disponible dans le storefront la prochaine fois que le catalogue sera synchronisé avec [!DNL Adobe Commerce Optimizer]. Si la facette n’est pas disponible au bout de deux heures, reportez-vous à la section [synchronisation des données](../../setup/data-sync.md).

## Modification des propriétés de facette (facultatif)

1. Recherchez la facette à modifier.
1. Cliquez sur le sélecteur (![Plus de sélecteurs](../../assets/btn-more.png)) plus .
1. Dans le menu, cliquez sur **Modifier**. Modifiez ensuite les propriétés suivantes selon vos besoins :

   - Libellé : saisissez le libellé de facette à utiliser.
   - Type de tri - Sélectionnez l’une des options suivantes :
      - Alphabétique : trie les facettes par ordre alphabétique
      - Nombre : trie les facettes en fonction du nombre de correspondances trouvées.
   - Valeur max - Saisissez le nombre maximal de valeurs de facette affichées dans le storefront. Entrées valides : 0 - 100 ; valeur par défaut : 8.

1. Une fois l’opération terminée, cliquez sur **Enregistrer**.

## Épingler/Détacher Les Facettes

L’épingle change de couleur lorsque vous cliquez dessus et est utilisée pour déplacer la facette vers la section *Facettes épinglées* ou *Facettes dynamiques*.

1. Pour épingler une facette en haut de la liste *Filtres*, recherchez-la dans la liste *Facettes dynamiques*, puis cliquez sur l’épingle grise (![Sélecteur d’épingle](../../assets/btn-pin-gray.png)).

   L’épingle devient bleue et la facette passe à la section *Facettes épinglées*.

1. Pour désépingler une facette, recherchez-la dans la liste *Facettes épinglées*, puis cliquez sur l’épingle bleue (![sélecteur d’épingle](../../assets/btn-pin-blue.png)).

   L’épingle devient grise et la facette passe à la section *Facettes dynamiques*.

>[!NOTE]
>
>L’ordre des facettes épinglées peut être incohérent s’il existe deux libellés portant le même nom.

## Suppression des facettes

1. Recherchez la facette dans la liste, puis cliquez sur le sélecteur (![Plus de sélecteur](../../assets/btn-more.png)) Plus .
1. Cliquez sur **Supprimer**.
1. Lorsque vous êtes invité à confirmer, cliquez sur **Supprimer la facette**.
La facette est supprimée du storefront une fois les modifications publiées.

## Publier les modifications

1. Pour mettre à jour le storefront avec vos modifications, cliquez sur **[!UICONTROL Publish]**.
1. Patientez environ 15 minutes pour que les mises à jour apparaissent dans votre boutique.

## Informations supplémentaires

- Pour configurer les intervalles et les regroupements de facettes de prix, voir [Paramètres](../../settings.md).
- En savoir plus sur les [types](type.md) de facettes.
