---
title: Comparaison entre Adobe Commerce SaaS et PaaS
description: Comparez les modèles SaaS Adobe Commerce aux modèles PaaS afin de déterminer la meilleure approche de mise en œuvre pour les besoins de votre entreprise.
feature: App Builder, GraphQL, Integration, Saas
role: Developer, Admin, Leader
level: Intermediate
exl-id: c8c9a0b4-f47c-46ec-bc9d-39dee9641f59
source-git-commit: e8e0c9f6a14232abc1332b48df7ae8bc3b955900
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 0%

---

# Comparaison des fonctionnalités

Adobe Commerce propose trois modèles de déploiement :

- [!BADGE SaaS uniquement]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."} [Adobe Commerce as a Cloud Service](overview.md) (SaaS)
- [!BADGE PaaS uniquement]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."} [Adobe Commerce on Cloud](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/overview) (PaaS)
- [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/overview) (On-premise)

Cette comparaison se concentre sur les différences entre les modèles SaaS (logiciel en tant que service) et PaaS (plateforme en tant que service). Ces modèles fournissent différents niveaux de personnalisation, d’extensibilité et de contrôle sur votre mise en œuvre Commerce.

>[!NOTE]
>
>Le modèle local partage des fonctionnalités similaires avec le modèle PaaS. Cette comparaison s’applique donc également lorsque vous considérez les implémentations SaaS par rapport aux implémentations sur site.

## Fonctionnalités de gestion des magasins

L’interface utilisateur d’administration de [Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/guide-overview) est l’interface principale permettant d’accéder aux fonctionnalités de gestion des opérations de la boutique principale, des stocks, des prix, des promotions et des interactions des clients. Cependant, [!DNL Adobe Commerce as a Cloud Service] propose des solutions uniques qui remplacent certaines des fonctionnalités connues disponibles dans les projets [!DNL Adobe Commerce on Cloud] et sur site.

Le tableau suivant décrit les fonctionnalités et solutions de remplacement disponibles dans [!DNL Adobe Commerce as a Cloud Service] :

<table>
    <thead>
        <tr>
            <th>Fonctionnalité</th>
            <th>Modèle PaaS [!BADGE PaaS only]{type=Informative url= »https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions » tooltip=« S’applique aux projets Adobe Commerce sur Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-Premise uniquement. »}</th>
            <th>Modèle SaaS [!BADGE SaaS only]{type=Positive url= »https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions » tooltip=« S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe). »}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>Gestion des ressources numériques</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/wysiwyg/gallery/media-gallery-asset-management">Galerie de médias</a></td>
            <td><a href="../aem-assets-integration/overview.md">Visuels du produit</a></td>
        </tr>
        <tr>
            <td>Gestion de contenu</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/guide-overview">Content Management System (CMS)</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/guide-overview">Page Builder</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/seo/url-rewrites/url-rewrite">réécritures d’URL</a></td>
            <td><a href="https://experienceleague.adobe.com/developer/commerce/storefront/merchants/get-started/">Storefront Builder</a></td>
        </tr>
        <tr>
            <td>Marchandisage des catalogues</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/content-design/staging/content-staging">Évaluation de contenu</a>, <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/merchandising/visual-merch/visual-merchandiser">Marchandiseur visuel</a></td>
            <td><a href="../catalog-service/overview.md">Service de catalogue</a></td>
        </tr>
        <tr>
            <td>Paiements</td>
            <td><a href="https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/payments/payments">Solutions de paiement</a></td>
            <td><a href="../payment-services/guide-overview.md">Services de paiement</a></td>
        </tr>
        <tr>
            <td>Fonctionnalité B2B</td>
            <td>Fonctionnalités B2B complètes disponibles après l’installation</td>
            <td>Préinstallé avec les principales fonctionnalités B2B <sup>1</sup></td>
        </tr>
        <tr>
            <td>Expérimentation</td>
            <td>Module complémentaire pour certains niveaux</td>
            <td>Tests AB natifs pour optimiser l’engagement et la conversion</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> les fonctionnalités principales <a href="https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/guide-overview">B2B</a> telles que la gestion d'entreprise et les devis, sont disponibles prêtes à l'emploi dans SaaS. Toutefois, les personnalisations spécifiques au secteur peuvent nécessiter des considérations d’implémentation supplémentaires.
            </td>
        </tr>
    </tfoot>
</table>

## Fonctionnalités d’extensibilité et de plateforme

Le tableau suivant compare les fonctionnalités de la plateforme et les fonctionnalités d’extensibilité afin de vous aider à comprendre les différences et à décider quel modèle convient le mieux aux besoins de votre entreprise avant de démarrer une implémentation.

<table>
    <thead>
        <tr>
            <th>Fonctionnalité</th>
            <th>Modèle PaaS [!BADGE PaaS only]{type=Informative url= »https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions » tooltip=« S’applique aux projets Adobe Commerce sur Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-Premise uniquement. »}</th>
            <th>Modèle SaaS [!BADGE SaaS only]{type=Positive url= »https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions » tooltip=« S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe). »}</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Fonctionnalités de Platform</strong></td>
        </tr>
        <tr>
            <td>Mises à jour des fonctionnalités et de la sécurité</td>
            <td>Nécessite une mise à niveau manuelle et l’application de correctifs. Six versions de correctifs et une version mineure par an.</td>
            <td>Mise à niveau automatique par Adobe via un modèle SaaS sans version</td>
        </tr>
        <tr>
            <td>Infrastructure d'accueil</td>
            <td>À locataire unique</td>
            <td>Multi-tenant</td>
        </tr>
        <tr>
            <td>Performances et évolutivité</td>
            <td>Mise à l’échelle automatique horizontale pour une architecture mise à l’échelle. Mise à l’échelle automatique verticale pour le niveau web en cours de déploiement en accès anticipé pour tous les commerçants, y compris l’architecture non mise à l’échelle.</td>
            <td>Application native cloud à plusieurs clients avec mise à l’échelle automatique complète sur la pile</td>
        </tr>
        <tr>
            <td>Observability</td>
            <td>[!DNL New Relic] accès permettant aux clients de surveiller et de gérer l’environnement</td>
            <td>Adobe géré. Les clients peuvent utiliser [!DNL OpenTelemetry] pour les applications [!DNL App Builder] et les tableaux de bord RUM pour storefront. [!DNL New Relic] licence non incluse. Les clients peuvent configurer [!DNL API Mesh] et [!DNL App Builder] pour envoyer des données à leur propre compte [!DNL New Relic].</td>
        </tr>
        <tr>
            <td>CDN</td>
            <td>[!DNL Fastly] compris</td>
            <td>Réseau CDN Edge entièrement géré associé étroitement à Commerce Storefront. BYO-CDN est également pris en charge.</td>
        </tr>
        <tr>
            <td>Sécurité et conformité</td>
            <td>SOC2, PCI, certifications ISO par fournisseur d'hébergement, HIPAA</td>
            <td>SOC2, PCI, ISO, RGPD. HIPAA n’est actuellement pas disponible.</td>
        </tr>
        <tr>
            <td>Reprise après sinistre et contrats de niveau de service</td>
            <td>99,99 % de l’infrastructure, 99,9 % de l’application (Managed Services)</td>
            <td>99,9 % (infrastructure et application), RPO/RTO plus rapides</td>
        </tr>
        <tr>
            <td>Régions d'accueil</td>
            <td>Azure (24 emplacements), AWS (22 emplacements), GCP (8 emplacements, non standard)</td>
            <td>Disponible dans le monde entier. Pour plus d’informations sur les environnements de production de votre région, contactez votre représentant du service client. Emplacements supplémentaires déployés selon la demande.</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Personnalisation de Commerce Admin</strong></td>
        </tr>
        <tr>
            <td>Extensibilité d’Admin Console</td>
            <td>Personnalisation et thème PHP, extensibilité App Builder (recommandé)</td>
            <td>Extensibilité d’App Builder</td>
        </tr>
        <tr>
            <td colspan="3" style="background:lightgray;"><strong>Extensibilité</strong></td>
        </tr>
        <tr>
            <td>Modèle d’extensibilité</td>
            <td>En cours (personnalisation PHP) et hors processus (Recommandé : API, événements, App Builder)</td>
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
            <td>Attributs personnalisés pour les entités principales et B2B<sup>1</sup></td>
        </tr>
        <tr>
            <td>Technologies</td>
            <td>CSS, CLI, HTML, JS, PHP, XML</td>
            <td>CSS, INTERFACE DE LIGNE DE COMMANDE, HTML, JS, nœud</td>
        </tr>
        <tr>
            <td>App Marketplace</td>
            <td>[Magento Marketplace](https://marketplace.magento.com/) (extensions PHP) et [Exchange Marketplace](https://commercemarketplace.adobe.com) pour les applications [!DNL App Builder] (Recommandé)</td>
            <td>[!DNL App Builder] applications de [[!DNL Exchange Marketplace]](https://commercemarketplace.adobe.com)</td>
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
            <td>Bibliothèque d’état App Builder (fichier uniquement)<sup>2 - <a href="https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/database">Stockage de base de données pour App Builder</a> est actuellement en accès anticipé.</sup></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="3">
                <sup>1</sup> L’extensibilité du modèle de données en SaaS prend en charge <a href="https://developer.adobe.com/commerce/webapi/graphql/schema/attributes/mutations/">l’extension des entités principales</a> au-delà du produit et du client, y compris les entités B2B. Cependant, les modèles de données spécifiques au secteur (par exemple, les attributs spécifiques aux revendeurs) peuvent nécessiter des considérations architecturales supplémentaires.
                <br><br>
                <sup>2</sup> Adobe travaille activement à l’intégration de la base de données Document pour répondre aux besoins de stockage persistant pour SaaS. Actuellement, les implémentations nécessitant un stockage de données à long terme peuvent avoir besoin de configurer et de gérer des infrastructures supplémentaires.
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
>- Tenez compte des [!DNL API Mesh] d’extension de la fonctionnalité d’API.
>- Surveillez l’évolution continue de la plateforme Adobe et les nouvelles versions de fonctionnalités.
>- Évaluez les exigences des modèles de données spécifiques au secteur par rapport aux options d’extensibilité disponibles.
>- Envisagez d’adopter des [services de marchandisage optimisés par des vues et des politiques de catalogue](../optimizer/setup/catalog-view.md).
