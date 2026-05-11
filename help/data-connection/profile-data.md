---
title: Mettre à jour le schéma d’enregistrement de profil pour l’ingestion de données Commerce
description: Découvrez comment créer un schéma, un jeu de données et un flux de données pour collecter et envoyer des données d’enregistrement de profil Commerce à Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
exl-id: 25741837-f423-4204-8520-80b7cd9d44bd
TQID: https://experienceleague.adobe.com/I8bptw1tNdzXfCC6hFtn7fuz-BIiALXG4g6lLhga6ec
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 340
ht-degree: 0%

---

# Mettre à jour le schéma d’enregistrement de profil pour l’ingestion de données Commerce

Lorsque vos clients créent un profil sur votre site Commerce, un enregistrement de profil est créé et les données sont capturées. Vous devez créer un schéma et un jeu de données spécifiques à cet enregistrement de profil avant de pouvoir diffuser ces données de profil vers Experience Platform.

1. [Créez](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas) un schéma et définissez la classe sur **Profil individuel**.

1. [Ajoutez](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas) les groupes de champs spécifiques au profil suivants :

   - identityMap
   - Détails démographiques
   - Coordonnées personnelles
   - Détails du compte utilisateur

1. [Activer](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas) le schéma pour Profil.

   Lorsqu’un schéma est activé pour Profil, tous les jeux de données créés à partir de ce schéma participent à Real-Time CDP, qui fusionne les données de sources disparates pour créer une vue complète de chaque client.

1. [Créez un jeu de données](https://experienceleague.adobe.com/en/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform) en fonction du schéma que vous avez créé ou mis à jour.

   Un jeu de données est une structure de stockage et de gestion pour une collecte de données, généralement sous la forme d’un tableau contenant un schéma (colonnes) et des champs (lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

1. Créez un [espace de noms personnalisé](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/namespaces#create-namespaces) dans Experience Platform avec les valeurs suivantes :

   - **Nom d’affichage** : _ID de client Commerce_
   - **Symbole d’identité** : _CustomerId_
   - **Type** : _identifiant individuel sur l’ensemble des appareils_

   ![Créer un espace de noms personnalisé](assets/custom-namespace.png){width="700" zoomable="yes"}

   Cliquez sur **[!UICONTROL Create]**. Un espace de noms personnalisé est utilisé par le service de profil unifié pour regrouper les fragments de profil.

Une fois le schéma, le jeu de données et l’espace de noms personnalisé configurés pour les données d’enregistrement de profil client, vous pouvez [configurer](connect-data.md#data-collection) votre instance Commerce pour collecter et envoyer ces données à Experience Platform.

Pour créer un schéma, un jeu de données et un flux de données pour les données comportementales et d’événement back-office, consultez [mise à jour des schémas d’événement de série temporelle pour l’ingestion de données Commerce](update-xdm.md).
