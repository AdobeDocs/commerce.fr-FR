---
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%
---
# Obtention des détails de l’instance [!DNL Commerce Optimizer]

Récupérez l’_identifiant du client_ à partir du champ _[!DNL Instance Id]_de l’instance [!DNL Commerce Optimizer] [[!DNL Instance details] page](/help/optimizer/get-started.md#manage-instances) ou à partir de l’URL utilisée pour accéder à l’instance. Par exemple, dans `https://experience.adobe.com/#/@<your organization>/in:<tenant>/commerce-optimizer-studio/home`.

1. Dans l’Administration de Commerce, sélectionnez **[!UICONTROL Adobe Commerce Optimizer]** pour afficher la page de configuration avec les instructions.

   ![[!DNL Commerce Optimizer] page de configuration](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. À partir de la ligne de commande, [utilisez SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) pour vous connecter à l’environnement d’évaluation [!DNL Adobe Commerce].

1. Pour configurer l’intégration, exécutez la commande d’interface de ligne de commande [!DNL Adobe Commerce] suivante, en remplaçant les valeurs d’espace réservé par les valeurs de votre projet [!DNL Commerce Optimizer] :

   ```shell
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Vérifiez la connexion en revenant à l’administration Commerce et en sélectionnant l’option [!UICONTROL Adobe Commerce Optimizer] .

   Lorsque vous sélectionnez l’option , elle ouvre l’interface utilisateur de [!DNL Commerce Optimizer] dans un nouvel onglet.
