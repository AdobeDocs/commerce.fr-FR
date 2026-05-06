---
title: Utiliser  [!DNL Adobe LLM Optimizer]  avec  [!DNL Adobe Commerce]
description: Parcourez les opportunités Commerce dans LLM Optimizer, examinez le PDP et l’enrichissement du catalogue, déployez les mises à jour sur  [!DNL Adobe Commerce], vérifiez dans l’administration et le storefront, et découvrez comment les remplacements et l’ingestion marquent les opportunités comme obsolètes.
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '1175'
ht-degree: 0%

---

# Utilisation de [!DNL Adobe LLM Optimizer] avec [!DNL Adobe Commerce]

>[!IMPORTANT]
>
>L’accès à cette intégration est restreint. Contactez votre gestionnaire de compte technique pour plus d’informations.

Après avoir [connecté Commerce à LLM Optimizer](connect-to-llmo.md), vous travaillez principalement dans l’interface utilisateur **[!DNL Adobe LLM Optimizer]** pour examiner les opportunités et intégrer les modifications approuvées dans le catalogue lorsque vous êtes prêt(e). Cet article décrit les deux types d’optimisation axés sur Commerce, l’utilisation de **[!UICONTROL Opportunities]**, le comportement des actions de déploiement dans [!DNL Adobe Commerce] et la manière dont les mises à jour externes interagissent avec les suggestions de LLM Optimizer. Pour une vue d’ensemble de l’intégration, consultez la [présentation de l’intégration](../overview.md).

## Présentation des optimisations de Commerce dans LLM Optimizer {#understand-optimizations}

Pour les catalogues pris en charge par Commerce, LLM Optimizer propose des **[!UICONTROL Product Detail Page Enrichment]** et des **[!UICONTROL Product Catalog Enrichment]**.

| Focus | À quoi cela sert-il ? |
| --- | --- |
| **[!UICONTROL Product Detail Page Enrichment]** (enrichissement PDP) | Suggestions qui améliorent la lecture d’une page produit pour une découverte pilotée par l’IA, sans remplacer votre disposition de storefront. |
| **[!UICONTROL Product Catalog Enrichment]** | Suggestions de mises à jour **nom du produit** et **description du produit** pour des produits spécifiques que vous pouvez consulter, modifier si nécessaire et appliquer à votre catalogue Commerce. |

Utilisez **[!UICONTROL Opportunities]** pour ouvrir la liste des produits ou des URL et parcourir les suggestions pour le type que vous avez sélectionné.

## Navigation dans les opportunités Commerce {#navigate-commerce-opportunities}

**Pour ouvrir des opportunités liées à Commerce, procédez comme suit**

1. Dans le rail de gauche, cliquez sur **[!UICONTROL Opportunities]**.
1. Cliquez sur **[!UICONTROL Commerce Opportunity]** pour afficher les types d’optimisation qui ciblent votre catalogue [!DNL Adobe Commerce].
1. Sélectionnez **[!UICONTROL Product Catalog Enrichment]** ou **[!UICONTROL Product Detail Page Enrichment]**, selon ce sur quoi vous souhaitez travailler.

![types de filtrage et d’optimisation des opportunités ](../assets/llmo-opportunities.png)

### Présentation des mesures d’opportunité {#opportunity-metrics}

Chaque vue d’opportunité résume l’impact afin que vous puissiez hiérarchiser le travail :

- **Pages de produits** ou **URL** : pages ou produits évalués pour ce type d’optimisation.
- **Trafic des agents** : visites et interactions lancées par des agents d’IA qui peuvent vous aider à hiérarchiser les opportunités à fort impact en premier.

### Comprendre les états des suggestions {#suggestion-states}

Les deux types d’enrichissement utilisent les mêmes vues de workflow :

- **[!UICONTROL Current Suggestions]** : éléments nouveaux ou actifs à vérifier.
- **[!UICONTROL Fixed Suggestions]** : éléments déjà déployés ou résolus.
- **[!UICONTROL Ignored Suggestions]** : éléments que vous avez intentionnellement exclus de l’action.

### Examen et déploiement de l’enrichissement PDP {#review-deploy-pdp}

L’enrichissement du PDP est destiné aux équipes qui souhaitent des messages de page produit plus clairs dans le cadre d’une découverte pilotée par l’IA, tout en conservant l’expérience storefront conçue par vos marchandiseurs.

**Pour vérifier et déployer l’enrichissement PDP, procédez comme suit**

1. Ouvrez **[!UICONTROL Product Detail Page Enrichment]** à partir de **[!UICONTROL Opportunities]**.
1. Dans le tableau **[!UICONTROL URLs with Suggestions]**, sélectionnez **[!UICONTROL Current Suggestions]**.
1. Pour une URL ou un SKU, cliquez sur **[!UICONTROL Preview]** pour passer en revue l’analyse d’IA et l’enrichissement proposé.
1. Facultatif : cliquez sur **[!UICONTROL Copy]** pour coller le contenu dans un éditeur externe ou cliquez sur **[!UICONTROL Edit suggestion]** pour le modifier sur place.
1. Facultatif : si une suggestion ne correspond pas à votre stratégie, déplacez-la vers **[!UICONTROL Ignored Suggestions]**.
1. Une fois la révision et l’approbation effectuées, sélectionnez la ligne de l’URL ou du SKU à mettre à jour, puis cliquez sur **[!UICONTROL Deploy optimizations]** et confirmez.

Après le déploiement, les suggestions sont transférées vers **[!UICONTROL Fixed Suggestions]** avec un statut d’optimisation dans LLM Optimizer.

>[!NOTE]
>
>Le déploiement de l’enrichissement PDP nécessite l’intégration terminée **Optimisation sur Edge** dans LLM Optimizer. Si l’intégration est incomplète, l’interface utilisateur vous invite à terminer la configuration avant le déploiement.

### Examen et déploiement de l’enrichissement du catalogue de produits {#review-deploy-catalog}

L’enrichissement du catalogue s’adresse aux équipes qui souhaitent renforcer les noms de produits et les descriptions longues directement dans Commerce, avec des suggestions que vous pouvez examiner avant d’enregistrer quoi que ce soit.

**Pour vérifier et déployer l’enrichissement du catalogue de produits :**

1. Ouvrez **[!UICONTROL Product Catalog Enrichment]** à partir de **[!UICONTROL Opportunities]**.
1. Dans le tableau **[!UICONTROL URLs with Suggestions]**, sélectionnez **[!UICONTROL Current Suggestions]**.
1. Cliquez sur le contrôle de développement de la ligne URL ou SKU pour afficher les mises à jour proposées **Nom du produit** et **Description du produit**.
1. Facultatif : cliquez sur l’icône de modification pour ajuster le nom ou la description proposés avant le déploiement.
1. Facultatif : si une suggestion ne correspond pas à votre stratégie, déplacez-la vers **[!UICONTROL Ignored Suggestions]**.
1. Une fois la révision et l’approbation effectuées, sélectionnez la ligne de l’URL ou du SKU à mettre à jour, puis cliquez sur **[!UICONTROL Deploy optimizations]** et confirmez.

Les modifications de nom et de description approuvées sont enregistrées dans votre catalogue [!DNL Adobe Commerce] comme les autres mises à jour de produits.

>[!IMPORTANT]
>
>Traiter le déploiement comme une modification du catalogue de production. Utilisez vos pratiques normales de contrôle des modifications, d’évaluation et d’assurance qualité. Déployez uniquement après que les parties prenantes du merchandising et du SEO se sont mises d’accord sur la copie finale.

Après le déploiement, les suggestions sont déplacées vers les **[!UICONTROL Fixed Suggestions]** avec un statut **Appliqué**.

## Vérifier les mises à jour dans l’administrateur Commerce {#verify-in-admin}

**Pour vérifier l’enrichissement du catalogue déployé :**

1. Connectez-vous à l’[!DNL Adobe Commerce] **Admin**.
1. Accédez à **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.
1. Utilisez les filtres et le sélecteur **vue du magasin** selon les besoins (par exemple, **[!UICONTROL Default Store View]**), puis recherchez le **SKU**.
1. Ouvrez le produit en mode d’édition.

   Le formulaire de produit affiche le **nom du produit** enrichi.

   ![Champ du nom du produit après l’enrichissement du LLM Optimizer](../assets/llmo-admin-name.png)

1. Facultatif : sélectionnez **[!UICONTROL Override LLM Optimizer provided Product Name]** si vous souhaitez conserver un nom saisi manuellement à la place.

Les remplacements manuels affectent la manière dont les opportunités restent synchronisées avec le catalogue. Voir [Remplacement manuel dans l’administrateur](#manual-override-in-the-admin).

1. Développez la section **[!UICONTROL Content]** et recherchez le champ **description**.

   La description enrichie s’affiche lorsque vous avez déployé des modifications de description.

   ![Champ Description après l’enrichissement du LLM Optimizer](../assets/llmo-admin-description.png)

1. Facultatif : sélectionnez **[!UICONTROL Override LLM Optimizer provided Description]** si vous souhaitez conserver une description saisie manuellement à la place.

## Vérifier les mises à jour sur le storefront {#verify-storefront}

Recherchez le SKU sur votre storefront et ouvrez le PDP. Vérifiez que le **nom** et toutes les régions qui font surface à la longue **description** reflètent ce que vous avez approuvé. Confirmez également tous les canaux en aval qui consomment les mêmes attributs de catalogue, le cas échéant en fonction de votre déploiement.

<!--
## PDP enrichment rollback {#pdp-rollback}

If your project includes PDP enrichment opportunities, **rollback** behavior may support **bulk** or **per-URL** actions, depending on your LLM Optimizer release. Follow the in-product options for rollback. For **[!UICONTROL Product Catalog Enrichment]**, undoing a name or description in Commerce is effectively a new catalog edit or a follow-up opportunity, not a separate undo control in the Admin unless your team implements one.
-->

## Remplacements, ingestion et opportunités obsolètes {#overrides-ingestion}

Après la mise à jour du nom ou de la description d’un produit par LLM Optimizer, d’autres systèmes d’ingestion, tels que les appels API REST, les importations CSV, les flux PIM ou des processus similaires, peuvent modifier les mêmes champs. Les sections suivantes décrivent ce qui se passe dans ce cas.

### L’ingestion renvoie la valeur de catalogue d’origine

Si un processus externe écrit le nom ou la description d’origine (la valeur qui existait avant le déploiement de LLM Optimizer), Commerce continue à honorer la valeur déployée par LLM Optimizer pour ce champ en fonction des règles d’intégration. L’opportunité peut ne pas être rétablie automatiquement en fonction de cette seule ingestion.

### L’ingestion envoie une nouvelle valeur

Si le processus externe envoie une nouvelle valeur qui n’est pas simplement une répétition du texte antérieur à LLM Optimizer (par exemple, renommer « Red Shoes » en « Iconic Red Shoes »), cette nouvelle valeur de catalogue est honorée et l’opportunité LLM Optimizer associée est généralement marquée comme *Obsolète* dans LLM Optimizer, car le catalogue en direct ne correspond plus au contexte de suggestion.

### Remplacement manuel dans l’administrateur {#manual-override-in-the-admin}

Si vous modifiez manuellement le nom ou la description du produit dans l’[!DNL Adobe Commerce] *Admin* :

- La valeur *Admin* est sélectionnée en tant que système d’enregistrement pour cette modification manuelle.
- L’opportunité LLM Optimizer est marquée *obsolète*.
- Dans LLM Optimizer, l’interface utilisateur revient à l’état d’origine de cette opportunité afin que vous puissiez réorganiser ou accepter une nouvelle suggestion si l’analyse s’exécute à nouveau.

Ces règles vous aident à savoir si LLM Optimizer, les flux d’ingestion ou les modifications *Admin* font autorité lorsque plusieurs canaux touchent le même SKU.

## Bonnes pratiques

- **Documenter la propriété du système** pour le nom et la description du produit afin que les tâches PIM ou de flux ne soient pas involontairement en conflit avec les attentes de LLM Optimizer.
- **Coordonnez-vous avec les équipes SEO et de marque** avant de déployer des titres ou des descriptions en masse.
- **resynchroniser** ou **analyser** après des importations de catalogue majeures afin que les opportunités reflètent l’état actuel du catalogue.

## Faites un essai dans la démonstration

Utilisez l’environnement de démonstration Frescopa pour voir les deux types d’opportunités Commerce en action :

- [Afficher la démonstration de l’enrichissement du catalogue de produits](https://play.llmo.now/org/demo-org/opportunities/commerce-product-catalog-enrichment/e5f2a854-7477-421c-820f-74d5dd595647?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)
- [Démonstration de l’enrichissement de la page des détails du produit](https://play.llmo.now/org/demo-org/opportunities/commerce-product-page-enrichment/4e8b0428-0893-4864-a00e-fc1d77fb3372?siteId=9ae8877a-bbf3-407d-9adb-d6a72ce3c5e3)

## Rubriques connexes

- [Connexion d’Adobe Commerce à LLM Optimizer](connect-to-llmo.md)
- [Présentation de l’intégration](../overview.md)
- [Limites et limites de l’intégration](../boundaries-limits.md)
