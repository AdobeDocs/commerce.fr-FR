---
title: Types de données Commerce
description: Découvrez les types de données que vous pouvez collecter et envoyer à Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Types de données Commerce

L’extension [Data Connection](overview.md) connecte vos données Commerce à Experience Platform. Les données destinées à être utilisées dans Experience Platform sont regroupées en deux types de comportement : les données de série temporelle, qui appartiennent à la classe **Événement d’expérience**, et les données d’enregistrement, qui appartiennent à la classe **Profil individuel**.

En savoir plus sur les [comportement des données](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#data-behaviors) et les [classes](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html#class) dans Experience Platform.

## Données de série temporelle

Les données de série temporelle fournissent un instantané du système au moment où une action a été entreprise directement ou indirectement par un objet d’enregistrement. Par exemple, lorsqu’un acheteur parcourt un produit sur votre site, ajoute un produit à son panier, passe une commande, etc. Les données de série temporelle sont ingérées dans Experience Platform à l’aide d’un schéma dont la classe est définie sur **Événement d’expérience**.

### Données de série temporelle capturées

Voir [événements comportementaux](events.md) et [événements back-office](events-backoffice.md) pour savoir quelles données sont capturées lorsqu’un événement de série temporelle est généré.

### Schéma nécessaire à l’ingestion des données d’événement de série temporelle

Découvrez comment [créer un schéma](update-xdm.md) qui peut ingérer des données d’événement de série temporelle comportementale et de back-office.

## Données d’enregistrement

Les données d’enregistrement fournissent des informations sur les attributs d’un sujet. Un sujet peut être une organisation ou un individu. Par exemple, un acheteur sur votre site crée un compte qui génère des données d’enregistrement. Ces données sont ingérées dans Experience Platform à l’aide d’un schéma dont la classe est définie sur **Profil individuel**. Vous pouvez envoyer ces données d’enregistrement au service de gestion des profils et de segmentation d’Adobe : [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=fr).

### Données d’enregistrement de profil capturées

Voir [Données d’enregistrement de profil client](events-profilerecord.md) pour savoir quelles données sont capturées lorsqu’un enregistrement de profil est généré.

### Schéma nécessaire à l’ingestion des données d’enregistrement de profil

Découvrez comment [créer un schéma](profile-data.md) qui peut ingérer des données d’enregistrement de profil.
