---
title: Configuration du processus en arrière-plan
description: Configurez les plannings des processus  [!DNL Store Fulfillment]  arrière-plan utilisés pour synchroniser les données avec les services d'exécution.
role: Admin, Developer
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Configuration du processus en arrière-plan

L&#39;intégration Store Fulfillment utilise des processus en arrière-plan et des files d&#39;attente de messages pour des performances et une échelle optimales. Créez des environnements pour vos magasins Adobe Commerce à l’aide de [variables de déploiement](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-deploy#cron_consumers_runner) qui démarrent automatiquement [exécuteurs de files d’attente de messages](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/message-queues/message-queue-framework).

Les processus en arrière-plan sont gérés à l&#39;aide de la fonctionnalité standard Adobe Commerce [Tâches planifiées](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/cron). Ces processus sont chargés de synchroniser les données de configuration des commandes et des magasins marchands avec les services web d’exécution des magasins.

## Gérer les tâches planifiées pour la Store Fulfillment

Depuis l’administrateur, accédez à **[!UICONTROL Stores > Configuration > Advanced > System > Cron (Scheduled Tasks) > Cron configuration options for group:store_fulfillment]**.

Vérifiez la configuration par défaut pour les services Store Fulfillment. Vous pouvez personnaliser ces paramètres en fonction du volume de traitement des commandes et de la disponibilité des ressources.
