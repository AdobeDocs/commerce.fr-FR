---
title: Estimation du volume de données et de la durée de synchronisation
description: Découvrez comment estimer le volume des données et le temps de synchronisation des flux pour planifier les synchronisations  [!DNL Adobe Commerce Optimizer Connector]  catalogue et éviter les interruptions.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---


# Estimation du volume de données et de la durée de synchronisation

Adobe recommande d’estimer le volume et la durée de synchronisation des données avant de démarrer la synchronisation des flux afin d’assurer une planification fluide et d’éviter toute interruption du fonctionnement du site. Ceci est particulièrement important lors de la planification de synchronisations initiales ou de mises à jour de catalogue à grande échelle, telles que des modifications de prix en masse.

Par défaut, le connecteur traite les flux en mode thread unique. Il n’y a pas de parallélisation du processus de soumission des flux. L’API d’ingestion accepte jusqu’à 2 requêtes par seconde. Cependant, l’affectation de base pour le taux d’ingestion [!DNL Adobe Commerce Optimizer] limite le débit aux valeurs suivantes :

- Jusqu’à 1 000 produits par minute (un produit est un SKU avec des attributs dans une vue de magasin spécifique). Voir [Limites et limites](../../optimizer/boundaries-limits.md) pour les détails de l&#39;allocation de base.
- Jusqu&#39;à 50 000 prix par minute

## Facteurs affectant l’heure de synchronisation

Les estimations ci-dessous supposent les conditions suivantes :

- Nombre de threads : 1 (par défaut)
- Taux d’acceptation des flux : 2 requêtes par seconde (0,5 seconde par requête)
- Tous les produits sont affectés à tous les sites web existants

La vitesse de transmission réelle varie en fonction de la taille de la payload de la requête et de la charge actuelle sur le serveur d’applications Commerce.

## Calculer le temps de synchronisation par flux

Utilisez le tableau suivant pour estimer le nombre d’enregistrements, de requêtes et de temps de synchronisation pour chaque flux du connecteur. Les valeurs de taille de lot reflètent les limites définies dans la référence [flux pris en charge](connector-reference.md#supported-feeds).

>[!NOTE]
>
>Le temps de synchronisation des produits est basé sur la limite d’allocation de base de 1 000 produits par minute. Pour les autres flux, les calculs sont basés sur un taux de transmission de 2 requêtes par seconde. La vitesse réelle dépend de la taille de la payload et de la charge du serveur.
>
>L’estimation des prix suppose que tous les groupes de clients ont des prix uniques.

| Flux | Exemple de données | Formule | Requêtes prévues | Heure de synchronisation prévue |
| ---- | ------------ | ------- | ------------------ | ------------------- |
| Produits | Produits (P) : 10 000, Vues de la boutique (SV) : 4 | P × SV = 40 000 enregistrements | Taille de lot de 40 000 ÷ (100) = 400 | 40 000 ÷ 1 000 enregistrements/min = **40 min** |
| Catégories | Catégories (C) : 500, Vues de la boutique (SV) : 4 | C × SV = 2 000 enregistrements | 2 000 ÷ de lot (100) = 20 | (20 × 0,5 s) ÷ 60 = **~10 s** |
| Attributs de produit | Attributs (A) : 200, Vues de la boutique (SV) : 4 | A × SV = 800 enregistrements | Taille de lot de 800 ÷ (100) = 8 | (8 × 0,5 s) ÷ 60 = **~4 s** |
| Prix | Produits (P) : 10 000, Sites Web (WS) : 2, Groupes de clients (CG) : 6 | P × WS × CG = 120 000 enregistrements | Taille de lot de 120 000 ÷ (500) = 240 | (240 × 0,5 s) ÷ 60 = **2 min** |
| Catalogues de prix | Sites web (WS) : 2, groupes de clients (CG) : 6 | WS × CG = 12 enregistrements | Taille de lot de 12 ÷ (500) = 1 | (1 × 0,5 s) ÷ 60 = **&lt; 1 s** |

>[!MORELIKETHIS]
>
> - [Modules de connecteur et points d’entrée de flux](connector-reference.md) - Examinez les limites de lots et les flux pris en charge
> - [Gérer la synchronisation](../data-sync-manage.md) - Surveiller le statut de la synchronisation et déclencher des resynchronisations manuelles
> - [Pipeline de synchronisation du connecteur](../connector-sync-pipeline.md) - Découvrez le fonctionnement des plannings cron et de la synchronisation automatisée.
