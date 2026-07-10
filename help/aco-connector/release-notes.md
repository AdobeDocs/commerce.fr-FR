---
title: Notes de mise à jour de [!DNL Adobe Commerce Optimizer Connector]
description: Découvrez les notes  [!DNL Adobe Commerce Optimizer Connector]  mise à jour d’, y compris les nouvelles fonctionnalités, les correctifs et les problèmes connus de synchronisation et d’exportation de catalogues.
autotag-review: '2026-06-17T15:08:59.000Z'
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: f08fa0de-a550-4acd-b570-f81cf1d03aafid: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2: id: dad884f1-e840-49a1-970e-2f965bdbc410id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2: id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 4eb33526927e1c5a81612aab0de0ce4bc7746368
workflow-type: tm+mt
source-wordcount: 366
ht-degree: 0%

---

# Notes de mise à jour du connecteur Adobe Commerce Optimizer

Ces notes de mise à jour décrivent toutes les versions du [!DNL Adobe Commerce Optimizer Connector] et incluent les éléments suivants :

![Nouveau](../assets/new.svg) Nouvelles fonctionnalités
![Correction d’un problème](../assets/fix.svg) Correctifs et améliorations
![Problème connu](../assets/bug.svg) Problèmes connus

## Versions De 2026

### Version 1.0.15

_10 juillet 2026_

![Correctif](../assets/fix.svg) Ajout de la prise en charge du tri au flux Catégories . <!--MDEE-1409-->

### Version 1.0.14

_1 juin 2026_

![Correctif](../assets/fix.svg) **Compatibilité PHP 8.5** - Le [!DNL Adobe Commerce Optimizer Connector] prend désormais en charge PHP 8.5, ce qui vous permet de mettre à niveau votre environnement [!DNL Adobe Commerce] sans interrompre les fonctionnalités du connecteur ou la synchronisation des catalogues. <!--MDEE-1388-->

![Correctif](../assets/fix.svg) **Mise à jour des tarifs après les modifications de devise** - Les tarifs mis à jour sont automatiquement répercutés dans Adobe Commerce Optimizer après les modifications de devise. <!--MDEE-1384-->

![Correctif](../assets/fix.svg) **La navigation respecte les catégories parentes désactivées ou masquées** - Les produits provenant des hiérarchies de catégories désactivées ou masquées n’apparaissent plus de manière inattendue dans les expériences de navigation.<!--MDEE-1385-->

![Correctif](../assets/fix.svg) **URL de catégorie cohérentes après les mises à jour d’évaluation** - Les liens de catégorie et la navigation restent précis après l’application des mises à jour d’évaluation. <!--MDEE-1395-->

### Version 1.0.13

_6 mai 2026_

![Correctif](../assets/fix.svg) **Amélioration des instructions de configuration du [!DNL Adobe Commerce Optimizer Connector]** - Mise à jour de la page de configuration du [!DNL Adobe Commerce Optimizer] dans Commerce Admin afin de renvoyer vers le guide d’intégration du _[!DNL Adobe Commerce Optimizer Connector]_.


![Correctif](../assets/fix.svg) amélioration **[!DNL Adobe Commerce Optimizer Connector]métadonnées** - La [!DNL Adobe Commerce Optimizer Connector] inclut désormais sa version installée dans l’en-tête des métadonnées. Cette amélioration permet aux équipes d’identifier rapidement la version du connecteur utilisée lors des missions de dépannage ou d’assistance.<!--MDEE-1323-->

### Version 1.0.12

_2 avril 2026_

![Nouveau](../assets/new.svg) **Ajout de la prise en charge du flux Catégories dans `saas:resync` commande**-Vous pouvez désormais facilement actualiser et afficher vos dernières données de catégorie à l’aide de la commande d’interface de ligne de commande `saas:resync` :

```shell
bin/magento saas:resync --feed=categories
```

### Version 1.0.11

_10 mars 2026_

![Correction d’un problème de compatibilité](../assets/fix.svg) correction d’un problème de compatibilité qui bloquait l’accès à la page de configuration de [!DNL Commerce Services Connector] à partir du **[!UICONTROL System]** d’administration de Commerce et des menus **[!UICONTROL Configuration]** lorsque le [!DNL Adobe Commerce Optimizer Connector] est installé sur une instance [!DNL Adobe Commerce].  Vous pouvez désormais accéder à la page de configuration [!DNL Commerce Services Connector] lorsque les deux extensions sont installées. <!--MDEE-1322-->


### Version 1.0.10

_9 mars 2026_

![Correctif](../assets/fix.svg) Si vous accédez à la page de **[!UICONTROL Data Feed Sync Status]** avant d’avoir terminé la configuration du connecteur, vous êtes désormais automatiquement redirigé vers la page de configuration du connecteur. Ce flux guidé garantit que la configuration du connecteur est terminée et permet d’éviter les erreurs dues à des paramètres de configuration manquants qui pourraient entraîner des éléments d’état en échec ou incomplets.<!--MDEE-1296-->

### Version 1.0.9

_1er mars 2026_

Disponibilité générale de la [!DNL Adobe Commerce Optimizer Connector].

>[!NOTE]
>
>Si vous avez participé au programme Beta pour la [!DNL Adobe Commerce Optimizer Connector] et qu’une version antérieure de l’extension est installée, effectuez une mise à niveau vers la version de disponibilité générale pour recevoir les dernières mises à jour.
