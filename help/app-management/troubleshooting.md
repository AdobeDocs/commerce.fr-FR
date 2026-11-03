---
title: '[!DNL App Management] de dépannage'
description: Résolvez les problèmes courants liés à l’association, l’installation, la configuration et les mises à niveau des applications.
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: a00b9e1654a572e1773b5b7e321683332882d86f
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%
---
# [!DNL App Management] de dépannage

Utilisez les solutions suivantes pour résoudre les problèmes courants liés à l&#39;association, l&#39;installation, la configuration et les mises à niveau de l&#39;application.

## Avant de contacter votre fournisseur d’applications

Suivez les étapes relatives à votre problème ci-dessous. Si vous avez besoin d’aide de la part du développeur ou du fournisseur d’applications, collectez les informations suivantes :

* Nom de l’application et version installée, si disponible à partir de **[!UICONTROL Manage]** > **[!UICONTROL Details]** sur la carte de l’application.
* Instance Commerce et organisation Adobe affectées.
* Opération ayant échoué, telle que l’installation ou la mise à niveau, et étape ayant échoué.
* Message d’erreur affiché avec une capture d’écran de l’échec, le cas échéant.
* Heure approximative de la panne, fuseau horaire compris.
* Toutes les tentatives de reprise et leurs résultats.

## L’application n’est pas affichée.

Si l’application n’apparaît pas dans la liste après le déploiement, vérifiez les étapes suivantes :

1. Vérifiez que l’application est déployée et disponible dans votre organisation.

1. Vérifiez que vous êtes connecté à l’organisation Adobe appropriée dans Developer Console.

1. Assurez-vous que l’application est prête à se connecter (votre développeur ou partenaire d’application peut confirmer).

Si l&#39;application n&#39;apparaît toujours pas, contactez le développeur de votre application ou consultez la documentation [Extensibilité  [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} pour obtenir des informations techniques.

## Échec de la synchronisation de l’étendue

Si la synchronisation de l’étendue échoue lors de l’association d’une application, essayez les méthodes suivantes :

1. Vérifiez que votre instance Commerce est accessible et en ligne.

1. Vérifiez que vos informations d’identification API sont valides et disposent des autorisations appropriées.

1. Essayez de synchroniser manuellement à partir de **[!UICONTROL Manage Scopes]** dans la configuration de l’application.

## Configuration non enregistrée

Si les modifications de configuration ne sont pas enregistrées, essayez les méthodes suivantes :

1. Vérifiez que tous les champs obligatoires sont renseignés et valides.

1. Vérifiez que vous disposez des autorisations appropriées pour modifier la configuration de l’application.

1. Essayez d’actualiser la page et enregistrez à nouveau.

Si le problème persiste, recherchez des erreurs dans la console de votre navigateur ou contactez votre développeur ou développeuse d’applications.

## Échec de l’installation

Laissez la page d’installation ouverte sans actualiser jusqu’à la fin de l’installation. Sa fermeture ou son actualisation peut empêcher l&#39;installation de se terminer correctement.

Si l’installation signale un échec :

1. Notez l’élément en échec et tout message d’erreur affiché.

1. Vérifiez que vous avez terminé les instructions de préinstallation de l’application.

1. Demandez à votre développeur d&#39;application d&#39;inspecter l&#39;étape ayant échoué et de corriger la cause avant de tenter à nouveau l&#39;installation.

Une installation ayant échoué, certaines modifications peuvent être appliquées. Lorsque l’installation est relancée, les étapes personnalisées enregistrées comme réussies sont ignorées ; les étapes ayant échoué ou interrompues peuvent s’exécuter à nouveau. Demandez à votre développeur de rechercher les ressources créées par une exécution partielle.

## Échec de la mise à niveau

Une mise à niveau ayant échoué, certaines opérations peuvent être appliquées. Ne désassociez pas et ne réinstallez pas l’application en tant qu’étape de récupération de routine, car la dissociation supprime la configuration et peut exécuter des scripts de nettoyage destructeurs.

1. Identifiez l’étape ayant échoué et enregistrez tout message d’erreur affiché.

1. Demandez à votre développeur d’application d’examiner les journaux, de vérifier les modifications déjà apportées à Commerce ou à des ressources externes, et de corriger la cause.

1. Dans [!DNL App Management], sélectionnez **[!UICONTROL Retry Upgrade]**. Cette action est disponible pour les modes de mise à niveau manuelle et automatique.

Chaque reprise crée un plan à partir de l’état actuel. Les étapes d’installation personnalisée enregistrées comme réussies sont ignorées ; les étapes ayant échoué ou été interrompues peuvent s’exécuter à nouveau. En mode automatique, le déploiement de l’application déclenche également une autre tentative de mise à niveau.

Si plusieurs tentatives échouent, demandez à votre développeur d&#39;application de conserver les ID d&#39;exécution ou de tentative et tout ID d&#39;activation d&#39;exécution pour le dépannage. Pour les commandes d’état, l’historique des tentatives et les journaux d’exécution, consultez [Réessayer une mise à niveau ayant échoué](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/#retry-a-failed-upgrade){target="_blank"} dans la documentation du développeur.

## Les ressources restent après une mise à niveau

La suppression d’une étape d’installation personnalisée de la configuration d’une application n’exécute pas son script de désinstallation ni ne supprime les ressources qu’elle a créées. Le plan de mise à niveau avertit qu’aucun script ne s’exécute pour l’étape supprimée et l’étape n’apparaît pas sur l’écran de progression ou dans les détails de l’application après la mise à niveau.

Demandez à votre développeur d’application de confirmer si les ressources sont toujours nécessaires et de fournir une migration de nettoyage si nécessaire. Voir [Mettre à niveau une application](manage-app.md#upgrade-an-app) pour le workflow d’administration.

Pour la résolution des problèmes techniques, voir [Extensibilité de  [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} pour plus d&#39;informations.
