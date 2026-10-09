---
title: Types de données Commerce
description: Découvrez les types de données que vous pouvez collecter et envoyer à Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
exl-id: 6354963c-f27f-4e69-9ecb-acb4befb7c2a
TQID: 'https://experienceleague.adobe.com/LXMqOhHAZpUHaCeeU5ioKKXVrkLftospQEPDd9H-MD8'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 0%
---
# Types de données Commerce

L’extension [Data Connection](overview.md) connecte vos données Commerce à Experience Platform. Les données destinées à être utilisées dans Experience Platform sont regroupées en deux types de comportement : les données de série temporelle, qui appartiennent à la classe **Événement d’expérience**, et les données d’enregistrement, qui appartiennent à la classe **Profil individuel**.

En savoir plus sur les [comportement des données](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition#data-behaviors) et les [classes](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/schema/composition#class) dans Experience Platform.

## Données de série temporelle

Les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise directement ou indirectement par un objet d’enregistrement. Par exemple, lorsqu’un acheteur parcourt un produit sur votre site, ajoute un produit à son panier, passe une commande, etc. Les données de série temporelle sont ingérées dans Experience Platform à l’aide d’un schéma dont la classe est définie sur **Événement d’expérience**.

### Données de série temporelle capturées

Voir [événements comportementaux](events.md) et [événements back-office](events-backoffice.md) pour savoir quelles données sont capturées lorsqu’un événement de série temporelle est généré.

### Schéma nécessaire à l’ingestion des données d’événement de série temporelle

Découvrez comment [créer un schéma](update-xdm.md) qui peut ingérer des données d’événement de série temporelle comportementale et de back-office.

## Données d’enregistrement

Les données d’enregistrement fournissent des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu. Par exemple, un acheteur sur votre site crée un compte qui génère des données d’enregistrement. Ces données sont ingérées dans Experience Platform à l’aide d’un schéma dont la classe est définie sur **Profil individuel**. Vous pouvez envoyer ces données d’enregistrement au service de gestion des profils et de segmentation d’Adobe : [Real-Time CDP](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview).

### Données d’enregistrement de profil capturées

Voir [Données d’enregistrement de profil client](events-profilerecord.md) pour savoir quelles données sont capturées lorsqu’un enregistrement de profil est généré.

### Schéma nécessaire à l’ingestion des données d’enregistrement de profil

Découvrez comment [créer un schéma](profile-data.md) qui peut ingérer des données d’enregistrement de profil.
