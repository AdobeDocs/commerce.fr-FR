---
title: Estimation du volume de données et de la durée de transmission
description: Découvrez comment estimer le volume de données et le temps de transmission requis pour que l’outil  [!DNL data export]  synchroniser les données de flux entre Adobe Commerce et les services connectés.
role: Admin, Developer
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Estimation du volume de données et de la durée de transmission pour la synchronisation des données

Adobe recommande d’estimer le volume et la durée de synchronisation des données avant de démarrer la synchronisation des flux de données afin d’assurer une planification fluide et d’éviter toute interruption des opérations sur le site. Cette estimation est importante lors de la planification de synchronisations initiales ou de mises à jour de catalogue à grande échelle, telles que des modifications de prix en masse.

Par défaut, l’outil d’exportation de données traite les données en mode thread unique avec une taille de lot par défaut. Avec la configuration par défaut, il n’y a pas de parallélisation du processus d’envoi des flux. En outre, ce composant accepte les requêtes par seconde (RPS), ce qui se traduit par :

- Jusqu’à 10 000 produits par minute lorsqu’un produit est un SKU avec des attributs dans un magasin spécifique
- Jusqu&#39;à 50 000 prix par minute

Les facteurs suivants affectent le temps de transmission des données lors de la synchronisation.

- Le nombre de threads est défini sur 1 (par défaut)
- La taille du lot est définie sur _100_ pour tous les flux, à l’exception du flux `prices`, où elle est définie sur _500_.
- Le taux d’acceptation des flux est de 2 requêtes par seconde.
- Tous les produits sont affectés à tous les sites web existants
- Pour les scénarios de calcul des prix, des prix spéciaux et groupés sont attribués à tous les produits


## Calculer la transmission des données par flux

Utilisez les valeurs et les formules du tableau suivant pour calculer le volume de données et la durée de synchronisation pour chaque flux de données.

>[!NOTE]
>
>Ces calculs sont basés sur un taux de transmission de 2 requêtes par seconde. La vitesse est basée sur le temps nécessaire à la collecte et à la soumission des données. La vitesse de transmission réelle varie en fonction de la taille de la payload de la requête et de la charge actuelle sur le serveur d’applications Commerce.

| Flux | Exemple de données | Formule de calcul des enregistrements | Nombre de demandes prédit | Durée de resynchronisation prévue |
| --- | --- | --- | --- | --- |
| Produits | Produits (P) : 10000, Vues de la boutique (SV) : 4 | P * SV = 40000 | 40000/taille du lot (100) = 400 requêtes | (400 requêtes * 0,5 seconde par requête) / 60 = 3,3 minutes |
| Catégories | Catégories (C) : 500, Vues de la boutique (SV) : 4 | C * SV = 2000 | 2000 / Taille du lot (100) = 20 requêtes | (20 requêtes * 0,5 seconde par requête) / 60 = 0,1 minute (4 secondes) |
| Prix | Produits (P) : 10000, Groupes de clients (CG) : 6 (par exemple, prix unique dans le catalogue partagé), Sites web (WS) : 2 | P \* WS * CG = 120000 | 120000/taille du lot (500) = 240 requêtes | (240 requêtes * 0,5 seconde par requête) / 60 = 2 minutes |
| Remplacements de produit | Produits avec autorisations ou dans le catalogue partagé (P) : 10000, Groupes de clients affectés (CG) : 5, Sites web attribués WS : 2 | P \* WS * CG = 100000 | 100000/taille du lot (100) = 1 000 requêtes | (1 000 requêtes * 0,5 seconde par requête)/60 = 8,3 minutes |
| Variantes de produit | Variantes (produits enfants) affectées aux produits configurables (VA) : 100000 | PV = 100000 | 100000/taille du lot (100) = 1 000 requêtes | (1 000 requêtes * 0,5 seconde par requête)/60 = 8,3 minutes |
| Autorisations de catégorie | Nombre de toutes les autorisations de catégorie + 4 enregistrements de secours (CP) : 10000 | CP = 10000 | 10000/taille du lot (100) = 100 requêtes | (100 requêtes * 0,5 seconde par requête) / 60 = 0,8 minute (50 secondes) |
| Statut du stock de stock | Produits (P) : 10000, Stocks produits affectés à (S) : 5 (en supposant que chaque produit est affecté à chaque stock) | P * S = 50000 | 50000/taille du lot (100) = 500 requêtes | (500 requêtes * 0,5 seconde par requête) / 60 = 4,2 minutes |
| Commandes client | Tous les enregistrements de commande (y compris les factures, les expéditions, etc.) (SO) : 10000 | SO = 10000 | 10000/taille du lot (100) = 100 requêtes | (100 requêtes * 0,5 seconde par requête) / 60 = 0,8 minute (50 secondes) |
