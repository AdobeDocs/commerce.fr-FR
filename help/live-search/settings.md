---
title: Paramètres
description: Configurez la recherche sémantique, les plages de facettes de prix et la langue d’indexation par défaut pour le  [!DNL Live Search] .
exl-id: 6387a365-7e23-4023-95ac-27908164d81c
TQID: https://experienceleague.adobe.com/Dn4x8Boo-1F5RQgMXVx6Dpt7iYWFIlqOlO5QwhJrjVU
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
source-git-commit: 015f88e540fe5bf7acc4469d7c91b4f606709809
workflow-type: tm+mt
source-wordcount: 650
ht-degree: 1%

---

# Paramètres

Utilisez l’espace de travail **Paramètres** pour configurer la recherche sémantique, les intervalles et les plages de facettes de prix, ainsi que la langue par défaut de l’index.

![Paramètres](assets/settings.png)

## Recherche sémantique {#semantic-search}

La recherche sémantique utilise l’IA pour faire correspondre des produits en fonction du sens et du contexte, et pas seulement des mots-clés exacts. Lorsque **[!UICONTROL Semantic search]** est activé, les acheteurs qui utilisent un langage naturel ou un libellé qui ne correspond pas mot pour mot à votre catalogue peuvent toujours trouver des produits appropriés. [!DNL Live Search] offre une correspondance sémantique et de mots-clés dans une expérience de recherche unifiée sur le storefront. La recherche sémantique fonctionne avec votre configuration existante ; les [règles de recherche](rules.md), [synonymes](synonyms.md), [facettes](facets.md), boots et [marchandisage de catégorie](category-merch.md) continuent de s’appliquer.

**Pour activer la recherche sémantique (PaaS uniquement) :**

1. Dans Admin, accédez à **Marketing** > *SEO et recherche* > **[!DNL Live Search]**.
1. Dans l’espace de travail **Paramètres**, activez **[!UICONTROL Semantic search]**.

   Lorsqu’elle est activée, la recherche correspond aux produits en fonction de leur signification et de leur contexte, ce qui se traduit par des résultats plus pertinents, moins de recherches à résultat nul et une conversion améliorée.

1. Cliquez sur **[!UICONTROL Save]**.

   Les résultats de recherche sont mis à jour une fois l’indexation terminée. Pour un catalogue de taille moyenne, l’indexation peut prendre jusqu’à une demi-heure. Pour les catalogues volumineux contenant des millions de produits, cela peut prendre quelques heures.

>[!NOTE]
>
> La recherche sémantique est disponible uniquement pour les catalogues **anglais**. Si vous définissez **Langue** sur un catalogue non anglophone (voir [Langue](#language)), **[!UICONTROL Semantic search]** est automatiquement désactivé.

Pour en savoir plus sur les avantages, les conseils de validation, les bonnes pratiques, le dépannage et les limites, voir [Recherche sémantique](semantic-search.md).

### Descriptions des champs

| Champ | Description |
| --- | --- |
| Recherche sémantique | Lorsqu’elle est activée, [!DNL Live Search] utilise la signification et le contexte ainsi que la correspondance des mots-clés. Les attributs de catalogue prédéfinis sont utilisés automatiquement ; aucune configuration d’attribut n’est requise dans l’administration. Activé par défaut pour [!DNL Adobe Commerce as a Cloud Service] ; les commerçants PaaS l’activent manuellement. |

## Facettage des prix {#price-faceting}

Vous pouvez spécifier le nombre de groupes de fourchettes de prix et la manière dont les valeurs de prix sont réparties entre eux. Chaque gamme de prix chevauche le groupe précédent d&#39;une seule. Par exemple, cinq groupes avec un intervalle de 20 créent les gammes de prix suivantes : 0-20, 20-40, 40-60, 60-80 et >80. Si le catalogue ne contient pas suffisamment de produits pour remplir toutes les plages définies, l’affichage des groupes disponibles est ajusté en conséquence. Par exemple : 0-20, 60-80, >80.

**Pour configurer la facettisation des prix, procédez comme suit**

1. Dans Admin, accédez à **Marketing** > *SEO et recherche* > **[!DNL Live Search]**.
1. Dans l’espace de travail **Paramètres** sous *Facettisation des prix*, procédez comme suit :
   * Entrez le **nombre de sélections** ou les regroupements de prix à rendre disponibles. Avec [!DNL Live Search] 4.4.0, vous pouvez définir jusqu’à 100 regroupements de prix. Les versions antérieures autorisaient 50 regroupements de prix.
   * Entrez la **valeur de l&#39;intervalle** ou la fourchette de prix pour chaque groupe. La valeur maximale est de 40 000 000.
1. Cliquez sur **[!UICONTROL Save]**.

   Il faut environ 15 minutes pour que les paramètres mis à jour soient disponibles dans le storefront.

### Descriptions des champs

| Champ | Description |
|--- |--- |
| Nombre de sélections | Spécifie le nombre de regroupements de plages de prix qui peuvent être utilisés comme filtres de recherche dans le storefront. Valeur par défaut : 8, Valeur maximale : 100 (à partir de la [!DNL Live Search] 4.4.0) |
| Valeur de l’intervalle | Spécifie l&#39;intervalle de fourchette de prix pour chaque groupe. Par exemple, cinq sélections avec une valeur d’intervalle de 20 créent cinq regroupements de 0 à 20, 20 à 40, 40 à 60, 60 à 80 et >80. Valeur par défaut : 5, valeur maximale : 40 000 000 |

## Langue {#language}

Le paramètre Langue [!DNL Live Search] indique la langue attendue lors de la lecture du catalogue et de l’écriture de l’index.

Les langues ont différents ensembles de règles grammaticales : la façon dont les mots sont séparés, les verbes et les formes de mots, par exemple.
Le paramètre Langue garantit que l’ensemble correct de règles est appliqué au mécanisme d’indexation.

Définissez le paramètre Langue sur la langue principale du catalogue. Lors du changement de la langue de l’index, il peut s’écouler de 5 à 60 minutes pour refléter le changement sur le storefront, en fonction de la taille et de la complexité du catalogue.

| Langue | Code |
|----|----|
| Arabe | ar |
| Arménien | hy |
| Basque | ue |
| Bengali | bn |
| Brésilien | pt-br |
| Bulgare | bg |
| Catalan | ca |
| Chinois (simplifié) | zh-cn |
| Chinois (traditionnel) | zh-tw |
| Tchèque | cs |
| Danois | jour |
| Néerlandais | nl |
| Anglais | fr |
| Estonien | et |
| Finlandais | fi |
| Français | fr |
| Galicien | gl |
| Allemand | de |
| Grec | el |
| Hindi | bonjour |
| Hongrois | hu |
| Indonésien | id |
| Irlandais | ga |
| Italien | it |
| Japonais (Katakana) | ja |
| Coréen | ko |
| Letton | lv |
| Lituanien | lt |
| Norvégien | non |
| Perse | fa |
| Portugais | pt |
| Roumain | ro |
| Russe | ru |
| Sorani | ku |
| Espagnol | es |
| Suédois | sv |
| Turc | tr |
| Thaïlandais | ème |
