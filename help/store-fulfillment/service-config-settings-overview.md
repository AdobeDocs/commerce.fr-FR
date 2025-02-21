---
title: Présentation de la configuration pour la Store Fulfillment
description: Découvrez les types de paramètres de configuration d’administration disponibles pour personnaliser les fonctionnalités d’exécution étendues fournies par la solution Store Fulfillment et obtenez des liens vers des instructions pour terminer la configuration.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Présentation de la configuration pour la Store Fulfillment

Dans Adobe Commerce Admin, les paramètres de configuration des services Store Fulfillment Services de Walmart Commerce Technologies sont classés par type.

**Paramètres de configuration de l&#39;exécution des commandes en magasin par type**

| **Type** | **Description** | **API configurable** |
|--------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|
| [Configuration générale](enable-general.md) | Configuration générale de l&#39;intégration pour la solution Store Fulfillment, ses fonctionnalités actives et les informations d&#39;identification pour se connecter aux services d&#39;exécution. | Non |
| [Configuration des e-mails de vente](sales-emails.md) | Configurez des modèles d’e-mail supplémentaires pour les notifications client envoyées pendant le processus d’enregistrement. | Non |
| [Configuration de la boutique marchande](merchant-store-configuration.md) | Configurez les sources Inventory management améliorées comme magasins marchands. | Oui |
| [Gestion des stocks de produits](product-stock.md) | Configurez la messagerie et les fonctionnalités de stock marchand disponibles pour les clients. | Oui |
| [Transfert Source Inventory management](inventory-stock-transfer.md) | Configurer un nouveau stock, transférer le stock en dehors du stock par défaut. | Oui |
| [Configuration de plusieurs sites web/étendues](multi-site-and-scope-config.md) | Configurez les stocks et les méthodes de diffusion pour plusieurs sites web/étendues de magasin. | Non |
| [Configuration du système de processus en arrière-plan](background-processes.md) | Configurez les plannings pour les processus en arrière-plan utilisés pour synchroniser les données avec les services d&#39;exécution. | Non |
| [Emplacement du magasin et configuration du mappage](store-location-map-provider-setup.md) | Configurer la possibilité d&#39;utiliser un fournisseur à distance pour rechercher des magasins de vente au détail et afficher ces informations dans le mappage SLS | Oui |
| [Configuration de l’expérience d’enregistrement](check-in-experience-setup.md) | Configurez la couleur de la voiture et les options de rendu de la voiture qui seront disponibles pendant le processus d&#39;enregistrement | Oui |
| [Configuration utilisateur](user-setup.md) | Gérez les comptes utilisateur, les rôles et les autorisations des associés de la boutique qui utilisent l’application Store Assist. portées. | Oui |
| [Configuration de l’application](app-setup.md) | Passez en revue les configurations disponibles pour l’application d’assistance en magasin requises pour terminer le processus d’intégration. Ces paramètres ne peuvent pas être configurés à partir de l’administration Adobe Commerce. | Oui |

## Utiliser la référence de configuration

Affichez la référence de configuration pour chaque type de paramètre en sélectionnant le nom du type dans le tableau _Paramètres de configuration de l&#39;exécution du magasin par type_.

Dans la référence de configuration pour chaque type, les détails de la configuration sont affichés dans un tableau avec les en-têtes de colonne suivants :

- **Champ** fait référence au nom du champ à configurer

- **Description** fournit des détails importants sur l’objectif et le comportement du champ

- **Portée** indique la portée de la configuration Adobe Commerce pour le paramètre (global, site web, magasin)

- **Obligatoire** la valeur indique si une valeur doit être définie sur le champ

Pour référence technique, vous pouvez également trouver le chemin de configuration interne pour chaque champ.
