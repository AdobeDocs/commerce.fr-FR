---
title: Mettre à jour les schémas d’événement de série temporelle pour l’ingestion de données Commerce
description: Découvrez comment créer un schéma, un jeu de données et un flux de données pour collecter et envoyer des données d’événement de série temporelle pour l’ingestion de données Commerce.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 0%

---

# Mettre à jour les schémas d’événement de série temporelle pour l’ingestion de données Commerce

L’une des [ étapes d’intégration ](overview.md#onboarding-steps) pour utiliser l’extension [!DNL Data Connection] consiste à accéder à l’espace de travail du flux de données et [créer un flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr) qui est spécifique à Adobe Commerce. Lorsque vous créez ce flux de données, vous devez également sélectionner un schéma qui décrit les données que vous prévoyez d’ingérer. Ce schéma doit inclure des groupes de champs spécifiques à Commerce.

Cet article vous fournit les groupes de champs que votre schéma doit inclure pour collecter avec succès les données de série temporelle suivantes fournies par les événements Adobe Commerce :

- [Comportemental](events.md) - Inclut les événements de storefront, de profil, de recherche et B2B.
- [Back office](events-backoffice.md) - Inclut le statut de la commande et les événements de profil.

En savoir plus sur les [données de série temporelle](data-ingestion.md).

En savoir plus sur les [principes de base de la composition des schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr).

## Mettre à jour le schéma avec les données comportementales et d’événement back-office de la série temporelle

Dans cette section, vous apprendrez à mettre à jour votre schéma existant ou à créer un schéma pour inclure des données comportementales et d’événement de back-office.

>[!NOTE]
>
>Voir [Données d’événement de profil de série temporelle](#time-series-profile-event-data) pour savoir comment ajouter des champs spécifiques au profil.

1. Si vous ne disposez pas déjà d’un schéma, [créez](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=fr#create) un schéma dont la classe est définie sur **Événement d’expérience**.

1. [Ajoutez](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=fr#add-field-groups) les groupes de champs spécifiques à Commerce suivants (ou modifiez votre schéma existant et ajoutez ces groupes de champs) :

   - Recherche de site
   - Page web de la visite
   - Processus de connexion de l’utilisateur
   - Clés de référence
   - Coordonnées personnelles
   - Détails du canal
   - Détails Commerce
   - Commerce Adobe Analytics ExperienceEvent (si vous souhaitez envoyer des données à Adobe Analytics)

   >[!NOTE]
   >
   > Ne définissez aucun groupe de champs spécifique à Commerce comme `Primary identity`. Ce faisant, identifie le champ comme requis et Experience Platform s’attend à ce que ce champ soit présent dans chaque événement. Si ce champ est absent, l’ingestion des données échoue.

   Votre schéma contient désormais des groupes de champs spécifiques à Commerce, de sorte que les données de série temporelle collectées à partir des événements Commerce [comportementaux](events.md) et [ back-office](events-backoffice.md) soient représentées dans le schéma.

1. [Activer](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=fr#profile) le schéma pour Profil.

   Lorsqu’un schéma est activé pour Profil, tous les jeux de données créés à partir de ce schéma participent à Real-Time CDP, qui fusionne les données de sources disparates pour créer une vue complète de chaque client.

1. [Créez un jeu de données](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=fr#create-a-dataset) basé sur le schéma que vous avez créé ou mis à jour.

   Un jeu de données est une structure de stockage et de gestion pour une collecte de données, généralement sous la forme d’un tableau contenant un schéma (colonnes) et des champs (lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

1. [Créez un flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr) puis sélectionnez le schéma contenant les groupes de champs spécifiques à Commerce et le jeu de données correspondant.

   Le flux de données transfère les données collectées vers le jeu de données. Les données sont représentées dans le jeu de données en fonction du schéma sélectionné.

Une fois les schémas, les jeux de données et les flux de données configurés pour les données comportementales et d’arrière-plan, vous pouvez [configurer](connect-data.md#data-collection) votre instance Commerce pour collecter et envoyer ces données à Experience Platform.

Pour inclure les informations de profil de votre acheteur, voir [Données d’événement de profil de série temporelle](#time-series-profile-event-data).

## Données d’événement de profil de série temporelle

Les données d’événement de profil de série temporelle sont générées à partir des événements suivants :

- [`accountCreated`](events-backoffice.md#accountcreated)
- [`accountUpdated`](events-backoffice.md#accountupdated)
- [`accountDeleted`](events-backoffice.md#accountdeleted)

Si vous souhaitez ingérer les données d’événement de profil de votre client dans Experience Platform, vous pouvez mettre à jour votre schéma Commerce existant et utiliser le même flux de données déjà configuré, ou vous pouvez créer un flux de données et un schéma spécifiques au profil. Cette décision est basée sur la gouvernance des données de votre entreprise. Les deux sections suivantes vous guident dans les deux cas.

### Envoyez les données d’événement de profil de série temporelle à Experience Platform à l’aide de votre flux de données existant

Si vous souhaitez ajouter des séries temporelles [données d’événement de profil côté serveur](events-backoffice.md#customer-profile-events-server-side) à votre flux de données Commerce existant, ajoutez le groupe de champs `Demographic Details` à votre schéma. Votre schéma contient désormais les groupes de champs spécifiques à Commerce suivants :

- Recherche de site
- Page web de la visite
- Processus de connexion de l’utilisateur
- Clés de référence
- Coordonnées personnelles
- Détails du canal
- Détails Commerce
- Commerce Adobe Analytics ExperienceEvent (si vous souhaitez envoyer des données à Adobe Analytics)
- Nouveau : **Détails démographiques**

Avec l’ajout du groupe de champs `Demographic Details` dans votre schéma Commerce existant, le jeu de données et le flux de données déjà associés à votre schéma Commerce sont utilisés pour ces données de profil de série temporelle.

### Envoyez les données d’événement de profil de série temporelle à Experience Platform dans un flux de données distinct

Si vous souhaitez ajouter des [données d’événement de profil côté serveur](events-backoffice.md#customer-profile-events-server-side) à un nouveau flux de données et à un nouveau schéma spécifiques au profil, procédez comme suit.

1. [Créez](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=fr#create) un schéma et définissez la classe sur **Événement d’expérience**.

1. [Ajoutez](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=fr#add-field-groups) les groupes de champs spécifiques au profil suivants :

   - Détails démographiques
   - Coordonnées personnelles
   - Détails du canal
   - Détails Commerce

1. [Activer](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html?lang=fr#profile) le schéma pour Profil.

   Lorsqu’un schéma est activé pour Profil, tous les jeux de données créés à partir de ce schéma participent à Real-Time CDP, qui fusionne les données de sources disparates pour créer une vue complète de chaque client.

1. [Créez un jeu de données](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html?lang=fr#create-a-dataset) basé sur le schéma que vous avez créé.

   Un jeu de données est une structure de stockage et de gestion pour une collecte de données, généralement sous la forme d’un tableau contenant un schéma (colonnes) et des champs (lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

1. [Créez un flux de données](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr) puis sélectionnez le schéma XDM contenant les groupes de champs spécifiques à Commerce et le jeu de données correspondant.

   Le flux de données transfère les données collectées vers le jeu de données. Les données sont représentées dans le jeu de données en fonction du schéma sélectionné.

Une fois les schémas, les jeux de données et les flux de données configurés pour les données de profil client, vous pouvez [configurer](connect-data.md#data-collection) votre instance Commerce pour collecter et envoyer ces données à Experience Platform.

Pour créer un schéma, un jeu de données et un flux de données pour les données d’enregistrement de profil, voir [Envoyer les données d’enregistrement de profil à Experience Platform](profile-data.md).
