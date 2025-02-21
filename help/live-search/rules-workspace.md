---
title: Rechercher dans le Workspace de marchandisage
description: Découvrez l’espace de travail de marchandisage de la recherche.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---

# Rechercher dans le Workspace de marchandisage

L’espace de travail *Marchandisage de recherche* répertorie la sélection actuelle de règles et leur statut. Il permet également d’accéder aux outils dont vous avez besoin pour créer et gérer des règles. Dans l’espace de travail , vous pouvez :

* Rechercher des règles
* Afficher les détails de la règle
* Activer/désactiver les règles
* Supprimer les règles
* Accès à l’éditeur de règles

![Rechercher dans le Workspace de marchandisage](assets/rules-workspace.png)

## Définir la portée

Si votre installation d’Adobe Commerce comprend plusieurs vues de magasin, définissez **Portée** sur la [ vue de magasin](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) où vos règles s’appliquent.

## Afficher/masquer les colonnes

1. Dans le coin supérieur droit, cliquez sur **Afficher/masquer** ![Sélecteur de colonne](assets/btn-show-hide-columns.png) colonnes.
Les colonnes visibles comportent une coche bleue dans le menu d’options. Le nom de la règle est la seule colonne qui ne peut pas être masquée.

1. Dans le menu, effectuez l’une des opérations suivantes :

   * Pour afficher une colonne masquée, cliquez sur un nom de colonne sans coche.
   * Pour masquer une colonne visible, cliquez sur un nom de colonne avec une coche.

## Filtrer les règles par statut

1. Si votre boutique comporte de nombreuses règles, vous pouvez les filtrer par statut pour raccourcir la liste. Par défaut, la liste Règles affiche toutes les règles.

1. Pour répertorier uniquement les règles avec un paramètre de statut spécifique, définissez **Statut** sur l’une des options suivantes :

   * Tous
   * Actif
   * Inactif
   * Planifié

## Rechercher des règles de recherche par nom

Commencez à saisir le nom de la règle ou tout autre mot dans le nom de la règle.
La recherche trouve la ou les règles correspondantes au fur et à mesure que vous tapez. La chaîne de caractères correspondante est mise en surbrillance dans le nom de chaque règle trouvée.

![Règles - Rechercher par nom](assets/rules-workspace-search-name.png)

## Afficher les détails

Le panneau des détails affiche le nom de la règle, le statut, les conditions et les événements, les dates de début et de fin, la description et la date de la dernière modification. Les règles peuvent être activées, modifiées et supprimées à partir du panneau des détails.

1. Dans l’espace de travail *Marchandisage de recherche*, recherchez la règle de la grille à afficher, puis cliquez sur **Plus** (...).
1. Cliquez sur **Afficher les détails**.
Vous pouvez effectuer l’une des opérations suivantes à partir du panneau Afficher les détails :

   * Modifier la règle
   * Supprimer la règle
   * Activer/Désactiver La Règle

1. Pour fermer le panneau *Afficher les détails*, cliquez sur **Fermer** (X) dans le coin supérieur droit.

   ![Règle - détails](assets/rules-workspace-details.png)

## Descriptions des colonnes

| Colonne | Description |
|--- |--- |
| Nom | Nom de la règle. |
| Dernière mise à jour | Date de la dernière mise à jour de la règle. |
| Date de début | Date de début d’une règle planifiée. |
| Date de fin | Date de fin d’une règle planifiée. |
| Statut | L’état avec code couleur indique l’état actuel de la règle. Utilisez la commande Statut au-dessus de la grille pour filtrer les règles par statut. Values:<br />All status - Affiche toutes les règles, quel que soit leur statut.<br />Actif (bleu) - Affiche uniquement les règles actives.<br />Planifié (orange) - affiche uniquement les règles planifiées.<br />Inactif (gris) - affiche uniquement les règles inactives. |

## Contrôles

| Contrôle | Description |
|--- |--- |
| Ajouter une règle | Ouvre l’[éditeur de règles](rules-add.md). |
| Statut | Filtre la liste des règles par statut. Options : Tous, Actif, Inactif, Planifié |
| ![Sélecteur de colonnes](assets/btn-show-hide-columns.png) | Spécifie les colonnes visibles dans la grille. Options : Dernière mise à jour, Date de début, Date de fin, Statut |
| Rechercher | Recherche une règle par nom complet ou correspondance partielle. |
| ![Plus de sélecteur](assets/btn-more.png) | Affiche un menu d’actions supplémentaires pouvant être appliquées à la règle sélectionnée. Options : Modifier, Afficher les détails, Supprimer |

## Détails de la règle

| Champ | Description |
|--- |--- |
| Statut | Statut actuel de la règle. |
| Conditions | Requête de recherche qui décrit les conditions associées à la règle. |
| Date de début | Date d’entrée en vigueur de la règle, le cas échéant. |
| Date de fin | Date d’expiration de la règle, le cas échéant. |
| Description | Brève description de la règle. |
| Dernière mise à jour : | Date et heure de la dernière mise à jour de la règle. |
| Activé | Contrôle qui modifie le statut de la règle. Options : Activé / Désactivé |
