---
title: Vérifier s’il existe des mises à jour d’extension
description: Découvrez comment Adobe Commerce recherche et informe les administrateurs des nouvelles versions de l’extension Intégration AEM Assets, y compris de la vérification manuelle de l’interface de ligne de commande.
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7950f5d171b35054be42ca60d19bafcf43c53cd6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%
---
# Rechercher les mises à jour d’extension

Avec les versions 1.4.6 et ultérieures de l’extension d’intégration AEM Assets, Adobe Commerce vérifie automatiquement si une version plus récente de l’extension est disponible et en informe les administrateurs. Ce contrôle s’exécute de manière asynchrone dans le cadre du traitement planifié et ne bloque pas le rendu des pages d’administration.

## Fonctionnement de la vérification de la mise à jour

* La vérification de mise à jour compare la version de package `aem-assets-integration` installée à la version compatible la plus élevée disponible à partir de [repo.magento.com](https://repo.magento.com/admin/dashboard).
* Les résultats sont mis en cache. Le chargement d’une page d’administration lit le résultat en cache le plus récent plutôt que de déclencher une requête réseau active.
* Si `repo.magento.com` n’est pas disponible ou si les métadonnées renvoyées ne sont pas valides, Commerce conserve le dernier résultat mis en cache et ne bloque pas l’administrateur.

>[!NOTE]
>
>La vérification de la mise à jour est destinée aux déploiements Adobe Commerce sur le cloud et sur site.

## Afficher les notifications de mise à jour

Les administrateurs peuvent voir une notification de mise à jour disponible à l’un des emplacements :

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* Menu déroulant de notification de l’administrateur

Chaque notification affiche :

* Version installée
* La version disponible
* La classification de version
* Un lien vers les notes de mise à jour

Sélectionnez **[!UICONTROL Remind me later]** pour répéter la notification pour cette instance Commerce ou pour exclure entièrement les notifications de mise à jour.

## Exécuter une vérification de mise à jour manuelle

Pour vérifier immédiatement la disponibilité d’une mise à jour, exécutez la commande suivante à partir du répertoire racine Commerce :

```bash
bin/magento aem:assets:check-update
```

Cette commande recherche et signale uniquement une mise à jour disponible. Il ne modifie pas les fichiers du compositeur et ne déploie pas de mise à jour. Pour installer une mise à jour, suivez les instructions du compositeur dans [Installation des packages Adobe Commerce](configure-commerce.md).

## Métadonnées de version des packages d’extension

Le contrôle de mise à jour lit les métadonnées de version à partir de la section `extra` du fichier `composer.json` du package installé :

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## Étape suivante

* [Installation des packages Adobe Commerce](configure-commerce.md)
