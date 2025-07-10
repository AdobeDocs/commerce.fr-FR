---
title: Correspondance automatique par défaut
description: Découvrez comment la règle de correspondance automatique par défaut permet une synchronisation transparente entre Adobe Commerce et l’intégration d’AEM Assets, en veillant à ce que les ressources soient automatiquement liées aux entités de marchandisage appropriées.
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
source-git-commit: 6640635fca5c53fe4b06b9bbb3120fffc46cb0b8
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Correspondance automatique par défaut

L’intégration d’AEM Assets pour Commerce fournit un mécanisme de correspondance automatique par défaut (**[!UICONTROL Match by product SKU]**) en fonction de la configuration des métadonnées **AEM Assets**. Cette règle permet une synchronisation transparente entre **Adobe Commerce** et **AEM Assets**, en veillant à ce que les ressources soient automatiquement liées aux entités de marchandisage correctes.

## Configuration du mécanisme de correspondance automatique

1. Dans l’Administration Commerce, accédez à **[!UICONTROL Store]** > Configuration > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Spécifiez **[!UICONTROL Match by SKU]** comme règle correspondante.

   ![règle de rapprochement automatisé par défaut](../assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. Saisissez le nom du champ de métadonnées utilisé pour l’identification de la ressource dans AEM Assets.

   >[!NOTE]
   >
   > Si le processus d’intégration standard a été suivi, cette valeur doit être définie sur `commerce:skus`.

## Fonctionnement du mécanisme de correspondance automatique

Lorsque la règle de correspondance de **[!UICONTROL Match by product SKU]** est configurée dans l’administration Commerce, les fichiers de ressources Commerce se synchronisent automatiquement entre AEM Assets et votre projet Commerce en fonction des métadonnées de ressources configurées pour chaque fichier. Vous configurez les métadonnées à partir de l’onglet AEM **Commerce** dans l’environnement de création **AEM Assets** :

![ Exemple de métadonnées ](../assets/example-metadata.png){width="600" zoomable="yes"}

1. Dans AEM Assets, mettez à jour les métadonnées de l’image pour ajouter l’association Adobe Commerce, `Commerce=yes`.

1. Configurez les métadonnées ([!UICONTROL SKU], [!UICONTROL position] et [!UICONTROL role]) qui lient la ressource au SKU du produit associé.

   >[!NOTE]
   >
   > Si une ressource est utilisée pour plusieurs produits, configurez les métadonnées de chaque SKU associé.

Cette approche permet de s’assurer que les ressources numériques sont correctement liées et affichées dans Adobe Commerce. Il permet également aux marchandiseurs et aux marketeurs de gérer les rôles et le positionnement des ressources directement dans AEM Assets, fournissant ainsi un mécanisme cohérent et centralisé pour la sélection et la commande des images sur tous les canaux d’engagement.
