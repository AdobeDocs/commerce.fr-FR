---
title: Connexion [!DNL Adobe Commerce] à [!DNL Adobe LLM Optimizer]
description: Activez les services Commerce requis, configurez la connexion LLM Optimizer, validez l’accès au catalogue et confirmez que le client est prêt avant d’examiner les opportunités ou de déployer des mises à jour.
role: Admin, User
recommendations: noCatalog
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# Connexion de [!DNL Adobe Commerce] à [!DNL Adobe LLM Optimizer]

>[!IMPORTANT]
>
>L’accès à cette intégration est restreint. Contactez votre gestionnaire de compte technique pour plus d’informations.

Cet article explique comment connecter votre catalogue [!DNL Adobe Commerce] disponible pour LLM Optimizer.

>[!NOTE]
>
>Cet article se concentre sur le côté Commerce de l’intégration. Pour obtenir des informations générales sur LLM Optimizer, consultez la documentation du produit [LLM Optimizer](https://experienceleague.adobe.com/en/docs/llm-optimizer/using/home).

## Activation des services Commerce requis {#enable-commerce-services}

Contactez votre administrateur Commerce ou votre partenaire d’implémentation pour vous assurer que :

- Les données de catalogue que LLM Optimizer doit lire sont **exportées ou synchronisées** en fonction de votre architecture (y compris tout exportateur de données SaaS ou connecteur dans votre déploiement).
- Les URL d’accès, d’identification et d’environnement de l’API (sandbox ou production) correspondent au **client** que vous avez l’intention d’utiliser dans LLM Optimizer.

## Configuration de la connexion Commerce dans LLM Optimizer {#configure-commerce-connection}

**Pour configurer la connexion Commerce, procédez comme suit**

1. Dans l’interface utilisateur de [!DNL Adobe LLM Optimizer], ouvrez **Configuration client**, puis sélectionnez l’onglet **[!UICONTROL Commerce]** .

   Configuration de ![Commerce dans l’onglet Configuration du client](../assets/llmo-commerce-config.png)

1. Cliquez sur **[!UICONTROL Add Store View]** pour créer une nouvelle ligne ou développez une entrée d’affichage de magasin existante pour la modifier.
1. Saisissez le **[!UICONTROL Store View URL]** (obligatoire).

   Utilisez l’URL du storefront pour cette vue de magasin, y compris tout paramètre régional ou préfixe de chemin d’accès (par exemple, `https://brand.example.com/` ou `https://brand.example.com/fr/`).

1. Saisissez le **[!UICONTROL Environment ID]** (obligatoire), à savoir l’identifiant de l’environnement Adobe Commerce auquel LLM Optimizer doit se connecter.
1. Saisissez **[!UICONTROL Website Code]**, **[!UICONTROL Store Code]** et **[!UICONTROL Store View Code]** (obligatoire).

   Ces valeurs doivent correspondre aux codes dans votre administrateur Commerce pour la vue de site web, de magasin et de magasin à laquelle vous vous connectez.

1. Facultatif : saisissez **[!UICONTROL Host Name]** avec le nom d’hôte de votre instance Commerce (par exemple, `www.example.com`) si cette valeur est différente de l’URL.
1. Saisissez l’**[!UICONTROL Adobe Commerce Endpoint]** : l’URL de base de votre instance Adobe Commerce utilisée pour l’accès à l’API.
1. Saisissez ou collez les **[!UICONTROL API Key]** utilisées pour authentifier les requêtes dans les API Commerce.

   Cliquez sur **[!UICONTROL Copy]** en regard du champ si vous devez copier la clé ailleurs en toute sécurité.

1. Cliquez sur **[!UICONTROL Save]** pour stocker la configuration.

Après l’enregistrement, attendez la fin de toute tâche de synchronisation ou de validation **initiale** avant de vous fier aux résultats du catalogue ou de l’audit pour cette vue de magasin.

Pour supprimer une configuration d’affichage de magasin, ouvrez cette entrée et cliquez sur **[!UICONTROL Delete]**.

### Descriptions des champs {#commerce-connection-fields}

| Champ | Description |
| --- | --- |
| URL de la vue Boutique | L’URL publique de la vue de magasin LLM Optimizer doit traiter comme dans la portée des workflows de catalogue et d’audit. |
| Identifiant de l’environnement | Identifiant de l’environnement Commerce (issu de votre documentation cloud ou de déploiement, ou Admin le cas échéant). |
| Code du site web | **[!UICONTROL Website Code]** Commerce pour le site web propriétaire du catalogue. |
| Code de magasin | **[!UICONTROL Store Code]** Commerce pour le magasin sous ce site web. |
| Code d’affichage du magasin | **[!UICONTROL Store View Code]** Commerce pour la vue du magasin (par exemple, `default`). |
| Nom d’hôte | Nom d’hôte du storefront ou de l’instance Commerce lorsque le formulaire le demande en plus d’autres URL. |
| Point d’entrée Adobe Commerce | Instance URL que LLM Optimizer utilise pour atteindre les API Commerce. |
| Clé API | Clé secrète pour l’authentification API ; traitez-la comme n’importe quelles informations d’identification de production. |

## Confirmation de la préparation du client et de l’environnement {#confirm-tenant-readiness}

- Vérifiez que les projets **sandbox** connectés ne sont pas mélangés avec les données Commerce **de production**, sauf si cela est intentionnel.
- Alignez les **rôles utilisateur** dans Experience Cloud et Commerce afin que les personnes qui approuvent les actions de déploiement disposent des autorisations appropriées des deux côtés.

## Étapes suivantes {#next-steps}

[Utilisez LLM Optimizer avec Adobe Commerce](use-llmo-with-commerce.md) pour passer en revue les opportunités, déployer les mises à jour de catalogue et comprendre le comportement de remplacement.
