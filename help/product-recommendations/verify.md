---
title: Vérifier la collecte des événements
description: Découvrez comment vérifier que les données comportementales sont envoyées à Adobe Commerce.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# Vérifier la collecte des événements

Après avoir [installé et configuré](install-configure.md) le module `magento/product-recommendations`, vous pouvez vérifier que les données comportementales sont envoyées à Adobe Commerce. Vous pouvez utiliser les outils de développement disponibles dans Chrome ou installer l’extension Snowplow Chrome. Si vous avez besoin d’aide supplémentaire, reportez-vous à la section [Dépannage [!DNL Product Recommendations] module](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/troubleshoot-product-recommendations-module-in-magento-commerce.html?lang=fr) de la base de connaissances du support.

## Vérification à l’aide des outils de développement dans Chrome

Pour vous assurer que le fichier JS du collecteur d’événements se charge sur toutes les pages du site :

1. Dans Chrome, choisissez **Personnaliser et contrôler Google Chrome** puis sélectionnez **Plus d’outils** > **Outils de développement**.
1. Sélectionnez l’onglet **Network** puis sélectionnez le type **JS**.
1. Filtrer par `ds.`
1. Rechargez la page.
1. Vous devriez voir `ds.js` ou `ds.min.js` dans la colonne **Nom**.

![JS du collecteur d’événements](assets/filter-ds.png)
_JS du collecteur d’événements_

Pour vous assurer que les événements se déclenchent sur les pages de votre site (accueil, produit, passage en caisse, etc.) :

1. Assurez-vous de désactiver tous les bloqueurs de publicités sur votre navigateur et d&#39;accepter les cookies sur le site.
1. Dans Chrome, choisissez **Personnaliser et contrôler Google Chrome** (les trois points verticaux dans le coin supérieur droit du navigateur), puis sélectionnez **Plus d’outils** > **Outils de développement**.
1. Sélectionnez l’onglet **Réseau** et filtrez les `tp2`.
1. Rechargez la page.
1. Vous devriez voir les appels sous `tp2` dans la colonne **Nom**.

![ Déclenchement d’événements ](assets/filter-tp2.png)
_Vérifier que les événements se déclenchent_

## Vérifier à l’aide de l’extension Snowplow Chrome

Installez l’extension [Snowplow Analytics Debugger pour Chrome](https://chrome.google.com/webstore/detail/snowplow-analytics-debugg/jbnlcgeengmijcghameodeaenefieedm). Cette extension affiche les événements collectés et envoyés à Adobe Commerce.

1. Assurez-vous de désactiver tous les bloqueurs de publicités sur votre navigateur et d&#39;accepter les cookies sur le site.

1. Dans Chrome, choisissez **Personnaliser et contrôler Google Chrome** (les trois points verticaux dans le coin supérieur droit du navigateur), puis sélectionnez **Plus d’outils** > **Outils de développement**.

1. Sélectionnez l’onglet **Débogueur d’analyse Snowplow**.

1. Dans la colonne **Événement**, sélectionnez **Événement structuré**.

1. Faites défiler jusqu’à afficher **Données contextuelles _n_**. Recherchez l’instance storefront dans le **schéma**.

1. Vérifiez que l&#39;identifiant de l&#39;espace de données [SaaS](https://experienceleague.adobe.com/docs/commerce-admin/config/services/saas.html?lang=fr) est correctement défini.

![Filtre Snowplow](assets/snowplow-filter.png)
_Filtre Snowplow_

>[!NOTE]
>
> Une valeur `Data validity : NOT FOUND` dans le débogueur indique un schéma interne. Le plug-in Snowplow Chrome ne peut pas valider les événements avec un schéma interne. Cela n’a aucun impact sur les fonctionnalités réelles.

## Vérifier que les événements se déclenchent correctement

Pour vérifier que les événements utilisés pour les mesures se déclenchent correctement, recherchez les événements `impression-render`, `view` et `rec-click` dans le débogueur Snowplow Analytics. Voir la [liste complète des événements](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/events.html?lang=fr).

>[!NOTE]
>
> Si le [Mode de restriction des cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=fr) est activé, Adobe Commerce ne collecte pas de données comportementales tant que l’acheteur n’a pas donné son consentement. Si le Mode de restriction des cookies est désactivé, les données comportementales sont collectées par défaut.
