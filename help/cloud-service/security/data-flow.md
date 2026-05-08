---
title: Architecture de sécurité et flux de données
description: Découvrez l’architecture de sécurité et le flux de données d’Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 0%

---


# Architecture de sécurité et flux de données

L’exemple suivant illustre la manière dont les données sont généralement transmises en [!DNL Adobe Commerce as a Cloud Service] :

![Diagramme de flux de données Adobe Commerce as a Cloud Service](../assets/data-flow-1.png)

## Récapitulatif du flux de données

**Étape 1** : l’acheteur saisit l’URL du storefront du vendeur dans son navigateur, qui envoie l’URL au réseau de diffusion de contenu (CDN externe) du storefront Commerce.

**Étape 2** : si l’URL du site est mise en cache, le réseau CDN Storefront la renvoie à l’acheteur. S’il n’est pas déjà mis en cache, ce qui peut se produire s’il s’agit de la première requête pour une ressource, le réseau CDN externe transfère la requête de l’acheteur au réseau CDN interne et met en cache la réponse pour les requêtes suivantes.

**Étape 2a** : si la demande porte sur des images ou des vidéos, elle est envoyée à [!DNL Product Visuals] pour exécution et renvoyée au storefront.

**Étape 3** : si l’URL du site est mise en cache sur le réseau CDN interne, elle est renvoyée à partir de ce cache. Dans le cas contraire, elle est envoyée à [!DNL API Mesh] et la réponse est mise en cache pour les requêtes suivantes.

**Étape 4** : [!DNL API Mesh] agit comme couche d’orchestration et détermine s’il faut envoyer la requête à [!DNL Adobe Commerce as a Cloud Service] ou à un système tiers pour répondre à la requête.

>[!NOTE]
>
>[!DNL API Mesh] n’envoie des requêtes à des systèmes tiers que si vous avez personnalisé votre configuration de maillage pour ce faire.

**Étape 5** : les requêtes envoyées à [!DNL Adobe Commerce as a Cloud Service] transitent par un pare-feu d’application web (WAF) qui bloque les requêtes suspectes ou malveillantes. Si l’URL demandée est mise en cache sur le réseau CDN [!DNL Commerce], elle est diffusée à partir de ce cache. S’il n’est pas mis en cache, il est renvoyé par un ou plusieurs microservices [!DNL Adobe Commerce as a Cloud Service] (par exemple, foundation, search et recommendations), puis mis en cache pour les requêtes ultérieures.

**Étape 5a** : si la demande est envoyée à un système tiers, la réponse est renvoyée à [!DNL API Mesh].

**Étape 5b** : si la demande porte sur le traitement des paiements, le fournisseur de services de paiement insère un iframe dans le storefront pour que l’acheteur puisse saisir en toute sécurité les informations de carte de crédit et effectuer la transaction de paiement.

**Étape 6** : une fois que les réponses des services [!DNL Adobe Commerce as a Cloud Service] ou tiers sont reçues par [!DNL API Mesh], elles sont regroupées dans un graphique unifié et renvoyées à [!DNL Commerce Storefront] pour répondre à la requête de l’acheteur.
