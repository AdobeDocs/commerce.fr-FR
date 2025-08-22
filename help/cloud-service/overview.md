---
title: Vue d’ensemble des [!DNL Adobe Commerce as a Cloud Service]
description: Découvrez les principales fonctionnalités et avantages de  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Architect, Developer, User, Leader
exl-id: 1b7e2731-4a10-4c2b-9bfc-8945729ed523
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: 8fc46b0b93ac5102477f33bf2a8ae70a7acaf85d
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---


# Vue d’ensemble des [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] offre flexibilité, évolutivité et efficacité en permettant aux entreprises de fournir et d’adapter rapidement leurs opérations numériques et d’accélérer l’innovation. L’infrastructure native au cloud d’Adobe ajuste automatiquement les ressources pour répondre aux pics de demande de trafic, de commandes et de gestion de catalogues.

Le tableau suivant présente les produits qui alimentent [!DNL Adobe Commerce as a Cloud Service] :

<table style="table-layout:auto">
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>Commerce Storefront</strong>
    </td>
    <td>
      Interface destinée aux clients dans laquelle les acheteurs parcourent et achètent des produits
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong> Services de marchandisage </strong>
    </td>
    <td>
      Services principaux de gestion des catalogues de produits, des prix et des stocks
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>Visuels du produit</strong>
    </td>
    <td>
      Gestion des ressources numériques pour les images et les médias de produits
    </td>
  </tr>
  <tr>
    <td>
      <span style="display: inline-block; width: 20px; height: 20px; background: white; border: 1px solid #d32f2f; border-radius: 50%; margin-right: 8px; vertical-align: middle;">
        <span style="color: #d32f2f; font-size: 14px; line-height: 18px; display: block; text-align: center;">✓</span>
      </span>
      <strong>Developer Platform</strong>
    </td>
    <td>
      Outils de développement de base et API pour la création de fonctionnalités personnalisées
    </td>
  </tr>
</table>

## Architecture

Regardez la vidéo suivante pour une brève présentation de l’architecture [!DNL Adobe Commerce as a Cloud Service]. Des diagrammes illustrant l’architecture sont fournis sous la vidéo.

>[!VIDEO](https://video.tv.adobe.com/v/3443232?learn=on)

Ce diagramme illustre le flux de données entre [!DNL Adobe Commerce as a Cloud Service] et toutes les solutions Adobe Experience Cloud.

![[!DNL Adobe Commerce as a Cloud Service] le diagramme d’architecture ](./assets/data-flow.svg){zoomable="yes"}

## Commerce Storefront

Utilisez Adobe [Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront) optimisé par Edge Delivery Services pour créer des expériences riches en quelques minutes avec une création simple basée sur des documents ou une modification visuelle avec Storefront Builder.

Le storefront Commerce est entièrement découplé avec une architecture découplée qui fournit tous les services et données de marchandisage via une couche d’API GraphQL. Cette architecture permet aux équipes de développer leurs interfaces indépendamment de Commerce Foundation, offrant ainsi l’agilité nécessaire pour créer et tester de nouveaux points de contact avec les technologies émergentes.

>[!NOTE]
>
>[!DNL Adobe Commerce as a Cloud Service] ne prend pas en charge les storefronts Luma. Si vous migrez depuis Adobe Commerce on Cloud ou on-premise, consultez [storefronts existants](https://experienceleague.adobe.com/developer/commerce/storefront/discovery/#existing-storefronts) pour obtenir des conseils sur la transition.

## Services de marchandisage et services de paiement

Adobe fournit un ensemble riche de services de marchandisage intelligents et composables pour vous aider à atteindre vos principaux objectifs commerciaux. Ces services fournissent également des API qui sont essentielles pour optimiser les performances à grande échelle.

- [Recherche en direct](../live-search/overview.md) : obtenez des résultats plus intelligents, plus rapides et pertinents pour les acheteurs grâce à cet outil de recherche optimisé par l’IA.
- [Recommandations de produits](../product-recommendations/overview.md) : ajoutez des recommandations optimisées par l’IA en fonction du comportement des acheteurs, des tendances populaires, de la similarité des produits, etc.
- [Services de marchandisage optimisés par des vues et des politiques de catalogue](../optimizer/setup/catalog-view.md)—Gérez des catalogues de produits complexes et volumineux avec une modélisation de données flexible afin de fournir des catalogues commerciaux hautement performants et flexibles alignés sur la structure de l’entreprise et les stratégies de commercialisation. Utilisez avec [Commerce Optimizer](../optimizer/overview.md) pour optimiser les performances du catalogue et améliorer les taux de conversion.
- [Services de paiement](../payment-services/guide-overview.md)—Augmentez la satisfaction des clients en offrant diverses méthodes de paiement, y compris des acomptes provisionnels sans intérêt, et une vue unique du traitement des paiements, des commandes et des factures.

## Visuels de produit optimisés par AEM Assets

Les visuels de produit permettent de simplifier la gestion des ressources à l’aide d’un système de gestion des ressources numériques (DAM) qui s’intègre à Adobe Experience Manager pour gérer le contenu multimédia.

L’intégration garantit que les ressources numériques, telles que les images de produit ou le contenu marketing, sont liées dynamiquement aux entités de marchandisage appropriées, y compris les produits et les catégories dans Adobe Commerce, en fonction du SKU ou d’autres attributs clés.

La fonctionnalité Visuels de produit est disponible prête à l’emploi avec [!DNL Adobe Commerce as a Cloud Service], offrant certaines des fonctionnalités d’AEM Assets.

Les fonctionnalités natives d’[!DNL Adobe Commerce as a Cloud Service] offrent également des outils de gestion des ressources de base pour le stockage et la gestion des ressources numériques.

### Visuels de produit pour AEM Assets

La comparaison suivante vous aide à sélectionner la meilleure option pour vos besoins de chaîne d’approvisionnement de contenu :

<table style="width: 100%; border-collapse: collapse; margin: 20px 0;">
  <tr style="border: none;">
    <td style="width: 45%; vertical-align: top; border: 2px solid #e0e0e0; padding: 20px; background: #fafafa;">
      <p style="color: #d32f2f; border-bottom: 2px solid #d32f2f; padding-bottom: 10px; margin-top: 0;">Visuels de produit optimisés par AEM Assets</h3>
      <ul style="margin: 0; padding-left: 20px;">
        <li>Gestion des ressources numériques (DAM), vidéo et image de produit automatisée et intégrée</li>
        <li>Redimensionnement, recadrage et conversion d’images</li>
        <li>Diffusion d’images et de vidéos à grande vitesse</li>
        <li>Optimisez les formats, tailles et qualité des images en fonction des fonctionnalités du navigateur client.</li>
        <li>Accès à Adobe Express et Adobe Firefly</li>
        <li>Limites d’utilisation de la capacité de diffusion image/vidéo et de l’accès utilisateur</li>
        <li>Sélecteur de ressources intégré</li>
      </ul>
    </td>
    <td style="width: 10%; text-align: center; vertical-align: middle; font-size: 98px; color: #d32f2f; font-weight: bold;">
      ›
    </td>
    <td style="width: 45%; vertical-align: top; border: 2px solid #e0e0e0; padding: 20px; background: #fafafa;">
      <p style="color: #d32f2f; border-bottom: 2px solid #d32f2f; padding-bottom: 10px; margin-top: 0;">AEM Assets</h3>
      <ul style="margin: 0; padding-left: 20px;">
        <li>Toutes les fonctionnalités des visuels de produit</li>
        <li>Gestionnaire de ressources numériques (DAM) Full Marketing</li>
        <li>Utilisateurs illimités (payant par utilisateur)</li>
        <li>Diffusion illimitée d’images et de vidéos</li>
        <li>Fonctionnalité avancée de gestion des ressources :</li>
        <ul>
          <li>Visionneuses à 360° et visionneuses interactives</li>
          <li>Prise en charge des modèles 3D et contenu immersif</li>
          <li>Prise en charge de PDF</li>
          <li>Recadrage intelligent optimisé par l’IA</li>
         <li>Modèles d’images dynamiques</li>
        <li>Balisage intelligent</li>
        <li>Suivi et analyse des performances des ressources</li>
        </ul>
      </ul>
    </td>
  </tr>
</table>

<table style="width: 100%; margin: 20px 0;">
  <tr>
    <td style="background: #f5f5f5; padding: 15px; text-align: center; font-weight: bold;">
      L’intégration de la marque Adobe est disponible pour faciliter la migration entre les offres.
    </td>
  </tr>
</table>

Consultez le guide d’[intégration d’AEM Assets](../aem-assets-integration/overview.md) pour en savoir plus sur la manière d’intégrer des visuels de produit optimisés par AEM Assets à [!DNL Adobe Commerce as a Cloud Service].

## Plateforme du développeur

Adobe fournit aux développeurs des points d’extension et des outils complets pour créer des applications qui étendent les fonctionnalités de Commerce Foundation et s’intègrent à des systèmes tiers (tels que CRM, ERPS et PIMS). Ces outils permettent de réduire le coût total de possession de la plateforme comme suit :

- **Évolutivité** : les applications peuvent être mises à l&#39;échelle séparément du logiciel principal, ce qui permet d&#39;accroître l&#39;efficacité et de simplifier les mises à niveau.
- **Isolation**-Un environnement isolé signifie que les développeurs peuvent mettre à niveau ou modifier leurs extensions à leur guise sans avoir recours à une version principale.
- **Indépendance technologique**-Les développeurs peuvent choisir la pile technologique et le langage de codage qui correspondent à leurs besoins.

>[!TIP]
>
>Des applications créées par le fournisseur peuvent également être installées sur [Adobe Exchange](https://exchange.adobe.com/).

Adobe fournit les outils de développement suivants pour créer des intégrations et des personnalisations :

- [**Maillage API pour Adobe Developer App Builder**](https://developer.adobe.com/graphql-mesh-gateway/) : coordonnez et combinez plusieurs API, GraphQL, REST et d’autres sources en un seul point d’entrée GraphQL interrogeable.
- [**App Builder**](https://developer.adobe.com/app-builder/docs/overview/) : créez et déployez des applications web sécurisées et évolutives qui étendent les fonctionnalités de Commerce et s’intègrent à des solutions tierces.
- [**Événements**](https://developer.adobe.com/commerce/extensibility/events/) : utilisez des déclencheurs d&#39;événement personnalisés pour interagir avec d&#39;autres outils de développement extensibles.
- [**Webhooks**](https://developer.adobe.com/commerce/extensibility/webhooks/) : utilisez les webhooks pour déclencher automatiquement les interactions entre Commerce et les systèmes tiers.
- [**Admin UI SDK**](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/) : personnalisez et améliorez l’administration Commerce avec de nouvelles pages et fonctionnalités pour vos commerçants.
- [**kit de démarrage de l’intégration**](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) : accélérez vos intégrations back-office grâce à des intégrations de référence, des scripts d’intégration et une architecture normalisée.

## Commerce Foundation

Commerce Foundation fournit une plateforme d’hébergement automatisée sécurisée et des fonctionnalités en libre-service pour gérer votre application Commerce dans un environnement natif dans le cloud.

Les principales fonctionnalités sont les suivantes :

- Intégration simplifiée
- Mises à niveau transparentes
- Intégrations tierces

### Intégration simplifiée

Lancez le sandbox et les instances de production en quelques minutes avec le portail d’approvisionnement en libre-service [!UICONTROL Commerce Cloud Manager]. Tout ce dont vous avez besoin, y compris les services de marchandisage, une instance Commerce découplée et App Builder, est automatiquement configuré et intégré à vos instances.

Voir [Prise en main](getting-started.md) pour savoir comment créer et gérer des instances Commerce.

### Mises à niveau transparentes

Accédez aux dernières fonctionnalités et améliorations sans avoir à effectuer de mises à niveau manuelles. La diffusion continue de nouvelles fonctionnalités et de mises à jour élimine le besoin d&#39;appliquer manuellement des correctifs, ce qui garantit que vous avez toujours accès aux dernières fonctionnalités avec un coût total de possession faible.

Le processus de mise à niveau classique pour Adobe Commerce sur Cloud consistait à créer des sauvegardes, cloner des instances, exécuter des outils de compatibilité et résoudre des conflits de code. Ce n&#39;est plus nécessaire avec [!DNL Adobe Commerce as a Cloud Service]. Adobe vous envoie des notifications in-app lorsque de nouvelles fonctionnalités et mises à jour de sécurité sont publiées. Vous disposez d’une période de 30 jours pour évaluer les nouvelles fonctionnalités de vos instances sandbox avant que les mises à jour ne soient automatiquement appliquées à vos environnements de production.

>[!NOTE]
>
>Adobe garantit la rétrocompatibilité pour toutes les mises à jour. Cela signifie que lorsque des mises à jour sont appliquées, elles n’interrompent pas les fonctionnalités ou personnalisations existantes qui adhèrent au modèle [extensibilité API-first](https://developer.adobe.com/commerce/extensibility/).

### Intégrations tierces

Les développeurs peuvent utiliser des API [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/) et [REST](https://developer.adobe.com/commerce/webapi/rest/) complètes pour intégrer Commerce Foundation à des systèmes tiers et étendre les fonctionnalités de Commerce.

<!-- ## Experience Cloud integration

[!DNL Adobe Commerce as a Cloud Service] integrates with all Experience Cloud solutions to deliver [personalized commerce experiences at scale](https://experienceleague.adobe.com/en/docs/commerce-admin/customers/customers-menu/personalize-scale#customers-menu).

[Data Connection](../data-connection/overview.md) unlocks insights about your shoppers' buying behavior so that you can create personalized shopping experiences across all channels with other Adobe Digital Experience products. -->

## Avantages

Les sections suivantes fournissent des informations sur les avantages offerts par [!DNL Adobe Commerce as a Cloud Service] aux chefs d’entreprise et aux responsables informatiques.

### Chefs d’entreprise

- **Augmenter le chiffre d’affaires** : stimulez le trafic organique avec une vitrine haute performance qui stimule l’optimisation pour les moteurs de recherche. Créez des expériences personnalisées qui génèrent des conversions à l’aide de données enrichies.
- **Mise à l’échelle des opérations** : les services de mise à l’échelle automatique répondent aux demandes de pointe de votre entreprise avec une disponibilité de 99,9 %. Déployez plusieurs marques et régions et prenez en charge le B2B et le B2C à partir d’une seule instance. Prise en charge de catalogues de produits volumineux et complexes avec une modélisation de données flexible.
- **Augmenter la productivité du marchandiseur** : utilisez les services de marchandisage optimisés par l’IA pour améliorer la conversion. Faites des expériences en mode natif, directement dans le storefront. Gérez l’expérience du storefront pour créer des expériences riches en quelques minutes avec une création simple basée sur des documents ou un éditeur visuel.
- **Réduction du coût total de possession (TCO) et accélération de l’innovation** : des services toujours à jour vous donnent immédiatement accès à de nouvelles fonctionnalités. Activez de nouvelles fonctionnalités en installant facilement des applications à partir de la marketplace. Libérez des ressources de la maintenance fastidieuse pour vous concentrer sur la création de nouvelles fonctionnalités.

### Leaders en technologies de l&#39;information (TI)

- **Approvisionnement rapide** : commencez rapidement votre approvisionnement en libre-service en quelques minutes. Tous les services sont préconfigurés pour fonctionner de manière transparente afin de démarrer plus rapidement. Fournissez des sandbox pour l’expérimentation des développeurs, si nécessaire.
- **Faible coût de possession** : plus de mises à niveau avec des services toujours à jour. Restez sécurisé et conforme avec les derniers correctifs de sécurité automatiquement appliqués pour vous. Évoluez automatiquement pour répondre aux charges de travail les plus exigeantes.
- **Vitrine haute performance** : créez des expériences riches en quelques minutes avec une création simple basée sur des documents ou un éditeur visuel. Utilisez des services de marchandisage optimisés par l’IA pour améliorer la conversion. Expérimentation native intégrée au storefront.
- **Innovation plus rapide** : libérez des ressources nécessaires à une maintenance fastidieuse pour vous concentrer sur la création de nouvelles fonctionnalités offrant une valeur ajoutée à votre entreprise. Utilisez une extensibilité complète et des technologies standard (JavaScript, HTML, CSS et outils à code faible) pour créer des expériences différenciées. Installez des applications tierces en un clic pour ajouter de nouvelles fonctionnalités à votre plateforme commerciale.
