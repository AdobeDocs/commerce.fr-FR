---
title: Limites et limites de l’intégration
description: Découvrez les limites d’étendue pour les catalogues tiers, la couverture de correctif automatique, les conditions préalables explorées, les considérations à l’échelle de l’entreprise et les contraintes d’accès bêta restreintes pour LLM Optimizer avec Commerce.
role: Admin, User, Leader
recommendations: noCatalog
badgePaas: label="PaaS uniquement" type="Informative" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce on Cloud (infrastructure PaaS gérée par Adobe) et aux projets On-premise."
source-git-commit: 47348a44ff7c5f890c10594f44cae6e771be046f
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Limites et limites de l’intégration

>[!IMPORTANT]
>
>L’accès à cette intégration est restreint. Contactez votre gestionnaire de compte technique pour plus d’informations.

Utilisez cette rubrique pour définir les attentes en matière d’automatisation de l’intégration [!DNL Adobe Commerce] et [!DNL Adobe LLM Optimizer], les responsabilités et les contraintes qui continuent d’évoluer.

## Limites des catalogues tiers {#third-party-catalog}

Lorsque le catalogue **ne réside pas** dans [!DNL Adobe Commerce] :

- LLM Optimizer peut toujours identifier les problèmes et suggérer des améliorations à l’aide de données de catalogue importées ou mises en miroir, selon votre configuration.
- Le **correctif automatique direct** dans la plateforme commerciale du commerçant n’est pas identique à l’écriture dans le catalogue source du commerçant. Vous aurez peut-être besoin d’un catalogue miroir, d’une exportation/importation ou d’une automatisation des partenaires pour appliquer les modifications.

Pour les catalogues hébergés sur Commerce, les mises à jour de nom et de description approuvées sont transmises au système d’enregistrement Commerce. Voir [Utilisation de LLM Optimizer avec Adobe Commerce](get-started/use-llmo-with-commerce.md).

## Échelle et limites techniques {#scale-limits}

Des catalogues volumineux et un nombre d’URL élevé peuvent accentuer les modèles d’explore, d’analyse et de déploiement Edge.

## Explorer et lisibilité des robots {#crawling}

Des informations significatives sur les catalogues et les PDP supposent que les **robots) pertinents pour LLM peuvent accéder aux URL qui vous intéressent et que les pages sont structurées de sorte que l’analyse automatisée soit fiable** Les règles robotisées, l’authentification, le blocage géographique et une personnalisation poussée peuvent réduire la couverture.

## Rubriques connexes

- [Présentation de l’intégration](overview.md)
- [Connexion d’Adobe Commerce à LLM Optimizer](get-started/connect-to-llmo.md)
- [Utilisation de LLM Optimizer avec Adobe Commerce](get-started/use-llmo-with-commerce.md)
