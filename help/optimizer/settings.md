---
title: Paramètres
description: Configurez les paramètres de  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: 6ac223de-8e03-4842-8b67-92ce321d323d
TQID: https://experienceleague.adobe.com/9-BMXoWad0bbvsnwgHQrs19ZC9ngGrVE9J7PszcX4Zc
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 471
ht-degree: 0%

---

# Paramètres

Utilisez l’espace de travail *Paramètres* pour configurer les intervalles et les plages de facettes de prix, ainsi que la langue par défaut pour la découverte de produits.

La facettisation des prix spécifie le nombre de groupes de fourchettes de prix et la manière dont les valeurs de prix sont réparties entre eux.

Le paramètre **Language** indique [!DNL Adobe Commerce Optimizer] langue à laquelle s’attendre lors de l’écriture de l’index.

## Facettage des prix

Vous pouvez spécifier le nombre de groupes de fourchettes de prix et la manière dont les valeurs de prix sont réparties entre eux. Chaque gamme de prix chevauche le groupe précédent d&#39;une seule. Par exemple, cinq groupes avec un intervalle de 20 créent les gammes de prix suivantes : 0-20, 20-40, 40-60, 60-80 et >80. Si le catalogue ne contient pas suffisamment de produits pour remplir toutes les plages définies, l’affichage des groupes disponibles est ajusté en conséquence. Par exemple : 0-20, 60-80, >80.

1. Dans l’espace de travail **Paramètres**, sélectionnez **[!UICONTROL Search]**, puis sous **Facettisation des prix**, procédez comme suit :
   - Entrez le **nombre de sélections** ou les regroupements de prix à rendre disponibles. Jusqu&#39;à 100 regroupements de prix peuvent être définis.
   - Entrez la **valeur de l&#39;intervalle** ou la fourchette de prix pour chaque groupe. La valeur maximale est de 40 000 000.
1. Cliquez sur **Enregistrer**.

   Il faut environ 15 minutes pour que les paramètres mis à jour soient disponibles dans le storefront.

### Descriptions des champs

| Champ | Description |
|--- |--- |
| Nombre de sélections | Spécifie le nombre de regroupements de plages de prix qui peuvent être utilisés comme filtres de recherche dans le storefront. Valeur par défaut : 8, valeur maximale : 100 |
| Valeur de l’intervalle | Spécifie l&#39;intervalle de fourchette de prix pour chaque groupe. Par exemple, cinq sélections avec une valeur d’intervalle de 20 créent cinq regroupements de 0 à 20, 20 à 40, 40 à 60, 60 à 80 et >80. Valeur par défaut : 5, valeur maximale : 40 000 000 |

## Langue

Le paramètre Langue [!DNL Adobe Commerce Optimizer] indique la langue attendue lors de la lecture du catalogue et de l’écriture de l’index.

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
