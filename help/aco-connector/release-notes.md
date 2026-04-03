---
title: Notes de mise à jour de [!DNL Adobe Commerce Optimizer Connector]
description: Dernières informations de mise  [!DNL Adobe Commerce Optimizer Connector]  jour pour Adobe Commerce.
feature: Services, Catalog Service, Release Notes
source-git-commit: 205fca38b379f94027a965b58826ffd922577f61
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Notes de mise à jour du connecteur Adobe Commerce Optimizer

Ces notes de mise à jour décrivent toutes les versions du [!DNL Adobe Commerce Optimizer Connector] et incluent les éléments suivants :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correction d’un problème](../assets/fix.svg) Correctifs et améliorations
![Problème connu](../assets/bug.svg) Problèmes connus

## Versions De 2026

### Version 1.0.12

_2 avril 2026_

![Nouveau](../assets/new.svg) **Ajout de la prise en charge du flux Catégories dans `saas:resync` commande **-Vous pouvez désormais facilement actualiser et afficher vos dernières données de catégorie à l’aide de la commande de l’interface de ligne de commande `saas:resync` :

```terminal
bin/magento saas:resync --feed=categories
```

_10 mars 2026_

![Correction d’un problème](../assets/fix.svg) Correction d’un problème de compatibilité qui bloquait l’accès à la page de configuration du connecteur de services Commerce à partir des menus Système d’administration et Configuration de Commerce lorsque le connecteur Adobe Commerce Optimizer est installé sur une instance Commerce.  Vous pouvez désormais accéder à la page de configuration du connecteur de services Commerce lorsque les deux extensions sont installées. <!--MDEE-1322-->


### Version 1.0.10

_9 mars 2026_

![Correctif](../assets/fix.svg) Si vous accédez à la page Statut de la synchronisation des flux de données avant d’avoir terminé la configuration du connecteur, vous êtes désormais automatiquement redirigé vers la page de configuration du connecteur. Ce flux guidé garantit que la configuration du connecteur est terminée et permet d’éviter les erreurs dues à des paramètres de configuration manquants qui pourraient entraîner des éléments d’état en échec ou incomplets.<!--MDEE-1296-->

### Version 1.0.9

_1er mars 2026_

Version de disponibilité générale du connecteur Adobe Commerce Optimizer.

>[!NOTE]
>
>Si vous avez participé au programme Beta pour le connecteur Adobe Commerce Optimizer et qu’une version antérieure de l’extension est installée, effectuez une mise à niveau vers la version de disponibilité générale pour recevoir les dernières mises à jour.

