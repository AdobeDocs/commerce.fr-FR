---
title: Responsabilité partagée
description: Découvrez les responsabilités de chaque partie impliquée dans votre projet en matière  [!DNL Adobe Commerce Optimizer]  sécurité.
role: Admin, Architect, Leader
badgeSaas: label="SaaS uniquement" type="Positive" url="https://experienceleague.adobe.com/fr/docs/commerce/user-guides/product-solutions" tooltip="S’applique uniquement aux projets Adobe Commerce as a Cloud Service et  [!DNL Adobe Commerce Optimizer]  (infrastructure SaaS gérée par Adobe)."
exl-id: 9e09790f-832d-43ab-b2df-6389ad52b43d
source-git-commit: c7c21df464685783b5fae1c99d60ca91e0c334d2
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Sécurité à responsabilité partagée et modèle opérationnel

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
| Application de correctifs aux services d’assistance | RA | |
| Définir les règles WAF d’origine du serveur principal | RA | |
| Définition des règles de WAF du réseau CDN principal | RA | |
| Déploiement des règles WAF de la plateforme principale | RA | |
| Déploiement des règles de WAF du réseau CDN principal | RA | |
| Correction de bugs dans [!DNL Adobe Commerce Optimizer] | RA | I |
| Publication des correctifs d’infrastructure [!DNL Adobe Commerce Optimizer] | RA | |
| Évolutivité (infrastructure) | RA | I |
| Intégration d’applications externes | | RA |
| Installation des applications App Builder | | RA |
| Test des performances de toutes les applications App Builder | | RA |
| Thème et conception d’applications App Builder personnalisées | | RA |
| Configuration du serveur DNS principal | RA |  |
| Intégration du réseau CDN principal | RA |  |
| Prise en charge du réseau CDN principal | RA |  |
| Obtention d’un fournisseur DNS principal | RA | |
| Approvisionnement des environnements de production et de sandbox | A | R |
| Accès à Dynamics for [!DNL Adobe Commerce Optimizer] | R | C |
| Résolution des problèmes de sécurité du client principal | RA | I |
| Résolution des problèmes de sécurité du réseau CDN principal | RA | |
| Assister Adobe dans ses recherches sur la sécurité (analyses/audits) | RA | |
| Exécution d’analyses PCI ASV | RA | I |
| Correction des analyses PCI de l’infrastructure [!DNL Adobe Commerce Optimizer] | R | |
| Gestion des secrets de système d’exploitation et de plateforme | RA | |
| Surveillance des journaux de sécurité du serveur principal | RA | |
| Contrôle de l’assistance clientèle et de l’accès | A | R |
| Tests annuels et documentation du plan de reprise après sinistre, de sauvegarde et de restauration d’Adobe | RA | |
| Tests annuels et documentation du plan de reprise après sinistre | RA | |
| Débogage et isolation des problèmes | R | R |
| Prise en charge en temps voulu du débogage et du processus d’isolation des problèmes | R | R |
| Installation de mises à jour et de correctifs sur [!DNL Adobe Commerce Optimizer] | RA | I |
| Qualité des applications [!DNL Adobe Commerce Optimizer] | RA | |
