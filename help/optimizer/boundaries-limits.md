---
title: Limites et limites
description: Découvrez les limites et les limites de pour  [!DNL Adobe Commerce Optimizer]  assurer qu’il répond aux besoins de votre entreprise.
role: Admin, Developer
exl-id: 58d94da9-8d48-4513-8b6a-8e8c7c27a2a5
source-git-commit: 149b87fc822e5d07eed36f3d6a38c80e7b493214
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---

# Limites et limites

>[!NOTE]
>
>Cette documentation décrit les limites et les limites du développement en accès anticipé et ne reflète pas toutes les fonctionnalités destinées à une disponibilité générale.

Vous trouverez ci-dessous les limites de Adobe Commerce Optimizer.

## Catalogue

- Le taux garanti d’ingestion du catalogue est de 1 000 produits/minute et de 5 000 prix/minute
- Le nombre de base de mises à jour de produits par jour est de 1 000 000.
- Le nombre total de SKU autorisés dans une seule instance est de 250 000. 
- Le nombre maximal de portées est de 50.
- Le nombre de variantes par produit est de 10 000.
- La taille du produit ne peut pas dépasser 200 Ko.

## Prix

- Le nombre maximal de livres de prix est de 1 000.

## Recherche et storefront

- Le nombre de produits qu’une seule requête de recherche peut renvoyer est de 100.
- Le nombre maximal d’attributs filtrables est de 200
- Le nombre maximal d’attributs pouvant faire l’objet d’une recherche est de 200
- Le nombre maximal d’attributs triables est de 50
- Le nombre maximal de facettes est de 100. Toutes les facettes doivent être des attributs filtrables.
- Le nombre maximal d’options qu’un seul chat à facettes renvoie est de 100, ce qui peut être augmenté par demande d’assistance.

## Canaux et politiques

- Le nombre maximal de canaux par client est de 1 000.
- Le nombre maximal de politiques affectées à un canal est de 10.
- Le nombre maximal de valeurs d’attribut utilisées dans une politique est de 100. 

## Découverte de produits et recommandations

- Pour la découverte de produits, le marchandisage basé sur les attributs et les paramètres de prix ne sont pas pris en charge.
- Pour les recommandations :

   - [!DNL Adobe Commerce Optimizer] prend en charge le type de recommandation _Récemment consultés_ pour un accès anticipé.
   - Les inclusions ou exclusions de catégories ou d’attributs ne sont pas prises en charge.
   - Vous ne pouvez pas prévisualiser les recommandations dans [!DNL Adobe Commerce Optimizer].
