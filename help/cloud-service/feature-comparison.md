---
title: Comparaison entre Adobe Commerce SaaS et PaaS
description: Comparez les modèles SaaS Adobe Commerce aux modèles PaaS afin de déterminer la meilleure approche de mise en œuvre pour les besoins de votre entreprise.
role: Developer
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 0%

---

# Comparaison des fonctionnalités

Adobe Commerce propose trois modèles de déploiement :

- [!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."} [Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) (On-premise)

Cette comparaison se concentre sur les différences entre les modèles SaaS (logiciel en tant que service) et PaaS (plateforme en tant que service), qui fournissent différents niveaux de personnalisation, d’extensibilité et de contrôle sur votre implémentation commerciale.

>[!NOTE]
>
>Le modèle local partage des fonctionnalités similaires avec le modèle PaaS. Cette comparaison s’applique donc également lorsque vous considérez les implémentations SaaS par rapport aux implémentations sur site.

## Fonctionnalités de gestion des magasins

L’interface utilisateur d’administration de [Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) est l’interface principale permettant d’accéder aux fonctionnalités de gestion des opérations de la boutique principale, des stocks, des prix, des promotions et des interactions des clients. Cependant, [!DNL Adobe Commerce as a Cloud Service] propose des solutions uniques qui remplacent certaines des fonctionnalités connues disponibles dans les projets Adobe Commerce on Cloud et on-premise.

Le tableau suivant décrit les fonctionnalités et solutions de remplacement disponibles dans [!DNL Adobe Commerce as a Cloud Service] :

<table>
    <thead>
        <tr>
            <th>Modèle PaaS [!BADGE PaaS only]{type=Informative url=https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions tooltip="S’applique aux projets Adobe Commerce sur Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-Premise uniquement."}</th>
            <th>Modèle SaaS [!BADGE SaaS only]{type=Positive url=https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."}</th>
            <th>Détails</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Gestion des ressources numériques</a></td>
            <td><a href="../aem-assets-integration/overview.md">Intégration d’AEM Assets</a></td>
            <td>Système robuste de gestion des ressources numériques (DAM) qui s’intègre à Adobe Experience Manager pour gérer le contenu multimédia. Par ailleurs, la fonctionnalité de gestion des ressources et des fichiers numériques par défaut fournit des outils de gestion des ressources de base pour le stockage et la gestion des ressources numériques.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">Système de gestion de contenu (CMS)</a></td>
            <td rowspan="3"><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront Builder</a></td>
            <td rowspan="3">Un CMS permettant aux utilisateurs de créer et de gérer facilement du contenu de storefront à l’aide de la création de documents ou d’un éditeur visuel et inclut des fonctionnalités d’expérimentation natives.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">Page Builder</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">Réécritures d’URL</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">Évaluation du contenu</a></td>
            <td rowspan="2"><a href="../catalog-service/overview.md">Service de catalogue</a></td>
            <td rowspan="2">Service de modèle d’affichage enrichi (lecture seule) pour la gestion des données de catalogue et le rendu des expériences storefront liées aux produits.</td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Marchandiseur visuel</a></td>
        </tr>
        <tr>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">Paiements</a></td>
            <td><a href="../payment-services/guide-overview.md">Services de paiement</a></td>
            <td>Un service de paiement intégré qui facilite les transactions sécurisées et efficaces.</td>
        </tr>
    </tbody>
</table>

## Fonctionnalités d’extensibilité et de plateforme

Le tableau suivant compare les fonctionnalités de la plateforme et les fonctionnalités d’extensibilité afin de vous aider à comprendre les différences et à prendre une décision éclairée concernant le modèle qui répond le mieux aux besoins de votre entreprise avant de démarrer une implémentation.

<table>
    <thead>
        <tr>
            <th>Fonctionnalité</th>
            <th>Modèle PaaS [!BADGE PaaS only]{type=Informative url=https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions tooltip="S’applique aux projets Adobe Commerce sur Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-Premise uniquement."}</th>
            <th>Modèle SaaS [!BADGE SaaS only]{type=Positive url=https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Fonctionnalités de Platform</strong></td>
        </tr>
        <tr>
            <td>Fonctionnalité B2B</td>
            <td>Fonctionnalités B2B complètes disponibles après l’installation</td>
            <td>Préinstallé avec les principales fonctionnalités B2B <sup>1</sup></td>
        </tr>
        <tr>
            <td>Expérimentation</td>
            <td>Module complémentaire pour certains niveaux</td>
            <td>Tests AB pour optimiser l’engagement et la conversion</td>
        </tr>
        <tr>
            <td>Mises à jour des fonctionnalités et de la sécurité</td>
            <td>Nécessite une mise à niveau et un correctif manuels</td>
            <td>Déploiement automatique</td>
        </tr>
        <tr>
            <td>Infrastructure d'accueil</td>
            <td>À locataire unique</td>
            <td>Multi-tenant</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Personnalisation de Commerce Admin</strong></td>
        </tr>
        <tr>
            <td>Écrans d’administration principaux extensibles</td>
            <td>Personnalisation complète de la disposition et des fonctionnalités</td>
            <td>Filtres prédéfinis, contrôles de visibilité</td>
        </tr>
        <tr>
            <td>Nouveaux écrans d’administration extensibles</td>
            <td>Intégration de l’interface utilisateur d’administration standard et injection d’application externe (Admin UI SDK)</td>
            <td>Injection dans une application externe (Admin UI SDK)</td>
        </tr>
        <tr>
            <td>Thème d’administration personnalisable</td>
            <td>Framework de thème extensible</td>
            <td>Aucun framework de thème</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Extensibilité</strong></td>
        </tr>
        <tr>
            <td>Modèle d’extensibilité</td>
            <td>En cours (personnalisation PHP) et hors processus (API, événements, App Builder)</td>
            <td>Hors-processus uniquement (API, événements, App Builder)</td>
        </tr>
        <tr>
            <td>API web extensibles</td>
            <td>Extensibilité REST/GraphQL native et maillage API avec résolveurs personnalisés</td>
            <td>Maillage API avec résolveurs personnalisés</td>
        </tr>
        <tr>
            <td>Extensibilité du modèle de données</td>
            <td>Personnalisation complète du modèle de données</td>
            <td>Attributs personnalisés pour les entités principales et B2B<sup>2</sup></td>
        </tr>
        <tr>
            <td>Technologies</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, INTERFACE DE LIGNE DE COMMANDE, HTML, JS, nœud</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Données et stockage</strong></td>
        </tr>
        <tr>
            <td>Personnalisations des index de recherche</td>
            <td>Personnalisation native de la recherche</td>
            <td>Nécessite des solutions tierces</td>
        </tr>
        <tr>
            <td>Types d’e-mails personnalisés</td>
            <td>Personnalisation complète des e-mails</td>
            <td>Modèles d’e-mail standard uniquement</td>
        </tr>
        <tr>
            <td>Stockage de données personnalisé</td>
            <td>Base de données, fichier, cache, file d'attente</td>
            <td>Bibliothèque d’état App Builder (fichier uniquement)<sup>3</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> les fonctionnalités principales <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B</a> telles que la gestion d'entreprise et les devis, sont disponibles prêtes à l'emploi dans SaaS. Toutefois, les personnalisations spécifiques au secteur peuvent nécessiter des considérations d’implémentation supplémentaires.
                <br><br>
                <sup>2</sup> L’extensibilité du modèle de données en SaaS prend en charge <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">l’extension des entités principales</a> au-delà du produit et du client, y compris les entités B2B. Cependant, les modèles de données spécifiques au secteur (par exemple, les attributs spécifiques aux revendeurs) peuvent nécessiter des considérations architecturales supplémentaires.
                <br><br>
                <sup>3</sup> Adobe travaille activement à l’intégration de la base de données Document pour répondre aux besoins de stockage persistant pour SaaS. Actuellement, les implémentations nécessitant un stockage de données à long terme peuvent avoir besoin de configurer et de gérer des infrastructures supplémentaires.
            </td>
        </tr>
    </tfoot>
</table>

>[!NOTE]
>
>Lorsque vous envisagez une migration vers SaaS, Adobe vous recommande de :
>
>- Dans la mesure du possible, déplacez les fonctionnalités appropriées vers l’extensibilité hors processus.
>- Réduisez la surface nécessitant une transition.
>- Tenez compte du maillage API pour étendre les fonctionnalités de l’API.
>- Surveillez l’évolution continue de la plateforme Adobe et les nouvelles versions de fonctionnalités.
>- Évaluez les exigences des modèles de données spécifiques au secteur par rapport aux options d’extensibilité disponibles.
>- Envisagez d’adopter des [services de marchandisage optimisés par des vues et des politiques de catalogue](../optimizer/setup/catalog-view.md).
