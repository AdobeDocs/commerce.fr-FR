---
title: Responsabilité partagée
description: Découvrez les responsabilités de chaque partie impliquée dans votre projet Adobe Commerce as a Cloud Service en matière de sécurité.
role: Admin, Architect, Leader
source-git-commit: 19c49b2b9d630898353addd778e062d3208505c1
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---


# Sécurité à responsabilité partagée et modèle opérationnel

Adobe Commerce as a Cloud Service est un service à la demande qui repose sur un modèle opérationnel et de sécurité à responsabilité partagée. Ces responsabilités sont partagées entre Adobe et les clients. Chaque partie assume la responsabilité distincte de la sécurisation et de l’exploitation de l’application Adobe Commerce.

>[!BEGINSHADEBOX]

Les tableaux récapitulatifs ci-après utilisent le modèle RACI pour montrer les responsabilités en matière de sécurité partagées entre Adobe et les clients.

**R** — Responsable
**A** — Responsabilité
**C** — Consulté
**I** — Informé

>[!ENDSHADEBOX]

| Tâche | Adobe | Client |
| --- | --- | --- |
| Application de correctifs d’infrastructure Adobe Commerce | RA | |
| Application de correctifs aux services de support (par exemple, Nginx ou MySQL) | RA | |
| Définir les règles WAF d’origine du serveur principal | RA | |
| Définition des règles de WAF du réseau CDN principal | RA | |
| Déploiement des règles WAF de la plateforme principale | RA | |
| Déploiement des règles de WAF du réseau CDN principal | RA | |
| Correction des bugs principaux dans Adobe Commerce as a Cloud Service | RA | I |
| Publication des correctifs d’infrastructure d’Adobe Commerce as a Cloud Service | RA | |
| Évolutivité (infrastructure) | RA | |
| Mise à l’échelle (application principale) | RA | |
| Intégration d’applications externes | | RA |
| Installation des applications App Builder | | RA |
| Test des performances de toutes les applications App Builder | | RA |
| Thème et conception d’applications App Builder personnalisées | | RA |
| Configuration du serveur DNS principal | RA | I |
| Intégration du réseau CDN principal | RA | I |
| Prise en charge du réseau CDN principal | RA | I |
| Obtention d’un fournisseur DNS principal | RA | |
| Approvisionnement des environnements de production et de sandbox | A | R |
| Accès à Dynamics pour Adobe Commerce sur les infrastructures cloud | R | C |
| Résolution des problèmes de sécurité du client principal | RA | I |
| Résolution des problèmes de sécurité du réseau CDN principal | RA | |
| Assister Adobe dans ses recherches sur la sécurité (analyses/audits) | RA | |
| Exécution d’analyses PCI ASV | RA | I |
| Correction des analyses PCI de l’infrastructure Adobe Commerce | R | |
| Gestion des secrets de système d’exploitation et de plateforme | RA | |
| Surveillance des journaux de sécurité du serveur principal | RA | |
| Contrôle de l’assistance clientèle et de l’accès | A | R |
| Tests annuels et documentation du plan de reprise après sinistre, de sauvegarde et de restauration d’Adobe | RA | |
| Tests annuels et documentation du plan de reprise après sinistre | RA | |
| Débogage et isolation des problèmes | R | R |
| Prise en charge en temps voulu du débogage et du processus d’isolation des problèmes | R | R |
| Publication de mises à jour et de correctifs sur Adobe Commerce Core | RA | I |
| Installation de mises à jour et de correctifs sur Adobe Commerce Core | RA | I |
| Qualité des applications Adobe Commerce principales | RA | |
