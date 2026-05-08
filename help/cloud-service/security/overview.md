---
title: Présentation de la sécurité
description: Découvrez les fonctionnalités de sécurité d’Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et Adobe Commerce Optimizer (infrastructure SaaS gérée par Adobe)."
source-git-commit: feb48068137c6a63e6594167fe969c3aa4b044c4
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 0%

---


# Présentation de la sécurité

La solution [!DNL Adobe Commerce as a Cloud Service] est conçue pour offrir une sécurité au cœur de la solution, une plateforme commerciale moderne et native en SaaS qui offre une protection de niveau entreprise, une résilience opérationnelle et une tranquillité d’esprit aux entreprises de toutes tailles.

Contrairement aux modèles PaaS traditionnels, le modèle SaaS élimine le fardeau des cycles manuels de correction, de maintenance de l&#39;infrastructure et de mise à niveau. La sécurité est intégrée à chaque couche de la plateforme, depuis l’infrastructure gérée par Adobe et les pipelines de déploiement automatisés jusqu’à la gestion des identités et des accès en passant par le [!DNL Adobe IMS].

[!DNL Adobe Commerce as a Cloud Service] exploite le framework de sécurité et de conformité global d’Adobe, en assurant l’alignement sur les normes du secteur telles que ISO 27001, SOC 2 et le RGPD. Les clients bénéficient d’un [modèle de responsabilité partagée](./shared-responsibility.md) qui délimite clairement le rôle d’Adobe dans la sécurisation de la plateforme et le rôle du client dans la gestion des données et des accès.

Grâce à des protections intégrées telles que le pare-feu d&#39;application web (WAF), l&#39;atténuation des attaques DDoS, le provisionnement sécurisé et l&#39;analyse continue des vulnérabilités, [!DNL Adobe Commerce as a Cloud Service] permet aux entreprises d&#39;innover plus rapidement sans compromettre la sécurité.

Ce document décrit l’architecture de sécurité, les garanties opérationnelles et la position de conformité de [!DNL Adobe Commerce as a Cloud Service], ce qui permet aux clients de prendre des décisions éclairées et d’étendre en toute confiance leurs opérations de commerce numérique.

## Réseau de diffusion de contenu (CDN) et pare-feu d’application web (WAF)

### Réseau CDN Storefront

Les commerçants peuvent choisir de déployer un réseau CDN géré par Adobe ou d’acheter leur propre solution CDN pour protéger leur storefront alimenté par Commerce.

>[!IMPORTANT]
>
>Si les clients choisissent de déployer un réseau CDN géré par Adobe, ils ne peuvent pas configurer de règles CDN. Les règles de mise en cache personnalisées ou les règles de WAF peuvent être configurées par les clients lorsqu’ils apportent leur propre réseau CDN pour protéger leurs storefronts.

### [!DNL API Mesh for Adobe Developer App Builder] CDN

La couche de réseau CDN de [!DNL API Mesh] met fin à TLS, exécute la passerelle GraphQL en tant que Workers, fournit une mise en cache de périphérie globale et des DDoS/WAF automatiques, et expose `edge‑graph.adobe.io`/`edge‑sandbox‑graph.adobe.io` en tant que points d’entrée de maillage public ; les clients peuvent ajouter leur propre réseau CDN en amont, mais le réseau CDN de [!DNL API Mesh] est fixe et géré par Adobe et les clients ne peuvent pas configurer leurs propres règles WAF.

Pour plus d’informations sur les fonctionnalités de sécurité de [!DNL API Mesh], consultez la documentation sur le [&#x200B; maillage API &#x200B;](https://developer.adobe.com/graphql-mesh-gateway/mesh/security/){target="_blank"}.

### Réseau CDN principal

Un réseau CDN intégré protège les [!DNL Adobe Commerce as a Cloud Service].

En raison de l’architecture [!DNL Adobe Commerce as a Cloud Service], lorsqu’un commerçant approvisionne une instance dans une cellule composite, telle que `na1`, `eu1`, `au1` ou d’autres régions géographiques, trois surfaces publiques sont exposées :

| Surface | Exemple de modèle d’URL |
| --- | --- |
| Interface utilisateur d’administration | `https://<region>.admin.commerce.adobe.com/<tenant-id>/admin/` |
| API REST | `https://<region>.api.commerce.adobe.com/<tenant-id>/<endpoint>` |
| API GRAPHQL | `https://na1.api.commerce.adobe.com/<tenant_id>/graphql/` |

[!DNL Adobe Commerce as a Cloud Service] utilise un WAF et un réseau CDN combinés :

- **&#x200B;**&#x200B;- Protection par pare-feu d&#39;application web pour toutes les surfaces publiques [!DNL Adobe Commerce as a Cloud Service].
- **CDN** - Mise en cache Edge pour les ressources statiques et les réponses GraphQL pouvant être mises en cache.

WAF et le réseau CDN sont gérés par la plateforme [!DNL Adobe Commerce as a Cloud Service] et ne sont pas configurables par les clients.

### Protection DDoS

Le réseau CDN et le WAF intégrés fournissent une protection DDoS à la fois à la couche réseau et à la couche HTTP. [!DNL Adobe Commerce as a Cloud Service] n’expose pas directement ces journaux WAF ou DDoS aux commerçants.

## Stockage et chiffrement des données

Si les données sont stockées dans [!DNL App Builder], un commerçant peut se référer aux [!DNL App Builder] [options de stockage](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/storage/). [!DNL App Builder] applique l’isolement du client et l’accès aux données stockées dans ces services est limité à l’espace de noms d’exécution dans lequel l’action est exécutée. Les données stockées ne sont pas chiffrées.

Lors de l’utilisation de [!DNL API Mesh], les secrets doivent être stockés dans le fichier `secrets.yaml` de votre configuration de maillage. [!DNL API Mesh] chiffre ces secrets en utilisant le chiffrement AES-256 ([https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/secrets/)).

Toutes les données stockées dans [!DNL Adobe Commerce as a Cloud Service] sont chiffrées au repos à l’aide du chiffrement AES 256 bits et toutes les données sont chiffrées sur HTTPS à l’aide de TLS 1.2 ou version ultérieure en transit.
